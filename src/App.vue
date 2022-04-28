<template>
  <div id="app">
    <div class="top" @keyup.space="refreshColor()">
      <p class="title">Color Palette Generator</p>

      <div class="buttons">
        <div @click="addColor()" class="button">Add a color</div>
        <div @click="removeColor()" class="button">Remove color</div>
      </div>
    </div>

    <div class="colors">
      <Color v-for="(color, index) in colors" :key="index" :color="color" />
    </div>

    <div class="bottom">
      <div class="refresh-colors" @click="refreshColor()">Generate Palette</div>
      <p class="text">
        Or just press <span>space</span> to generate new palettes.
      </p>
    </div>
  </div>
</template>

<script>
import Color from "./components/color.vue";

export default {
  name: "App",
  components: { Color },
  data() {
    return {
      colors: [],
    };
  },
  methods: {
    randomColor: function () {
      var letters = "0123456789abcdef";
      var color = "#";
      for (var i = 0; i < 6; i++) {
        color += letters[Math.floor(Math.random() * 16)];
      }
      return color;
    },
    refreshColor: function () {
      this.colors.forEach((color) => {
        if (!color.locked) {
          color.color = this.randomColor();
        } else {
          return;
        }
      });
    },
    addColor: function () {
      this.colors.push({ color: this.randomColor(), locked: false });
    },
    removeColor: function () {
      this.colors.pop();
    },
  },
  beforeMount: function () {
    window.addEventListener("keyup", (event) => {
      if (event.code === "Space") {
        this.refreshColor();
      }
    });
    for (let i = 0; i < 5; i++) {
      this.colors.push({ color: this.randomColor(), locked: false });
    }
  },
};
</script>

<style lang="scss">
#app {
  height: 100vh;
  * {
    box-sizing: border-box;
    font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
  }
  .top {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    padding: 50px;
    .title {
      font-size: 32px;
      font-weight: 600;
    }
    .buttons {
      display: flex;
      align-items: center;
      justify-content: space-between;
      .button {
        margin-right: 20px;
        padding: 10px 20px;
        background-color: #edf2f7;
        border-radius: 10px;
        font-weight: 600;
      }
    }
  }
  .colors {
    margin: 0 auto;
    max-width: 1440px;
    display: grid;
    grid-template-columns: repeat(5, 1fr);
    grid-column-gap: 30px;
    grid-row-gap: 30px;
  }
  .bottom {
    display: flex;
    align-items: center;
    flex-direction: column;
    padding: 20px 0;
    .refresh-colors {
      cursor: pointer;
      width: fit-content;
      border-radius: 10px;
      font-weight: 600;
      margin: 0 auto;
      padding: 20px 40px;
      font-size: 18px;
      background-color: #edf2f7;
    }
    .text {
      span {
        font-weight: bold;
        border-radius: 5px;
        background-color: #edf2f7;
        padding: 5px;
      }
    }
  }
}
</style>
