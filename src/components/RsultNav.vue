<template>
    <div class="section section-result">
      <div>
        <h3>Current points</h3>
        <h4>{{currentScore}}</h4>
      </div>
      
      <div>
        <h3>Record</h3>
        <h4>{{recordScore}}</h4>
      </div>

      <div class="startGame" v-on:click="$emit('startButton')">Start game</div>
    </div>
</template>

<script>
export default {
  props: ['currentScore', 'recordScore']
}
</script>

<style scoped lang="scss">
    .section-result {
      display: flex;
      flex-direction: column;
      justify-content: space-around;
      align-items: center;

      .startGame {
          background: #bada55;

          padding: 30px;
          border-radius: 10px;
          cursor: pointer;
      }

      @media screen and (orientation: portrait) {
        flex-direction: row;
        flex-wrap: wrap;

        .startGame {
          width: 100vw;
        }
      }
    }
</style>
