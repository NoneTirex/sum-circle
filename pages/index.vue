<template>
  <div class="main">
    <header>
      <img id="image" class="image"
           src="https://scontent-frt3-2.xx.fbcdn.net/v/t1.15752-9/283440723_750168605999669_7578058218754862595_n.jpg?_nc_cat=101&ccb=1-7&_nc_sid=ae9488&_nc_ohc=wiOVghN0o4QAX9vNUOM&_n">
    </header>
    <section class=" box">
      <h1>KOŁO ZATOCZYŁO SIĘ JUŻ <span style="color:#e74c3c;">{{ counter.value }}</span> RAZY</h1>
      <button @click="spin">ZATOCZ</button>
    </section>


  </div>
</template>

<script>
export default {
  name: 'IndexPage',
  async asyncData({$axios}) {
    const counter = await $axios.$get('https://api.countapi.xyz/get/sum/spins');
    return {counter}
  },
  head() {
    return {
      title: "ŚUM Circle"
    }
  },
  data() {
    return {
      rotation: 0
    }
  },
  methods: {
    spin() {
      setTimeout(this.animate, 5);
    },
    animate() {
      if (this.rotation >= 360) {
        this.rotation = 0;
      } else {
        setTimeout(this.animate, 5);
      }
      this.rotation += 2;
      document.getElementById("image").style.transform = "rotate(" + this.rotation + "deg)";
    }
  }
}
</script>

<style>
.main {
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
}

.image {
  margin: 128px 0 64px 0;
}

.box {
  display: flex;
  flex-direction: column;
  align-items: center;
}

button {
  padding: 10px;
  font-size: 10em;
}

h1 {
  font-size: 6rem;
}
</style>
