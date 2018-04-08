<template>
  <div id="app">
    <div id='app-container'>
      <div class='pricing-example'>
        <div class="columns">
          <div class='pricing-stats column'>
            <div>
              <div class="field">
                <label class="label">Price</label>
                <div class="control">
                  <input type="number"
                         class='input is-small'
                         v-model='price'>
                  <div class='control-group'>
                    <button class='button is-small control-button'
                            @click='increment'>+</button>
                    <button class='button is-small control-button'
                            @click='decrement'>-</button>
                  </div>
                  <div class='control-group'>
                    <button class='button is-small control-button'
                            :class='{"is-primary": auto }'
                            @click='toggleAutomaticValues'>
                      Auto
                    </button>
                    <button class='button is-small control-button'
                            :class='{"is-primary": debug }'
                            @click='debug = !debug'>
                      Debug
                    </button>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class='fancy-price-wrapper column'>
            <label class="label">Fancy Price</label>
            <FancyPrice :price='price'
                        :debug='debug' />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import FancyPrice from "@/components/FancyPrice.vue";

const MAX_AUTO_PRICE = 10000000;
const AUTO_INTERVAL_IN_MS = 2000;

export default {
  name: "app",
  components: {
    FancyPrice
  },
  data() {
    return {
      price: 12345,
      auto: false,
      debug: false
    };
  },
  methods: {
    increment() {
      this.price += 1;
    },
    decrement() {
      this.price -= 1;
    },
    toggleAutomaticValues() {
      if (this.auto) {
        clearInterval(this.automaticValues);
      } else {
        this.automaticValues = setInterval(() => {
          this.price = Math.floor(Math.random() * MAX_AUTO_PRICE);
        }, AUTO_INTERVAL_IN_MS);
      }
      this.auto = !this.auto;
    }
  }
};
</script>

<style>
#app {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100vh;
}

.pricing-example {
  width: 300px;
}

.control-button {
  margin-right: 6px;
}

.control-group {
  margin-top: 6px;
}
</style>
