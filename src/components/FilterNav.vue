<template>
  <nav class="filter-nav">

           <!-- conditional classs sets to active when current is equal to updateFilter() -->
    <button @click="updateFilter('all')" :class="{active: current === 'all'}"> View All</button>
    <button @click="updateFilter('completed')" :class="{active: current === 'completed'}"> Completed</button>
    <button @click="updateFilter('ongoing')" :class="{active: current === 'ongoing'}"> On going</button>
  </nav>
</template>

<script>
export default {
// accept current prop from HomeView
    props:['current'], 
    methods:{
        updateFilter(by){
            this.$emit('filterChange', by)
        }
    }
}
</script>

<style>

.filter-nav button {
    background: none;
    border: none;
    color: #bbb;
    outline: none;
    font-size: 12px;
    text-transform: uppercase;
    margin-right: 10px;
    letter-spacing: 1px;
    font-weight: bold;
    cursor: pointer;
}

.filter-nav button.active {
    color: #555;
}

</style>