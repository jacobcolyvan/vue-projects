<template>
  <div id="main">
    <DefaultOptions :unarrangedChoices="unarrangedChoices" />
    <ArrangedOptions :arrangedChoices="arrangedChoices" />
  </div>
</template>

<script>
import {ref} from 'vue'
import choicesObject from './assets/choices.json'

import DefaultOptions from './components/DefaultOptions'
import ArrangedOptions from './components/ArrangedOptions'

export default {
  name: 'choice-slider',
  components: {
    DefaultOptions,
    ArrangedOptions,
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

<style lang="scss">

* {
  box-sizing: border-box;
}

#main {
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
