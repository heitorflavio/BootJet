<template>
    <div class="bg-gradient-primary" id="login">
        <div class="container">
            <div class="row justify-content-center">
                <div class="col-md-9 col-lg-12 col-xl-10">
                    <div class="card shadow-lg o-hidden border-0 my-5">
                        <div class="card-body p-0">
                            <div class="row">
                                <div class="col-lg-6 d-none d-lg-flex">
                                    <div class="flex-grow-1 bg-login-image"
                                        style="background-image: url(&quot;assets/img/dogs/image3.jpeg&quot;);"></div>
                                </div>
                                <div class="col-lg-6">
                                    <div class="p-5">
                                        <div class="text-center">
                                            <h4 class="text-dark mb-4">Welcome Back!</h4>
                                        </div>
                                        <div class="text-center" v-if="error">
                                            <div class="alert alert-danger" role="alert" v-for="error in error"
                                                :key="error">
                                                {{ error[0] }}
                                            </div>
                                        </div>
                                        <form @submit.prevent="submit()" class="user" ref="form">
                                            <div class="mb-3"><input class="form-control form-control-user" type="email"
                                                    required id="exampleInputEmail" aria-describedby="emailHelp"
                                                    placeholder="Enter Email Address..." name="email"></div>
                                            <div class="mb-3"><input class="form-control form-control-user" type="password"
                                                    required id="exampleInputPassword" placeholder="Password"
                                                    name="password"></div>
                                            <div class="mb-3">
                                                <div class="custom-control custom-checkbox small">
                                                    <div class="form-check"><input
                                                            class="form-check-input custom-control-input" type="checkbox"
                                                            id="formCheck-1"><label
                                                            class="form-check-label custom-control-label"
                                                            for="formCheck-1">Remember Me</label></div>
                                                </div>
                                            </div><button class="btn btn-primary d-block btn-user w-100"
                                                type="submit">Login</button>
                                            <hr><a class="btn btn-primary d-block btn-google btn-user w-100 mb-2"
                                                role="button"><i class="fab fa-google"></i>&nbsp; Login with Google</a><a
                                                class="btn btn-primary d-block btn-facebook btn-user w-100" role="button"><i
                                                    class="fab fa-facebook-f"></i>&nbsp; Login with Facebook</a>
                                            <hr>
                                        </form>
                                        <div class="text-center"><a class="small" href="forgot-password.html">Forgot
                                                Password?</a></div>
                                        <div class="text-center"><a class="small" href="register.html">Create an
                                                Account!</a></div>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import { Head, Link, useForm } from '@inertiajs/vue3';
export default {
    name: "Login",
    components: {
        Head,
        Link,
        useForm
    },
    data() {
        return {
            error: null
        }
    },
    methods: {
        submit() {
            axios.post(route('login'), this.$refs.form).then(() => {
                window.location = '/';
            }).catch((error) => {
                this.error = error.response.data.errors;
                console.log(this.error);
            });
        }
    }


}
</script>

<!-- <script setup>
import { Head, Link, useForm } from '@inertiajs/vue3';
import AuthenticationCard from '@/Components/AuthenticationCard.vue';
import AuthenticationCardLogo from '@/Components/AuthenticationCardLogo.vue';
import Checkbox from '@/Components/Checkbox.vue';
import InputError from '@/Components/InputError.vue';
import InputLabel from '@/Components/InputLabel.vue';
import PrimaryButton from '@/Components/PrimaryButton.vue';
import TextInput from '@/Components/TextInput.vue';

defineProps({
    canResetPassword: Boolean,
    status: String,
});

const form = useForm({
    email: '',
    password: '',
    remember: false,
});

const submit = () => {
    form.transform(data => ({
        ...data,
        remember: form.remember ? 'on' : '',
    })).post(route('login'), {
        onFinish: () => form.reset('password'),
    });
};
</script> -->

<style>
#app {
    height: 100vh;
}

#login {
    height: 100vh;
}
</style>