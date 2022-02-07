<template>
  <div>
    <h1>Привет, {{ name }}</h1>
    <h3>{{ about }}</h3>
    <h3 v-if="errMessage" class="text-danger">{{ errMessage }}</h3>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      name: localStorage.getItem("username"),
      about: "",
      errMessage: "",
    };
  },
  methods: {
    getAbout: function () {
      axios
        .get("http://localhost:3000/about", {
          headers: {
            Authorization: `Bearer ${localStorage.getItem("token")}`,
          },
        })
        .then((res) => {
          this.about = res.data.message;
        })
        .catch((err) => {
          this.errMessage = err.message;
        });
    },
  },
  beforeMount() {
    this.getAbout();
  },
};
</script>