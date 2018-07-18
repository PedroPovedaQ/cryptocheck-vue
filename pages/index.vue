<template>
  <div>
    <header class="App-header">
      <img src="/logo.png" class="App-logo" alt="logo">
      <h1 class="title">Welcome to your Crypto Portfolio</h1>
    </header>
  </div>
</template>

<script>
  export default {
    components: {
    }
  }
</script>

<style>
header {
  background-color: #222;
  height: 200px;
  padding: 20px;
  color: #fff;
  text-align: center;
}
.container {
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}
.title {
  margin-top: 20px;
}
.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}
.links {
  padding-top: 15px;
}
.App-logo {
  animation: App-logo-spin infinite 20s linear;
  height: 80px;
}
@keyframes App-logo-spin {
  from {
    transform: rotate(0deg);
  }
  to {
    transform: rotate(360deg);
  }
}

.title {
  font-size: 1.5em;
  color: #fff;
}
</style>
