<template>
  <div class='fancy-character'>
    <div class='fancy-character__list'
         :class='{"fancy-character__list--debug": debug}'
         :style='styles'>
      <div v-for='(item, index) in list'
           class='fancy-character__item'
           :key='index'>
        {{ item }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "FancyCharcater",
  props: {
    value: {
      type: String
    },
    debug: {
      type: Boolean,
      default: false
    },
    list: {
      type: Array,
      default() {
        return [
          "$",
          ".",
          ",",
          "0",
          "1",
          "2",
          "3",
          "4",
          "5",
          "6",
          "7",
          "8",
          "9"
        ];
      }
    }
  },
  computed: {
    styles() {
      const index = this.list.indexOf(this.value);
      const offset = index * -24;

      return {
        transform: `translateY(${offset}px)`
      };
    }
  }
};
</script>

<style lang="scss" scoped>
$character-height: 24px;
$character-width: $character-height / 2;

.fancy-character {
  height: $character-height;
  text-align: center;
  width: $character-width;
  overflow: hidden;

  &__list {
    transition: transform 1.2s cubic-bezier(0.165, 0.84, 0.44, 1) 0.2s;

    &--debug {
      border: 1px solid blue;
    }
  }

  &__item {
    height: $character-height;
  }
}
</style>
