<template>
<button @click="gotoEdit">Редагувати інформацію про компанію</button>
<div>
<h1>{{company.Name}}</h1>

<p>Виробництво:{{company.TypeOfProducts}}</p>
                <p>Кількість робітників:{{company.NumberOfWorkers}}</p>
               Країни-співробітники:
                 <ul>
                  <li v-for="country in company.Countries" :key="country">{{country}}</li>
                </ul>
</div>
</template>

<script>
import storage from '../Storage';
export default{
    props:{
        id:String
    },
    data(){
        return{
            company:{}
        }
    },
    mounted(){
        this.company = storage.companies.find(x => x.Id == Number(this.id));
    },
    methods:{
        gotoEdit(){
            this.$router.push(`/edit/${this.id}`);
        }
    }
}
</script>

<style scoped>
body{
    position:relative;
}
div{
    position:absolute;
    height:250px;
    width:400px;
    color:white;
    background-color:blue;
    top:50px;
    left:10px;
}
</style>