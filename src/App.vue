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
        :container="containerOne"
        @getAllChecked="getAllChecked"
        @putList="handlePutList"
      />
      <the-lists
        :title="'List 2'"
        :checked="allSecondChecked"
        :list="secondList"
        :container="containerTwo"
        @getAllChecked="getAllChecked"
        @putList="handlePutList"
      />
      <the-lists
        :title="'List 3'"
        :checked="allThirdChecked"
        :list="thirdList"
        :container="containerThree"
        @getAllChecked="getAllChecked"
        @putList="handlePutList"
      />
    </div>
    <div class="right-side">
      <the-container
        :title="'Container 1'"
        :container="containerOne"
        @deleteItemFromContainer="deleteItemFromContainer"
      />
      <the-container
        :title="'Container 2'"
        :container="containerTwo"
        @deleteItemFromContainer="deleteItemFromContainer"
      />
      <the-container
        :title="'Container 3'"
        :container="containerThree"
        @deleteItemFromContainer="deleteItemFromContainer"
      />
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
          count: 6,
          color: '#ffffff',
          checked: false,
        },
        {
          id: 2,
          count: 10,
          color: '#244526',
          checked: false,
        },
        {
          id: 3,
          count: 4,
          color: '#654745',
          checked: false,
        },
        {
          id: 4,
          count: 15,
          color: '#855363',
          checked: false,
        },
        {
          id: 5,
          count: 47,
          color: '#934f93',
          checked: false,
        },
        {
          id: 6,
          count: 54,
          color: '#59de34',
          checked: false,
        },
      ],
      secondList: [
        {
          id: 1,
          count: 10,
          color: '#11ee11',
          checked: false,
        },
        {
          id: 2,
          count: 20,
          color: '#22ee22',
          checked: false,
        },
        {
          id: 3,
          count: 30,
          color: '#33ee33',
          checked: false,
        },
        {
          id: 4,
          count: 40,
          color: '#44ee44',
          checked: false,
        },
        {
          id: 5,
          count: 50,
          color: '#55ee55',
          checked: false,
        },
        {
          id: 6,
          count: 60,
          color: '#66ee66',
          checked: false,
        },
        {
          id: 7,
          count: 70,
          color: '#77ee77',
          checked: false,
        },
        {
          id: 8,
          count: 80,
          color: '#88ee88',
          checked: false,
        },
      ],
      thirdList: [
        {
          id: 1,
          count: 1,
          color: '#1e2e45',
          checked: false,
        },
        {
          id: 2,
          count: 2,
          color: '#2a2eee',
          checked: false,
        },
        {
          id: 3,
          count: 3,
          color: '#5ee5ee',
          checked: false,
        },
        {
          id: 4,
          count: 4,
          color: '#33e1a2',
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
    deleteItemFromContainer(item) {
      item.count -= 1;
    },
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
            } else {
              this.firstContainer = [];
            }
          });
          break;
        case 'List 2':
          this.allSecondChecked = payload.checked;
          this.secondList.forEach((item) => {
            if (!item.checked && item.count !== 0) {
              this.secondContainer = [...this.secondList];
            } else {
              this.secondContainer = [];
            }
          });
          break;
        case 'List 3':
          this.allThirdChecked = payload.checked;
          this.thirdList.forEach((item) => {
            if (!item.checked && item.count !== 0) {
              this.thirdContainer = [...this.thirdList];
            } else {
              this.thirdContainer = [];
            }
          });
      }
    },
    helperAllChecked(container, list) {},
    // ===========================
    handlePutList(payload) {
      switch (payload.title) {
        case 'List 1':
          this.helperHandlePutList(payload, this.firstContainer);
          break;
        case 'List 2':
          this.helperHandlePutList(payload, this.secondContainer);

          break;
        case 'List 3':
          this.helperHandlePutList(payload, this.thirdContainer);
      }
    },
    helperHandlePutList(payload, container) {
      payload.item.checked = !payload.item.checked;
      if (payload.item.checked) {
        container.push(payload.item);
      } else {
        container.splice(payload.item.id - 1, 1);
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
