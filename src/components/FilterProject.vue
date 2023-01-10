<template>
  <div class="filter-nav">
      <button @click="updateFilter('all')" :class="{active: current === 'all'}">All</button>
      <button @click="updateFilter('complated')" :class="{active: current === 'complated'}">Complated</button>
      <button @click="updateFilter('ongoing')" :class="{active: current === 'ongoing'}">Ongoing</button>
  </div>
</template>

<script>
export default {
    name: 'FilterProject',
    props: ['current'],
    data(){
        return {}
    },
    methods: {
        updateFilter(by){
            this.$emit('filterChange', by);
        }
    }
}
</script>

<style>

.filter-nav button{
    background-color: none;
    border: none;
    color :#bbb;
    outline: none;
    font-size: 12px;
    text-transform: uppercase;
    margin-right: 10px;
    letter-spacing: 1px;
    font-size: bold;
    font-weight: bold;
    cursor: pointer;
}

.filter-nav button.active {
    color: #555;
}

</style>