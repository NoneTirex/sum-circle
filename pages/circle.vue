<template>
  <div class="main">
    <header>
      <img id="image" class="image"
           src="~/static/sum-circle.jpg">
    </header>
    <section class=" box">
      <h1>KOŁO ZATOCZYŁO SIĘ JUŻ <span style="color:#e74c3c;">{{ counter.value }}</span> RAZY</h1>
      <button @click="spin" :disabled="disabled">ZATOCZ</button>
    </section>


  </div>
</template>

<script>
import countapi from 'countapi-js';

export default {
  name: 'IndexPage',
  async asyncData({$axios}) {
    const counter = await countapi.get("sum-edu.pl", "spins");
    return {counter}
  },
  head() {
    return {
      title: "ŚUM Circle"
    }
  },
  data() {
    return {
      stepTimeout: 10,
      rotation: 0,
      disabled: false
    }
  },
  methods: {
    async spin() {
      this.rotate();
      this.disabled = true;
      this.counter = await countapi.hit("sum-edu.pl", "spins");
      setTimeout(() => {
        this.disabled = false;
      }, 5000);
    },
    rotate() {
      this.rotation += 1802;
      document.getElementById("image").style.transform = "rotate(" + this.rotation + "deg)";
    }
  }
}
</script>

<style>
body {
  box-sizing: border-box;
}

.main {
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
}

.image {
  margin: 9vh 0 9vh 0;
  height: 50vh;
  max-height: 90vw;
  transition: transform 5s cubic-bezier(0.16, 1, 0.3, 1);;
}

.box {
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
}

button {
  margin: 8vh 32px 32px;
  font-size: 4em;
}

h1 {
  font-size: min(4vw, 3vh);
}
</style>
