<template>
  <form @submit.prevent="handleSubmit">
    <div class="form-group form-check" v-for="item in Items" v-bind:key="item.id">
      <label class="form-check-label" :for="item.id">{{ item.title }}</label>
      <input type="checkbox" v-model="user.fruitCollection" :id="item.id" :value="item.title">
    </div>
    <!-- print result -->
    <div class="form-group">
      {{ user.fruitCollection }}
    </div>
    <div class="form-group">
      <button class="btn btn-primary">Submit</button>
    </div>
  </form>
</template>
<script>
export default {
  data() {
    return {
      Items: [
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
      user: {
        fruitCollection: [],
      },
    };
  },
  methods: {
    handleSubmit() {
      alert(JSON.stringify(this.user));
    },
  },
};
</script>
