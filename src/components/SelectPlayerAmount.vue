<template>
  <div id="select-player-amounts">
    <button
      v-for="(amountValue, index) in playerAmountArray"
      :key="index"
      class="amount-button"
      v-bind:id="amountValue === numberOfPlayers? 'selected': false"
      v-on:click="$emit('togglePlayerAmount', amountValue)"
    >
      {{ amountValue }}
    </button>

    <!-- NOTE:  -->
  </div>
</template>

<script>
  export default {
    name: "SelectPlayerAmount",
    props: {
      numberOfPlayers: {
        type: Number,
        required: true
      },
      playerAmountArray: {
        type: Object,
        required: true
      },
    },
  }
</script>

<style lang="scss" scoped>
#select-player-amounts {
  width: 90vw;
  max-width: 500px;
  margin-bottom: 12px;

  .amount-button {
    width: calc(100% / 3);
    border: 1px solid #6060c7;

    &:hover {
      cursor: pointer;
    }

    &:focus {
      outline: none;
      box-shadow: none;
    }
  }

  #selected {
    border: 1px solid #df6a6a;
  }

}

</style>