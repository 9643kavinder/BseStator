<template>
  <div id="app">
    <form @submit.prevent = "searchcompany">
      <input type="search" class="form-outline form-control" placeholder="Enter The Company Name"
      aria-label="Search" v-model="name"/>
    </form>
    <table class="table mt-4">
      <thead>
        <th>Company Name</th>
        <th>Code</th>
        <th>Open</th>
        <th>High</th>
        <th>Low</th>
        <th>Close</th>
      </thead>
      <tbody>
        <tr v-for="company in companies" :key="company.name">
          <td>{{company.name}}</td>
          <td>{{company.code}}</td>
          <td>{{company.open}}</td>
          <td>{{company.high}}</td>
          <td>{{company.low}}</td>
          <td>{{company.close}}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>

export default {
  name: 'App',
  data(){
    return{
          name : '',
          companies : []
    }
  },
  async created(){
      var response = await fetch ('https://bseapp.osc-fr1.scalingo.io/api/');
      this.companies = await response.json();
  },
  methods : {
    async searchcompany(){
      var response = await fetch (`https://bseapp.osc-fr1.scalingo.io/api/${this.name}`);
      this.companies = await response.json();
      // this.name = '';
    }
  }


}

</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

</style>
