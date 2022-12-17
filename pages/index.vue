<template>
  <div class="chest">
    <div class="chest__body">
      <div class="chest__left-bg">
        <div class="chest__play-place">
          <fire class="tourch_animation" />
          <div class="chest__wrap">
            <img class="chest__logo" src="../assets/Logo-main.png" alt="" />
            <div class="chest__place">
              <div
                class="chest__item"
                @click="openChest(item.itemKey)"
                :key="item.itemKey"
                v-for="item in items"
              >
                <img
                  :class="{ animate: activeGame }"
                  v-if="
                    (lostGame !== item.itemKey && vinGame !== item.itemKey) ||
                    activeGame
                  "
                  src="..//assets/chest.png"
                  alt=""
                />

                <div class="OpenedBox" v-if="!activeGame">
                  <img
                    v-if="vinGame === item.itemKey && vinPart"
                    :src="require(`../static/${item.VinImage}`)"
                    alt="/"
                  />

                  <img
                    v-if="lostGame === item.itemKey && !vinPart"
                    :src="require(`../static/${item.lostImage}`)"
                    alt="/"
                  />
                </div>
              </div>
            </div>
            <p class="instruction">
              Для игры Вам необходимо купить попытки, а затем нажать кнопку
              “ИГРАТЬ”
            </p>
          </div>
          <div class="varvar">
            <img class="varvar__image" src="../assets/Varvar.png" alt="/" />
            <div class="hint">
              <span>
                {{ varvarText }}
              </span>
            </div>

            <button
              class="play__btn"
              :disabled="isNotAvailableGame || activeGame"
              @click="toPlay"
            >
              ИГРАТЬ
            </button>
          </div>
        </div>
      </div>

      <div class="chest__right-bg">
        <img src="../assets/chest-right.png" alt="" />
        <div class="main">
          <PlayInfo
            @available-game="isAvailableGame"
            :availableGame="availableGame"
            :activeGame="activeGame"
          />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "IndexPage",
  data: () => ({
    activeGame: false,
    availableGame: 0,
    openedGame: false,
    playedGame: 0,
    playedGame: 0,
    disableBtn: false,
    vinPart: true,
    vinGame: null,
    lostGame: null,
    openedGame: false,
    activeChestGame: false,
    items: [
      {
        VinImage: "vin-chest.png",
        lostImage: "lost-chest.png",
        itemKey: 1,
      },

      {
        VinImage: "vin-chest.png",
        lostImage: "lost-chest.png",
        itemKey: 2,
      },
      {
        VinImage: "vin-chest.png",
        lostImage: "lost-chest.png",
        itemKey: 3,
      },
      {
        VinImage: "vin-chest.png",
        lostImage: "lost-chest.png",
        itemKey: 4,
      },
      {
        VinImage: "vin-chest.png",
        lostImage: "lost-chest.png",
        itemKey: 5,
      },
      {
        VinImage: "vin-chest.png",
        lostImage: "lost-chest.png",
        itemKey: 6,
      },
      {
        VinImage: "vin-chest.png",
        lostImage: "lost-chest.png",
        itemKey: 7,
      },
      {
        VinImage: "vin-chest.png",
        lostImage: "lost-chest.png",
        itemKey: 8,
      },
      {
        VinImage: "vin-chest.png",
        lostImage: "lost-chest.png",
        itemKey: 9,
      },
    ],
  }),

  computed: {
    isNotAvailableGame() {
      return this.availableGame === 0;
    },

    varvarText() {
      if (this.activeGame) {
        return "Вскрой сундук, который по твоему мнению выиграшный! Удачи!";
      }

      if (this.openedGame && this.vinPart && !this.isNotAvailableGame) {
        return "Поздаравляем ты открыл выиграшный сундук! Так Держать!";
      }

      if (this.openedGame && !this.vinPart && !this.isNotAvailableGame) {
        return "Не повезло! Не отчаивайся, в слейдущий раз точно повезёт!";
      }

      if (this.openedGame && this.vinPart && this.isNotAvailableGame) {
        return "Поздаравляем ты выиграл! Что-бы продолжить жми КУПИТЬ!";
      }

      if (this.openedGame && !this.vinPart && this.isNotAvailableGame) {
        return "Не повезло! Не отчаивайся. Что-бы продолжить жми КУПИТЬ!";
      }

      return "Вскрывай сундуки из моей сокровищницы! Ищи несметные богатства!";
    },
  },

  methods: {
    isAvailableGame(data) {
      this.availableGame = data;
    },

    toPlay() {
      this.openedGame = false;
      this.activeGame = true;
      this.playedGame++;
      this.disableBtn = true;
      this.availableGame--;
      this.vinPart = !this.vinPart;
    },

    openChest(key) {
      if (this.activeGame) {
        (this.lostGame = key), (this.vinGame = key);
        this.openedGame = true;
        this.activeGame = false;
      }
    },
  },
};
</script>

<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=PT+Sans&display=swap");
@font-face {
  font-family: "aBremen";
  src: url("../assets/fonts/aBremen.ttf");
}

.chest__logo {
  margin-bottom: 20px;
}

.tourch_animation {
  position: absolute;
  top: 24%;
  -webkit-transform: translate(25%, -50%);
  -ms-transform: translate(25%, -50%);
  transform: translate(25%, -50%);
  left: 0;
}

.instruction {
  font-family: "PT Sans", sans-serif;
  line-height: 20px;
  text-shadow: 0 0 30px #1f2020;
  font-size: 16px;
  font-weight: 400;
  color: #fff;
  text-align: center;
  max-width: 307px;
  margin: 0 auto;
}

.chest__place {
  max-width: 515px;
  max-height: 515px;
  margin: 0 auto;
  display: grid;
  grid-template-columns: repeat(3, 1fr);
}
.chest__item {
  background: url("..//assets/Chest_bg.png") center/cover no-repeat;
  width: 165px;
  height: 165px;

  img {
    transform: scale(0.8);
    transition: 0.2s;
  }

  .OpenedBox img {
    transform: scale(1);
  }

  img.animate {
    transform: scale(1);
  }
}

.varvar {
  position: relative;
  transform: translateX(80px);

  &__image {
    height: 694px;
    width: 411px;
  }
}

.play__btn {
  background: url("../assets/play_btn.png") center/cover no-repeat;
  width: 228px;
  color: #333333;
  font-size: 36px;
  font-weight: 400;
  text-align: center;
  text-transform: uppercase;
  padding: 16px;
  position: absolute;
  bottom: 100px;
  transition: 0.2s;

  &:hover {
    transform: scale(1.05);
  }
}

.hint {
  font-family: "aBremen";
  display: flex;
  align-items: flex-end;
  position: absolute;
  top: 121px;
  left: -40px;
  background: url("../assets/Prompt\ box.png") center/cover no-repeat;
  width: 310px;
  height: 289px;

  span {
    color: #333333;
    font-size: 22px;
    font-weight: bold;
    line-height: 22px;
    text-align: center;
    padding: 0 15px;
    padding-bottom: 39px;
  }
}

.chest {
  position: relative;
  font-family: "aBremen";
  height: 100vh;
  &__body {
    height: 100vh;
    display: flex;
    align-items: center;
    justify-content: space-between;
    margin: 0 auto;
  }
}

.chest__left-bg {
  height: 100vh;
  flex: 0 1 70%;
  display: flex;
  align-items: center;
  background: url("../assets/chest_main-left.png") center/cover no-repeat;
}

.chest__right-bg {
  position: relative;
  flex: 0 1 30%;
  height: 100vh;

  img {
    position: relative;
    z-index: 4;
    height: 100%;
    width: 100%;
  }
}

.chest__play-place {
  display: flex;
  align-items: center;
  max-width: 860px;
  margin: 0 0 0 auto;
}

*,
*::before,
*::after {
  box-sizing: border-box;
}

ul[class],
ol[class] {
  padding: 0;
}

body,
h1,
h2,
h3,
h4,
p,
ul[class],
ol[class],
li,
figure,
figcaption,
blockquote,
dl,
dd {
  margin: 0;
}

body {
  min-height: 100vh;
  scroll-behavior: smooth;
  text-rendering: optimizeSpeed;
  line-height: 1.5;
  margin: 0;
}

ul[class],
ol[class] {
  list-style: none;
}

a:not([class]) {
  text-decoration-skip-ink: auto;
}

img {
  max-width: 100%;
  display: block;
}

input,
button,
textarea,
select {
  font: inherit;
}
</style>
