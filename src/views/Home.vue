<template>
    <div class="home">
        <h1>Home</h1>
        <FilterNav @filterValue="current = $event" :current="current"></FilterNav>
        <div v-if="projects.length > 0">
            <div v-for="project in filteredProjects" :key="project.id">
                <SingleProject :project="project" @delete="deleteProject" @update="updateProject"></SingleProject>
            </div>
        </div>
        <div v-else>
            <h2>No Projects Found.</h2>
        </div>

    </div>
</template>

<script>
import FilterNav from '../components/FilterNav'
import SingleProject from '../components/SingleProject'
export default {
    components: {
        FilterNav, SingleProject
    },
    data() {
        return {
            projects: [],
            current: 'all'
        }
    },
    mounted() {
        fetch('http://localhost:3000/projects')
            .then(response => response.json())
            .then(datas => this.projects = datas)
            .catch(error => console.log(error))
    },
    methods: {
        deleteProject(id) {
            this.projects = this.projects.filter(project => project.id != id)
        },
        updateProject(id) {
            let findProject = this.projects.find(project => project.id === id)
            findProject.complete = !findProject.complete
        }
    },
    computed: {
        filteredProjects() {
            if (this.current === 'ongoing') {
                return this.projects.filter(project => !project.complete)
            }
            if (this.current === 'completed') {
                return this.projects.filter(project => project.complete)
            }
            return this.projects
        }
    }
}
</script>

<style>
h2{
    color: #777;
    text-align: center;
    margin-top: 100px;
}
</style>