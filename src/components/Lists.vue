<template>
  <ul>
    <li>
      <input
        type="checkbox"
        v-model="checked"
        @change="this.$emit('getAllChecked', checked)"
      />
      List 1.
      <ul>
        <li v-for="(item, idx) in list" :key="idx">
          <input
            type="checkbox"
            :disabled="item.count === 0 || item.color === '#ffffff'"
            :checked="item.checked"
            @change="this.$emit('putList', item)"
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
  name: 'FirstList',
  props: {
    list: {
      type: Array,
      default: () => [],
    },
  },
  data() {
    return {
      checked: false,
    };
  },
};
</script>
