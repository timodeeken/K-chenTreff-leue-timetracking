<script>
    import CustomButton  from '@/components/SubmitButton.vue'
    import axios from 'axios'
    import { useToast } from "vue-toastification";
    export default {
        setup() {
            const toast = useToast();
            return { toast }
        },
        components: {
            CustomButton
        },
         data() {
            return {
                url: import.meta.env.VITE_API_URL,
                memberList: [], 
                errors: [],
                personal_number: null,
                baseUrl: import.meta.env.VITE_BASE_URL
            }
        },
        methods: {
            listMembers(){
                axios.get(this.url  + '/listMembers').then(response => {
                    this.memberList = response.data
                }).catch(errors => {
                    console.log(errors)
                });
            },
            checkInCheckOut(e){
                e.preventDefault(); 
                if(this.personal_number == null){
                    this.toast.error('Bitte gebe eine Personal Nummer an.');
                    this.personal_number = null
                    this.listMembers();
                    this.$refs.personal_number.focus();
                } else {
                    axios.post(this.url + '/checkInCheckOut/' + this.personal_number).then(response => {
                        this.listMembers();
                        this.personal_number = null
                        this.toast.success(response.data.message);
                    }).catch(errors => {
                        console.log(errors)
                    });
                }
            }
        },
        created() { 
            this.listMembers() 
        }
    }
</script>


<template>
    <div class="container mt-5">
        <div class="row mb-3">
            <div class="col-md-12">
                <div class="alert alert-danger">
                    <b>Achtung!</b>
                    <p>Absofort steht die neue Domain bereit. {{ baseUrl }}</p>
                    <p>Bei Fragen oder Problemen, bitte einfach kurz Anrufen.</p>
                </div>
            </div>
        </div>
        <div class="row">
            <div class="col-md-12">
                <div class="card">
                    <div class="card-header">
                        Zeiterfassung
                    </div>
                    <div class="card-body">
                        <div class="row">
                            <div class="col-md-7 mb-4">
                                <form v-on:submit="checkInCheckOut">
                                    <div class="form-floating mb-3">
                                        <input type="text" class="form-control" inputmode="numeric" autofocus v-model="personal_number" ref="personal_number" id="personal_number" name="personal_number" placeholder="Personal Nummer">
                                        <label for="personal_number">Personal Nummer</label>
                                    </div>
                                    <div class="mt-3 justify-content-end d-flex">
                                        <CustomButton label="Anmelden / Abmelden" />
                                    </div>
                                </form>
                            </div>
                            <div class="col-md-5">
                                <div class="table-responsive">
                                    <table class="table">
                                        <thead class="table-leue">
                                            <tr>
                                                <th>Name</th>
                                                <th>Pers. Nummer</th>
                                                <th>Status</th>
                                            </tr>
                                        </thead>
                                        <tbody>
                                           <tr v-for="member in memberList" :key="member.id">
                                                <td>{{ member.name }}</td>
                                                <td>{{ member.personal_number }}</td>
                                                <td v-html="member.status"></td>
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