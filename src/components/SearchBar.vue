<template>
  <div>
    <input @input="onInput" />
  </div>
</template>

<script>
export default {
  name: "SearchBar",
  methods: {
    onInput: function(event) {
      this.$emit("termChange", event.target.value);
    },
  },
};
</script>

<!-- "scoped" is there so the CSS is applied only for this component, 
by default it becomds global -->
<style scoped>
input {
  width: 75%;
}

div {
  text-align: center;
  margin: 1.25rem;
}
</style>
