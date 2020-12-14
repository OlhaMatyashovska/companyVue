<template>
<form @submit.prevent="saveCompany">
Назва компанії:<br>
            <input v-model="editCompany.Name"><br>
            Число робітників:<br>
            <input type="number" v-model.number="editCompany.NumberOfWorkers"> <br>
            Продукти виробництва:<br>
            <input v-model="editCompany.TypeOfProducts"><br>
            Компанії-співробітники:<br>
            <input v-model="editCompany.Countries"><br>
            <button type="submit">Save</button>
            </form>
</template>

<script>
import storage from '../Storage';
export default{
    props:{
        id:String
    },
    data(){
        return{
            editCompany:{}
        }
    },
    mounted(){
        this.editCompany = storage.companies.find(x => x.Id == Number(this.id));
    },
    methods:{
        saveCompany(){
            this.editCompany.Countries=this.editCompany.Countries.split(",");
            this.$router.push(`/companydetails/${this.id}`);
        }
    }
}
</script>
<style scoped>
body{
    position:relative;
}
form{
    position:absolute;
    top:50px;
    left:10px;
    background-color:blue;
    width:200px;
    height:250px;
    color:white;
}
</style>
