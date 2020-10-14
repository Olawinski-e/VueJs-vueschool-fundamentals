<template>
  <div id="shopping-list" class="container">
    <div class="header col mb-2">
      <h1>{{ header.toLocaleUpperCase() }}</h1>
      <button
        v-if="state === 'default'"
        @click="changeState('edit')"
        class="btn btn-primary"
      >
        Add item
      </button>
      <button v-else @click="changeState('default')" class="btn btn-danger">
        Cancel
      </button>
    </div>
    <b-container fluid v-if="state === 'edit'">
      <b-row class="my-1">
        <b-col sm="9">
          <b-form-input
            type="text"
            v-model="newItem"
            placeholder="Add an object"
            @keyup.enter="saveItem"
            class="mb-2"
          ></b-form-input>
        </b-col>
        <b-col sm="3">
          <button @click="saveItem" class="btn btn-info">Save item</button>
        </b-col>
      </b-row>
    </b-container>
    <ul>
      <li v-for="(item, index) of items" :key="index">{{ item }}</li>
    </ul>
    <p v-if="items.length === 0" class="">Nice job you've bought everything</p>
  </div>
</template>

<script>
export default {
  name: "App",
  components: {},
  data() {
    return {
      state: "default",
      header: "Shopping list App",
      newItem: "",
      items: [
        // "10 party hats", "2 board games", "20 cups"
      ],
    };
  },
  methods: {
    saveItem() {
      this.items.push(this.newItem);
      this.newItem = "";
    },
    changeState(newState) {
      this.state = newState;
    },
  },
};
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
</style>
