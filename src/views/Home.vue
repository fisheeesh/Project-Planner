<template>
    <div class="home">
        <h1>Home</h1>
        <FilterNav @filterValue="current = $event" :current="current"></FilterNav>
        <div v-for="project in projects" :key="project.id">
            <SingleProject :project="project" @delete="deleteProject" @update="updateProject"></SingleProject>
        </div>
    </div>
    {{ current }}
</template>

<script>
import FilterNav from '../components/FilterNav'
import SingleProject from '../components/SingleProject'
export default {
  components: {
    FilterNav, SingleProject },
    data(){
        return{
            projects : [],
            current : 'all'
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
        },
        updateProject(id){
            let findProject = this.projects.find(project => project.id === id)
            findProject.complete = !findProject.complete
        }
    }
}
</script>

<style>

</style>