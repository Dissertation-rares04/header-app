<template>
  <q-toolbar class="header-toolbar">
    <q-btn flat round icon="home" @click="goHome" color="primary" />
    <q-toolbar-title> Disertation </q-toolbar-title>
    <q-space />

    <template v-if="!isAuthenticated">
      <div class="q-gutter-lg">
        <q-btn @click="signUp" flat color="grey" icon="person_add"
          >Sign Up</q-btn
        >
        <q-btn @click="logIn" flat color="grey" icon="login">Log In</q-btn>
      </div>
    </template>
    <template v-else>
      <div class="q-gutter-lg">
        <q-btn @click="goProfile" flat color="grey" icon="person"
          >Profile</q-btn
        >
        <q-btn @click="goRecommendations()" flat color="grey" icon="recommend"
          >Recommendations</q-btn
        >
        <q-btn @click="goCategoriesPosts()" flat color="grey" icon="category"
          >Categories</q-btn
        >
        <q-btn @click="goMyPosts()" flat color="grey" icon="bookmark_border"
          >My Posts</q-btn
        >
        <q-btn @click="goCreatePost()" flat color="grey" icon="add"
          >Create new post</q-btn
        >
        <q-btn @click="logOut()" flat color="grey" icon="logout">Log Out</q-btn>
      </div>
    </template>
  </q-toolbar>
  <q-separator />
</template>

<style lang="scss" scoped>
.header-toolbar {
  background-color: $dark;
}
</style>

<script>
export default {
  name: "HeaderComponent",
  methods: {
    goHome() {
      this.$router.push("/");
    },
    goProfile() {
      this.$router.push("/profile");
    },
    goMyPosts() {
      this.$router.push("/my-posts");
    },
    goCreatePost() {
      this.$router.push("/create-post");
    },
    goRecommendations() {
      this.$router.push("/recommendations");
    },
    goCategoriesPosts() {
      this.$router.push("/categories-posts");
    },

    signUp() {
      this.$auth0.loginWithRedirect({
        appState: {
          target: "/profile",
        },
        authorizationParams: {
          prompt: "login",
          screen_hint: "signup",
        },
      });
    },

    logIn() {
      this.$auth0.loginWithRedirect({
        appState: {
          target: "/profile",
        },
        authorizationParams: {
          prompt: "login",
        },
      });
    },

    logOut() {
      this.$auth0.logout({
        logoutParams: {
          returnTo: window.location.origin,
        },
      });
    },
  },
  computed: {
    isAuthenticated() {
      return this.$auth0.isAuthenticated.value;
    },
  },
};
</script>
