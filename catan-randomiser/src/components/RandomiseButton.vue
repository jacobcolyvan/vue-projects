<template>
  <div>
    <button
      id="randomise-button"
      v-on:click="$emit('setReRandomiseToTrue')"
    >
      <i>re-randomise</i>
    </button>
  </div>
</template>

<script>
  export default {
    name: "RandomiseButton",
  }
</script>

<style lang="scss" scoped>
  #randomise-button {
    width: 90vw;
    max-width: 500px;
    margin-top: 12px;

    &:hover {
      cursor: pointer;
    }

    &:focus {
      outline: none;
      box-shadow: none;
    }
  }
</style>