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
        <b-col sm="6">
          <b-form-input
            type="text"
            v-model="newItem"
            placeholder="Add an item"
            @keyup.enter="saveItem"
            class="mb-2"
          ></b-form-input>
        </b-col>
        <b-col sm="3">
          <button
            :disabled="newItem.length === 0"
            @click="saveItem"
            class="btn btn-info"
          >
            Save item
          </button>
        </b-col>
      </b-row>
    </b-container>
    <ul>
      <li
        v-for="(item, index) of reversedItem"
        :key="index"
        @click="togglePurchased(item)"
        :class="[
          item.purchased ? 'strikeout' : '',
          item.highPriority ? 'priority' : '',
        ]"
      >
        {{ item.label }}
      </li>
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
        {
          label: "10 party hats",
          purchased: false,
          highPriority: true,
        },
        { label: "2 board games", purchased: true, highPriority: false },
        { label: "20 cups", purchased: false, highPriority: false },
      ],
    };
  },
  computed: {
    reversedItem() {
      return this.items.slice(0).reverse();
    },
  },
  methods: {
    saveItem() {
      this.items.push({
        label: this.newItem,
      });
      this.newItem = "";
    },
    changeState(newState) {
      this.state = newState;
    },
    togglePurchased(item) {
      item.purchased = !item.purchased;
    },
  },
};
</script>

<style>
.strikeout {
  text-decoration: line-through;
}
.priority {
  color: orange;
}
li {
  cursor: pointer;
}
</style>
