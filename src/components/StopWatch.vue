<template>
  <h1>{{formatTime}}</h1>
  <div v-if="!running">
    <button @click="startTime">Start</button><br/><br/>
  </div>
  <div v-else>
    <button>Start</button><br/><br/>
  </div>
  <button @click="stopTime">stop</button>

</template>

<script>
export default {
  data() {
    return {
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
      return utc.substr(utc.indexOf(":") - 2, 8);
    }
  },
  methods:{
    startTime() {
      this.running=true
      this.polling=setInterval(()=>{
        this.time+=1000
      },1000)
    },
    stopTime() {
      clearInterval(this.polling)
      this.running=false
    }
  }
};

</script>
