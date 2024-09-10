<template>
    <div class="project" >
        <div class="flexing">
            <div>
                <h3 @click="showDetail">{{ project.title }}</h3>
            </div>
            <div>
                <span class="material-icons" @click="deleteProject">delete</span>
                <span class="material-icons">edit</span>
                <span class="material-icons">done</span>
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
            api : 'http://localhost:3000/projects'
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
            let deleteRoute = this.api + "/" + this.project.id
            fetch(deleteRoute, {method : "DELETE"})
            .then(()=> this.$emit('delete', this.project.id))
            .catch(error => console.log(error))
        }
    }
}
</script>
<style>
.project {
    padding: 20px;
    background-color: #f2f2f2;
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
</style>