<template>
  <header class="site-header">
    <form @submit.prevent="handleSubmit">
      <h3>Join a Adventure</h3>
      <div class="content-section">
        <div class="form-group">
          <label>Adventure Id</label>
          <input
            type="group"
            name="group"
            v-model="group"
            class="form-control"
          />
        </div>
        <div class="form-group">
          <button class="btn btn-primary btn-block">Create</button>
        </div>
      </div>
    </form>
    <div class="alert alert-danger" role="alert" v-if="error">
      {{ error_msg }}
    </div>
  </header>
</template>

<script>
import router from "@/router";
import axios from "axios";
import { mapGetters } from "vuex";
export default {
  name: "JoinGroup",
  data() {
    return {
      title: "",
      content: "",
      group: 0,
      error: false,
    };
  },
  computed: {
    ...mapGetters({
      user: "user",
    }),
  },
  methods: {
    async handleSubmit() {
      this.error = false;
      await axios
        .post("/user/" + this.user.id + "/group/" + this.group)
        .catch((err) => {
          console.log(err);
          this.error = true;
          this.error_msg = "Invalid group id! Please try again.";
        });
      if (this.error == false) {
        await router.push("/");
      }
    },
  },
};
</script>

<style>
@import "../assets/styles.css";
</style>
