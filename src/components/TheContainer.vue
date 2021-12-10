<template>
  <div class="boxes">
    <h2>{{ title }}</h2>
    <div class="box-container" v-for="item in container" :key="item.id">
      <div
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
  display: flex;
  flex-direction: column;
  border: 1px solid;
  margin-bottom: 10px;
  border-radius: 14px;
  box-shadow: 0px 0px 10px 0px black;
  padding: 10px;
}
.box-container {
  display: grid;
  grid-template-columns: repeat(auto-fill, 25px);
  row-gap: 5px;
  margin-bottom: 5px;
}
.box-item {
  margin-left: 10px;
  width: 15px;
  height: 15px;
}
</style>
