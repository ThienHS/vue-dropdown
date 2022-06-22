<template>
  <div class="selected">
    <div
      class="item"
      v-for="selectedLocation in selectedLocations" 
      :key="selectedLocation.id"
    >
      <span class="item-name" >{{selectedLocation.name}}</span>
      <FontAwesome icon="xmark" @click="$emit('deleteLocation', selectedLocation.id)" />
    </div>
  </div>
</template>

<script>
export default {
    name: 'Selected',
    props: {
      selectedLocations: Array
    },
}
</script>

<style scoped>
.selected {
    margin-top: 8px;
    width: 480px;
    min-height: 48px;
    background-color: #fff;
    border: 1px solid #999999;
    border-radius: 4px;
    padding: 8px 8px 4px 4px;
    display: flex;
    flex-wrap: wrap;
    align-items: center;
}

.item {
    display: inline-flex;
    justify-content: space-between;
    align-items: center;
    min-width: 104px;
    min-height: 32px;
    background: #F8F8F8;
    border-radius: 32px;
    font-size: 16px;
    color: #333;
    line-height: 24px;
    margin-bottom: 4px;
    margin-left: 4px;
    padding: 4px 10px 4px 16px;
}

.item-name {
  margin-right: 5px;
}

</style>