<template>
  <div class="level">
    <div class="brojkarata" v-show="!igra">
      <button class="btn" v-on:click="broj = 8; igra = true; pair = 4; pogodeno = 4;">8</button>
      <button class="btn" v-on:click="broj = 16; igra = true; pair = 8; pogodeno = 8;">16</button>
      <button class="btn" v-on:click="broj = 32; igra = true; pair = 16; pogodeno = 16;">32</button><br/>
    </div>
    <section class="obrub" :class="[{ 'is-Inactive': win}, ]" :key="lvl" v-show="igra">
    <div class="navbar">
      <div class="lijevi">
        <span class="timer" :class="[{ 'is-Inactive': win}]" :key="time">Timer <br/>{{time}}</span>
      </div>
      <div class="srednji">
      </div>
      <div class="desni">
        <button @click="resetgame" class="btn">
          GO BACK
        </button>
      </div>
    </div>
    <ul class="karte" :class="[{'is-Waiting': !clickable }]" :key="game">
      <Card
        v-for="n in broj"
        :key="n"
        :n="n"
        @click.native="checkCard(n)"
        :class="[{ 'is-Clicked': clicked.includes(n) }, { 'is-Revealed': pairs.includes(n) || pairs.includes(n-1) }]"
        />
    </ul>
    <div class="bot">
      <span class="tries">Tries {{tries}}</span>
      <span class="left">Pairs Left {{left}}</span>
    </div>
    </section>
    <transition name="fade">
      <div class="pobjeda" v-if="win">
        <h2>Congratulations!</h2>
        <p>Game finished in {{ tries }} tries.</p>
        <p>The time it took to clear was {{ times }} seconds.</p>
        <button @click="resetgame" class="btn">RETRY</button>
        <button class="btn" style="margin-left:15px;" @click.native="scoreboard">SCOREBOARD</button>
        <input type="text" v-model="username" placeholder="username"/>
      </div>
    </transition>
    <div class="scoreboard">
    <button @click="resetgame" class="btn">
          GO BACK
    </button>
      <ul>
        <li><p>Player {{username}} scored {{score}}</p></li>
      </ul>
    </div>
  </div>
</template>

<script>
import Card from "../components/Card";

function poce_stanje(){
  return{
    clicks:0,
    pairs:[],
    fist:null,
    second:null,
    clickable:true,
    time:0,
    clicked: [],
    tries:0,
    times:0,
    game:[],
    broj:0,
    left:null,
    igra:false,
  };
}
export default{
  name: 'level',
  components: {
    Card 
  },
  data(){
    return poce_stanje();
    return score;
  },
  methods:{
    checkCard(n){
      this.clicks++;
      this.clicked.push(n);
      if(n % 2 === 0){
        n = n -1;
      }
      this.left = this.pair;
      if(this.clicks % 2 === 0){
        this.second = n;
          if(this.first === this.second){
            this.pairs.push(this.first);
            this.left--;
            this.pair--;
          }
          else{
            this.clickable = false;
            setTimeout(() => {
              this.clickable = true;
              this.second = null;
              this.clicked = [];
            }, 1000);
          }
        }
      else{
        this.first = n;
        this.tries++;
        this.second = null;
        }
      if(this.clicks === 1 && this.time === 0){
        let vrijeme = setInterval(() => {
        this.time++;
        }, 1000);
        this.times=this.time;
      }
      this.times = this.time;
  },
  resetgame(){
    Object.assign(this.$data, poce_stanje());
    this.game.push();
    clearInterval(this.vrijeme);
    }
  },
  computed: {
    win(){
      if (this.pairs.length === 1) {
        return true;
        this.game.push();
        clearInterval(this.vrijeme);
        this.score = this.pogodeno*5;
        }
      else{
        return false;
      }
    }
  },
  created:{
    scoreboard(){
      scored = true;
    }
  }
};
</script>

<style lang="scss">
body{
  padding: 0;
  margin: 0;
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  color:#39394a;
  background-color:#ebeff2;
}
#level {
  padding: 0;
  margin: 0;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
.navbar{
  padding-top:2px;
  width:99.9%;
  float:left;
  border-bottom: 1px solid #39394a;
  padding-bottom:10px;
}
.lijevi{
  padding: 0;
  margin: 0;
  width:33%;
  float:left;
}
.srednji{
  padding: 0;
  margin: 0;
  width:33%;
  float:left;
}
.desni{
  padding: 0;
  margin: 0;
  width:34%;
  float:right;
}
.timer{
  margin-top:10px;
  padding-left:10px;
  width:100px;
  float:left;
  color:#39394a;
}
.btn{
  margin-top:5px;
  text-align:center;
  display:block;
  float: right;
  width:160px;
  padding:10px;
  text-decoration:none;
  background-color:#58595B;
  color:white;
  border-radius:4px;
  font-size: 12px;
  transition: 0.4s ease;
  font-weight: 900;
}
.btn:hover,active,visited {
  background: transparent;
  border: 2px solid #39394a;
  color:#39394a;
}
.karte{
  list-style: none;
  margin: 0 auto;
  width:95%;
  padding: 5px;
  display: grid;
  grid-template-columns: repeat(8, minmax(140px, 1fr));
  grid-gap:30px;
}
.karte.is-Waiting {
  pointer-events: none;
}
.obrub.is-Inactive {
  filter: blur(8px);
}
.card{
  width:140px;
  height:140px;
  border-radius:4px;
}
.bot{
  padding-top:5px;
  width:99%;
  float:left;
  text-align:center;
}
.tries{
  padding-right:5px;
}
.left{
  padding-left:5px;
}
.pobjeda {
  position: fixed;
  padding: 30px;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  background: white;
  border-radius: 5px;
  z-index: 100;
  box-shadow: 0 0 30px rgba(0, 0, 0, 0.5);
  min-width: 300px;
}
.pobjeda h2 {
  color: #CC2039;
  font-size: 32px;
  font-weight: 300;
}
.fade-enter-active,
.fade-leave-active {
  transition: opacity 500ms;
}
.fade-enter,
.fade-leave-to {
  opacity: 0;
}
.brojkarata{
  width:32%;
  margin:300px auto;
}
.scoreboard{
  width:50%;
  margin:0 auto;
}
</style>