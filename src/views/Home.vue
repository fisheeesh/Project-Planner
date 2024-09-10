<template>
    <div class="home">
        <h1>Home</h1>
        <div v-for="project in projects" :key="project.id">
            <SingleProject :project="project" @delete="deleteProject"></SingleProject>
        </div>
    </div>
</template>

<script>
import SingleProject from '../components/SingleProject'
export default {
  components: { SingleProject },
    data(){
        return{
            projects : []
        }
    },
    mounted(){
        fetch('http://localhost:3000/projects')
        .then(response => response.json())
        .then(datas => this.projects = datas)
        .catch(error => console.log(error))
    },
    methods: {
        deleteProject(id){
            this.projects = this.projects.filter(project => project.id != id)
        }
    }
}
</script>

<style>

</style>