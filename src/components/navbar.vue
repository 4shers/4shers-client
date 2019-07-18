<template>
    <nav class="navbar navbar-dark bg-dark d-flex justify-content-space-between sticky-top">
          <div class="logo d-flex align-items-center">
            <img src="https://i.pinimg.com/originals/16/de/5f/16de5f8dd1ffe99f9e169a0605a960b3.png" width="60" height="60" class="d-inline-block align-top" alt="Hacktivox!">
            <a class="navbar-brand" href="#">
              Hacktivox
            </a>
          </div>
    
          <div class="logo d-flex align-items-center" style="position: absolute; right: 22px">
            <a v-if="!isLogin" class="navbar-brand" href="#" data-target="#signinModal" data-toggle="modal">Sign In</a>
            <a v-if="!isLogin" class="navbar-brand" href="#" data-target="#signupModal" data-toggle="modal">Sign Up</a>
          </div>
          <div class="logo d-flex align-items-center">
            <a v-if="isLogin" class="navbar-brand" href="#" data-dismiss="modal" @click.prevent="signout">Sign Out</a>
          </div>
    </nav>
</template>

<script>
export default {
    name: 'navbar'
}
</script>

<style>

</style>
