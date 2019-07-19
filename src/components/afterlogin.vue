<template>
    <nav class="navbar navbar-expand-lg navbar-light bg-light">
            <a class="navbar-brand" href="#" onClick="history.go(0)"><strong>FOX</strong><i>shared</i></a>

            <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarNavDropdown" aria-controls="navbarNavDropdown" aria-expanded="false" aria-label="Toggle navigation">
                <span class="navbar-toggler-icon"></span>
            </button>

            <div class="collapse navbar-collapse" id="navbarNavDropdown" style="position: absolute; right: 25px !important">
                <ul class="navbar-nav">
                    <li class="nav-item dropdown">
                        <a class="nav-link dropdown-toggle" href="#" id="navbarDropdownMenuLink" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
                            Profile
                        </a>
                        <div class="dropdown-menu right" aria-labelledby="navbarDropdownMenuLink">
                            <a class="dropdown-item" href="#" data-toggle="popover" title="Welcome!" data-trigger="hover" data-content="activeUser">Info</a>
                            <div class="dropdown-divider"></div>
                            <a class="dropdown-item" id="logout" href="#" @click.prevent="logout">Logout</a>
                        </div>
                    </li>
                    <li class="nav-item">
                        <a class="nav-link" href="#" data-toggle="modal" data-target="#form" aria-expanded="false" aria-controls="collapseExample">
                            Create project
                        </a>
                    </li>
                    
                    
                </ul>
            </div>

            <!-- Search -->
            <!-- <form id="formSearch" class="form-inline">
                <div class="input-group">
                    <div class="input-group-prepend">
                        <a type="submit"><span class="input-group-text" id="basic-addon1">@</span></a>
                    </div>
                    <input type="text" class="form-control" placeholder="Search" aria-label="Search" id="contentSearch" aria-describedby="basic-addon1">
                </div>
                <div class="form-group">
                <select class="form-control" id="tipeSearch">
                    <option value="project">Project</option>
                    <option value="todo">Todo</option>
                </select>
                </div>
            </form> -->

            <!-- Upload file modal -->
            <div class="modal fade" id="form" tabindex="-1" role="dialog" aria-labelledby="exampleModalLabel" aria-hidden="true">
                <div class="modal-dialog modal-dialog-centered" role="document">
                    <div class="modal-content">
                        <div class="modal-header border-bottom-0">
                            <h5 class="modal-title" id="exampleModalLabel">Upload file</h5>
                            <button type="button" class="close" data-dismiss="modal" aria-label="Close">
                            <span aria-hidden="true">&times;</span>
                            </button>
                        </div>
                        <form id="uploadFile">
                            <div class="modal-body">
                                <div class="form-group">
                                    <label for="filename">Filename: </label>
                                    <input type="text" class="form-control" id="filename" v-model="filename" placeholder="File name to upload">
                                </div>
                                <div class="form-group">
                                    <label for="bucket">Choose your bucket:</label>
                                    <select class="form-control" v-model="chosenbucket">
                                        <option v-for="(bucket, index) in buckets" :key="index">{{bucket.name}}</option>
                                    </select>
                                </div>
                            </div>
                            <div class="modal-footer border-top-0 d-flex justify-content-center">
                            <button type="submit" class="btn btn-light" style="border-color: #E9ECEF; position: absolute; right: 15px; bottom: 15px" data-dismiss="modal">Submit</button>
                            </div>
                        </form>
                    </div>
                </div>
            </div>
        </nav>
</template>

<script>
import Swal from 'sweetalert2';
export default {
    name: 'afterlogin',
    data() {
        return {
            filename: '',
            buckets: [],
            choosenbucket: '',
        }
    },
    props: ['activeUser'],
    methods: {
        logout() {
            localStorage.removeItem('token'),
            localStorage.removeItem('username'),
            this.$emit('logout')
            Swal.fire({
                toast: true,
                position: 'top-end',
                showConfirmButton: false,
                timer: 3000,
                type: 'success',
                title: 'Logged out',
                customClass: 'fadeIn'
            })
        }
    },
    mounted: {
        fetchbucket() {

        }
    }
}
</script>

<style>

</style>
