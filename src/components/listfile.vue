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
                        <a v-for="file in fileList.files" :key="file" class="list-group-item list-group-item-action" data-toggle="list" :href="'#'+file" role="tab">{{file}}</a>
                    </div>
                </div>
                <div class="col-8">
                    <div class="tab-content" id="nav-tabContent">
                        <div v-for="file in fileList.files" :key="file" class="tab-pane fade" :id="file" role="tabpanel" aria-labelledby="list-home-list">
                            {{file}} expanded
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>  
</template>

<script>
export default {
    name: 'listfile',
    data() {
        return {

        }
    },
    props: ['fileList'],
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
