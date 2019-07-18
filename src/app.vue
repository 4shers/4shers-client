<template>
    <loginpage/>
</template>

<script>
    import navbar from './components/navbar.vue'
    import loginpage from './components/loginpage.vue'
    export default {
        data() {
            return {
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