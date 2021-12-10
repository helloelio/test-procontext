// TODO: Пофиксить работу чекбоксов, перенести контейнеры в отдельный компонент,
// (возможно перенести данные передающиеся в компоненты в сами компоненты) //
Пофиксить чекбоксы выбирающие все элементы

<template>
  <div class="container">
    <div class="left-side">
      <the-lists
        :title="'List 1'"
        :checked="allFirstChecked"
        :list="firstList"
        :container="firstContainer"
        @getAllChecked="getAllChecked"
        @putList="handlePutList"
      />
      <the-lists
        :title="'List 2'"
        :checked="allSecondChecked"
        :list="secondList"
        :container="secondContainer"
        @getAllChecked="getAllChecked"
        @putList="handlePutList"
      />
      <the-lists
        :title="'List 3'"
        :checked="allThirdChecked"
        :list="thirdList"
        :container="thirdContainer"
        @getAllChecked="getAllChecked"
        @putList="handlePutList"
      />
    </div>
    <div class="right-side">
      <the-container :title="'Container 1'" :container="containerOne" />
      <the-container :title="'Container 2'" :container="containerTwo" />
      <the-container :title="'Container 3'" :container="containerThree" />
    </div>
  </div>
</template>

<script>
import TheLists from './components/TheLists.vue';
import TheContainer from './components/TheContainer.vue';

export default {
  name: 'App',

  components: {
    TheLists,
    TheContainer,
  },

  data() {
    return {
      allFirstChecked: false,
      allSecondChecked: false,
      allThirdChecked: false,
      firstList: [
        {
          id: 1,
          count: 0,
          color: '#ffffff',
          checked: false,
        },
        {
          id: 2,
          count: 0,
          color: '#ffffff',
          checked: false,
        },
        {
          id: 3,
          count: 0,
          color: '#ffffff',
          checked: false,
        },
        {
          id: 4,
          count: 0,
          color: '#ffffff',
          checked: false,
        },
        {
          id: 5,
          count: 0,
          color: '#ffffff',
          checked: false,
        },
        {
          id: 6,
          count: 0,
          color: '#ffffff',
          checked: false,
        },
      ],
      secondList: [
        {
          id: 1,
          count: 0,
          color: '#ffffff',
          checked: false,
        },
        {
          id: 2,
          count: 0,
          color: '#ffffff',
          checked: false,
        },
        {
          id: 3,
          count: 0,
          color: '#ffffff',
          checked: false,
        },
        {
          id: 4,
          count: 0,
          color: '#ffffff',
          checked: false,
        },
        {
          id: 5,
          count: 0,
          color: '#ffffff',
          checked: false,
        },
        {
          id: 6,
          count: 0,
          color: '#ffffff',
          checked: false,
        },
        {
          id: 7,
          count: 0,
          color: '#ffffff',
          checked: false,
        },
        {
          id: 8,
          count: 0,
          color: '#ffffff',
          checked: false,
        },
      ],
      thirdList: [
        {
          id: 1,
          count: 0,
          color: '#ffffff',
          checked: false,
        },
        {
          id: 2,
          count: 0,
          color: '#ffffff',
          checked: false,
        },
        {
          id: 3,
          count: 0,
          color: '#ffffff',
          checked: false,
        },
        {
          id: 4,
          count: 0,
          color: '#ffffff',
          checked: false,
        },
      ],
      firstContainer: [],
      secondContainer: [],
      thirdContainer: [],
    };
  },

  computed: {
    containerOne() {
      return this.firstContainer.filter(
        (item) => item.checked !== false && item.count !== 0,
      );
    },
    containerTwo() {
      return this.secondContainer.filter(
        (item) => item.checked !== false && item.count !== 0,
      );
    },
    containerThree() {
      return this.thirdContainer.filter(
        (item) => item.checked !== false && item.count !== 0,
      );
    },
  },

  watch: {
    allFirstChecked(newValue) {
      this.handleAllCheck(newValue, 'first');
    },
    allSecondChecked(newValue) {
      this.handleAllCheck(newValue, 'second');
    },
    allThirdChecked(newValue) {
      this.handleAllCheck(newValue, 'third');
    },
  },

  methods: {
    // ===========================
    handleAllCheck(value, name) {
      /* eslint-disable */
      switch (name) {
        case 'first':
          this.firstList.map((item) => {
            item.checked = value;
          });
          break;
        case 'second':
          this.secondList.map((item) => {
            item.checked = value;
          });
          break;
        case 'third':
          this.thirdList.map((item) => {
            item.checked = value;
          });
      }
    },
    // ===========================
    getAllChecked(payload) {
      switch (payload.title) {
        case 'List 1':
          this.allFirstChecked = payload.checked;
          this.firstList.forEach((item) => {
            if (!item.checked && item.count !== 0) {
              this.firstContainer = [...this.firstList];
            }
          });
          break;
        case 'List 2':
          this.allSecondChecked = payload.checked;
          this.secondList.forEach((item) => {
            if (!item.checked && item.count !== 0) {
              this.secondContainer = [...this.secondList];
            }
          });
          break;
        case 'List 3':
          this.allThirdChecked = payload.checked;
          this.thirdList.forEach((item) => {
            if (!item.checked && item.count !== 0) {
              this.thirdContainer = [...this.thirdList];
            }
          });
      }
    },
    // ===========================
    handlePutList(payload) {
      console.log(payload);
      switch (payload.title) {
        case 'List 1':
          this.putListToContainer(payload.item, this.firstContainer);
          break;
        case 'List 2 ':
          this.putListToContainer(payload.item, this.secondContainer);
          break;
        case 'List 3':
          this.putListToContainer(payload.item, this.thirdContainer);
      }
    },
    putListToContainer(item, container) {
      item.checked = !item.checked;
      if (container.length === 0) {
        container.push(item);
      } else {
        container.push(item);
      }
    },
    // ===========================
  },
};
</script>

<style lang="scss">
body {
  margin: 0;
}
li {
  list-style: none;
}
.container {
  display: grid;
  grid-template-columns: 50% 50%;
  padding: 10px;
}
</style>
