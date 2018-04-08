<template>
  <div class='fancy-price'
       :class='{"fancy-price--debug": debug}'>
    <FancyCharacter v-for='(character, index) in characters'
                    :key='index'
                    :debug='debug'
                    :value='character' />
  </div>
</template>

<script>
import FancyCharacter from "@/components/FancyCharacter.vue";

export default {
  name: "FancyPrice",
  components: {
    FancyCharacter
  },
  props: {
    price: {
      type: [Number, String],
      default: 0
    },
    debug: {
      type: Boolean,
      default: false
    }
  },
  computed: {
    characters() {
      return this.prettyPrice.split("");
    },
    prettyPrice() {
      const priceAsInteger = parseInt(this.price);
      return `$${priceAsInteger.toLocaleString("en")}`;
    }
  }
};
</script>

<style lang="scss" scoped>
.fancy-price {
  display: inline-flex;

  &--debug {
    border: 1px solid red;
  }
}
</style>
