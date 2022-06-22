<script>
import Options from "./components/Options.vue";

export default {
  components: { Options },
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
    };
  },
};
</script>

<template>
  <div class="container">
    <Options :data="locations" />
  </div>
</template>

<style>
@import url("https://fonts.googleapis.com/css2?family=Noto+Sans:wght@400;700&display=swap");
html {
  font-size: 62.5%;
}

* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: "Noto Sans", sans-serif;
  font-size: 1.6rem;
  line-height: 1.5;
  color: #333;
}

body ::-webkit-scrollbar {
  width: 8px;
}

body ::-webkit-scrollbar-thumb {
  background-color: #dcdcdc;
  border-radius: 6px;
}

body ::-webkit-scrollbar-track {
  background-color: #fff;
}

body button {
  font-family: "Noto Sans", sans-serif;
}

body li {
  list-style: none;
}

.container {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-top: 50px;
}
</style>
