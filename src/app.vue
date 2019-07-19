<template>
    <div>
        <h1 v-if="isLogin">Setelah login</h1>
        <loginpage v-if="!isLogin"/>
    </div>
    
</template>

<script>
    import navbar from './components/navbar.vue'
    import loginpage from './components/loginpage.vue'
    import register from './components/register.vue'
    export default {
        data() {
            return {
                isLogin: false,
                message: 'Hello world'
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