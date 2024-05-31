<template>
  <q-toolbar>
    <q-btn flat round icon="home" @click="goHome" />
    <q-toolbar-title>
      Disertation
    </q-toolbar-title>
    <q-space/>

    <template v-if="!isAuthenticated">
      <div class="q-gutter-lg">
        <q-btn @click="signUp()" color="secondary">Sign Up</q-btn>
        <q-btn @click="logIn()" color="secondary">Log In</q-btn>
      </div>
    </template>
    <template v-else>
      <div class="q-gutter-lg">
        <q-btn @click="goProfile()" color="secondary">Profile</q-btn>
        <q-btn @click="goRecommendations()" color="secondary">Recommendations</q-btn>
        <q-btn @click="goCategoriesPosts()" color="secondary">Categories</q-btn>
        <q-btn @click="goMyPosts()" color="secondary">My Posts</q-btn>
        <q-btn @click="goCreatePost()" color="secondary">Create new post</q-btn>
        <q-btn @click="logOut()" color="secondary">Log Out</q-btn>
      </div>
    </template>
  </q-toolbar>
</template>

<script>
export default {
  name: 'HeaderComponent',
  methods: {
    goHome() {
      this.$router.push('/')
    },
    goProfile() {
      this.$router.push('/profile')
    },
    goMyPosts() {
      this.$router.push('/my-posts')
    },
    goCreatePost() {
      this.$router.push('/create-post')
    },
    goRecommendations() {
      this.$router.push('/recommendations')
    },
    goCategoriesPosts() {
      this.$router.push('/categories-posts')
    },

    signUp() {
      this.$auth0.loginWithRedirect({
        appState: {
          target: "/profile",
        },
        authorizationParams: {
          prompt: "login",
          screen_hint: "signup",
        }
      });
    },

    logIn() {
      this.$auth0.loginWithRedirect({
        appState: {
          target: "/profile",
        },
        authorizationParams: {
          prompt: "login",
        }
      });
    },

    logOut() {
      this.$auth0.logout({
        logoutParams: {
          returnTo: window.location.origin,
        }
      });
    }
  },
  computed: {
    isAuthenticated () {
      return this.$auth0.isAuthenticated.value
    }
  }
}
</script>
