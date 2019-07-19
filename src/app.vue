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
        },
        created: function() {
            console.log('here')
            if (localStorage.getItem('token')) {
                axios({
                    url: 'http://localhost:3000/buckets/userBucket',
                    method: 'get',
                    headers: {
                        token: localStorage.getItem('token')
                    }
                })
                .then( ({data}) => {
                    this.isLogin = true
                })
                .catch( (err) => {
                    console.log(err)
                })
            } else {
                console.log('gaada token')
            }
        }
    }
</script>

<style scoped>
</style>