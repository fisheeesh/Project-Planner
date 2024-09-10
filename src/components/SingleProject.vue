<template>
    <div class="project" @click="showDetail">
        <h3>{{ project.title }}</h3>
        <div v-if="isShow">
            <p>{{ project.projectDetail }}</p>
        </div>
    </div>
</template>

<script>
export default {
    data(){
        return{
            isShow : false
        }
    },
    props: [
        'project'
    ],
    methods: {
        showDetail(){
            this.isShow = !this.isShow
        }
    }
}
</script>
<style>
.project{
    padding: 20px;
    background-color: #f2f2f2;
    cursor: pointer;
    margin: 10px;
}
h3{
    color: indigo;
}
</style>