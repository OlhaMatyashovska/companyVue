<template>
<form @submit.prevent="add">
Назва компанії:<br>
            <input v-model="newCompany.Name"><br>
            Число робітників:<br>
            <input type="number" v-model.number="newCompany.NumberOfWorkers"> <br>
            Продукти виробництва:<br>
            <input v-model="newCompany.TypeOfProducts"><br>
            Компанії-співробітники:<br>
            <input v-model="newCompany.Countries"><br>
            <button type="submit">Додати компанію до бази даних</button>
            </form>
</template>
<script> 
import storage from '../Storage';
export default{
   data(){
       return{
           newCompany:
      {
          Name:"",
          Countries:"",
          NumberOfWorkers:0,
          TypeOfProducts:""
      },
       }
   },
   methods:{
       add(){
           
      let newCompanyCopy = Object.assign({}, this.newCompany);
      newCompanyCopy.Id = Date.now();
      newCompanyCopy.Countries=newCompanyCopy.Countries.split(",");
      storage.companies.push(newCompanyCopy);
      this.$router.push(`/companydetails/${newCompanyCopy.Id}`);
    
       }
   }
}
</script>
<style scoped>
body{
    position:relative;
}
form{
    width:200px;
    height:250px;
    background-color:blue;
    position:absolute;
    top:50px;
    left:10px;
    color:white;
}
</style>