<template>
  <div id="app">
    <div class="container">
      <div v-for="(box, index) in boxes" class="yellow-box" :key="index" @click="handleClick">{{index+1}}</div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      boxex: [],
      clickedOrder: []
    }
  },
  created() {
    this.boxes = new Array(7).fill(0)
  },
  watch: {
    clickedOrder: {
      handler(data){
        if (data?.length === this.boxes?.length) {
          data.forEach((div, i) => {
            setTimeout(() => div.classList.remove('green'), (i + 1) * 1000)
          });
          this.clickedOrder = [];
        }
      },
      deep: true,
      immediate: true
    },
  },
  components: {
  },
  
  methods: {
    handleClick(e) {
      if (!e.target.classList.contains('green')) {
        e.target.classList.add('green');
        this.clickedOrder.push(e.target)
      }
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.container {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
}

.yellow-box {
  width: min-content;
  background-color: yellow;
  padding: 3rem;
  margin: 1rem;
  border: 1px solid green;
  user-select: none;
}

.green {
  background-color: green;
}

.yellow-box:nth-child(4) {
  grid-column: span 3;
}

</style>
