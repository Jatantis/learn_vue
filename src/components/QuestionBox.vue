<template>
  <div id="buttonCounter">
    <h1 :style="myStyle">hello, world!</h1>
    <input type="text" v-model="message" @keyup.enter="inputTextButton" />
    <button type="text" @click="inputTextButton">+ ADD</button>
    <button type="text" @click="showGroceryList">show/hide</button>
    <br />
    <br />
    <div v-show="show" class="lists" :key="index" v-for="(item, index) in groceryList">
      <input
        :class="{completedList:item.completedToDo}"
        class="inputShow"
        type="text"
        v-model=" item.text "
        @keyup.enter="inputTextButton"
        :readonly="item.readOnly"
        @click="completed(index)"
      />
      <div>
        <button type="text" @click="removeList(index)">delete</button>
        <button @click="renameList(index)">{{ item.changesButtonName }}</button>
      </div>
    </div>
    <hr />
  </div>
</template>


<script>
export default {
  name: "buttonCounter",
  data() {
    return {
      groceryList: [
        {
          id: 1,
          text: "Vegetables",
          readOnly: true,
          completedToDo: false,
          changesButtonName: "rename"
        },
        {
          id: 2,
          text: "Cheese",
          readOnly: true,
          completedToDo: false,
          changesButtonName: "rename"
        },
        {
          id: 3,
          text: "Whatever else humans are supposed to eat",
          readOnly: true,
          completedToDo: false,
          changesButtonName: "rename"
        }
      ],
      counter: 4,
      message: "",
      valueMessage: "",
      readonlyInput: true,
      show: true,
      isActive: false,
      changesButtonName: "rename",
      checkButton: true,
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

    inputTextButton() {
      this.groceryList.push({
        text: this.message,
        id: this.counter,
        readOnly: true,
        completedToDo: false
      }),
        this.counter++,
        (this.message = "");
    },
    completed(index) {
      console.log("checked", this.groceryList[index]);
      if (this.checkButton === true) {
        if (this.groceryList[index].completedToDo === false) {
          this.groceryList[index].completedToDo = true;
        } else if (this.groceryList[index].completedToDo === true) {
          this.groceryList[index].completedToDo = false;
        }
      }
    },

    removeList(index) {
      console.log("delete", index), this.groceryList.splice(index, 1);
    },

    renameList(index) {
      if (this.checkButton === true) {
        this.checkButton = !this.checkButton;
        this.groceryList[index].readOnly = false;
        this.groceryList[index].completedToDo;
        this.groceryList[index].changesButtonName = "save";
        console.log(this.groceryList[index]);
      } else if (this.checkButton === false) {
        this.groceryList[index].readOnly = true;
        this.checkButton = !this.checkButton;
        this.groceryList[index].changesButtonName = "rename";
        console.log(this.groceryList[index]);
      }
    }
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
.inputShow {
  border: none;
  width: 70%;
}
.text-block {
  text-align: left;
}
.lists {
  width: 90%;
  max-width: 670px;
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
}

.completedList {
  text-decoration: line-through;
}
</style>
