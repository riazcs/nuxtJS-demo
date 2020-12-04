<template>
  <div>
    <h1>{{$route.params.id}}</h1>
    <table class="table">
  <thead class="thead-dark">
    <tr>
      <th scope="col">ID</th>
      <th scope="col">Name</th>
      <th scope="col">Email</th>
      <th scope="col">Phone</th>
      <th scope="col">Gender</th>
      <th scope="col">Blood Group</th>
      <th scope="col">Action</th>
      <th scope="col">Action</th>
    </tr>
  </thead>
  <tbody>
    <tr v-for="(data,index) in studentData" :key="index">
      <td>{{data.student_id}}</td>
      <td>{{data.name}}</td>
      <td>{{data.email}}</td>
      <td>{{data.phone}}</td>
      <td>{{data.gender}}</td>
      <td>{{data.blood_group}}</td>
      <td><button type="button" class="btn btn-danger" @click="deleteStudent" :value="data.student_id">Delete</button></td>
      <td><NLink :to="{name:'student-id',params:{id:data.student_id}}">
      <button type="button" class="btn btn-success">Edit</button> 
    </NLink></td>    
    </tr>
  </tbody>
</table>
<div class="container">
<form>
        
        <div class="row">
          <div class="col-sm">
            <input type="text" class="form-control" v-model="name" placeholder="Enter name">
          </div>
          <div class="col">
            <input type="text" class="form-control" v-model="email" placeholder="Enter email">
          </div>
          <div class="col">
            <input type="number" class="form-control" v-model="phone" placeholder="Enter Phone">
          </div>
        </div>
          <div class="row">
          <div class="col">
            <input type="text" class="form-control" v-model="gender" placeholder="Enter gender">
          </div>       
          <div class="col">
            <input type="text" class="form-control" v-model="religion" placeholder="Enter religion">
          </div>
          <div class="col">
            <input type="date" class="form-control" v-model="date_of_birth" placeholder="Enter Birth date">
          </div>
          </div>
        <div class="row">
          <div class="col">
            <input type="text" class="form-control" v-model="father_name" placeholder="Enter Father name">
          </div>
          <div class="col">         
                  <select v-model="blood_group" class="form-control">
                  <option :value="null">--Select--</option>
                  <option value="A+">A+</option>
                  <option value="A-">A-</option>
                  <option value="B+">B+</option>
                  <option value="B-">B-</option>
                  <option value="AB+">AB+</option>  
                  <option value="AB-">AB-</option>
                  <option value="O+">O+</option>
                  <option value="O-">O-</option>
                  <option value="Unknown">Unknown</option>
                  </select>
          </div> 
          <div class="col">
            <input type="text" class="form-control" v-model="mother_name" placeholder="Enter Mother Name">
          </div> 
        </div><br>
        <button type="submit" class="btn btn-primary" @click="addSubmit">Add</button>        
      </form>
    </div>
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
      studentData:null,
      name:null,
      email:null,
      phone:null,
      gender:null,
      religion:null,
      date_of_birth:null,
      father_name:null,
      blood_group: null,          
      mother_name: null,
      student_id:null
}
  },
  head: {
    title: 'User'
  }, 
  mounted(){
      axios.get('http://localhost/university/api/user/student/data').then(response => {
          this.studentData=response.data;
          //console.log(this.studentData);
      })
  },
   methods:{
       addSubmit:function(){
         axios.post("http://localhost/university/api/user/student/post",
          {
            name: this.name,
            email: this.email,
            phone: this.phone,
            gender: this.gender,
            religion: this.religion,
            date_of_birth: this.date_of_birth,
            father_name: this.father_name,
            blood_group: this.blood_group,          
            mother_name: this.mother_name          
          },
          { "Content-Type": "application/x-www-form-urlencoded" }
        )
        .then(response => {
           console.log(response.data);
        });
       },
       deleteStudent:function(e){        
         this.student_id=e.currentTarget.getAttribute("value");
         //alert(this.student_id);
         axios.post("http://localhost/university/api/user/student/delete",
          {
            student_id: this.student_id       
          },
          { "Content-Type": "application/x-www-form-urlencoded" }
        )
        .then(response => {
          console.log(response.data);
         // window.location.href="/student/index";
        });

       }

   }
}
</script>