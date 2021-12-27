<template>
  <div id="app" v-bind:class="{clickable: clickable}">
    <div class="section section-1" v-bind:class="{active: activeSection == 1}" v-on:click="sectorClick(1)"></div>
    <div class="section section-2" v-bind:class="{active: activeSection == 2}" v-on:click="sectorClick(2)"></div>
    <div class="section section-3" v-bind:class="{active: activeSection == 3}" v-on:click="sectorClick(3)"></div>
    <div class="section section-4" v-bind:class="{active: activeSection == 4}" v-on:click="sectorClick(4)"></div>

    <ResultNav 
      v-bind:currentScore="currentScore"
      v-bind:recordScore="recordScore"

      @startButton="startGame"
    />
  </div>
</template>

<script>
import ResultNav from "@/components/RsultNav.vue";

export default {
  name: 'App',
  data() {
    return {
      targetSeq: [],
      currentScore: 0,
      recordScore: 0,
      sectorsClicked: 0,
      steps: 1,
      gameStarted: false,
      activeSection: 0,
      clickable: true
    }
  },
  components: {
    ResultNav : ResultNav
  },
  methods: {
    startGame() {
      this.targetSeq = [];
      this.steps = 1;
      this.currentScore = 0;
      this.sectorsClicked = 0;

      this.targetSeq.push(Math.floor(Math.random() * 4) + 1);

      this.gameStarted = true;

      this.hightligthSectors();
    },
    endGame() {
      alert('Game over');
      this.gameStarted = false;

      if (this.recordScore < this.currentScore) {
        this.recordScore = this.currentScore;
      }
    },
    sectorClick(id) {
      if (this.gameStarted) {
        if (id == this.targetSeq[this.sectorsClicked]) {

          this.sectorsClicked++;

          if (this.sectorsClicked == this.targetSeq.length) {
            this.nextStep();
          }
        } else {
          this.endGame();
        }

      } else {
        this.startGame();
      }
    },
    nextStep() {
      this.steps = this.steps + 1;
      this.targetSeq.push(Math.floor(Math.random() * 4) + 1);
      this.sectorsClicked = 0;
      this.currentScore++;

      this.hightligthSectors();
    },
    hightligthSectors() {
      let counter = 0;
      let $this = this;
      let timer = 1100;
      function show() {
        if (counter < $this.targetSeq.length) {
          setTimeout(function() {
            $this.activeSection = $this.targetSeq[counter];
            setTimeout( () => $this.activeSection=0, 700);
            counter++;
            show();
          }, timer);
        }
      }

      show();
    },
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

  &.clickable {
    .section {
      &-1, &-2, &-3, &-4 {
        cursor: pointer;
        &:hover {
          opacity: 1;
        }
      }
    }
  }

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
      opacity: .5;
      transition: all .2s ease;
      box-sizing: border-box;

      &.active {
        opacity: 1;
        border: 5px solid	#383838;
      }
    }  
  }

  @media screen and (orientation: portrait) {
    flex-direction: column;

    .section {
      width: 100%;
      height: 15%;

      &:last-child {
        height: 40%;
      }
    }
  }
}
</style>
