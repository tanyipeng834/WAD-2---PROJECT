<template>
  <div class="row header mt-5">
    <Sidebar :haveTopbar="true" />
    <div class="text-center">
      <h1>Create a new Mutiple Choice Quiz</h1>
    </div>
  </div>
  <div class="row">
    <div class="col-3"></div>
    <div class="col-6">
      <div class="input-group mb-3">
        <input
          type="text"
          class="form-control"
          placeholder="Quiz Name"
          aria-label="Username"
          aria-describedby="basic-addon1"
          v-model="title"
        />
      </div>
      <div class="input-group mb-3">
        <input
          type="text"
          class="form-control"
          placeholder="Description"
          aria-label="Username"
          aria-describedby="basic-addon1"
          v-model="description"
        />
      </div>
      <MutipleChoice
        :key="this.questionNumber"
        @new-question="addQuestion"
        @add-database="addDatabase()"
      />
    </div>
  </div>
</template>

<script>
import MutipleChoice from "../QuizPage/MutipleChoice.vue";

import { db } from "@/main.js";
import Sidebar from "@/components/Navigation/Sidebar.vue";
import {
  addDoc,
  collection,
  doc,
  setDoc,
  query,
  orderBy,
} from "firebase/firestore";
export default {
  name: "MutipleChoicePage",
  emits: ["toggle-mutiple"],
  data() {
    return {
      questionNumber: 1,
      title: "",
      description: "",
    };
  },

  created() {
    this.questions = {};
  },

  components: {
    MutipleChoice,
    Sidebar,
  },
  methods: {
    addQuestion(array) {
      // force the child component to rerender
      this.questionNumber += 1;
      this.questions[array[0]] = array[1];

      console.log(this.questions);
    },
    async addDatabase() {
      this.$emit("add-summary-card", [this.title, this.description]);
      let email = localStorage.getItem("email");
      let collectionRef = collection(db, "users", email, "MutipleChoiceQuiz");

      const docref = await addDoc(collectionRef, {
        title: this.title,
        description: this.description,
        data: this.questions,
      })
        .then(() => {})
        .catch((error) => {
          alert("Unsuccessful operation,error" + error);
        });
      this.$emit("toggle-mutiple");
    },
  },
};
</script>

<style>
.add-question {
  position: fixed;
  bottom: 10%;
  right: 10%;
}
.finish {
  position: fixed;
  bottom: 10%;
  left: 10%;
}
h1 {
  font-weight: bold;
  font-family: "Roboto", sans-serif;
}
</style>
