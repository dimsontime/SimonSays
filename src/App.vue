<template>
  <div id="app">
    <div class="section section-1"></div>
    <div class="section section-2"></div>
    <div class="section section-3"></div>
    <div class="section section-4"></div>

    <div class="section section-result">
      <div>
        <div>Current points</div>
        <div>123</div>
      </div>
      
      <div>
        <div>Record</div>
        <div>123</div>
      </div>

      <div class="startGame">Start game</div>
    </div>
  </div>
</template>

<script>


export default {
  name: 'App',
  components: {

  }
}
</script>

<style lang="scss">
body {
  margin: 0;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;

  width: 100vw;
  height: 100vh;
  display: flex;
  flex-direction: row;
  justify-content: flex-start;
  align-items: flex-start;

  .section {
    width: 20%;
    height: 100%;

    &-1 {
      background: blue;
    }

    &-2 {
      background: red;
    }

    &-3 {
      background: green;
    }

    &-4 {
      background: yellow;
    }

    &-1, &-2, &-3, &-4 {
      opacity: .7;

      &:hover {
        opacity: 1;
      }
    }

    &-result {
      display: flex;
      flex-direction: column;
      justify-content: space-around;
      align-items: center;
    }
  }

  .startGame {
    background: #bada55;

    padding: 30px;
    border-radius: 10px;
    cursor: pointer;
  }
}
</style>
