<template>
  <div id="app">
    <Navbar />
    <router-view />
    <Footer />
  </div>
</template>

<script>
import Footer from '@/components/Footer'
import Navbar from '@/components/Navbar'

export default {
  name: 'App',
  components: {
    Navbar,
    Footer,
  },
}
</script>

<style lang="scss">
@import '~@mdi/font/css/materialdesignicons.css';
@import '~@mdi/font/css/materialdesignicons.min.css';
@import "~bulma/css/bulma.css";

html {
  scroll-behavior: smooth;
}
body.opened.mobile {
  #home, #how, #about, #video {
    display: none;
  }
}
button {
  cursor: pointer;
}

.group-message .message {
  background-color: inherit;
}
.conversation-container .message .response {
  height: inherit !important;
}
</style>
