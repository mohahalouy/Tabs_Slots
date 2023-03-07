<template>
  <div class="tabs">
    <ul class="tabs__header">
      <li
          v-for="title in tableTitles"
          :key="title"
          :class="{selected: title==selectedTitle}"
          @click="selectedTitle=title"
      >
        {{ title }}
      </li>
    </ul>
    <slot></slot>
  </div>
</template>

<script>
import {ref} from "vue";
import {provide} from "vue";

export default {
  name: "TabsWrapper",
  setup(props, {slots}) {
    const tableTitles = ref(slots.default().map((table) => table.props.title))
    let selectedTitle = ref(tableTitles.value[0])

    provide("selectedTitle", selectedTitle)
    return {
      tableTitles,
      selectedTitle
    }
  }
}
</script>

<style scoped>
.tabs {
  max-width: 400px;
  margin: 0 auto;
}

.tabs__header {
  margin-bottom: 10px;
  list-style: none;
  padding: 0;
  display: flex;
}

.tabs__header li {
  width: 800px;
  text-align: center;
  padding: 10px 20px;
  margin-right: 10px;
  background-color: #ddd;
  color: black;
  border-radius: 5px;
  cursor: pointer;
  transition: 0.4s all ease-out;
}

.tabs__header li.selected {
  background-color: #0984e3;
  color: white;
}
</style>