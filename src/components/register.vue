<template>
  <div class="container">
		<div class="row" style="text-align: center; padding: 150px">
			<form id="formLogin" style="margin-left: auto; margin-right: auto; margin-top: auto; margin-bottom: auto;">
				<h5><strong>FOX</strong><i>shared</i></h5>
				<br>
				<div class="form-group" style="width: 650px;">
          <label for="fullname">Fullname</label>
          <input type="text" class="form-control" id="fullname" v-model="fullname" placeholder="Full Name">
				</div>
        <div class="col-sm-6">
          <label for="username">Username</label>
          <input type="text" class="form-control" id="username" v-model="username" placeholder="Username">
        </div>
        <div class="col-sm-6">
          <label for="email">Email</label>
          <input type="text" class="form-control" id="email" v-model="email" placeholder="Email">
        </div>
				<div class="form-group" style="width: 650px;">
          <label for="password">Password</label>
          <input type="password" class="form-control" id="password" v-model="password" placeholder="Password">
				</div>
		
				<button type="submit" class="btn btn-primary" style="margin-left: auto; margin-right: auto; background: #E9ECEF; color: black; border: #E9ECEF; left: 22px" @click.prevent="login">Submit</button><br>
				<button @click.prevent="show-register" type="button" class="btn btn-link" data-toggle="modal" data-target="#formregister" aria-expanded="false">Or register here?</button>
				<br>
			</form>
		</div>
	</div>
</template>

<script>
import Swal from 'sweetalert2';
export default {
	name: 'registerpage',
	data() {
		return {
      fullname : '',
      username : '',
			email: '',
			password: '',
		}
	},
	methods: {
		register() {
			axios({
				method: 'POST',
				url: 'http://localhost:3000/users/signup',
				data: {
          fullname : this.fullname,
          username : this.username,
					email : this.email,
					password : this.password,
				},
				headers : {
					token : localStorage.token
				}
			})
			.then(({ data }) => {
				Swal.fire({
					toast: true,
					position: 'top-end',
					showConfirmButton: false,
					timer: 3000,
					type: 'success',
					title: 'Register Successful',
					customClass: 'fadeIn'
				})
				localStorage.setItem('token', data.token)
			})
			.catch((err) => {
				Swal.fire({
					showConfirmButton: false,
					timer: 3000,
					type: 'error',
					title: err.response.data.message,
					customClass: 'fadeIn'
				});
			})
		}
	}
}
</script>
<style>
</style>
