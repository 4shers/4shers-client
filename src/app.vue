<template>
    <div>
        <h1 v-if="isLogin">Setelah login</h1>
        <loginpage :kelogin="message" @darianak="ubahtext" v-if="!isLogin"/>
    </div>
    
</template>

<script>
    import navbar from './components/navbar.vue'
    import loginpage from './components/loginpage.vue'
    export default {
        data() {
            return {
                isLogin: false,
                message: 'Hello world'
            }
        },
        methods: {
            ubahtext(payload) {
                console.log(payload)
                this.message=payload.username
            }
        },
        components: {
            navbar,
            loginpage
        },
    }
</script>

<style scoped>
</style>