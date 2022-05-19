<script>
    import CustomButton  from '@/components/SubmitButton.vue'

     export default {
        components: {
            CustomButton
        },
     }
</script>

<template>
    <div class="container mt-5">
        <div class="row justify-content-center">
            <div class="col-md-6">
                <div class="card">
                    <div class="card-header">
                        Login
                    </div>
                    <div class="card-body">
                        <form>
                            <div class="form-floating mb-3">
                                <input type="text" class="form-control" id="floatingInput" placeholder="name@example.com">
                                <label for="floatingInput">E-Mail / Nutzername</label>
                            </div>
                            <div class="form-floating">
                                <input type="password" class="form-control" id="floatingPassword" placeholder="Password">
                                <label for="floatingPassword">Passwort</label>
                            </div>
                            <div class="mt-4 justify-content-end d-flex">
                                <CustomButton label="Anmelden"></CustomButton>
                            </div>
                        </form>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>