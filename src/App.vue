// TODO: Пофиксить работу чекбоксов, перенести контейнеры в отдельный компонент,
// (возможно перенести данные передающиеся в компоненты в сами компоненты) //
Пофиксить чекбоксы выбирающие все элементы

<template>
  <div class="container">
    <div class="left-side">
      <Lists
        :checked="allFirstChecked"
        :list="firstList"
        @getAllChecked="getAllFirstChecked"
        @putList="putFirstList"
      />
      <Lists
        :checked="allSecondChecked"
        :list="secondList"
        @getAllChecked="getAllSecondChecked"
        @putList="putSecondList"
      />
      <Lists
        :checked="allThirdChecked"
        :list="thirdList"
        @getAllChecked="getAllThirdChecked"
        @putList="putThirdList"
      />
    </div>
    <div class="right-side">
      <div class="boxes">
        <h1>Container 1</h1>
        <div
          class="box-container"
          v-for="item in firstContainer"
          :key="item.id"
        >
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
      <div class="boxes">
        <h1>Container 2</h1>
        <div
          class="box-container"
          v-for="item in secondContainer"
          :key="item.id"
        >
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
      <div class="boxes">
        <h1>Container 3</h1>
        <div
          class="box-container"
          v-for="item in thirdContainer"
          :key="item.id"
        >
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
    </div>
  </div>
</template>

<script>
import Lists from './components/Lists.vue';

export default {
  name: 'App',

  components: {
    Lists,
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
      console.log(item);
      if (item.checked) {
        container.push(item);
      } else {
        container.filter((containerItem) => {
          if (containerItem.id === item.id) {
            containerItem.checked = false;
          }
        });
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
.boxes {
  display: flex;
  flex-direction: column;
  border: 1px solid;
  margin-bottom: 10px;
  border-radius: 14px;
  box-shadow: 0px 0px 10px 0px black;
  padding: 15px;
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
