<template>
    <div class="registerPage">
        <div class="container">
            <div class="row">
                <div class="col-sm-4"></div>
                <div class="col-sm-4">
                    <div class="text-center">
                    </div>

                    <form class="mt-4">
                        <div class="a-box a-spacing-extra-large">
                            <div class="a-box-inner">
                                 <h1 class="a-spacing-small">Sign In</h1>
                                 <!-- Email  -->
                                 <div class="a-row a-spacing-base">
                                     <label for="ap_customer_name" class="a-form-label">Email</label>
                                     <input type="email" id="ap_customer_name" class="a-input-text form-control auth-autofocus auth-required-field auth-contact-verification-request-info" v-model="email"/>
                                 </div>
                                 <!-- Password  -->
                                 <div class="a-row a-spacing-base mt-2">
                                     <label for="ap_customer_name" class="a-form-label">Password</label>
                                     <input type="password" id="ap_customer_name" class="a-input-text form-control auth-autofocus auth-required-field auth-contact-verification-request-info" v-model="password"/>
                                     <div class="a-alert-container">
                                        <div class="a-alert-content">Password must be atleast 6 characters</div>
                                    </div>
                                 </div>
                                <!-- Button -->
                                <div class="a-row a-spacing-extra-large mb-4">
                                    <span class="a-button-primary">
                                        <span class="a-button-inner">
                                            <span class="btn btn-dark btn-small mt-4" @click="onLogin">Login</span>
                                        </span>
                                    </span>
                                    <div class="a-row a-spacing-top-medium a-size-small mt-4">
                                        <b>
                                            By creating an account, you agree to Handmade Happiness's
                                            <a href="#">Conditons of use</a> and 
                                            <a href="#">Privacy Notice</a>
                                        </b>
                                    </div>
                                </div>
                                <hr/>
                                <div class="a-row mb-4">
                                    <b>
                                        Dont have an account?
                                        <a href="/hh/signup" class="a-link-emphasis">Sign Up</a>
                                    </b>
                                </div>
                                 
                            </div>
                        </div>
                    </form>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    middleware: "auth",
    auth: "guest",
     data(){
         return{
             email: "",
             password: ""
         };
     },
     methods: {
         async onLogin() {
            try{
                this.$auth.loginWith("local", {
                        data: {
                            email: this.email,
                            password: this.password
                        }
                    });

                    this.$router.push("/");

            } catch(err){
                console.log(err);
            }
         }
     }
}
</script>