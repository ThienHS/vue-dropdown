<template>
  <div class="wrapper">
    <div
      :class="{ options: true, active: isDropdown }"
      @click="handleOpenDropdown"
    >
      <span> Chọn tỉnh thành </span>
      <svg
        width="8"
        height="4"
        viewBox="0 0 8 4"
        fill="none"
        xmlns="http://www.w3.org/2000/svg"
      >
        <path d="M8 0H0L4 4L8 0Z" fill="#666666" />
      </svg>
    </div>
    <div v-if="isDropdown" class="dropdown">
      <ul class="dropdown-list">
        <li
          v-for="location in data"
          :key="location.id"
          class="dropdown-list__item"
        >
          <label :for="location.id">
            <input
              :id="location.id"
              type="checkbox"
              :value="location"
              v-model="selectedLocations"
            />
            <FontAwesome icon="check" />
            <span>
              {{ location.name }}
            </span>
          </label>
        </li>
      </ul>
      <div class="btns">
        <button
          :class="{ btns__accept: true, active: isBtnActive }"
          @click="handleSetAcceptedLocations"
        >
          Đồng ý
        </button>
        <button class="btns__cancel" @click="handleHideDropdown">Hủy</button>
      </div>
    </div>
    <Selected
      :selected-locations="acceptedLocations"
      @delete-location="handleDeleteLocation"
    />
  </div>
</template>

<script>
import Selected from "./Selected.vue";
export default {
  name: "Options",
  components: { Selected },
  props: {
    data: Array,
    hideDropdown: Boolean,
  },
  data() {
    return {
      selectedLocations: [],
      isBtnActive: false,
      isDropdown: false,
      acceptedLocations: [],
      isChecked: false,
    };
  },
  watch: {
    selectedLocations(newArr) {
      if (newArr.length > 0) {
        this.isBtnActive = true;
      }
    },
    acceptedLocations(newArr) {
      if (newArr.length > 0) {
        this.isBtnActive = true;
      } else {
        this.isBtnActive = false;
      }
    },
  },
  methods: {
    handleOpenDropdown() {
      this.isDropdown = true;
    },
    handleHideDropdown() {
      this.isDropdown = false;
      this.selectedLocations = this.acceptedLocations;
    },
    handleSetAcceptedLocations() {
      this.acceptedLocations = [...this.selectedLocations];
      this.isDropdown = false;
      this.isBtnActive = false;
    },
    handleDeleteLocation(locationId) {
      const index = this.acceptedLocations.findIndex(
        (location) => location.id === locationId
      );
      this.selectedLocations.splice(index, 1);
      this.acceptedLocations = [...this.selectedLocations];
    },
  },
};
</script>

<style lang="scss" scoped>
.options {
  width: 480px;
  height: 48px;
  background-color: #fff;
  border: 1px solid #999999;
  border-radius: 4px;
  color: #999999;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 16px 18px 16px 10px;
  user-select: none;

  &.active {
    border: 1px solid #007bc3;
    box-shadow: 0px 0px 8px rgba(0, 123, 195, 0.32);
  }
}

.dropdown {
  width: 480px;
  min-height: 304px;
  background: #ffffff;
  box-shadow: 0px 1px 8px rgba(102, 102, 102, 0.2);
  border-radius: 4px;
  padding: 8px 0 16px;
  user-select: none;

  &-list {
    height: 270px;
    overflow-y: auto;

    &__item {
      display: flex;
      align-items: center;
      width: 100%;
      background-color: #fff;
      transition: all ease-out 0.2s;
      position: relative;

      label {
        width: 100%;
        display: flex;
        align-items: center;
        padding: 11px 0px 11px 19px;
      }

      &:hover {
        background-color: #e7f1fd;
      }

      span {
        margin-left: 12px;
      }

      img {
        height: 24px;
        width: 24px;
      }

      svg {
        position: absolute;
        top: 15px;
        left: 22px;
        font-size: 14px;
        color: #fff;
        display: none;
      }
    }
  }

  button {
    border: none;
    border-radius: 4px;
    padding: 4px 19px;
    cursor: pointer;
    background-color: #fff;
  }

  .btns {
    padding: 16px 0 0 16px;

    &__accept {
      width: 104px;
      height: 32px;
      background-color: #dcdcdc;
      color: #fff;
      font-weight: 700;
      font-size: 16px;
      margin-right: 11px;
      pointer-events: none;

      &.active {
        background-color: #007bc3;
        pointer-events: initial;
      }
    }

    &__cancel {
      background-color: transparent;
      color: #007bc3;
      font-size: 16px;
      width: 82px;
      height: 24px;
    }
  }
}

input[type="checkbox"] {
  appearance: none;
  width: 18px;
  height: 18px;
  border: 1px solid #000;
  border-radius: 3px;
}

input[type="checkbox"]:checked {
  background-color: #45d1c9;
  border: 1px solid #45d1c9;
}

input[type="checkbox"]:checked ~ svg {
  display: block;
}
</style>
