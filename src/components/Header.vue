<template >
  <header>
    <h1><router-link to="/">
      <img src="../assets/logo.svg">
    </router-link></h1>

  </header>
</template>

<script>
  export default {
    name: 'Header',
    props: {
      title: String
    },
    data() {
      return {
        show: false,
        name: 'Ryan'
      };
    },

  };
</script>

<style scoped>
header {
  background-color: #111;
  padding: 20px;
  color: white;
}
h1 {
  margin: 0;
}
.fade-enter-active, .fade-leave-active {
  transition: all .3s ease;
}
.fade-enter, .fade-leave-to {
  opacity: 0;
  transform: scale(0);
}


</style>
