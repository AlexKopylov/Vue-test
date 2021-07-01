<!-- eslint-disable -->
<template>
  <div class="tree-wrapper">
    <div
        :style="{'margin-left': `${depth * 20}px`}"
        @dblclick="makeFolder"
        class="node">
      <span
          class="node-arrow"
          @click="toggle"
          v-if="isFolder"
          >
        [{{ isOpen ? '&#9660;' : '&#9658;' }}]
      </span>
      {{ node.name }}
      <button
          class="btn"
          @click="$emit('add-item', node)"
      ></button>
    </div>
    <div class="node__list">
        <tree
            v-show="isOpen" v-if="isFolder"
            class="node__item"
            v-for="(child, index) in node.children"
            :key="index"
            :node="child"
            :depth="depth + 1"
            make-folder="$emit('make-folder', $event)"
            @add-item="$emit('add-item', $event)"
        />
    </div>
  </div>
</template>

<script>
export default {
  name: 'tree',
  props: {
    node: Object,
    depth: {
      type: Number,
      default: 0
    }
  },
  data: function() {
    return {
      isOpen: false
    };
  },
  computed: {
    isFolder: function() {
      return this.node.children && this.node.children.length;
    }
  },
  methods: {
    toggle: function() {
      if (this.isFolder) {
        this.isOpen = !this.isOpen;
      }
    },
    makeFolder: function() {
      if (!this.isFolder) {
        this.$emit("make-folder", this.item);
        this.isOpen = true;
      }
    }
  }
}
</script>

<style scoped>
.tree-wrapper {
  width: 50%;
}

.node {
  padding: 1rem;
  background-color: #34cde3;
  border-radius: 1rem;
  width: 11rem;
  margin-bottom: 1rem;
  display: flex;
  align-items: center;
  justify-content: center;
  position: relative;
  z-index: 0;
}

.node__item {
  position: relative;
}

.node__list {
  position: relative;
  display: flex;
  flex-direction: column;
  list-style-type: none;
  justify-content: flex-start;
}
.node__list li  {
  width: 2rem;
  position: relative;
  top: -10px;
}
.node__list .btn {
  left: 0;
}

.node-arrow {
  display: block;
  width: 1rem;
  height: 1rem;
  position: relative;
  top: -3px;
  cursor: pointer ;
  margin-right: 1rem;
}

.btn {
  background-color: transparent;
  border-radius: 50%;
  padding: .5rem;
  border: 1px solid;
  width: 1.5rem;
  height: 1.5rem;
  position: relative;
  z-index: 1;
  cursor: pointer;
  margin-left: 1rem;
}

.btn::before {
  content: '';
  width: 1rem;
  height: 2px;
  background-color: #000;
}

.btn::after {
  content: '';
  height: 1rem;
  width: 2px;
  background-color: #000;
}

.btn::before,
.btn::after {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}
</style>
<!-- eslint-enable -->
