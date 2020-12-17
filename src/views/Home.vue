<template>
<div class="mt-3">
<div v-if="user" class="text-center">
  <div class="text-secondary text-center">
    Welcome back
    <span class="font-weight-bold text-info">{{user}}</span>
  </div>
</div>

  <div class="container text-center">
  <div class="row justify-content-center">
    <div class="col-10 col-md-10 col-lg-8 col-xl-7">
      <h4 class="display-4 text-primary mb-2">Meeting Log</h4>
      <p class="lead">
        With the growing need for on-demand services, the home services market segment is coming up with innovative ways to keep up with the ongoing market trends. Investors have started investing in on-demand companies and this is what is boosting the growth of the online on-demand home services sector. The improvements in the technological sector and advancements in networking have given rise to consumer services such as home education, packaging, relocation, and spa and beauty services to draw new consumers and expand the market room.T
        <a
          href="https://vuejs.org/"
        >Vue.js</a>
        with
        <a href="https://firebase.google.com">Firebase</a>.
      </p>

      <router-link class="btn btn-outline-primary mr-2" to="/register" v-if="!user">Register</router-link>
      <router-link class="btn btn-outline-primary mr-2" to="/login" v-if="!user">Log In</router-link>
      <router-link class="btn btn-primary" to="/providers" v-if="user">Providers</router-link>
    </div>
    
  </div>
</div>
</div>
</template>

<script>
// import { FontAwesomeIcon } from "@fortawesome/vue-fontawesome";
// import db from "../db.js";
export default {
name: "home",
props: ["user"]

};
</script>