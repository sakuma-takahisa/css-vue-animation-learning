<template>
  <v-app>
    <v-content>
      <v-container fluid>
        <h1 class="text-center mb-6 ">Vuetify</h1>
        <div class="text-center mb-4">
          <v-btn @click="add">add</v-btn>
          <v-btn @click="remove">remove</v-btn>
        </div>
        <transition-group appear name="cards" @before-enter="beforeEnter" @after-enter="afterEnter">
          <v-card
            class="mx-auto mb-2 card"
            color="#26c6da"
            dark
            max-width="400"
            v-for="(item, index) in items"
            :key="item"
            :data-index="index"
          >
            <v-card-title>
              <v-icon large left>
                mdi-twitter
              </v-icon>
              <span class="title font-weight-light">{{ item }} </span>
            </v-card-title>
            <!-- <v-card-text class="headline font-weight-bold">
              "Turns out semicolon-less style is easier and safer in TS because most gotcha edge cases are type invalid
              as well."
            </v-card-text> -->
          </v-card>
        </transition-group>
      </v-container>
    </v-content>
  </v-app>
</template>

<script>
export default {
  data() {
    return {
      items: [1, 2, 3, 4, 5, 6, 7]
    }
  },
  mounted() {
    // for (let i = 0; i < 7; i++) {
    //   setTimeout(() => {
    //     this.items.push(i)
    //   }, i * 200)
    // }
  },
  methods: {
    add() {
      this.items.splice(Math.random() * this.items.length, 0, this.items.length + 1)
    },
    remove() {
      this.items.splice(Math.random() * this.items.length, 1)
    },
    beforeEnter(el) {
      el.style.transitionDelay = 100 * parseInt(el.dataset.index, 10) + 'ms'
      console.log('before Enter')
    },

    afterEnter(el) {
      el.style.transitionDelay = ''
      console.log('after Enter')
    }
  }
}
</script>

<style lang="scss" scoped>
.cards {
  &-enter {
    opacity: 0;
    transform: scale(0.5) translateX(100%);
  }
  &-leave {
    &-to {
      opacity: 0;
      // transform: scale(0.5) translateX(100%);
      transform: scale(0.5);
    }
    &-active {
      position: absolute;
      left: 50%;
      transform: translate(-50%); //←これを無効で右にスライドしながら消える
      width: 400px; //幅固定にしないとcardがinline-blockになって横幅縮む
    }
  }
}

.card {
  transition: 0.5s;
  // display: inline-block;
}
</style>
