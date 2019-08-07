<template>
  <div id="buttonCounter">
    <button @click="counter++">Click me: {{ counter }}</button>
    <h1 :style="myStyle">hello, world!</h1>
    <input type="text" v-model="message" @keyup.enter="inputTextButton" />
    <p>{{ message }}</p>

    <button type="text" @click="inputTextButton">+ ADD</button>
    <button type="text" @click="showGroceryList">show/hide</button>
    <br />
    <br />
    <div v-show="show" class="lists" :key="index" v-for="(item, index) in groceryList">
      <div class="text-block">
        <span :class="{completedList:isActive}" @click="completed(index)">{{item.text}}</span>
        <br />
        <!-- <input type="text" v-model="valueMessage" @keyup.enter="inputTextButton" /> -->
      </div>
      <div>
        <button type="text" @click="removeList(index)">delete</button>
        <button @click="renameList(index)">{{ changesButtonName }}</button>
      </div>
    </div>
    <p v-on:mousemove="updateCoordinates">Coordinates: {{ x }} / {{ y }}</p>
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
      valueMessage: "",
      showButton: true,
      show: true,
      isActive: false,
      changesButtonName: "rename",
      checkButton: true,
      x: 0,
      y: 0
    };
  },

  watch: {
    counter() {
      if (this.counter > 20) {
        this.counter = 4;
      }
    }
  },

  computed: {
    myStyle() {
      return {
        color: this.message
      };
    }
  },

  methods: {
    showGroceryList() {
      this.show = !this.show;
    },

    updateCoordinates() {
      this.x = event.clientX;
      this.y = event.clientY;
    },

    inputTextButton() {
      this.groceryList.push({
        text: this.message,
        id: this.counter
      }),
        this.counter++,
        (this.message = "");
    },

    completed(index) {
      console.log("checked", index, this.isActive);
    },

    removeList(index) {
      console.log("delete", index), this.groceryList.splice(index, 1);
    },

    renameList(index) {
      if (this.checkButton === true) {
        this.message = this.groceryList[index].text;
        this.checkButton = !this.checkButton;
        this.changesButtonName = 'save';
      } else if(this.checkButton === false) {
        this.groceryList[index].text = this.message;
        this.checkButton = !this.checkButton;
        this.changesButtonName = 'rename';
      }
    }

    // saveList(index) {

    //   console.log("save", index);
    // }
  }
};
</script>

<style>
html,
body {
  width: 100%;
  height: 100%;
  margin: 5px;
  padding: 0;
}
h1 {
  color: rgb(204, 48, 48);
}

.text-block {
  text-align: left;
}
.lists {
  width: 90%;
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
}

.completedList {
  text-decoration: line-through;
}
</style>
