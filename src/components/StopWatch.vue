<template>
  <!-- <h1>{{hh}}:{{mm}}:{{ss}}:{{ms}}</h1> -->
  <h1>{{formatTime}}:{{millis}}</h1>
  <div  v-if="!running">
    <button class="btn-button1"  @click="startTime">Start</button>
    <button class="btn-button" @click="stopTime">Stop</button>
    <button class="btn-button" @click="resetTime">Reset</button>
  </div>
  <div v-else>
    <button class="btn-button1">Start </button>
    <button class="btn-button" @click="stopTime">Stop </button>
    <button class="btn-button" @click="resetTime">Reset </button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      millis:0,
      time:0,
      running:false,
      polling:null
    };
  },
  computed:{
    formatTime() {
      const date = new Date(null);
      date.setSeconds(this.time / 1000);
      const utc = date.toUTCString();
      return utc.substr(utc.indexOf(":")-2,8);
    }
  },
  methods:{
    startTime() {
      this.running=true
      this.polling=setInterval(()=>{
        this.time+=1000
      },1000)
      this.timer = setInterval(()=>{
        this.millis+=1
        if (this.millis==100) {
          this.millis=0
        }
      },10)
    },
    stopTime() {
      clearInterval(this.timer)
      clearInterval(this.polling)
      this.running=false
    },
    resetTime() {
      clearInterval(this.timer)
      clearInterval(this.polling)
      this.time=0;
      this.millis=0;
      this.running=false;
    }
  }
};
</script>
<style>
h1 {
  font-size:250px;
}

.btn-button {
  display:inline-block;
  color:#fff!important;
  font-size:70px;
  font-family: "Lucida Console", "Courier New", monospace;
  background-color:#000!important;
  padding:5px;
  margin:25px;
}
.btn-button1 {
  display:inline-block;
  color:#fff!important;
  font-size:70px;
  font-family: "Lucida Console", "Courier New", monospace;
  background-color:#000!important;
  padding:5px;
  margin:15px;
}
</style>
