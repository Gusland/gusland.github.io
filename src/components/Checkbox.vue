<template>
  <div class="wrapper">
    <label v-show="!isToggle"
           @click="toggleCheckbox"
           v-bind:class="{'checkbox-wrapper': true, 'checkbox-wrapper-white': isChecked}"
           :for="id">{{ title }}
      <input :disabled="disabled" type="checkbox" :id="id" v-model="isChecked" @change="toggleCheckbox"
             :value="title">
      <span class="checkmark">
          <svg width="11" height="9" viewBox="0 0 11 9" fill="none" xmlns="http://www.w3.org/2000/svg">
            <path
              d="M4.00002 8.4L0.300019 4.7C0.117455 4.51371 0.0157851 4.2629 0.0171025 4.00207C0.0184198 3.74125 0.122618 3.49148 0.307054 3.30704C0.49149 3.1226 0.741261 3.0184 1.00209 3.01709C1.26292 3.01577 1.51373 3.11744 1.70002 3.3L4.00002 5.6L9.30002 0.300004C9.48631 0.11744 9.73712 0.0157699 9.99795 0.0170872C10.2588 0.0184046 10.5085 0.122603 10.693 0.307039C10.8774 0.491475 10.9816 0.741246 10.9829 1.00207C10.9843 1.2629 10.8826 1.51371 10.7 1.7L4.00002 8.4Z"
              fill="#4AB4FF"/>
          </svg>
        </span>
    </label>

    <!--    <label class="switch">-->
    <!--      <input type="checkbox">-->
    <!--      <span class="slider"></span>-->
    <!--    </label>-->
  </div>
</template>

<script>
export default {
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
    };
  },
  methods: {
    toggleCheckbox() {
      if (!this.disabled) {
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


@keyframes draw-checkbox {
  0% {
    stroke-dashoffset: 33;
  }
  100% {
    stroke-dashoffset: 0;
  }
}
</style>
