<script setup >
import Options from './components/Options.vue'
</script>

<template>
  <div class="container">
    <Options />
  </div>
</template>

<style>
html {
    font-size: 62.5%;
}

* {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
}

body {
    font-family: 'ProximaNova', sans-serif;
    font-size: 1.6rem;
    line-height: 1.5;
    color: #333;
}

body ::-webkit-scrollbar {
  width: 8px;
}

body ::-webkit-scrollbar-thumb {
  background-color: #DCDCDC;
  border-radius: 6px;
}

body ::-webkit-scrollbar-track {
  background-color: #fff;
}

.container {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-top: 50px;
}

</style>
