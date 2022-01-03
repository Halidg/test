<template>
 <form class="form">
  <div v-for="(item,index) in items" :key="item.id">
      <input class="main__list"
        v-if="item.id == 0"
        v-model="mainCheck"
         type="checkbox"
        :indeterminate.prop="mainCheck === undefined"
        :value="item.id"
        :checked="mainCheck"
        
      />
      <input class="list"
        v-else
        v-model="item.isChecked"
        :checked="item.isChecked"
        type="checkbox"
        :value="item.id"
      />
      <span>
        {{item.title}}   
      </span>
        <input class="input__number" id="dva" v-if="item.isChecked && item.id>0" type="number" v-model="item.number" @input="dataInput(index)">
        <input class="input__color" type="color" v-if="item.isChecked && item.id>0" v-model="item.color" @input="dataInput(index)" >
  </div>
 </form>
 
</template>

<script>
export default {
 data(){
   return{
     items: [
      {id:0, title: "list1",isChecked: true},
      {id:1, title: "item1",isChecked: true, color: "#AC8686",number:1},
      {id:2, title: "item2",isChecked: true, color: "#AC8686",number:1},
      {id:3, title: "item3",isChecked: true, color: "#AC8686",number:1}],
      
      allChecked:true,
      noneChecked:false
   }
 },

 computed: {
  checkedList() {
    return this.items
      .filter(el => el.isChecked && el.id !== 0)
      .map(el => el.title)
  },
  mainCheck: {
    get() {
      [this.allChecked, this.noneChecked] = this.items
        .reduce(
          (acc, val) => {
            if (val.id === 0) {
              return acc
            }
            acc[0] &= val.isChecked
            acc[1] &= !val.isChecked
            return acc
          },
          [true, true]
        )
      if (this.allChecked) {
        return true
      }
      if (this.noneChecked) {
        return false
      }
      return undefined
    },
    set(check) {
      this.items.forEach(
        el => {
          el.isChecked = check
        }
      )
    }
  }
  },
  methods:{
    dataInput(index){
     this.items[index].id = index  
     this.$emit('dataInput',this.items[index])
    }
  }
}

</script>

<style lang="scss" scoped>

*{
  box-sizing: border-box;
}


 .form{
   max-width: 300px;
   width: 100%;
   min-height: 500px;

   margin-top:15px;
   margin-left:15px;

   border: 1px solid black;
 }
 
.main__list{
   list-style-type:none;
   margin-left:20px;
   margin-top:25px;
 }

 .list{
   list-style-type:none;
   margin-left:50px;
   margin-top:5px;  
 }

 #dva {
  width: 35px;
}

.input__number{
  margin-left: 100px;
  border: none;
}

.input__color{
  width: 25px;
  border: none;
}



</style>

