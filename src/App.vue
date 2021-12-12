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
      <the-container
        :title="'Container 1'"
        :container="firstContainer"
        @deleteItemFromContainer="deleteItemFromFirstContainer"
      />
      <the-container
        :title="'Container 2'"
        :container="secondContainer"
        @deleteItemFromContainer="deleteItemFromSecondContainer"
      />
      <the-container
        :title="'Container 3'"
        :container="thirdContainer"
        @deleteItemFromContainer="deleteItemFromThirdContainer"
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

  // ===========================
  // computed: {
  // Вариант отправлять отсортированный массив в контйнер[ ],
  //  чтобы они отображались в контейнере идентично порядку листа
  // containerOne() {
  //   return this.firstContainer.sort((a, b) => a.id - b.id);
  // },
  // },
  // ===========================

  // ===========================
  // наблюдатель за главным чекбоксам,
  // при его изменении вызывает метод
  // где проставляет для каждого айтема
  // значение != значение
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
  // ===========================

  methods: {
    handleAllCheck(value, name) {
      /* eslint-disable */
      switch (name) {
        case 'first':
          this.firstList.map((item) => (item.checked = value));
          break;
        case 'second':
          this.secondList.map((item) => (item.checked = value));
          break;
        case 'third':
          this.thirdList.map((item) => (item.checked = value));
      }
    },
    // ===========================
    // метод вызывающийся путем нажатия на Главный чекбокс
    // Простовляет в дату первого чекбокса = true
    // и присваивает определенному контейнеру элементы листа(после проверки)
    // если проверка не сработала просто очищаем массив
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
    // ===========================
    handlePutList(payload) {
      switch (payload.title) {
        case 'List 1':
          payload.item.checked = !payload.item.checked;
          if (payload.item.checked) {
            this.firstContainer.push(payload.item);
          } else {
            this.firstContainer = this.firstContainer.filter((item) => {
              return item.id !== payload.item.id;
            });
          }
          break;
        case 'List 2':
          payload.item.checked = !payload.item.checked;
          if (payload.item.checked) {
            this.secondContainer.push(payload.item);
          } else {
            this.secondContainer = this.secondContainer.filter((item) => {
              return item.id !== payload.item.id;
            });
          }
          break;
        case 'List 3':
          payload.item.checked = !payload.item.checked;
          if (payload.item.checked) {
            this.thirdContainer.push(payload.item);
          } else {
            this.thirdContainer = this.thirdContainer.filter((item) => {
              return item.id !== payload.item.id;
            });
          }
      }
    },
    // ===========================
    // Метод который удаляет item при нажатии на квадратик в контейнере
    deleteItemFromFirstContainer(item) {
      item.count -= 1;
      if (item.count === 0) {
        this.firstContainer.filter((conItem) => {
          return conItem.id !== item.id;
        });
        item.checked = false;
      }
    },
    deleteItemFromSecondContainer(item) {
      item.count -= 1;
      if (item.count === 0) {
        this.secondContainer = this.secondContainer.filter((conItem) => {
          return conItem.id !== item.id;
        });
        item.checked = false;
      }
    },
    deleteItemFromThirdContainer(item) {
      item.count -= 1;
      if (item.count === 0) {
        this.thirdContainer = this.thirdContainer.filter((conItem) => {
          return conItem.id !== item.id;
        });
        item.checked = false;
      }
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
