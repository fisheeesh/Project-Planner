<template>
    <nav class="filter-nav">
        <button @click="filterBy('all')" :class="{active : current === 'all'}">ALL</button>
        <button @click="filterBy('ongoing')" :class="{active : current === 'ongoing'}">ONGOING</button>
        <button @click="filterBy('completed')" :class="{active : current === 'completed'}">COMPLETED</button>
    </nav>
</template>

<script>
export default {
    props : [
        'current'
    ],
    methods: {
        filterBy(value){
            this.$emit('filterValue', value)
        }
    }
}
</script>

<style>
.filter-nav button{
    background: none;
    border: none;
    color: #bbb;
    outline: none;
    font-size: 12px;
    text-transform: uppercase;
    margin: 0 10px;
    letter-spacing: 1px;
    font-weight: bold;
    cursor: pointer;
}
.filter-nav button.active{
    color: #00ce89;
}
</style>