<template>
  <div class="about">
    <h1>About</h1>
    <div>
      <p class="aboutText">This page was created using the <a class="linkApi" href="https://pokeapi.co/" target="_blank">PokeApi</a> and Vue.js by Maria Constance.</p>
      <p class="aboutText">If you want to learn more about the developer or want to see more projects, you can contact via  <a class="linkApi" href="mailto:maria-constance@hotmail.com" target="_blank">email</a> or check my social medias bellow.</p>
    </div>
  </div>
  <footer>
      <a href="https://www.linkedin.com/in/mariaconstance/" target="_blank"><img src="@/assets/linkedin.svg"/></a>
      <a href="https://github.com/constance03/" target="_blank"><img src="@/assets/github.svg"/></a>
      <a href="https://instagram.com/heydearmaria/" target="_blank"><img src="@/assets/instagram.svg"/></a>
  </footer>
</template>

<style>
  .about {
    height: 58vh;
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 2vw;
    margin-top: 4vh;
    background-color: antiquewhite;
    padding-top: 40px;
  }

  .linkApi {
    text-decoration: none;
    color: brown;
    cursor: pointer;
  }

  .aboutText{
    font-size: 20px;
    text-align: center;
  }

  footer {
    display: flex;
    background-color: #686767;
    align-items: center;
    justify-content: center;
    gap: 20px;
    padding: 2vh;
  }

</style>
