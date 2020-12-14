<template>
<div>
  <section class="control">
    Вибрано книгу {{ selected }}
    <input type="button" value="Додати нову компанію" v-on:click="showForm" />
    <input type="button" value="Редагувати компанію" v-on:click="showEditForm" />
    <input type="button" value="Вилучити інфу про компанію" v-on:click="deleteCompany"/>
    <input type="number" placeholder="min" v-model.number="minWorkerCount">
          <input type="number" placeholder="max" v-model.number="maxWorkerCount">
          <input type="button" value="знайти" v-on:click="Find()">
    
  </section>
  <div>
    <new-book-form 
      v-model = "newCompany"
      @submit.prevent="addNewCompany"
      ref="newBookForm"> </new-book-form>
      </div>
      <div>
    <new-book-form
      v-model = "editCompany"
      ref="editBookForm">
    </new-book-form>
    </div>
    <ul>
      <book-template
        v-for="c in companies"
        :key="c.Id"
        class="companyvie"
        v-on:click="selectCompany(c.Id)"
        v-bind:company="c">
      </book-template>
    </ul>
  </div>
</template>

<script>
import BookTemplate from './BookTemplate.vue';
import NewBookForm from './NewBookForm.vue';
import storage from '../Storage';
export default {
  name: "App",
  components:{
    BookTemplate,
    NewBookForm
  },
  data() {
    return {
      
      selected: -1,
      minWorkerCount:0,
      maxWorkerCount:0,
      companies:storage.companies,
      newCompany:
      {
          Name:"",
          Countries:"",
          NumberOfWorkers:0,
          TypeOfProducts:""
      },
      editCompany: {},
    };
  },
  methods: {
    addNewCompany() {
      console.log(this.newBook);
      let newCompanyCopy = Object.assign({}, this.newCompany);
      newCompanyCopy.Id = parseInt(Date.now());
      newCompanyCopy.Countries=newCompanyCopy.Countries.split(",");
      this.companies.push(newCompanyCopy);
      this.showNewCompanyForm = false;
    },
    showForm() {
      this.$refs.newBookForm.show();
    },
    selectCompany(id) {
      this.selected = id;
    },
    showEditForm() {
      if (this.selected >= 0) {
        let index = this.companies.findIndex(book => book.Id == this.selected);
        this.editCompany = this.companies[index];
        console.log(this.editCompany);
        
        this.$refs.editBookForm.show();
      } else alert("Виберіть компанію");
    },
    deleteCompany() {
      let index = this.companies.findIndex(company => company.Id == this.selected);
      if (this.selected >= 0) this.companies.splice(index, 1);
    },
    closeForm(){
      this.showNewCompanyForm = false;
    },
    Find(){
        var z=this.minWorkerCount;
        var m=this.maxWorkerCount;
        this.companies=this.companies.filter(x=>Number(x.NumberOfWorkers)>=z && Number(x.NumberOfWorkers)<=m);
    }
  },
  
};
</script>

<style scoped>

ul {
  list-style: none;
  position: relative;
}
.wrap {
  position: relative;
}

</style>
