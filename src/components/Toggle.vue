<template>
  <div class="toggle" @click="toggle">
    <div :class="{ 'toggle-switch': true, 'toggle-on': toggled }"></div>
  </div>
</template>

<script>

export default {
  data() {
    return {
      toggled: false
    };
  },
  methods: {
    toggle() {
      this.toggled = !this.toggled;
    }
  }
};
</script>

<style scoped>
.toggle {
  width: 50px;
  height: 25px;
  background-color: #ccc;
  border-radius: 25px;
  position: relative;
  cursor: pointer;
}

.toggle-switch {
  width: 25px;
  height: 25px;
  border-radius: 50%;
  background-color: #fff;
  position: absolute;
  transition: transform 0.3s;
}

.toggle-on {
  transform: translateX(100%);
}
</style>
