<template>
  <div id="app">
    <button @click="addItems" class="button">
      Add 10 items
    </button>
    <ListRender tag="div" step="10" class="list">
      <div v-for="item in list" :key="item" class="item">
        {{ item }}
      </div>
    </ListRender>
     <button @click="clear" class="button">
      Clear
    </button>
  </div>
</template>

<script>
import ListRender from "./components/ListRender";

export default {
  name: 'App',
  components: {
    ListRender
  },
  data: () => ({
    items: [0, 1, 2, 3, 4, 5, 6, 7, 8, 9],
    counter: 0
  }),
  computed: {
    list() {
      return this.items;
    }
  },
  methods: {
    addItems() {
      let result = [];
      for(let i = this.list.length; i < this.list.length + 10; i++) {
        result.push(i);
      }
      this.items = [...this.items, ...result];
      this.counter++;
    },
    clear() {
      this.items = [];
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  color: #2c3e50;
  display: flex;
  flex-direction: column;
  width: 15em;
  margin: 0 auto;
}
.button {
  top: 0;
  left: 0;
  position: sticky;
  background-color: #2c3e50;
  color: white;
  padding: 0.5em 1.5em;
  border: none;
  border-radius: 4px;
  height: 34px;
  margin: 4px 0;
  cursor: pointer;
}

#app .list {
  display: flex;
  flex-direction: column;
  height: 90vh;
  overflow-y: auto;
  width: 15rem;
  gap: 4px;
}
#app .list .item {
  position: relative;
  padding: 4px 0;
  background: #fea;
  border-radius: 4px;
  width: 15em;
  text-align: center;
}
</style>
