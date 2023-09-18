<template>
  <div class="dropdown-container" v-click-outside="closeDropdown">
    <button class="btn" @click="toggleDropdown">
      <DropdownIcon/>
    </button>
    <transition name="dropdown-slide">
      <div v-if="isDropdownOpen" class="dropdown" :class="dropdownPosition">
        <ul>
          <li class="dropdown-item" @click="selectItem('Option 1')">Первый</li>
          <li class="dropdown-item" @click="selectItem('Option 2')">Второй</li>
          <li class="dropdown-item" @click="selectItem('Option 3')">Третий</li>
          <li class="dropdown-item dropdown-item-disabled" @click="selectItem('Option 4')">Четвертый</li>
          <li class="dropdown-item dropdown-item-disabled" @click="selectItem('Option 5')">
            <DummyImage class="dropdown-item-icon"/>
            Пятый
          </li>
          <li class="dropdown-item" @click="selectItem('Option 6')">
            <DummyImage class="dropdown-item-icon"/>
            Шестой
          </li>
        </ul>
      </div>
    </transition>
  </div>
</template>

<script>
import ClickOutsideDirective from '../directives/ClickOutsideDirective';
import DummyImage from '../assets/icons/dummy-image.svg';
import DropdownIcon from '../assets/icons/dropdown-icon.svg';

export default {
  components: {
    DummyImage,
    DropdownIcon,
  },
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

      if (buttonRect.left > 200) {
        this.dropdownPosition += ' dropdown-left';
      } else {
        this.dropdownPosition += ' dropdown-right';
      }
    },
  },
};
</script>

<style scoped>
.dropdown-container {
  position: relative;
  display: inline-block;
  align-self: flex-start;
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
  display: flex;
  align-items: center;
  padding: 6px 12px;
  cursor: pointer;
  color: var(--white);
  font-size: 14px;
  line-height: 20px;
  border-left: 2px solid transparent;
  background-color: var(--primary-500);
}

.dropdown-item-icon {
  margin-right: 6px;
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
  pointer-events: none;
}


.dropdown-slide-enter-active, .dropdown-slide-leave-active {
  transition: opacity 0.3s;
}

.dropdown-slide-enter, .dropdown-slide-leave-to {
  opacity: 0;
}

.dropdown-below {
  top: 108%;
}

.dropdown-above {
  top: -200px;
}

.dropdown-right {
  left: 0
}

.dropdown-left {
  right: 0
}

/* Add additional styles for other positions if needed */
</style>
