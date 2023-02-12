<template>
  <header>
      <img alt="Pokemon logo" src="@/assets/logo.png" width="125" height="125"/>
      <div>
        <RouterLink to="/"><button class="homeButton">Home</button></RouterLink>
        <RouterLink to="/about"><button class="aboutButton">About me</button></RouterLink>
      </div>
  </header>
</template>


<script>
import { RouterLink } from 'vue-router'
export default {
    name:'PageHeader'
  }
</script>

<style scoped>
header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 20px;
}

img {
  margin-left: 40px;
  width: 210px;
  height: 80px;
}

.homeButton {
  margin-right: 20px;
  width: 70px;
  height: 40px;
  border: 0;
  border-radius: 8px;
  cursor: pointer;
  font-size: 16px;
  font-weight: 700;
}

.homeButton:hover{
    background: rgb(172, 172, 172);
}

.aboutButton {
  margin-right: 40px;
  width: 100px;
  height: 40px;
  border: 0;
  border-radius: 8px;
  cursor: pointer;
  font-size: 16px;
  font-weight: 700;
}

.aboutButton:hover{
    background: rgb(172, 172, 172);
}

/* @media (min-width: 1024px) {
} */
</style>
