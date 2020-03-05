<template>
  <v-layout column justify-center align-center>
    <v-flex xs12 sm8 md6>
      <div class="text-center">
        <logo />
        <vuetify-logo />
      </div>
      <v-card>
        <v-card-title class="headline"
          >Welcome to the Vuetify + Nuxt.js template</v-card-title
        >
        <v-card-text>
          <ul>
            <li v-for="item in items" :key="item.id">{{ item.title }}</li>
          </ul>
          <p>
            Thank you for developing with Vuetify and I look forward to bringing
            more exciting features in the future.
          </p>
          <div class="text-xs-right">
            <em>
              <small>&mdash; John Leider</small>
            </em>
          </div>
          <hr class="my-3" />
          <a href="https://nuxtjs.org/" target="_blank">Nuxt Documentation</a>
          <br />
          <a href="https://github.com/nuxt/nuxt.js" target="_blank"
            >Nuxt GitHub</a
          >
        </v-card-text>
        <v-card-actions>
          <v-spacer />
          <v-btn color="primary" nuxt to="/inspire">Continue</v-btn>
        </v-card-actions>
      </v-card>
    </v-flex>
  </v-layout>
</template>

<script>
import axios from "axios";
import Logo from "~/components/Logo.vue";
import VuetifyLogo from "~/components/VuetifyLogo.vue";

export default {
  components: {
    Logo,
    VuetifyLogo
  },
  data() {
    return {
      title: "first",
      content: "first"
    };
  },
  head() {
    return {
      title: this.title,
      meta: [
        // hid is used as unique identifier. Do not use `vmid` for it as it will not work
        {
          hid: "description",
          name: "description",
          content: this.content
        }
      ]
    };
  },
  async asyncData() {
    const { data } = await axios.get(process.env.ENDPOINT);
    this.title = data[0].title;
    this.content = data[0].body;
    return {
      items: data
    };
  }
};
</script>
