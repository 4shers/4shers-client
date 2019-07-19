<template>
    <div>
        <div v-if="isLogin">
            <afterlogin :activeUser="activeUser" @logout="logout"/>
        </div>
        <div v-else>
            <loginpage @loginSuccess="loginSuccess" />
        </div>
    </div>
</template>

<script>
    import afterlogin from './components/afterlogin'
    import loginpage from './components/loginpage.vue'
    export default {
        data() {
            return {
                isLogin: false,
                message: 'Hello world',
                activeUser: ''
            }
        },
        components: {
            afterlogin,
            loginpage
        },
        methods: {
            loginSuccess(username) {
                this.isLogin = true
                this.activeUser = username
            },
            logout() {
                this.isLogin = false
            }
        }
    }
</script>

<style scoped>
</style>