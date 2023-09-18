<template>
  <div class="dropdown-container" v-click-outside="closeDropdown">
    <button class="btn" @click="toggleDropdown">
      <svg width="2" height="8" viewBox="0 0 2 8" fill="none" xmlns="http://www.w3.org/2000/svg">
        <path
          d="M2 1C2 1.55228 1.55228 2 1 2C0.447715 2 0 1.55228 0 1C0 0.447715 0.447715 0 1 0C1.55228 0 2 0.447715 2 1Z"
          fill="#4AB4FF"/>
        <path
          d="M2 4C2 4.55228 1.55228 5 1 5C0.447715 5 0 4.55228 0 4C0 3.44772 0.447715 3 1 3C1.55228 3 2 3.44772 2 4Z"
          fill="#4AB4FF"/>
        <path
          d="M2 7C2 7.55228 1.55228 8 1 8C0.447715 8 0 7.55228 0 7C0 6.44772 0.447715 6 1 6C1.55228 6 2 6.44772 2 7Z"
          fill="#4AB4FF"/>
      </svg>
    </button>
    <transition name="dropdown-slide">
      <div v-if="isDropdownOpen" class="dropdown" :class="dropdownPosition">
        <ul>
          <li class="dropdown-item" @click="selectItem('Option 1')">Первый</li>
          <li class="dropdown-item dropdown-item-disabled" @click="selectItem('Option 2')">Второй</li>
          <li class="dropdown-item" @click="selectItem('Option 3')">Третий</li>
          <li class="dropdown-item" @click="selectItem('Option 4')">Четвертый</li>
          <li class="dropdown-item" @click="selectItem('Option 5')">Пятый</li>
          <li class="dropdown-item" @click="selectItem('Option 6')"> Шестой</li>
        </ul>
      </div>
    </transition>
  </div>
</template>

<script>
import ClickOutsideDirective from '../directives/ClickOutsideDirective';

export default {
  directives: {
    'click-outside': ClickOutsideDirective,
  },
  data() {
    return {
      isDropdownOpen: false,
      dropdownPosition: '',
    };
  },
  methods: {
    toggleDropdown() {
      this.isDropdownOpen = !this.isDropdownOpen;
      this.calculateDropdownPosition();
    },
    closeDropdown() {
      this.isDropdownOpen = false;
    },
    selectItem(item) {
      console.log('Selected item:', item);
    },
    calculateDropdownPosition() {
      const buttonRect = this.$el.getBoundingClientRect();
      const windowHeight = window.innerHeight;

      if (windowHeight - buttonRect.bottom > 200) {
        this.dropdownPosition = 'dropdown-below';
      } else {
        this.dropdownPosition = 'dropdown-above';
      }
    },
  },
};
</script>

<style scoped>
.dropdown-container {
  position: relative;
  display: inline-block;
}

.btn {
  position: relative;
  z-index: 2;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 24px;
  height: 24px;
  padding: 4px;
  cursor: pointer;
  background: var(--primary-700);
  border: 1px solid var(--secondary-500);
  border-radius: 2px;
}

.dropdown {
  position: absolute;
  top: 1px;
  z-index: 1;
  width: 200px;
  background: var(--primary-700);
  box-shadow: 0px 0px 6px rgba(0, 0, 0, 0.75);
  border-radius: 2px;
  padding: 1px 0;
}

.dropdown ul {
  list-style: none;
  padding: 0;
  margin: 0;
}

.dropdown-item {
  padding: 6px 12px;
  cursor: pointer;
  color: var(--white);
  font-size: 14px;
  line-height: 20px;
  border-left: 2px solid transparent;
  background-color: var(--primary-500);
}

.dropdown-item:hover {
  background-color: var(--primary-400);
}

.dropdown-item:active {
  border-left: 2px solid var(--secondary-500);
  background-color: var(--primary-700);
}

.dropdown-item-disabled {
  color: var(--gradients-gray);
}


.dropdown-slide-enter-active, .dropdown-slide-leave-active {
  transition: opacity 0.3s;
}

.dropdown-slide-enter, .dropdown-slide-leave-to {
  opacity: 0;
}

.dropdown-below {
  top: 108%;
  right: 0;
}

/* Add additional styles for other positions if needed */
</style>
