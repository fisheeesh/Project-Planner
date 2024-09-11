<template>
  <h1>Edit Project</h1>
  <form>
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
    }
}
</script>

<style>

</style>