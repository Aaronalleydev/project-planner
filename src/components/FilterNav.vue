<template>
  <nav class="filter-nav">
    <button 
    @click="updateFilter('all')"
    :class="{ active: current === 'all' }" 
    >View All
    </button>
    <button 
    @click="updateFilter('complete')" 
    :class="{ active: current === 'complete' }" 
    >Completed
    </button>
    <button 
    @click="updateFilter('uncomplete')" 
    :class="{ active: current === 'uncomplete' }" 
    >Uncomplete
    </button>
  </nav>
</template>

<script>
export default {
  props: [ 'current'],
  methods: {
    updateFilter(by) {
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