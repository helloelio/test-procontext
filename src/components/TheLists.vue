<template>
  <ul>
    <li>
      <input
        type="checkbox"
        v-model="checked"
        @change="this.$emit('getAllChecked', { checked, title })"
      />
      <span class="list-title" @click="toggleList">
        <span> {{ title }}</span>
        <span class="arrow">
          <img v-if="!opened" src="../assets/down-arrow.svg" alt="" />
          <img v-else src="../assets/up-arrow.svg" alt="" />
        </span>
      </span>
      <ul class="list-items" :class="{ 'list-item-opened': opened }">
        <li v-for="(item, idx) in list" :key="idx">
          <input
            type="checkbox"
            :checked="item.checked"
            :disabled="item.count === 0"
            @change="this.$emit('putList', { item, title })"
          />
          <input v-model="item.count" max="10" type="number" />
          <input v-model="item.color" type="color" />
        </li>
      </ul>
    </li>
  </ul>
</template>

<script>
export default {
  name: 'TheList',
  props: {
    title: {
      type: String,
      default: '',
    },
    list: {
      type: Array,
      default: () => [],
    },
    container: {
      type: Array,
      default: () => [],
    },
  },
  data() {
    return {
      checked: false,
      opened: false,
    };
  },
  methods: {
    toggleList() {
      this.opened = !this.opened;
    },
  },
};
</script>

<style scoped>
.list-title {
  cursor: pointer;
}
.list-items {
  height: 0;
  display: none;
}
.list-item-opened {
  display: block;
  height: 100%;
}
.arrow {
  margin-left: 5px;
}
</style>
