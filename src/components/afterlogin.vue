<template>
    <div>
        <nav class="navbar navbar-expand-lg navbar-light bg-light">
            <a class="navbar-brand" href="#" onClick="history.go(0)"><strong>FOX</strong><i>shared</i></a>

            <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarNavDropdown" aria-controls="navbarNavDropdown" aria-expanded="false" aria-label="Toggle navigation">
                <span class="navbar-toggler-icon"></span>
            </button>

            <div class="collapse navbar-collapse" id="navbarNavDropdown" style="position: absolute; right: 25px !important">
                <ul class="navbar-nav">
                    
                    <li class="nav-item">
                        <a class="nav-link" href="#" data-toggle="modal" data-target="#form" aria-expanded="false" aria-controls="collapseExample">
                            Upload file
                        </a>
                    </li>

                    <li class="nav-item dropdown">
                        <a class="nav-link dropdown-toggle" href="#" id="navbarDropdownMenuLink" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
                            Profile
                        </a>
                        <div class="dropdown-menu dropdown-menu-right" aria-labelledby="navbarDropdownMenuLink">
                            <a class="dropdown-item" href="#" data-toggle="popover" title="Welcome!" data-trigger="hover" data-content="activeUser">Info</a>
                            <div class="dropdown-divider"></div>
                            <a class="dropdown-item" id="logout" href="#" @click.prevent="logout">Logout</a>
                        </div>
                    </li>
                    
                    
                </ul>
            </div>

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
                        <form id="uploadFile" >
                            <div class="modal-body">
                                <div class="form-group">
                                    <label for="filename">Filename: </label>
                                    <input type="text" class="form-control" id="filename" v-model="filename" placeholder="File name to upload">
                                    
                                </div>
                                <div class="form-group">
                                    <input type="text" class="form-control" id="bucketname" v-model="bucketname" placeholder="Bucket name to create">
                                </div>
                                <div class="form-group">
                                    <label for="bucket">Choose your bucket:</label>
                                    
                                    <select class="form-control" v-model="chosenbucket" required>
                                        <option v-for="(bucket, index) in buckets" :key="index" :value="bucket._id">{{bucket.bucketname}}</option>
                                    </select>

                                    <label style="margin-top: 10px">File
                                        <input type="file" id="file" ref="file" v-on:change="handleFileUpload()"/>
                                    </label>
                                </div>
                            </div>
                            <div class="modal-footer border-top-0 d-flex justify-content-center">
                            <button type="submit" class="btn btn-light" style="border-color: #E9ECEF; position: absolute; right: 15px; bottom: 15px" data-dismiss="modal" @click.prevent="upload">Submit</button>
                            </div>
                        </form>
                    </div>
                </div>
            </div>
        </nav>

        <div class="container">
            <div class="row">
                <!-- Search -->
                <form @submit.prevent="searchinfo" id="formSearch" class="form-inline" style="margin-top: 25px; margin-right: auto; margin-left: auto">
                    <div class="input-group" style="width: 400px;">
                        <div class="input-group-prepend">
                            <a type="submit"><span class="input-group-text" id="basic-addon1">@</span></a>
                        </div>
                        <input type="text" class="form-control" placeholder="Search" aria-label="Search" id="contentSearch" aria-describedby="basic-addon1">
                    </div>
                    <div class="form-group">
                    <select class="form-control" v-model="searchType">
                        <option value="Bucket" selected>Bucket</option>
                        <option value="File">File</option>
                    </select>
                    </div>
                </form>
            </div>
        </div>

        <div v-if="searched">
            <div class="container" style="display: flex; justify-content: center; margin-top: 50px">
                <div class="row">
                    <h3>Searched items</h3>
                </div>
            </div>
            <listfile :fileList="searchedFile"/>
        </div>

        <div v-else>
            <div class="container" style="display: flex; justify-content: center; margin-top: 50px">
                <div class="row">
                    <h3>My buckets</h3>
                </div>
            </div>
            <div class="container" style="display: flex ; flex-wrap: nowrap; overflow-x: auto;">                
                <div v-for="(bucket, index) in buckets" :key="index" @click.prevent="bucketDetail(bucket)" class="card" style="cursor: pointer; width: 13rem; height: auto; margin-bottom: 25px; margin-right: 5px; margin-left: 5px; flex: 0 0 auto">
                    <img class="card-img-top" src="https://static.thenounproject.com/png/29962-200.png" style="height: 50%; width: 50%; margin: 10px auto auto auto" alt="Card image cap">
                    <div class="card-body" style="margin: auto">
                        <h5 class="card-title">{{ bucket.bucketname }}</h5>
                    </div>
                </div>
            </div>
            
            <listfile v-if="bucketDetailClicked" :fileList="bucketinfo"/>
        </div>

    </div>
    
</template>

<script>
import Swal from 'sweetalert2'
import listfile from './listfile.vue'

export default {
    name: 'afterlogin',
    data() {
        return {
            bucketDetailClicked: false,
            searched: false,
            fileList: ['file1', 'file2', 'file3', 'file4', 'file5','file6', 'file7', 'file8', 'file9', 'file10'],
            fileUpload: '',
            searchType: '',
            searchedFile: [],
            filename: '',
            buckets: [],
            chosenbucket: '',
            bucketinfo: {},
            bucketname: '',
        }
    },
    props: ['activeUser'],
    components: {
        listfile
    },
    methods: {
        bucketDetail(bucket) {
            this.bucketinfo = bucket,
            this.bucketDetailClicked = true
        },
        searchinfo() {
            if (this.searchType == '') {
                Swal.fire({
                    toast: true,
                    position: 'top-end',
                    showConfirmButton: false,
                    timer: 3000,
                    type: 'error',
                    title: 'Choose search type!',
                    customClass: 'fadeIn'
                })
            } else {
                this.searched = true    
            }
        },
        handleFileUpload(){
            this.fileUpload = this.$refs.file.files[0];
        },
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
        },
        upload() {
            let formData = new FormData()
            formData.append('filepath', this.fileUpload)
            formData.append('filename', this.filename)
            formData.append('status', '')
            formData.append('bucketId', this.chosenbucket)
            console.log(formData)
            if (this.chosenbucket) {
                axios({
                    method: 'post',
                    url: 'http://localhost:3000/items',
                    data: formData,
                    config: {
                        headers: {
                            token: localStorage.getItem('token'),
                            'Content-Type': 'multipart/form-data',
                        }
                    },
                    headers: {
                        token: localStorage.getItem('token'),
                    }
                })
                .then( ({data}) => {
                    console.log(data)
                    this.fetchBucket()
                    Swal.fire({
                        toast: true,
                        position: 'top-end',
                        showConfirmButton: false,
                        timer: 3000,
                        type: 'success',
                        title: 'File uploaded',
                        customClass: 'fadeIn'
                    })
                })
                .catch( (err) => {
                    Swal.fire({
                        toast: true,
                        position: 'top-end',
                        showConfirmButton: false,
                        timer: 3000,
                        type: 'error',
                        title: 'Upload failed',
                        customClass: 'fadeIn'
                    })
                })
                
            } else {
                axios({
                    url: 'http://localhost:3000/buckets',
                    method: 'post',
                    headers: {
                        token: localStorage.getItem('token')
                    },
                    data: {
                        bucketname: this.bucketname
                    }
                }).then( ({data}) => {
                    axios.post('http://localhost:3000/items', formData, {
                        headers: {
                            token: localStorage.getItem('token'),
                            'Content-Type': 'multipart/form-data',
                            data: {
                                filename: this.filename,
                                status: '',
                                bucketId: data._id,
                            }
                        }
                    })
                    .then( ({data}) => {
                        console.log(data)
                        this.fetchBucket()
                        Swal.fire({
                            toast: true,
                            position: 'top-end',
                            showConfirmButton: false,
                            timer: 3000,
                            type: 'success',
                            title: 'File uploaded',
                            customClass: 'fadeIn'
                        })
                    })
                    .catch( (err) => {
                        Swal.fire({
                            toast: true,
                            position: 'top-end',
                            showConfirmButton: false,
                            timer: 3000,
                            type: 'error',
                            title: 'Upload failed',
                            customClass: 'fadeIn'
                        })
                    })
                })
            }
        },
        fetchBucket() {
            axios({
                method: 'get',
                url: 'http://localhost:3000/buckets/userBucket',
                headers: {
                    token: localStorage.getItem('token')
                }
            })
            .then( ({data})=> {
                this.buckets = data
                console.log(data)
            })
            .catch( (err) => {
                console.log(err)
            })
        }
    },
    created: function() {
        this.fetchBucket()
    }
}
</script>

<style>

</style>
