<template>
    <div class="project" :class="{complete : project.complete}">
        <div class="flexing">
            <div>
                <h3 @click="showDetail">{{ project.title }}</h3>
            </div>
            <div>
                <span class="material-icons" @click="deleteProject">delete</span>
                <router-link :to="{name : 'editProject', params : {id : project.id}}">
                    <span class="material-icons">edit</span>
                </router-link>
                <span class="material-icons" @click="updateProject" :class="{done : project.complete, undone : !project.complete}">done</span>
            </div>
        </div>
        <p v-if="isShow">{{ project.projectDetail }}</p>
    </div>
</template>

<script>
export default {
    data() {
        return {
            isShow: false,
            api : 'http://localhost:3000/projects/'
        }
    },
    props: [
        'project'
    ],
    methods: {
        showDetail() {
            this.isShow = !this.isShow
        },
        deleteProject(){
            let deleteRoute = this.api + this.project.id
            fetch(deleteRoute, {method : "DELETE"})
            .then(()=> this.$emit('delete', this.project.id))
            .catch(error => console.log(error))
        },
        updateProject(){
            let updateRoute = this.api + this.project.id
            fetch(updateRoute, {
                method : "PATCH",
                headers : {"Content-Type" : "application/json"},
                body : JSON.stringify({
                    complete : !this.project.complete
                })
            })
            .then(()=> this.$emit('update', this.project.id))
            .catch(error => console.log(error))
        }
    }
}
</script>
<style>
.project {
    padding: 20px;
    background-color: white;
    margin: 10px;
    border-left: 6px solid crimson;
    border-radius: 8px 0 0 5px;
}

h3 {
    color: indigo;
    cursor: pointer;
}
.flexing{
    display: flex;
    justify-content: space-between;
    align-items: center;
}
span{
    margin-left: 6px;
}
span:hover{
    color:  #777;
    cursor: pointer;
}
.complete{
    border-left: 6px solid green;
}
.done{
    color: green;
}
.undone{
    color: crimson;
}

</style>