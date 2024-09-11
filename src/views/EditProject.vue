<template>
  <h1>Edit Project</h1>
  <form @submit.prevent="updateProject">
    <label for="">Project Title</label>
    <input type="text" v-model="title">
    <label>Project Detail</label>
    <textarea name="" id="" v-model="detail"></textarea>
    <button>Update Project</button>
  </form>
</template>

<script>
export default {
    props : [
        'id'
    ],
    data(){
      return{
        title : "",
        detail : "",
      }
    },
    mounted(){
      fetch('http://localhost:3000/projects/' + this.id)
      .then(response => response.json())
      .then((datas)=>{
        this.title = datas.title
        this.detail = datas.projectDetail
      })
      .catch(error => console.log(error))
    },
    methods:{
      updateProject(){
        fetch('http://localhost:3000/projects/' + this.id, {
          method : "PATCH",
          headers : {"Content-Type" : "application/json"},
          body : JSON.stringify({
            title : this.title,
            projectDetail : this.detail
          })
        })
        .then(()=> this.$router.push({name : 'home'}))
      }
    }
}
</script>

<style>

</style>