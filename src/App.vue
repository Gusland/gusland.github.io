<template>
  <div id="app">
    <div class="wrapper">
      <div v-for="item in items" :key="item.id">
        <Checkbox
          :id="item.id"
          :title="item.title"
          :visible="item.visible"
          :disabled="item.disabled"
          :isToggle="item.isToggle"
          @toggle="handleToggle"
        />
      </div>
      <!-- print result -->
      <ul class="result">
        <li :key="item.id" v-for="item in selectedItems">{{ item.title }}</li>
      </ul>
    </div>
    <Dropdown/>
  </div>
</template>

<script>
import Checkbox from './components/Checkbox';
import Dropdown from './components/Dropdown';

export default {
  name: 'App',
  components: {
    Dropdown,
    Checkbox,
  },
  data() {
    return {
      items: [
        {
          id: 1, title: 'apple', disabled: true, isToggle: true,
        },
        {
          id: 2,
          title: 'melon',
          isToggle: true,
        },
        {
          id: 3,
          title: 'pineapple',
          isToggle: true,
        },
        {
          id: 4,
          title: 'cherry',
          isToggle: true,
        },
        {
          id: 5, title: 'mango', disabled: true, isToggle: false,
        },
        {
          id: 6,
          title: 'blueberry',
          isToggle: false,
        },
        {
          id: 7,
          title: 'strawberry',
          isToggle: false,
        },
        {
          id: 8,
          title: 'banana',
          isToggle: false,
        },
      ],
      selectedItems: [],
    };
  },
  methods: {
    handleToggle(id, isChecked) {
      if (isChecked) {
        const selectedItem = this.items.find(item => item.id === id);
        console.info(selectedItem);
        if (selectedItem) {
          this.selectedItems.push(selectedItem);
        }
      } else {
        this.selectedItems = this.selectedItems.filter(item => item.id !== id);
      }
    },
  },
};
</script>

<style>
:root {
  --white: #fff;
  --gradients-gray: #868F98;
  --primary-200: #92A4C8;
  --primary-300: #3E517A;
  --primary-400: #303F5F;
  --primary-500: #212B41;
  --primary-700: #151B29;
  --primary-900: #0E121B;
  --secondary-500: #4AB4FF;
}

#app {
  font-family: 'Gotham Pro', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  display: flex;
  align-items: center;
  justify-content: center;
}

body {
  background-color: var(--primary-500);
}

.wrapper {
  display: flex;
  flex-direction: column;
}

.result {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  list-style: none;
  color: var(--white);
  font-size: 16px;
}

.result li:not(:first-child) {
  margin-top: 10px;
}
</style>
