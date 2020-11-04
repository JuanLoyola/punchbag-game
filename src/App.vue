<template>
  <div id="app">
    <div class="container">
      <!-- Header-->
    <div id="header-text">
      <a href="https://www.linkedin.com/in/loyolajuan" target="_blank">
        <h2>{{title}}</h2>
      </a>
    </div>
    <!-- Bag image-->
    <div id="bag" v-bind:class="{burts:ended}"></div>
    <!-- Bag health-->
    <div id="bag-health">
      <div v-bind:style="{width:health + '%'}"></div>
    </div>
    <!-- Game controls-->
    <div id="controls">
      <button @click="punch" @click.prevent="playSound('http://soundbible.com/mp3/Realistic_Punch-Mark_DiAngelo-1609462330.mp3')" v-show="!ended">Punch</button>
      <button @click="restart" @click.prevent="playSound('http://soundbible.com/mp3/Boxing_arena_sound-Samantha_Enrico-246597508.mp3')" volume="100" >Reset</button>
    </div>
    <!-- Text-->
    <p class="controls__text"> {{ message }}</p>
    <p class="alert">{{alert}}</p>
    </div>
  </div>
</template>

<style lang="scss">
*{
  margin: 0;
  padding: 0;
}
body{
  background-image:url('./assets/box-bg.jpg');
  background-size: 100%;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #333;
}
a{
text-decoration:underline;
color: hsl(348, 83%, 37%);
}
a:hover{
text-decoration:none;
transition: linear 250ms;
color: hsl(355, 82%, 70%);
}
#header-text {
  max-width: 280px;
  font-size: 22px;
  position: relative;
  font-family: 'Gloria Hallelujah', cursive;
  right:-1%;
  margin-bottom: -9%;
}
#bag{
  width: 200px;
  height: 500px;
  margin: 0 auto;
  background: url('./assets/bag.png') center no-repeat;
  background-size: 80%;
}
#bag.burts{
  background: url('./assets/bag-burst.png') center no-repeat;
  background-size: 80%;
}

#bag-health{
  width: 200px;
  border: 2px solid #000;
  margin: 0 auto 10px auto;
}
#bag-health div{
  height: 20px;
  background: crimson;
}

#controls{
  width: 120px;
  margin: 0 auto;
}
#controls button {
  box-shadow: 0px 1px 0px 0px #fff5d6;
  background:linear-gradient(to bottom, #eae0c2 5%, #ccc2a6 100%);
  background-color:#eae0c2;
  border-radius:15px;
  border:2px solid #333029;
  display:inline-block;
  cursor:pointer;
  color:#505739;
  font-family:Arial;
  font-size:13px;
  font-weight:bold;
  padding:12px 9px;
  text-decoration:none;
  text-shadow:0px 1px 0px #ffffff;
}
#controls button:hover {
  background:linear-gradient(to bottom, #ccc2a6 5%, #eae0c2 100%);
  background-color:#ccc2a6;
}
#controls button:active {
  position:relative;
  top:1px;
}

.controls__text{
  font-size: 25px;
  font-family: Impact
  }

.alert{
  color: red;
  font-weight: bold;
  font-size: 1.3rem;
}
@media screen and (min-width: 320px) and (max-width:1000px){
  body{
    background-image:url('./assets/chalkboard.jpg');
    background-size: 100%;
  }
  .container{
    display:flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }
  #bag{
    height: 400px;
  }
  #bag-health{
    width: 200px;
    border: 2px solid #000;
    margin: 10px auto 20px auto;
  }
  .alert{
    margin: 10px;
  }
  #bag-health div{
    height: 20px;
    background: crimson;
  }

#controls{
    width: 120px;
    margin: 0 auto;
  }
}
@media screen and (min-width: 1920px) and (max-width:1920px){
  #bag{
    width: 200px;
    height: 900px;
    margin: 0 auto;
    background: url('./assets/bag.png') center no-repeat;
    background-size: 80%;
  }
}
@media screen and (min-width: 1280px) and (max-width:1280px){
  body{
    background-size: 200vh;
  }
}
</style>

<script>
export default {
  name: '',
  data () {
    return {
      health: 100,
      ended: false,
      message: '',
      title: 'Punchbag game',
      alert: 'Be careful! the sound is very loud'
    }
  },
  methods: {
    punch: function () {
      this.health -= 10
      if (this.health <= 0) {
        this.ended = true
      }
      this.messagePunch()
    },
    restart: function () {
      this.health = 100
      this.ended = false
      this.messagePunch()
    },
    messagePunch: function () {
      this.message = ''
      if (this.health > 0) {
        this.message = 'Let\'s hit it'
      } else if (this.health < 10) {
        this.message = 'Bro... you have to pay for it'
      }
    },
    playSound (sound) {
      if (sound) {
        const audio = new Audio(sound)
        audio.volume = 0.2
        audio.play()
      }
    }
  }
}
</script>
