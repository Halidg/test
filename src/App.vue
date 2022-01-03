<template>
 <div class="banner">
   <div class="wrapper">
    <Form 
    @dataInput="dataInput" 
     />
    <div class="block">  
     <div class="block__list">   
      <p>List1</p>    
       <div class="square__position"  v-for="(item,index) in numbers" :key="index">
        <div class="square"  :style="{'background-color': color}" v-for="(count,index) in item" :key="index"></div>  
       </div>
     </div>
    </div>
    </div>
 </div>
</template>

<script>
import Form from './components/Form.vue'


export default {
  components:{Form},
  data(){
    return{
      numbers:[],
      color:''
    }
  },
  methods:{
    dataInput(data){
      this.numbers[data.id] = data.number 
      this.color = data.color
    }
  }
}
</script>

<style lang="scss" scoped>

*{
  box-sizing: border-box;
}

 .banner{
   width: 100%;
   max-width: 800px;
   min-height: 560px;
  
   margin: 0 auto;

   border: 1px solid black;
 }
 
 .wrapper{
   display: flex;
   align-items: flex-start;
   justify-content: space-between;
   
   
   margin: 0 auto;
   margin-top: 5px;

   width: 100%;
   max-width: 780px;
   min-height: 550px;

   border: 1px solid black;
 }

 .block{
   max-width: 300px;
   width: 100%;
   min-height: 500px;

   margin-top:15px;
   margin-right:15px;

   border: 1px solid black;
   &__list{
    display: flex;
    flex-direction: column;

    max-width: 280px;
    width: 100%;
    min-height: 100px;

    overflow: hidden;
   
    margin: 0 auto;

    border: 1px solid black;
   }
 }

 .square{
  max-width: 10px;
  width: 100%;
  min-height: 10px;

  display: flex;
   
  float: left;
  margin-left:5px;
  margin-top: 5px;
}
 
.square__position{
  margin-bottom:20px;
}

</style>
