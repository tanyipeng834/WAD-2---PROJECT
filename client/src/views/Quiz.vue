<template>
  <div>
    <div>
      <Topbar :tabs="tabs" menuTitle="Test Yourself" />
    </div>
    <div class="container-fluid p-0 quiz">
      <div class="row">
        <div class="col-4">
          <Sidebar :haveTopbar="true" />
        </div>
        <div class="col-4"></div>
        <div class="col-4"></div>
      </div>

          <div class="row mt-4">
            <div class="col-2"></div>
            <div class="col-8">
              <div class="row">
                <div class="col">
                  <div
                  class="mt-4 jumbo text-white rounded text-center animate__animated  animate__fadeInLeft"
                  @click="redirect('flashcards')"
                >
                <div class="row">
                  <h1>Flashcards</h1>
                  <p>
                    Click to create your own online flashcards to test your
                    <b>memory!</b>
                  </p>

                </div>

                </div>

                </div>
              </div>

            <div class="row">
              <div class="col">

                <div
                  class="mt-4 jumbo text-white text-center rounded animate__animated  animate__fadeInRight"
                  @click="redirect('multi')"
                >
                <div class="row">
                  <h1>Quizzes</h1>
                  <p>
                    Click to create your own online Quiz to help with your
                    <b>concepts!</b>
                  </p>
                </div>

               

    </div>
  </div>

              </div>
            </div>
          </div>


              </div>

    <BottomBar class="bottomnav" />
  </div>
</template>

<script>
import Sidebar from "../components/Navigation/Sidebar.vue";
import Topbar from "../components/Navigation/Topbar.vue";
import BottomBar from "../components/Navigation/BottomBar.vue";

export default {
  name: "Quiz",
  name: "Forum",
  components: {
    Sidebar,
    Topbar,
    BottomBar,
  },
  data() {
    return {
      tabs: [],
    };
  },
  methods: {
    redirect(link) {
      if (link == "flashcards") {
        window.location.href = "/#/quiz/flashcards";
      } else {
        window.location.href = "/#/quiz/multi";
      }
    },
  },
};
</script>
<style scoped>
.quiz {
  width: 100vw;
  min-height: 100vh;
  margin-top: 60px;
  padding-bottom: 1000px;

  background-color: #eaf1f5;
  font-family: "Roboto", sans-serif;
  overflow-x: hidden;
  overflow-y: hidden;
}
.jumbo:hover {
  cursor: pointer;
}
.jumbo {
  background-color: #253f63;
  padding: 100px;

}
</style>
