<template>
  <div class="boxes">
    <h2>{{ title }}</h2>
    <div class="box-container" v-for="item in container" :key="item.id">
      <div
        @click="this.$emit('deleteItemFromContainer', item)"
        class="box-item"
        :style="{
          background: item.color,
        }"
        v-for="(box, idx) in item.count"
        :key="idx"
      ></div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'TheContainer',
  props: {
    title: {
      type: String,
      default: '',
    },
    container: {
      type: Array,
      default: () => [],
    },
  },
};
</script>

<style scoped>
.boxes {
  background-color: rgba(0, 0, 0, 0.1);
  display: flex;
  flex-direction: column;
  border: 1px solid;
  margin-bottom: 10px;
  border-radius: 8px;
  box-shadow: 0px 0px 5px 0px black;
  padding: 10px;
}
.box-container {
  display: grid;
  grid-template-columns: repeat(auto-fill, 15px);
  row-gap: 5px;
  padding-bottom: 5px;
  margin-bottom: 5px;
  border-bottom: 1px solid black;
}
.box-item {
  width: 10px;
  height: 10px;
  border-radius: 2px;
  filter: drop-shadow(0px 0px 1px rgba(0, 0, 0, 1));
  cursor: pointer;
}

.box-item:hover {
  background-image: url('../assets/cross.svg') !important;
}

.hr {
  background-color: black;
}
</style>
