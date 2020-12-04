<template>
  <div>
    <div class="container">
     <form>
        <div class="row">
          <div class="col-sm">
            <input type="text" class="form-control" v-model="studentName" placeholder="Enter name">
          </div>
          <div class="col">
            <input type="text" class="form-control" v-model="studentEmail" placeholder="Enter email">
          </div>
          <div class="col">
            <input type="number" class="form-control" v-model="studentPhone" placeholder="Enter Phone">
          </div>
        </div>
          <div class="row">
          <div class="col">
            <input type="text" class="form-control" v-model="studentGender" placeholder="Enter gender">
          </div>       
          <div class="col">
            <input type="text" class="form-control" v-model="studentReligion" placeholder="Enter religion">
          </div>
          <div class="col">
            <input type="date" class="form-control" v-model="studentBirth" placeholder="Enter Birth date">
          </div>
          </div>
        <div class="row">
          <div class="col">
            <input type="text" class="form-control" v-model="studentfather_name" placeholder="Enter Father name">
          </div>
          <div class="col">         
                  <select v-model="studentblood_group" class="form-control">
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
            <input type="text" class="form-control" v-model="studentmother_name" placeholder="Enter Mother Name">
          </div> 
        </div><br>
          <button type="submit" class="btn btn-primary" @click="updateSubmit">Update</button>         
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
    studentId:null,
    studentName:null,
    studentPhone:null,
    studentGender:null,
    studentReligion:null,
    studentBirth:null,
    studentfather_name:null,
    studentblood_group:null,
    studentmother_name:null,
    studentEmail:null
}
  },
       
  mounted(){
      axios.get('http://localhost/university/api/user/student/index/' + this.$route.params.id).then(response => {
       this.studentId=response.data.student_id;
       this.studentName=response.data.name;
       this.studentEmail=response.data.email;
       this.studentPhone=response.data.phone;
       this.studentGender=response.data.gender;
       this.studentReligion=response.data.religion;
       this.studentBirth=response.data.date_of_birth;
       this.studentfather_name=response.data.father_name;
       this.studentblood_group=response.data.blood_group;
       this.studentmother_name=response.data.mother_name;
          console.log(response.data);
      })
  },
 methods:{
       updateSubmit:function(){
         axios.post("http://localhost/university/api/user/student/update",
          {
            id: this.studentId,
            name: this.studentName,
            phone: this.studentPhone,
            gender: this.studentGender,
            religion: this.studentReligion,
            date_of_birth: this.studentBirth,
            father_name: this.studentfather_name,
            blood_group: this.studentblood_group,
            mother_name: this.studentmother_name,
            email: this.studentEmail      
          },
          { "Content-Type": "application/x-www-form-urlencoded" }
        )
        .then(response => {
           //alert(response.data);
           window.location.href="/student/"+this.$route.params.id;
        });
       }
       
   }
   }

</script>