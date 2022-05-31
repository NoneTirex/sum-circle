<template>
  <div class="main">
    <h1>KLUB MIŁOŚNIKÓW SUMÓW</h1>
    <img id="image" class="image"
         src="https://www.medianauka.pl/biologia/grafika/ryby/sum-pospolity.jpg">
  </div>
</template>

<script>
export default {
  name: 'IndexPage',
  head() {
    return {
      title: "SUMy"
    }
  }
}
</script>

<style>
body {
  box-sizing: border-box;
}

.main {
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
}

.image {
  max-width: 90vw;
}

h1 {
  text-align: center;
  font-size: 5vw;
}
</style>
