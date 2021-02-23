<template>
  <div id="app">
    <div class="option-div" id="option-div1">
      <h3>Choices:</h3>
      <div class="draggable-cont">
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
    </div>

    <div class="option-div" id="option-div2">
      <p>Choose the order you want to arrange them in below.</p>
      <div class="draggable-cont" >
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
  color: #2c3e50;
  margin-top: 90px;


  width: 100%;
  min-height: 300px;
  border: 1px solid #026691;
  display: flex;
  flex-direction: row;
  justify-content: space-evenly;
  align-items: center;

  padding: 0 4%;

  p, div {
    font-size: 1rem;
  }

  .option-div {
    width: 100%;
    height: 100%;
    display: flex;
    flex-direction: column;
    justify-content: space-evenly;

    h3, p {
      color: #37383C;
    }

    h3 {
      font-style: italic;
      text-decoration: underline;
      margin: 0 0 2px 0;
    }

    p {
      font-weight: 200;
      font-style: italic;
      margin: 0 0 4px 0;
    }

    .draggable-cont {
      display: flex;
      width: 100%;

      .draggable {
        border: 1px solid #026691;
        width: 100%;
      }

      #default-options {
        display: flex;
        flex-direction: column;
        justify-content: flex-start;

        min-height: 240px;
        padding: 12px 2%;

        .choice {
          width: 100%;
          height: 25%;
        }
      }

      #arranged-options {
        display: flex;
        flex-direction: row;
        justify-content: center;

        min-height: 60px;
        padding: 3px 2%;


        .choice {
          width: 25%;
          height: 100%;
        }
      }
    }

    .choice {
      display: flex;
      align-items: center;
      justify-content: center;

      background-color: #25AC82;
      color: #FFFFFF;

      border: 1px solid #1b8362;
      margin: 1px;

      &:hover {
        cursor: pointer;
      }
    }
  }

  #option-div1 {
    width: 18%;
  }

  #option-div2 {
    width: 72%;
  }


  @media screen and (max-width: 1000px) {
    padding: 0;

    p, div { font-size: 0.9rem; }

    #option-div1 {
      width: 19.5%;
    }

    #option-div2 {
      width: 78%;
    }
  }
}
</style>
