// ClickOutsideDirective.vue

<template>
  <div></div>
</template>

<script>
export default {
  bind(el, binding, vnode) {
    // eslint-disable-next-line no-param-reassign,func-names
    el.clickOutsideEvent = function (event) {
      // Check that the click was outside the el and its children
      if (!(el === event.target || el.contains(event.target))) {
        // Call method provided in the directive's value
        vnode.context[binding.expression](event);
      }
    };
    document.body.addEventListener('click', el.clickOutsideEvent);
  },
  unbind(el) {
    document.body.removeEventListener('click', el.clickOutsideEvent);
  },
};
</script>
