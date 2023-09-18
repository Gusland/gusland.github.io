<template>
  <div class="wrapper">
    <template v-if="isToggle">
      <div :class="{'toggle': true, 'toggle-disabled': disabled}" @click="toggleHandler">
        <div :class="{ 'toggle-switch': true, 'toggle-on': toggled }"></div>
        <div v-bind:class="{'toggle-text': true, 'toggle-text-white': toggled}"> {{ title }}</div>

      </div>
    </template>
    <template v-else>
      <label v-show="!isToggle"
             @click="toggleHandler"
             v-bind:class="{'checkbox-wrapper': true, 'checkbox-wrapper-white': isChecked}"
             :for="id">{{ title }}
        <input :disabled="disabled" type="checkbox" :id="id" v-model="isChecked" @change="toggleHandler"
               :value="title">
        <span class="checkmark">
          <TickIcon/>
        </span>
      </label>
    </template>

  </div>
</template>

<script>
import TickIcon from '../assets/icons/tick.svg';

export default {
  components: { TickIcon },
  props: {
    id: Number,
    title: String,
    disabled: Boolean,
    isToggle: {
      type: Boolean,
      default: false,
    },
  },
  data() {
    return {
      isChecked: false,
      toggled: false,
    };
  },
  methods: {
    toggleHandler() {
      if (this.isToggle) {
        this.toggled = !this.toggled;
        this.$emit('toggle', this.id, this.toggled);
      } else if (!this.disabled) {
        this.$emit('toggle', this.id, this.isChecked);
      }
    },
  },
};
</script>

<style scoped>
.checkbox-wrapper {
  display: block;
  position: relative;
  padding-left: 35px;
  margin-bottom: 12px;
  cursor: pointer;
  font-size: 22px;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
  color: var(--primary-200);
}

.checkbox-wrapper-white {
  color: var(--white);
}

.checkbox-wrapper input {
  position: absolute;
  opacity: 0;
  cursor: pointer;
  height: 0;
  width: 0;
}

.checkmark {
  display: flex;
  justify-content: center;
  align-items: center;
  position: absolute;
  top: 0;
  left: 0;
  height: 20px;
  width: 20px;
  border-radius: 4px;
  background-color: var(--primary-700);
  border: 1px solid var(--primary-400);
  transition: all 0.15s ease-out;
}

/* On mouse-over, add a grey background color */
.checkbox-wrapper:hover input ~ .checkmark {
  background-color: var(--primary-900);
}

.checkbox-wrapper input:disabled ~ .checkmark {
  background-color: var(--primary-500);
  border: 1px solid var(--primary-300);
}

/* When the checkbox is checked, add a blue background */
.checkbox-wrapper input:checked ~ .checkmark {
  color: var(--white);
  border: 1px solid var(--primary-300);
}


/* Create the checkmark/indicator (hidden when not checked) */
.checkmark > svg {
  content: "";
  position: absolute;
  display: none;
}

/* Show the checkmark when checked */
.checkbox-wrapper input:checked ~ .checkmark > svg {
  display: block;
}

input:checked {
  color: var(--white);
}

.wrapper {
  width: 400px;
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  justify-content: center;
}


.toggle {
  display: flex;
  align-items: center;
  width: 44px;
  height: 20px;
  background-color: var(--primary-700);
  border: 1px solid var(--primary-400);
  border-radius: 4px;
  position: relative;
  cursor: pointer;
  margin-bottom: 10px;
}

.toggle-disabled {
  pointer-events: none;
  background: var(--primary-500);
  border: 1px solid var(--primary-300);
}

.toggle:hover {
  background-color: var(--primary-900);
}

.toggle:active {
  border: 1px solid var(--primary-300);
}

.toggle-switch {
  width: 16px;
  height: 16px;
  position: absolute;
  top: 2px;
  left: 2px;
  border-radius: 2px;
  background-color: var(--primary-200);
  transition: transform 0.3s, color 0.3s;
}

.toggle-text {
  position: relative;
  left: 50px;
  font-size: 22px;
  color: var(--primary-200);
}

.toggle-text-white {
  color: var(--white);
}

.toggle-on {
  background-color: var(--secondary-500);
  transform: translateX(24px);
}
</style>
