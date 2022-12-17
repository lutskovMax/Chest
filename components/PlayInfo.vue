<template>
  <div class="menu">
    <img src="../assets/logoMenu.png" alt="" />
    <h3 class="grey__title">1 игра = 5 $</h3>

    <div class="buy">
      <h2>Вам доступно:</h2>
      <div class="buy__row">
        <h3 class="grey__title">Игр:</h3>
        <span class="numbers">{{ availableGame }}</span>
      </div>

      <h2>Покупка:</h2>
      <div class="buy__row">
        <h3 class="grey__title">Игр:</h3>
        <div class="counter">
          <input
            oninput="javascript: if (this.value.length > this.maxLength) this.value = this.value.slice(0, this.maxLength);"
            type="number"
            min="0"
            maxlength="3"
            class="numbers"
            v-model="buyCounter"
          />
          <div class="arrows">
            <div class="arrow top" @click="buyCounter++"></div>
            <div class="arrow bottom" @click="buyCounterDec"></div>
          </div>
        </div>
      </div>

      <div class="buy__row">
        <h3 class="grey__title">Сумма:</h3>
        <span class="numbers"
          >{{ sumToBuy }} <span class="grey__title dollar">$</span></span
        >
      </div>

      <button class="buy__btn" :disabled="buyCounter === 0" @click="buyGames">
        Купить
      </button>
      <div class="fill" v-if="currentResult"></div>
    </div>
  </div>
</template>

<script>
export default {
  data: () => ({
    buyCounter: 0,
    sumForBuy: 0,
    boughtGames: 0,
    activeGames: false,
  }),

  props: {
    activeGame: {
      type: Boolean,
      default: false,
    },

    availableGame: {
      type: Number,
      default: 0,
    },
  },

  computed: {
    sumToBuy() {
      return this.buyCounter * 5;
    },

    currentResult() {
      return (this.boughtGames = this.availableGame);
    },
  },

  methods: {
    buyCounterDec() {
      if (this.buyCounter <= 0) {
        return 0;
      } else {
        this.buyCounter--;
      }
    },

    buyGames() {
      this.boughtGames += Number(this.buyCounter);
      this.buyCounter = 0;
      this.$emit("available-game", this.boughtGames);
    },
  },
};
</script>

<style lang="scss">
.buy__btn {
  background: url("../assets/buy-btn.png") center/cover no-repeat;
  width: 100%;
  color: #52311b;
  font-size: 36px;
  font-weight: 400;
  text-align: center;
  text-transform: uppercase;
  padding: 16px;

  &:hover {
    transform: scale(1.05);
  }
}

.counter {
  color: #fff;
  display: flex;
  align-items: center;
  gap: 10px;

  .arrow {
    margin-left: 5px;
    width: 6px;
    height: 6px;
    border-top: 2px solid #fff;
    border-right: 2px solid #fff;
    padding: 3px;

    &.bottom {
      transform: rotate(135deg);
    }

    &.top {
      transform: rotate(-45deg);
    }
  }
}

input:active,
input:hover,
input:focus {
  outline: 0;
  outline-offset: 0;
}

input[type="number"] {
  -moz-appearance: textfield;
  color: #fec602;
}
input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button {
  appearance: none;
  -webkit-appearance: none;
  -moz-appearance: none;
}

.grey__title.dollar {
  font-size: 24px;
}

.menu {
  max-width: 228px;
  padding: 25px 20px;
  z-index: 7;
  position: absolute;
  top: 50%;
  -webkit-transform: translate(25%, -50%);
  -ms-transform: translate(25%, -50%);
  transform: translate(25%, -50%);
  background: url("../assets/buy_bg.png") center/cover no-repeat;
}

.buy {
  h2 {
    color: #fff;
    font-size: 18px;
  }

  &__row {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  input {
    background: none;
    width: 45px;
  }

  .numbers {
    text-shadow: -4px 6px 3px rgba(31, 32, 32, 0.4);
    color: #fec602;
    font-size: 30px;
    font-weight: 400;
    text-align: right;
  }
}

.grey__title {
  text-shadow: -4px 6px 3px rgba(31, 32, 32, 0.4);
  color: #a3a09f;
  font-size: 15px;
  font-weight: 400;
  line-height: 36px;
  text-transform: uppercase;
}
</style>
