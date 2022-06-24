<template>
  <div id="wrapper">
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
      <ul class="list">
        <li v-for="location in data" :key="location.id" class="list-item">
          <label :for="location.id">
            <input
              :id="location.id"
              type="checkbox"
              :value="location"
              v-model="selectedLocations"
            />
            <img
              class="list-item__uncheckedmarkimg"
              src="../assets/img/uncheckedmark.png"
              alt="unchecked"
            />
            <img
              class="list-item__checkedmarkimg"
              src="../assets/img/checkedmark.png"
              alt="checked"
            />
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

    <div class="selected">
      <div
        class="selected-item"
        v-for="acceptedLocation in acceptedLocations"
        :key="acceptedLocation.id"
      >
        <span class="selected-item__name">{{ acceptedLocation.name }}</span>
        <i @click="handleDeleteLocation">
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
  </div>
</template>

<script>
export default {
  name: "Options",
  props: {
    data: Array,
    hideDropdown: Boolean,
  },
  data() {
    return {
      selectedLocations: [],
      acceptedLocations: [],
      isBtnActive: false,
      isDropdown: false,
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
    isDropdown(isDropdown) {
      if (isDropdown) {
        document.addEventListener("click", this.handleCloseIfClickOutside);
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

      this.$emit("setAcceptedLocations", this.acceptedLocations);
    },
    handleDeleteLocation(locationId) {
      const index = this.acceptedLocations.findIndex(
        (location) => location.id === locationId
      );
      this.selectedLocations.splice(index, 1);
      this.acceptedLocations = [...this.selectedLocations];

      this.$emit("updateAcceptedLocations", this.acceptedLocations);
    },
    handleCloseIfClickOutside(e) {
      if (!document.getElementById("wrapper").contains(e.target)) {
        this.isDropdown = false;
        this.selectedLocations = this.acceptedLocations;

        removeEventListener("click", this.handleCloseIfClickOutside);
      }
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

  .list {
    height: 270px;
    overflow-y: auto;

    &-item {
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

      input[type="checkbox"] {
        appearance: none;
      }

      input[type="checkbox"]:checked ~ .list-item__checkedmarkimg {
        display: block;
      }

      input[type="checkbox"]:checked ~ .list-item__uncheckedmarkimg {
        display: none;
      }

      &:hover {
        background-color: #e7f1fd;
      }

      span {
        margin-left: 12px;
      }

      &__checkedmarkimg {
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
