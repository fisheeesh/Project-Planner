<template>
    <div class="home">
        <h1>This is Home Page</h1>
        <div v-for="project in projects" :key="project.id">
            <SingleProject :project="project"></SingleProject>
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
    }
}
</script>

<style>

</style>