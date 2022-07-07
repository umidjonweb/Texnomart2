<template>
  <div class="quizz" :class="{ 'quizz--slider--open': toggleSLider }">
    <main class="quizz_main">
      <header class="quizz_header">Matematika</header>

      <div class="quizz_content">
        <QuizzItem
          v-for="(quizz, index) in quizzes"
          :key="quizz.id"
          :quizz="quizz"
          :index="index + 1"
          @user-answer-change="handeUserAnsverChange"
          @click="met(quizz.id)"
          @salom="ixtiyor(index)"
        />
  
      </div>
      <div class="buttons">
        <button v-if="isButton" @click="checkquiz">testni yakunlash</button>
        <div class="qayta" v-else>
          <div class="checkquizz">
            <span style="display:block, width:100%">
              {{ k }}/{{ quizzes.length }}
            </span>
            <span style="display: block"> </span>
          </div>
          <button @click="checkqayta">qayta topshirish</button>
        </div>
      </div>
    </main>
    <Quizzsider
      v-model="toggleSLider"
      :quiz="quizzes"
      :key="id"
      :count="count"
      @changeEmit="(scrollToQuizz) => editT(btn, scrollToQuizz)"
    />
    <!-- <QuizzItem /> -->
  </div>
</template>

<script>
import QuizzItem from "./QuizzItem.vue";
// import QuizzChecked from "./QuizzChecked.vue";
import Quizzsider from "../components/QuizzSider.vue";
export default {
  name: "dasQuizzapp",
  components: {
    Quizzsider,
    QuizzItem,
   //  QuizzChecked,
  },
  data() {
    return {
      isClass: false,
      toggleSLider: false,
      sum: 0,
      k: 0,

      isButton: true,
      count: 0,
      quizzes: [
        {
          id: 1,
          question:
            "246*013579246∗013579 soni 99 ga bo‘linishi uchun yulduzchaning o‘rniga qanday raqam qo‘yilishi kerak?",
          options: ["7", "8", "0", "4"],
          correctAnsver: "8",
        },
        {
          id: 2,
          question:
            "4∗10 yozuvdagi yulduzchani shunday raqam bilan almashtiringki, hosil bo‘lgan son 4545 ga qoldiqsiz bo‘linsin.",
          options: ["5", "4", "6", "0"],
          correctAnsver: "4",
        },
        {
          id: 3,
          question:
            "Berilgan p=1018978560,p=1018978560, q=8976119441q=8976119441 va r=987610734r=987610734 sonlardan qaysilari 1616 ga qoldiqsiz bo‘linadi?",
          options: ["q", "p", "p va q", "r"],
          correctAnsver: "p",
        },
          {
            id: 4,
            question:
              "Agar m Nm∈N bo‘lsa, quyidagi keltirilganlardan qaysi biri doimo juft bo‘ladi?",
            options: ["2", "4", "4 va 4", "9"],
            correctAnsver: "4",
          },
          {
            id: 5,
            question:
              "4*104∗10 yozuvdagi yulduzchani shunday raqam bilan almashtiringki, hosil bo‘lgan son 4545 ga qoldiqsiz bo‘linsin.",
            options: ["0", "5", "54", "9"],
            correctAnsver: "0",
          },
          {
            id: 6,
            question:
              "xx raqamining qanday eng katta qiymatida sss son 33 ga qoldiqsiz bo‘linadi?",
            options: ["3", "6", "0", "4"],
            correctAnsver: "0",
          },
          {
            id: 7,
            question:
              "Agar m n Nm∈N bo‘lsa, quyidagi keltirilganlardan qaysi biri doimo juft bo‘ladi?",
            options: ["m=n", "m-b", "n", "m*n"],
            correctAnsver: "n",
          },
      ],
    
    };
  },
  methods: {
    handeUserAnsverChange(data) {
      this.quizzes = this.quizzes.map((quizz) => {
        if (quizz.id === data.id) {
          return { ...quizz, userAnswer: data.answer };
        } else {
          return quizz;
        }
      });
      this.count = this.quizzes.filter((quizz) => quizz.userAnswer).length;
      this.sum++;
      console.log(this.sum);
    },   
 

    ixtiyor(index) {
      console.log(this.userAnswer);
      this.isClass = true;
      console.log(index);
    },
   //  ixtiyor1(index) {
   //    console.log(this.userAnswer);
   //    this.isClass = true;
   //    console.log(index);
   //  },
    checkquiz() {
      this.k = this.quizzes.filter(
        (quizz) => quizz.correctAnsver === quizz.userAnswer
      ).length;
      // console.log(this.quizzes.correctAnsver);
      this.isButton = !this.isButton;
    },
    checkqayta() {
      console.log(this.quizzes);
      // console.log(Math.floor((this.k)));
    },
  },
};
</script>

<style lang="scss" scoped>
.quizz {
  .buttons {
    height: 300px;
    background: black;
    display: flex;
    align-items: center;
    justify-content: center;
    button {
      color: white;
      background: green;
      padding: 20px 36px;
    }
  }
  .quizz_main {
    width: calc(100% - 65px);
    transition: width 0.5s;
  }
  &--slider--open {
    .quizz_main {
      width: calc(100% - 530px);
    }
  }
  .quizz_header {
    text-align: center;
    height: 56px;
    display: flex;
    align-items: center;
    justify-content: center;
    border-bottom: 2px solid black;
  }
  .quizz_content {
    width: 80%;
    margin: 0 auto;
  }
  .checkquizz {
    color: white;
  }
  .qayta {
    display: flex;
    justify-content: center;
    flex-direction: column;
    align-items: center;
    .checkquizz {
      border: 2px solid white;
      width: 164px;
      height: 50px;
      font-size: 18px;
      display: flex;
      justify-content: center;
      flex-direction: column;
      align-items: center;
      margin: 0 auto;
      span {
        font-size: 23px;
      }
    }
  }
}
</style>