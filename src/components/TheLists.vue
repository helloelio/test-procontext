<template>
  <ul>
    <li>
      <input
        :class="{ mainCheckbox: getSingleCheck && !checked }"
        type="checkbox"
        v-model="checked"
        @change="this.$emit('getAllChecked', { checked, title })"
      />
      <span class="some-single-checked"></span>
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

  computed: {
    /* eslint-disable */
    getSingleCheck() {
      return this.list.some((item) => item.checked === true);
    },
    getSingleUncheck() {
      return this.list.every((item) => item.checked === true);
    },
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
.mainCheckbox::before {
  content: '';
  position: absolute;
  width: 5px;
  height: 5px;
  background: black;
  transform: translate(4px, 4px);
}
</style>
