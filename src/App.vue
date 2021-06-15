<template>
  <div id="app">
    <span class="two_pics">
      <Hero v-model="fightData" />
      <Enemy v-model="fightData" />
    </span>
    <h1 v-if="endTurn">End of turn. Enemy hits you</h1>
  </div>
</template>

<script>
import Hero from './components/Hero'
import Enemy from './components/Enemy'

export default {
  name: 'App',
  components: {
    Hero, Enemy
  },
  data() {
    return {
      fightData:{
        heroHealthCounter: 100,
        heroManaCounter: 200,
        heroActionPoints: 3,
        enemyHealthCounter: 200
      }
    }
  },
  watch: {
    endTurn(val=this.heroHealthCounter) {
      val.$nextTick() < val
    }
  }
}
</script>

<style scoped>
.two_pics{
  display: flex;
  justify-content: space-between;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin: 0;
  padding: 0;
}
</style>
