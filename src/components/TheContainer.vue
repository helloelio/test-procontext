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
      >
        <svg
          class="cross-img"
          :style="{ stroke: item.color, filter: 'invert(100%)' }"
          width="10"
          height="10"
          viewBox="0 0 24 24"
          xmlns="http://www.w3.org/2000/svg"
        >
          <path
            d="M20 4L4 20M20 20L4 4L20 20Z"
            stroke-width="2"
            stroke-linecap="round"
          />
        </svg>
      </div>
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
  position: relative;
  border: 1px solid rgba(0, 0, 0, 1);
  width: 10px;
  height: 10px;
  border-radius: 2px;
  filter: drop-shadow(0px 0px 1px rgba(0, 0, 0, 1));
  cursor: pointer;
}

.box-item:hover {
  border: 1px solid rgba(255, 0, 0, 0.5);
}
.cross-img {
  display: none;
  position: absolute;
}
.box-item:hover .cross-img {
  display: block;
}
.hr {
  background-color: black;
}
</style>
