<script>
    import CustomButton  from '@/components/SubmitButton.vue'
    import axios from 'axios'
    export default {
        components: {
            CustomButton
        },
         data() {
            return {
                url: import.meta.env.VITE_API_URL,
                userInfo: [], 
                errors: []
            }
        },
        methods: {
            doSomething(){
                axios.get(this.url  + '/listMembers').then(response => {
                    this.userInfo = response.data
                }).catch(errors => {
                    console.log(errors)
                });
            },
        },
        created() { 
            this.doSomething() 
        }
    }
</script>


<template>
    <div class="container mt-5">
        <div class="row">
            <div class="col-md-12">
                <div class="card">
                    <div class="card-body">
                        <div class="row">
                            <div class="col-md-6">
                                <div class="d-flex">
                                    <input type="text" name="" inputmode="number" id="" class="form-control">
                                     <CustomButton
                                        @click="doSomething()"
                                        theme="secondary"
                                        label="Anmelden" />
                                </div>
                            </div>
                            <div class="col-md-6">
                                <div class="table-responsive">
                                    <table class="table">
                                        <thead>
                                            <tr>
                                                <th>Name</th>
                                                <th>Pers. Nummer</th>
                                                <th>Status</th>
                                            </tr>
                                        </thead>
                                        <tbody>
                                           <tr v-for="user in userInfo" :key="user.id">
                                                <td>{{ user.name }}</td>
                                                <td>{{ user.personal_number }}</td>
                                                <td>{{ user.status }}</td>
                                            </tr>
                                        </tbody>
                                    </table>
                                </div>
                            </div>
                        </div>   
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>