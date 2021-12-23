<template>
  <div id="app">
    <div class="section section-1" v-on:click="sectorClick(1)"></div>
    <div class="section section-2" v-on:click="sectorClick(2)"></div>
    <div class="section section-3" v-on:click="sectorClick(3)"></div>
    <div class="section section-4" v-on:click="sectorClick(4)"></div>

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
      currentSeq: [],
      currentScore: 0,
      recordScore: 0,
      steps: 1,
      gameStarted: false
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
      this.currentSeq = [];

      this.targetSeq.push(Math.floor(Math.random() * 4) + 1);

      this.gameStarted = true;

      this.hightligthSectors();
    },
    sectorClick(id) {
      if (this.gameStarted) {
        this.currentSeq.push(id);


        if (this.currentSeq.length == this.targetSeq.length) {
          this.nextStep();
        }
      } else {
        this.startGame();
      }
    },
    nextStep() {
      this.steps = this.steps + 1;
      this.targetSeq.push(Math.floor(Math.random() * 4) + 1);
      this.currentSeq = [];

      this.hightligthSectors();
      console.log(this.steps, "next step");
    },
    hightligthSectors() {
      let items = [];
      let counter = 0;
      function show() {
        if (counter < items.length) {
          setTimeout(function() {
            // items[counter].classList.add('active');
            // setTimeout( () => items[counter].classList.remove('active'), 1000);
            document.getElementsByClassName(items[counter])[0].classList.add('active');
            setTimeout( () => document.getElementsByClassName(items[counter])[0].classList.remove('active'), 1000);
            console.log(counter);
            counter++;
            show();
          }, 1000);
        }
      }

      for (let i of this.targetSeq) {
        items.push('section-'+i);

        // for(let item of items){
        //   item.classList.add('active');
        //   item.classList.remove('active');
        // }
      }

      show();
    }
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
      opacity: .5;

      &:hover, &.active {
        opacity: 1;
      }
    }  
  }
}
</style>
