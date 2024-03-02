<template>
    <main>
        <Navbar/>
        <div class="container">
            <div class="row">
                <div class="col-md-12">
                    <h1 class="text-center fs-3">View Students</h1>
                    <table class="table">
                        <thead>
                          <tr>
                            <th scope="col">Id</th>
                            <th scope="col">Name</th>
                            <th scope="col">Email</th>
                            <th scope="col">Roll No</th>
                          </tr>
                        </thead>
                        <tbody>
                          <tr v-for="student in students" :key="student.id">
                            <th scope="row">{{student.id}}</th>
                            <td>{{student.name}}</td>
                            <td>{{student.email}}</td>
                            <td>{{student.rollNo}}</td>
                            <td>
                              <a class="btn btn-primary" :href="`/student/${student.id}`"> ✎</a>
                              <button class="btn btn-danger mx-2" @click="deleteStudent(student.id)">✘</button>
                            </td>
                          </tr>
                        </tbody>
                      </table>
                    
                      <a href="/add" class="btn btn-primary">Add Student</a>
                </div>
            </div>
        </div>
    </main>
</template>

<script>
import Navbar from '../components/Navbar.vue'

export default{
    name : 'ViewStudents',
    components: {
        Navbar
    },
    data(){
        return{
            students:[]
        }
    },
    beforeMount(){
            this.getStudents()
    },
    
    methods:{
        getStudents(){
            fetch('http://localhost:8080/students')
            .then(response=>response.json())
            .then(data=>{
                this.students = data
                console.log(data);
            })
        },
        deleteStudent(id){
            fetch(`http://localhost:8080/student/${id}`,
            {
                method: 'DELETE'
            }).then(data=>{
                console.log(data);
                this.getStudents()
            })
        }
    }
}
</script>