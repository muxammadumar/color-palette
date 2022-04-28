<template>
  <div class="color">
    <div :style="{ backgroundColor: color.color }" class="color_example">
      <img src="../../public/copy.png" v-clipboard:copy="color.color" />
    </div>
    <div class="text">
      <div class="lock-wrapper">
        {{ color.color }}

        <img
          class="lock"
          :class="{ locked: color.locked }"
          @click="color.locked = !color.locked"
          src="../../public/lock.png"
        />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["color"],
};
</script>

<style lang="scss">
.color {
  background-color: #edf2f7;
  padding: 12px;
  border-radius: 20px;
  .color_example {
    padding: 10px;
    border-radius: 10px;
    width: 100%;
    height: 250px;
    position: relative;
    img {
      cursor: pointer;
      position: absolute;
      top: 10px;
      right: 10px;
    }
  }
  .text {
    padding: 20px 0;
    .lock-wrapper {
      display: flex;
      align-items: center;
      justify-content: space-between;
      max-width: 150px;
      margin: 0 auto;
      .lock {
        width: 32px;
        height: 32px;
        cursor: pointer;
        opacity: 0.3;
        &.locked {
          opacity: 1;
        }
      }
    }
  }
}
</style>