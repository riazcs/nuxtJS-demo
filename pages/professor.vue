<template>
  <div>
    <h1>{{$route.params.id}}</h1>
    <table class="table">
  <thead class="thead-dark">
    <tr>
      <th scope="col">Name</th>
      <th scope="col">Email</th>
      <th scope="col">Phone</th>
      <th scope="col">Gender</th>
      <th scope="col">Blood Group</th>
    </tr>
  </thead>
  <tbody>
    <tr v-for="(data,index) in studentData" :key="index">
      <td>{{data.name}}</td>
      <td>{{data.email}}</td>
      <td>{{data.phone}}</td>
      <td>{{data.gender}}</td>
      <td>{{data.blood_group}}</td>
    </tr>
  </tbody>
</table>
    <NLink to="/">
      Home page
    </NLink>
  </div>
</template>

<script>
import axios from 'axios';
export default {
  data () {
    return {
      studentData:null
    }
  },
  head: {
    title: 'Professor'
  }, 
  mounted(){
      axios.get('http://localhost/university/api/user/professor/data').then(response => {
          this.studentData=response.data;
          //console.log(this.studentData);
      })
  }
}
</script>
