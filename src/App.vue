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
      <the-container :title="'Container 1'" :container="firstContainer" />
      <the-container :title="'Container 2'" :container="secondContainer" />
      <the-container :title="'Container 3'" :container="thirdContainer" />
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
    getChecked(item) {
      console.log(item);
    },
    getColor(event) {
      console.log(typeof event.target.value);
    },
    getAllFirstChecked(value) {
      this.allFirstChecked = value;
      console.log(this.allFirstChecked);
    },
    getAllSecondChecked(value) {
      this.allSecondChecked = value;
      console.log(this.allSecondChecked);
    },
    getAllThirdChecked(value) {
      this.allThirdChecked = value;
      console.log(this.allThirdChecked);
    },

    putListToContainer(item, container) {
      item.checked = !item.checked;
      if (item.checked) {
        container.push(item);
      }
    },

    putFirstList(item) {
      this.putListToContainer(item, this.firstContainer);
    },
    putSecondList(item) {
      this.putListToContainer(item, this.secondContainer);
    },
    putThirdList(item) {
      this.putListToContainer(item, this.thirdContainer);
    },
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
