<template>
  <div id="app">
    <div class="wrapper">
      <div v-for="item in items" :key="item.id">
        <Checkbox
          :id="item.id"
          :title="item.title"
          :visible="item.visible"
          :disabled="item.disabled"
          :isToggle="false"
          @toggle="handleToggle"
        />
      </div>
      <!-- print result -->
      <ul class="result">
        <li :key="item.id" v-for="item in selectedItems">{{ item.title }}</li>
      </ul>
    </div>
  </div>
</template>

<script>
import Checkbox from './components/Checkbox';

export default {
  name: 'App',
  components: {
    Checkbox,
  },
  data() {
    return {
      items: [
        {
          id: 1, title: 'apple', visible: true, disabled: true,
        },
        {
          id: 2,
          title: 'melon',
          visible: false,
        },
        {
          id: 3,
          title: 'pineapple',
          visible: true,
        },
        {
          id: 4,
          title: 'Cherry',
          visible: true,
        },
      ],
      selectedItems: [],
    };
  },
  methods: {
    handleToggle(id, isChecked) {
      if (isChecked) {
        const selectedItem = this.items.find(item => item.id === id);
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
