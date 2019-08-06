<template>
  <div id="buttonCounter">
    <button>Click me</button>
    <h1>hello, world!</h1>
    <input type="text" v-model="message" @keyup.enter="inputTextButton" />
    <p>{{ message }}</p>
    <button type="text" @click="inputTextButton">+ ADD</button>
    <button type="text" @click="show = !show">show/hide</button>
    <div class="lists" :key="index" v-for="(item, index) in groceryList" v-if="show">
      <span :todo="item" @click="completed(index)">{{item.text}}</span>
      <button type="text" @click="removeList(index)">remove</button>
    </div>
  </div>
</template>


<script>
export default {
  name: "buttonCounter",
  data() {
    return {
      groceryList: [
        { id: 1, text: "Vegetables" },
        { id: 2, text: "Cheese" },
        { id: 3, text: "Whatever else humans are supposed to eat" }
      ],

      counter: 4,

      message: "",

      show: true
    };
  },

  methods: {
    inputTextButton() {
      this.groceryList.push({
        text: this.message,
        id: this.counter
      }),
        this.counter++,
        (this.message = "");
    },

    completed(index) {
      console.log("checked", index);
    },

    removeList(index) {
      console.log("delete", index), this.groceryList.splice(index, 1);
    }
  }
};
</script>

<style>
html, body {
    margin: 5px;
    padding: 0;
}
h1 {
    color: rgb(204, 48, 48);
}

.lists {
    width: 400px;
    display: flex;
    justify-content: space-between;
}

.completedList {
    text-decoration: line-through;
}
</style>
