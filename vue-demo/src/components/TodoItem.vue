<template>
  <li>
    <slot name="prefix"></slot>
    <span v-if="!del"> {{ title }} </span>
    <span class="red" v-else style="text-decoration: line-through"> {{ title }} </span>
    <slot name="suffix" :value="value">DEFAULT</slot>
    <button v-show="!del" @click="handleClick">Delete</button>
  </li>
</template>
<script>
export default {
  props: {
    title: String,
    del: {
      type: Boolean,
      default: false,
    },
  },
  data: function () {
    return {
      value: Math.random(),
    };
  },
  methods: {
    handleClick() {
      console.log("You have clicked delete button.");
      this.$emit("delete", this.title);
    },
  }
}
</script>
<style scoped>
.red {
  color: red
}
</style>
