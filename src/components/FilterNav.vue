<template>
  <nav class="filter-nav">
      <button @click="updateFilter('View All')" :class="{active: current === 'View All'}">View All</button>
      <button @click="updateFilter('Completed')" :class="{active: current === 'Completed'}">Completed</button>
      <button @click="updateFilter('Ongoing')" :class="{active: current === 'Ongoing'}">Ongoing</button>
  </nav>
</template>

<script>
export default {
    props:['current'],

methods:{
    updateFilter(by){
        this.$emit('changeFilter', by);
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