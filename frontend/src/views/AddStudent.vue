<template>
    <main>
        <Navbar />
        <div class="my-5">
            <div class="mx-auto w-25 " style="max-width:100%;">
              <h2 class="text-center mb-3 fs-3">Add Student</h2>
              <form @submit.prevent="addStudent">
                <div class="row">
                  <div class="col-md-12 form-group mb-3">
                    <label for="name" class="form-label">Name</label>
                    <input id="name"  type="text" name="name" class="form-control" placeholder="Name" required v-model="student.name">
                  </div>
                </div>
                
                <div class="row">
                    <div class="col-md-12 form-group mb-3">
                      <label for="email" class="form-label">Email</label>
                      <input id="email" type="email"  name="email" class="form-control" placeholder="email" required v-model="student.email" >
                    </div>
                  </div>

                <div class="row">
                    <div class="col-md-12 form-group mb-3">
                      <label for="rollNo" class="form-label">Roll Number</label>
                      <input id="pNo" type="text"  name="rollNo" class="form-control" placeholder="Roll Number" required v-model="student.rollNo" >
                    </div>
                  </div>
               
                <div class="row">
                  <div class="col-md-12 form-group">
                    <input class="btn btn-primary w-100" type="submit" value="Submit">
                  </div>
                </div>

              </form>
        
            </div>
          </div>
    </main>
</template>


<script>
import Navbar from '../components/Navbar.vue';

    export default {
        name: 'AddStudent',
        components: {
            Navbar
        },

        data() {
            return {
                student : {
                    name: '',
                    email: '',
                    rollNo: ''
                }
            }
        },

        methods: {
            addStudent(){
                fetch('http://localhost:8080/add', {
                    method: 'POST',
                    headers: {
                        'Content-Type': 'application/json'
                    },
                    body: JSON.stringify(this.student)
                })
                .then(data => {
                    console.log(data)
                    this.$router.push("/");
                })

            }
        },
    }
</script>