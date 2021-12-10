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
        @getAllChecked="getAllFirstChecked"
        @putList="putFirstList"
      />
      <the-lists
        :title="'List 2'"
        :checked="allSecondChecked"
        :list="secondList"
        @getAllChecked="getAllSecondChecked"
        @putList="putSecondList"
      />
      <the-lists
        :title="'List 3'"
        :checked="allThirdChecked"
        :list="thirdList"
        @getAllChecked="getAllThirdChecked"
        @putList="putThirdList"
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
      this.handleAllFirstCheck(newValue);
    },
    allSecondChecked(newValue) {
      this.handleAllSecondCheck(newValue);
    },
    allThirdChecked(newValue) {
      this.handleAllThirdCheck(newValue);
    },
  },

  methods: {
    // ===========================
    handleAllFirstCheck(value) {
      /* eslint-disable */
      this.firstList.map((item) => {
        item.checked = value;
      });
    },
    handleAllSecondCheck(value) {
      /* eslint-disable */
      this.secondList.map((item) => {
        item.checked = value;
      });
    },
    handleAllThirdCheck(value) {
      /* eslint-disable */
      this.thirdList.map((item) => {
        item.checked = value;
      });
    },
    // ===========================
    getAllFirstChecked(value) {
      this.allFirstChecked = value;
      this.firstList.forEach((item) => {
        if (!item.checked && item.count !== 0) {
          this.firstContainer = [...this.firstList];
        }
      });
    },
    getAllSecondChecked(value) {
      this.allSecondChecked = value;
      this.secondList.forEach((item) => {
        if (!item.checked && item.count !== 0) {
          this.secondContainer = [...this.secondList];
        }
      });
    },
    getAllThirdChecked(value) {
      this.allThirdChecked = value;
      this.thirdList.forEach((item) => {
        if (!item.checked && item.count !== 0) {
          this.thirdContainer = [...this.thirdList];
        }
      });
    },
    // ===========================
    putFirstList(item) {
      this.putListToContainer(item, this.firstContainer);
    },
    putSecondList(item) {
      this.putListToContainer(item, this.secondContainer);
    },
    putThirdList(item) {
      this.putListToContainer(item, this.thirdContainer);
    },
    putListToContainer(item, container) {
      item.checked = !item.checked;
      if (item.checked && item.count !== 0) {
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
