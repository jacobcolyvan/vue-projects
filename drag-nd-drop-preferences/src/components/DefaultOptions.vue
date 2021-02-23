<template>
  <div class="option-div" id="option-div1">
      <h3>Choices:</h3>
      <div class="draggable-cont">
        <draggable
          id="default-options"
          class="draggable"
          :list="unarrangedChoices"
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
  name: 'defaultOption',
  components: {
    draggable
  },
  props: {
    unarrangedChoices: {
      type: Array,
      required: true
    }
  }
}
</script>

<style lang="scss" scoped>

</style>