<template>
    <div class="w-25">
        <input v-model="name" type="text" placeholder="Name" class="form-control mt-3 mb-3">
        <input v-model="email" type="email" placeholder="Email" class="form-control mb-3">
        <input v-model="password" type="password" placeholder="Password" class="form-control mb-3">
        <input v-model="password_confirmation" type="password" placeholder="Password confirmation"
               class="form-control mb-3">
        <input @click.prevent="register" type="submit" value="Registration" class="btn btn-outline-dark mb-3">
    </div>
</template>

<script>
export default {
    name: "Registration",

    data() {
        return {
            name: null,
            email: null,
            password: null,
            password_confirmation: null,
        }
    },

    methods: {
        register() {
            axios.get('/sanctum/csrf-cookie')
                .then(response => {
                    axios.post('/register',
                        {
                            name: this.name,
                            email: this.email,
                            password: this.password,
                            password_confirmation: this.password_confirmation
                        })
                        .then(res =>{
                            localStorage.setItem('x_xsrf_token', res.config.headers['X-XSRF-TOKEN'])
                            this.$router.push({name: 'user.personal'})
                        })
                })
        }
    }
}
</script>

<style scoped>

</style>
