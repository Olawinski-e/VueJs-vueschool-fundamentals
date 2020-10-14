<template>
  <div id="shopping-list">
    <h1>{{ header.toLocaleUpperCase() }}</h1>
    <b-container fluid>
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
  </div>
</template>

<script>
export default {
  name: "App",
  components: {},
  data() {
    return {
      header: "Shopping list App",
      newItem: "",
      items: ["10 party hats", "2 board games", "20 cups"],
    };
  },
  methods: {
    saveItem() {
      this.items.push(this.newItem);
      this.newItem = "";
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
