<template>
    <div>
        <h1 v-if="isLogin">Setelah login</h1>
        <loginpage v-if="!isLogin"/>
        <itemdetails v-if="isLogin"/>
    </div>
    
</template>

<script>
    import navbar from './components/navbar.vue'
    import loginpage from './components/loginpage.vue'
    import item from './components/fileDetails.vue'
    export default {
        data() {
            return {
                isLogin: false,
                message: 'Hello world'
            }
        },
        components: {
            navbar,
            loginpage,
            item
        },
    }
</script>

<style scoped>
</style>