<template>
  <div id="app">
    <div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/transfers">Transfers</router-link>
    </div>
    <router-view />
  </div>
</template>

<style lang="scss">
@import '@/assets/styles/base.scss';

#app {
  font-family: $fontFamily;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: $grey;
}

#nav {
  padding: 30px;

  a {
    font-weight: bold;
    color:$grey;

    &.router-link-exact-active {
      color: $green;
    }
  }
}
</style>
