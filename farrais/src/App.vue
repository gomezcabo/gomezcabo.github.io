<template>
  <div id="app">
    <!-- <textarea v-model="joke"></textarea> -->
    <div id="picture">
      <div id="quote" contenteditable="true" :style="{ 'font-size': `${fontSize}px` }">{{ joke }}</div>
    </div>
    <div id="actions">
      <div class="action" @click="fontSize += 2"> + </div>
      <div class="action" @click="fontSize -= 2"> – </div>
      <div class="action right" @click="exportImage">Guardar</div>
    </div>
  </div>
</template>

<script>
import html2canvas from 'html2canvas'

export default {
  name: 'app',
  data () {
    return {
      fontSize: 24,
      joke: 'Escribe aquí tu chiste'
    }
  },
  methods: {
    exportImage () {
      console.log(html2canvas)
      const div = document.getElementById('picture')

      html2canvas(div, {
        allowTaint: false,
        useCORS: false
      }).then(canvas => {
        var myImage = canvas.toDataURL();
        this.downloadURI('data:' + myImage, "chiste.png");
      });
    },
    downloadURI(uri, name) {
      var link = document.createElement("a");
      link.download = name;
      link.href = uri;
      console.log(uri)
      document.body.appendChild(link);
      link.click();
    }
  }
}
</script>

<style lang="scss">
* {
  box-sizing: border-box;
}

body, html {
  margin: 0;
  padding: 10px;
}

#app {
  textarea {
    width: 100%;
    height: calc(100vmax - 100vmin - 50px);
    font-family: Arial, Helvetica, sans-serif;
  }

  #actions {
    width: calc(100vmin - 40px);
    margin: 0 auto;
    padding: 0 10px;

    .action {
      display: inline-block;
      padding: 3px 10px;
      background-color: black;
      color: white;
      font-size: 18px;
      min-width: 30px;
      text-align: center;
      cursor: pointer;
      border-radius: 3px;

      &.right {
        float: right;
      }
    }
  }

  #picture {
    font-family: Arial, Helvetica, sans-serif;
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 20px;
    width: calc(100vmin - 60px);
    height: calc(100vmin - 60px);
    position: relative;
    margin: 0 auto;
    margin-bottom: 10px;
    background-image: url('./assets/background.png');
    background-repeat: no-repeat;
    background-size: 100% 100%;

    img {
      position: absolute;
      top: 0;
      bottom: 0;
      left: 0;
      right: 0;
      width: 100%;
      z-index: 10;
    }
  }

  #quote {
    z-index: 100;
    color: white;
    width: 100%;
    text-align: center;
    white-space: pre-line;
  }
}

</style>
