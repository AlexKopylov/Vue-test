<template>
  <tree
      :node="root"
      @make-folder="makeFolder"
      @add-item="addItem"
  />
</template>

<script>
import tree from "./components/tree";

export default {
  name: 'App',
  data() {
    return {
      root: {
        name: 'Food',
        children: [
          {
            name: "Plant",
            children: [
              {
                name: "Fruits",
                children: [
                  {name: "hello"},
                  {name: "wat"}]
              },
              {
                name: "Vegetables",
                children: [
                  {name: "hello"},
                  {name: "wat"}
                ]
              },
            ]
          },
          {
            name: "Animal",
            children: [
              {
                name: "child folder",
                children: [{name: "hello"}, {name: "wat"}]
              },
            ]
          },
          {
            name: "child folder",
            children: [
              {
                name: "child folder",
                children: [{name: "hello"}, {name: "wat"}]
              },
              {name: "hello"},
              {name: "wat"},
              {
                name: "child folder",
                children: [{name: "hello"}, {name: "wat"}]
              }
            ]
          }
        ]
      }
    }
  },
  methods: {
    makeFolder: function (item) {
      this.$set(item, "children", []);
      this.addItem(item);
    },
    addItem: function (item) {
      item.children.push({
        name: "new Child"
      })
    }
  },
  components: {
    tree
  }
}
</script>

<style>
#app {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
