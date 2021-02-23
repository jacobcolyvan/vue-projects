<template>
  <div class="option-div" id="option-div2">
      <p>Choose the order you want to arrange them in below.</p>
      <div class="draggable-cont" >
        <draggable
          id="arranged-options"
          class="draggable"
          :list="arrangedChoices"
          group="choices"
          item-key="id"
        >
          <template #item="{element}">
            <div class="choice">{{element.choice}}</div>
          </template>
        </draggable>
      </div>
    </div>
</template>

<script>
import draggable from 'vuedraggable'

export default {
  name: 'ArrangedOptions',
  components: {
    draggable
  },
  props: {
    arrangedChoices: {
      type: Array,
      required: true
    }
  }
}
</script>

<style lang="scss" scoped>

</style>