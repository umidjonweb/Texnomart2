<template>
  <div
    class="quizz-item"
    :class="{ 'quizz-item--selected': quizz.userAnswer }"
    @click="clasqosh"
  >
    <div class="quizz-item_question">
      <strong> {{ index + "." }} </strong> {{ quizz.question }}
    </div>
    <section>
      <label
        v-for="(option, optionIndex) in quizz.options"
        :key="optionIndex"
        class="quizz-item_option"
        :for="`option-${index}-${optionIndex}`"
        :class="{ 'quizz-item_option--selected': option === quizz.userAnswer }"
      >
        {{ "abcd"[optionIndex] }}){{ option }}
        <input
          type="radio"
          :id="`option-${index}-${optionIndex}`"
          :value="option"
          v-model="userAnswer"
          @change="inputchange"
        />
      </label>
      
    </section>
  </div>
</template>

<script>
export default {
  name: "dasQuizzitem",
  props: {
    quizz: {
      type: Object,
      required: true,
    },
    index: {
      type: Number,
      required: true,
    },
  },
  data() {
    return {
      userAnswer: null,
    };
  },

  methods: {
    inputchange(event) {
      this.$emit("user-answer-change", {
        id: this.quizz.id,
        answer: event.target.value,
      });
    },
    clasqosh() {
      this.$emit("salom", this.index);
    },
  },
};
</script>

<style lang="scss" scoped>
.quizz-item {
  border-bottom: dotted 4px lightgray;
  &--selected {
    border-left: 4px solid #ff8f5e;
  }
  &_question {
    padding: 2rem 1rem;
    font-size: 20px;
    strong{
      font-size: 22px;
    }
  }
  &_option {
    padding: 1.5rem 1rem;
    display: block;
    transition: 0.4s;
    cursor: pointer;
    &:not(&--selected):hover {
      background: #ff8f5e;
      color: white;
    }
    &--selected {
      background: black;
      padding-top: 2rem;
      padding-bottom: 2rem;
      color: white;
    }
    input {
      display: none;
    }
  }
}
</style>