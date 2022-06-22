<template>
  <div :class="{'options-wrapper': true, active: isDropdown}" @click="openDropdown" >
    <span>
        Chọn tỉnh thành
    </span>
    <FontAwesome icon="caret-down"/>
  </div>
    <div v-if="isDropdown" class="dropdown-wrapper">
      <ul class="dropdown">
        <li v-for="location in locations" :key="location.id" >
            <label :for="location.id" class="item" >
                <input 
                  :id="location.id" 
                  type="checkbox" 
                  :value="location" 
                  v-model="selectedLocations"
                  
                />
                <FontAwesome icon="check" />
                <span>
                    {{location.name}}
                </span>
            </label>
        </li>
      </ul>
      <div class="btns">
        <button :class="{'accept-btn': true, active: isBtnActive}" @click="setAcceptedLocations">Đồng ý</button>
        <button class="cancel-btn" @click="hideDropdown">Hủy</button>
      </div>
  </div>
  <Selected :selected-locations="acceptedLocations" @delete-location="deleteLocation" />
</template>

<script>
import Selected from './Selected.vue'
export default {
    name: "Options",
    data() {
        return {
            locations: [
                { id: 1, name: "Hà Nội" },
                { id: 2, name: "Hưng Yên" },
                { id: 3, name: "Tp HCM" },
                { id: 4, name: "Nam Định" },
                { id: 5, name: "Thanh Hóa" },
                { id: 6, name: "Nghệ An" },
                { id: 7, name: "Quảng Bình" },
                { id: 8, name: "Quảng Trị" },
            ],
            selectedLocations: [],
            isBtnActive: false,
            isDropdown: false,
            acceptedLocations: [],
        };
    },
    methods: {
      openDropdown() {
        this.isDropdown = true
      },
      hideDropdown() {
        this.isDropdown = false
        this.selectedLocations = this.acceptedLocations
      },
      setAcceptedLocations() {
        this.acceptedLocations = [...this.selectedLocations]
        this.isDropdown = false
        this.isBtnActive = false
      },
      deleteLocation(locationId) {
        const index = this.acceptedLocations.findIndex(location => location.id === locationId)
        this.selectedLocations.splice(index, 1)
        this.acceptedLocations = [...this.selectedLocations]
      }
    },
    watch: {
      selectedLocations(newArr) {
        if(newArr.length > 0) {
          this.isBtnActive = true
        } 
      },
      acceptedLocations(newArr) {
        if(newArr.length > 0) {
          this.isBtnActive = true
        } else {
          this.isBtnActive = false
        }
      },
    },
    components: { Selected }
}
</script>

<style scoped>
.options-wrapper {
    width: 480px;
    height: 48px;
    background-color: #fff;
    border: 1px solid #999999;
    border-radius: 4px;
    color: #999999;
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 16px 22px 16px 10px;
}

.options-wrapper.active {
  border: 1px solid #007BC3;
box-shadow: 0px 0px 8px rgba(0, 123, 195, 0.32);
}

.dropdown-wrapper {
    width: 480px;
    min-height: 304px;
    background: #FFFFFF;
    box-shadow: 0px 1px 8px rgba(102, 102, 102, 0.2);
    border-radius: 4px;
    padding: 8px 0 16px;
}

.dropdown {
    height: 270px;
    overflow-y: auto;
}

.item {
    display: flex;
    align-items: center;
    width: 100%;
    height: 40px;
    padding: 11px 0px 11px 19px;
    background-color: #fff;
    transition: all ease-out 0.2s;
    position: relative;
}

.item:hover {
    background-color: #E7F1FD;
    cursor: pointer;
}

.item span {
    margin-left: 12px;
}

li {
    list-style: none;
}

input[type="checkbox"] {
    appearance: none;
    width: 18px;
    height: 18px;
    border: 1px solid #000;
    border-radius: 3px;
}

input[type="checkbox"]:checked {
    background-color: #45D1C9;
    border: 1px solid #45D1C9;
}

input[type="checkbox"]:checked~svg {
    display: block;
}

.item svg {
   position: absolute;
    top: 12px;
    left: 22px;
    font-size: 14px;
    color: #fff;
    display: none;
}

button {
  border: none;
  border-radius: 4px;
  padding: 4px 19px;
  cursor: pointer;
}

.btns {
  padding: 16px 0 0 16px;
}

.accept-btn {
  width: 104px;
  height: 32px;
  background-color: #DCDCDC;
  color: #fff;
  font-weight: 700;
  font-size: 16px;
  margin-right: 11px;
  pointer-events: none;
}

.accept-btn.active {
  background-color: #007BC3;
  pointer-events: initial;
}

.cancel-btn {
  background-color: transparent;
  color: #007BC3;
  font-size: 16px;
  width: 82px;
  height: 24px;
}
</style>