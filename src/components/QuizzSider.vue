<template>
  <div class="quizz-slider" :class="{ 'quizz-slider--open': value }">
    <header class="quizz-slider-header">
      <button class="quizz-slider_btn" @click="toggleSLider">
        <svg
          v-if="!value"
          xmlns="http://www.w3.org/2000/svg"
          class="h-6 w-6"
          fill="none"
          viewBox="0 0 24 24"
          stroke="currentColor"
          width="22px"
        >
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            stroke-width="2"
            d="M15 19l-7-7 7-7"
          />
        </svg>
        <svg
          v-else
          xmlns="http://www.w3.org/2000/svg"
          class="h-6 w-6"
          fill="none"
          viewBox="0 0 24 24"
          stroke="currentColor"
          width="22px"
        >
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            stroke-width="2"
            d="M9 5l7 7-7 7"
          />
        </svg>
      </button>
      <div class="soat">
        <Clock />
      </div>
    </header>
    <div v-if="value" class="quizz-app">
      <div class="header_bottom">
        <p>Matematika</p>
        <h3>{{ count }}/{{ quiz.length }}</h3>
      </div>
      <div class="quizzNumber">
        <div class="num" :class="{ num_item: qiymat }">
          <button
            v-for="(btn, idd) in quiz"
            :key="idd"
            class="btn"
            :class="btn.userAnswer ? 'active' : ''"
            ref="butts"
            @click="emitScroll(btn)"
          >
            {{ idd + 1 }}
          </button>
        </div>
      </div>
    </div>
    <div v-else></div>
  </div>
</template>

<script>
import Clock from "./Clock.vue";
export default {
  name: "QuizzSider",
  components: {
    Clock,
  },
  props: {
    isClass: {
      type: Boolean,
      required: true,
    },
    value: {
      type: Boolean,
      default: false,
    },

    quiz: {
      type: Object,
      required: true,
    },
    quizz: {
      type: Object,
      required: true,
    },
    sum: {
      type: Number,
      required: true,
    },
    count: {
      type: Number,
      required: true,
    },
  },
  data() {
    return {
      qiymat: false,
      interval: true,
    };
  },

  methods: {
    emitScroll(btn) {
      console.log("222222", btn);
      this.$emit("changeEmit", btn);
    },
    toggleSLider() {
      this.$emit("input", !this.value);
    },

    testClick(event) {
      this.$refs.butts[0].qiymat = !this.qiymat;
      console.log(event);
    },
  },
};
</script>

<style lang="scss" scoped>
.quizz-slider {
  .soat {
    padding-left: 100px;
  }
  position: fixed;
  top: 0;
  right: 0;
  height: 100vh;
  background: #ff8f5e;
  transition: width 0.5s;
  width: 65px;

  .num {
    button {
      width: 60px;
      height: 60px;
      border-radius: 50%;
      background: transparent;
      border: 1px solid black;
      font-size: 25px;
      margin-right: 5px;
    }
  }
  .header_bottom {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 3px 29px;
    border-bottom: 3px dotted lightgray;
    p {
      font-size: 24px;
    }
    h3 {
      font-size: 24px;
    }
  }
}
.quizz-slider--open {
  width: 530px;
}
.quizz-slider_btn {
  //   margin-top: 15px;
  cursor: pointer;
  background: transparent;
  border: 0;
  background: darken(#ff8f5e, 5%);
}
.quizz-slider-header {
  height: 56px;
  display: flex;
}
.active {
  background: black !important;
  color: white;
}
.quizz-slider_btn:hover {
  background: black;
  svg path {
    color: white;
  }
}
</style>