<template>   
    <div>       
        <div class="container" style="display: flex; justify-content: center; margin-top: 50px">
            <div class="row">
                <h3>{{fileList.bucketname}}</h3>
            </div>
        </div>
        <div class="container">
            <div class="row">
                <div class="col-4" style="height: 300px">
                    <div class="list-group" id="list-tab" role="tablist" style="display: flex; flex: wrap; height: 250px; overflow-y: auto">
                        <a v-for="(file, index) in fileList.files" :key="index" class="list-group-item list-group-item-action" data-toggle="list" :href="'#'+file.filename" role="tab">{{file.filename}}</a>
                    </div>
                </div>                
            </div>
        </div>
        <div class="container">
        <div class="tab-content" id="nav-tabContent">
            <div v-for="(file, index) in fileList.files" :key="index" class="tab-pane fade d-flex" :id="file.filename" role="tabpanel" aria-labelledby="list-home-list" style="flex-direction : column">
                <item :itemdetails="file"/>
            </div>
        </div>
        </div>
    
    </div>  
</template>

<script>
import item from './fileDetails'
export default {
    name: 'listfile',
    data() {
        return {

        }
    },
    props: ['fileList'],
    components: {
        item
    },
    created() {
        console.log('created')
        console.log(this.fileList)
    },
    mounted() {
        console.log('mounted')
        console.log(this.fileList)
    }
}
</script>

<style>

</style>
