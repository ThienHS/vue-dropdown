<template>
  <div class="selected">
    <div
      class="selected-item"
      v-for="selectedLocation in selectedLocations"
      :key="selectedLocation.id"
    >
      <span class="selected-item__name">{{ selectedLocation.name }}</span>
      <i @click="$emit('deleteLocation', selectedLocation.id)">
        <svg
          width="12"
          height="12"
          viewBox="0 0 12 12"
          fill="none"
          xmlns="http://www.w3.org/2000/svg"
        >
          <path
            d="M0.5 0.5L11.5 11.5M11.5 0.5L0.5 11.5"
            stroke="#666666"
            stroke-linecap="round"
            stroke-linejoin="round"
          />
        </svg>
      </i>
    </div>
  </div>
</template>

<script>
export default {
  name: "Selected",
  props: {
    selectedLocations: Array,
  },
};
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

.selected-item {
  display: inline-flex;
  justify-content: space-between;
  align-items: center;
  min-width: 104px;
  width: 135px;
  min-height: 32px;
  background: #f8f8f8;
  border-radius: 32px;
  font-size: 16px;
  color: #333;
  line-height: 24px;
  margin-bottom: 4px;
  margin-left: 4px;
  padding: 4px 4px 4px 16px;
}

.selected-item__name {
  margin-right: 5px;
  min-width: 84px;
  min-height: 24px;
  text-align: center;
}

i {
  padding: 0 4px;
  cursor: pointer;
}
</style>
