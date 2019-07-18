<template>
    <div class="container">
        <div class="row" style="text-align: center; padding: 150px">
            <form id="formLogin" style="margin-left: auto; margin-right: auto; margin-top: auto; margin-bottom: auto;">
                <h5><strong>FOX</strong><i>shared</i></h5>
                <br>
                <div class="form-group" style="width: 650px;">
                    <label for="username">Username</label>
                    <input type="text" class="form-control" id="username" aria-describedby="usernameHelp" placeholder="Username">
                    <small id="userameHelp" class="form-text text-muted">Your username.</small>
                </div>
                <div class="form-group" style="width: 650px;">
                    <label for="password">Password</label>
                    <input type="password" class="form-control" id="password" placeholder="Password">
                </div>
            
                <button type="submit" class="btn btn-primary" style="margin-left: auto; margin-right: auto; background: #E9ECEF; color: black; border: #E9ECEF; left: 22px">Submit</button><br>
                <button type="button" class="btn btn-link" data-toggle="modal" data-target="#formregister" aria-expanded="false">Or register here?</button>
                <br>
            </form>
        </div>
    </div>
</template>

<script>
export default {
    name: 'loginpage'
}
</script>

<style>

</style>
