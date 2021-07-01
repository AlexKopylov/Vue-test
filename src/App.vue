<template>
  <div class="wrapper">
    <tree
        :node="root"
        @make-folder="makeFolder"
        @add-item="addItem"
    />
    <pre v-html="JSON.stringify(root).trim()"></pre>
  </div>
</template>

<script>
import tree from "./components/tree";
import root from './root.json'

export default {
  name: 'App',
  data() {
    return {
      root,
    }
  },
  methods: {
    makeFolder: function (item) {
      this.$set(item, "children", []);
      this.addChild(item);
    },

    addItem: function (item) {
      item.children.push({
        name: "new Child",
        children: []
      })
    },

  },
  components: {
    tree
  }
}
</script>

<style>
* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}
.wrapper {
  display: flex;
  flex-direction: column;
}

#app {
  margin: 60px auto 0;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;

}
</style>
