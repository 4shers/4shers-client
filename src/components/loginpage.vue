<template>
	<div class="container">
		<!-- Login -->
		<div v-if="whichForm" class="row" style="text-align: center; padding: 150px">
			<form id="formLogin" style="margin-left: auto; margin-right: auto; margin-top: auto; margin-bottom: auto;">
				<h5><strong>FOX</strong><i>shared</i></h5>
				<br>
				<div class="form-group" style="width: 650px;">
						<label for="username">Username</label>
						<input type="email" class="form-control" id="email" aria-describedby="usernameHelp" v-model="email" placeholder="Email">
						<small id="userameHelp" class="form-text text-muted">Insert Your Email Here.</small>
				</div>
				<div class="form-group" style="width: 650px;">
						<label for="password">Password</label>
						<input type="password" class="form-control" id="password" v-model="password" placeholder="Password">
				</div>
		
				<button type="submit" class="btn btn-primary" style="margin-left: auto; margin-right: auto; background: #E9ECEF; color: black; border: #E9ECEF; left: 22px" @click.prevent="login">Submit</button><br>
				<button @click.prevent="switchForm()" type="button" class="btn btn-link" data-toggle="modal" data-target="#formregister" aria-expanded="false">Or register here?</button>
				<br>
			</form>
		</div>
		<!-- Register -->
		<div v-if="!whichForm" class="row" style="text-align: center; padding: 150px">
			<form id="formLogin" style="margin-left: auto; margin-right: auto; margin-top: auto; margin-bottom: auto;">
				<h5><strong>FOX</strong><i>shared</i></h5>
				<br>
				<div class="form-group" style="width: 650px;">
					<label for="fullname">Fullname</label>
					<input type="text" class="form-control" id="fullname" v-model="fullname" placeholder="Full Name">
				</div>
				<div class="d-flex justify-content-space-between" style="flex-direction : row">
					<div style="width : 100%; margin-right : 10px">
						<label for="username">Username</label>
						<input type="text" class="form-control" id="username" v-model="username" placeholder="Username">
					</div>
					<div style="width : 100%; margin-left : 10px">
						<label for="email">Email</label>
						<input type="text" class="form-control" id="email" v-model="email" placeholder="Email">
					</div>
				</div>
				<div class="form-group" style="width: 650px;">
					<label for="password">Password</label>
					<input type="password" class="form-control" id="password" v-model="password" placeholder="Password">
				</div>
		
				<button type="submit" class="btn btn-primary" style="margin-left: auto; margin-right: auto; background: #E9ECEF; color: black; border: #E9ECEF; left: 22px" @click.prevent="register">Submit</button><br>
				<button @click.prevent="switchForm()" type="button" class="btn btn-link" aria-expanded="false">Already have an account?</button>
				<br>
			</form>
		</div>
	</div>
</template>

<script>
import Swal from 'sweetalert2';
export default {
	name: 'loginpage',
	data() {
		return {
			whichForm : true,
			email: '',
			password: '',
			username: '',
			fullname: ''
		}
	},
	methods: {
		login() {
			axios({
				method: 'POST',
				url: 'http://localhost:3000/users/signin',
				data: {
					email : this.email,
					password : this.password
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
					title: 'Signed in successfully',
					customClass: 'fadeIn'
				})
				localStorage.setItem('token', data.token)
				this.$emit('loginSuccess', data.fullname)
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
		},
		switchForm() {
			this.whichForm = !this.whichForm
			this.reset()
		},
		reset() {
			this.email = ''
			this.password = ''
			this.username = ''
			this.fullname = ''
		}
		,
		register() {
			axios({
				method: 'POST',
				url: 'http://localhost:3000/users/signup',
				data: {
					fullname : this.fullname,
					username : this.username,
					email : this.email,
					password : this.password
				}
			})
			.then(({ data }) => {
				this.switchForm()
				Swal.fire({
					toast: true,
					position: 'top-end',
					showConfirmButton: false,
					timer: 3000,
					type: 'success',
					title: 'Account Created',
					customClass: 'fadeIn'
				})
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
