<template>
    <div class="container d-flex">
      <div class="row">

        <div class="col-lg-4 col-md-6 mt-5 animate__animated animate__fadeInUp"  v-for="story in news" :key="story"  >
          <div class="card" style="min-width: 20rem; max-width: 20em;">
        <img class="card-img-top" :src="story.image" alt="no image" v-if="story.image!=null"/>
        <img class="card-img-top" src="../../assets/news.jpg" alt="no image" v-else />
        <div class="card-body">
      <h5 class="card-title">{{ story.title }}</h5>
      <p class="card-text">
        <div id="id">{{ story.id }}</div>
        {{ story.content }}
      </p>
      <a :href="story.url" target="_blank" class="btn btn-primary">Read More</a>
    </div>

        </div>
      </div>
    </div>


  </div>


</template>

<script>
import axios from "axios";
  import 'animate.css';

  export default {
    name: "News",

  data() {
    return {
      content: "",
      news: [],
    };
  },


    mounted() {
      axios
        .get(
          "https://newsapi.org/v2/top-headlines?country=sg&apiKey=796bf7e93e914141a649d4eadb2695a9", {
            headers: {},
          }
        )
        .then((res) => {
          console.log(res);
          for (let i = 0; i < 3; i++) {
            var data = res.data["articles"][i];

            var story = {};

            var headline = data["title"].split("- ");
            story.title = headline[0];
            story.id = headline[1];

          story.url = data["url"];
          // if (data["urlToImage"] == null) {
          //   story.image = "../../assets/news.jpg";  //does not work
          // } else {
            story.image = data["urlToImage"];


            if (data["content"] != null) {
              var contents = data["content"].split("[");
              story.content = contents[0];
            } else {
              story.content = "";
            }


            this.news.push(story);
            console.log(this.news);
          }

        })
        .catch((err) => {
          alert(err.message);
        });
    },
  };
</script>
<style scoped>
  img {
    height: 200px;
    width: auto;
  }

  #id {
    font-style: italic;
    font-weight: 400;
  }

  .btn {
    background-color: #253F63 !important;
  }

  .card {
    margin-left: 25px;
    margin-right: 25px;

  }
</style>