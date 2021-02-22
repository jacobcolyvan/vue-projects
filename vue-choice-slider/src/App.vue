<template>
  <div id="app">
    <div class="draggable-cont" id="draggable-cont1">
      <draggable
        id="default-options"
        class="draggable"
        :list="unarrangedChoices"
        group="choices"
      >
        <template #item="{element}">
          <div class="choice">{{element.choice}}</div>
        </template>
      </draggable>
    </div>

    <div class="draggable-cont" id="draggable-cont2">
      <draggable
        id="arranged-options"
        class="draggable"
        :list="arrangedChoices"
        group="choices"
      >
        <template #item="{element}">
          <div class="choice">{{element.choice}}</div>
        </template>
      </draggable>
    </div>
  </div>
</template>

<script>
import {ref} from 'vue'
import draggable from 'vuedraggable'
import choicesObject from './assets/choices.json'

export default {
  name: 'choice-slider',
  components: {
    draggable
  },
  setup() {
    const unarrangedChoices = ref([...choicesObject.choices]);
    const arrangedChoices = ref([]);

    return {
      unarrangedChoices,
      arrangedChoices
    }
  }
}
</script>

<style lang="scss" scoped>
* {
  box-sizing: border-box;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 90px;


  width: 100%;
  min-height: 300px;
  border: 1px solid black;
  display: flex;
  flex-direction: row;
  justify-content: space-evenly;
  align-items: center;


  .draggable-cont {
    display: flex;
    border: 1px solid #042c99;

    .draggable {
      width: 100%;
    }


    #default-options {
      display: flex;
      flex-direction: column;
      justify-content: flex-start;

      min-height: 200px;
      padding: 12px 2%;

      div {
        width: 100%;
        height: 25%;
      }
    }

    #arranged-options {
      display: flex;
      flex-direction: row;
      justify-content: center;

      min-height: 50px;
      padding: 3px 2%;


      div {
        width: 25%;
        height: 100%;
      }
    }
  }

  #draggable-cont1 {
    width: 18%;
  }

  #draggable-cont2 {
    width: 72%;
  }

  .choice {
    display: flex;
    align-items: center;
    justify-content: center;

    border: 1px solid black;

    &:hover {
      cursor: pointer;
    }
  }
}
</style>
