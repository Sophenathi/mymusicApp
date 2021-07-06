<template>
  <div>
    <v-toolbar flat height=90>
       <v-progress-circular  color="red darken-4" :size="70"
      value="20" width = "10" striped v-model="trackProgress"  @click="updateSeek($event)"><div v-if="progressCount(progress)*100 !==0">{{Math.round(progressCount(progress)*100)+"%"}}</div></v-progress-circular> 

      <v-spacer></v-spacer>
      <v-btn outline fab small color="red darken-4" @click="skipTrack('prev')">
        <v-icon>skip_previous</v-icon>
      </v-btn>
      <v-btn outline fab small color="red darken-4" @click="stopTrack">
        <v-icon>stop</v-icon>
      </v-btn>
      <div v-if="!isPlaying">
 <v-btn outline fab color="red darken-4" @click="playTrack()">
        <v-icon large>play_arrow</v-icon>
      </v-btn>
      </div>
     <div v-else-if="isPlaying"><v-btn outline fab color="red darken-4" @click="pauseTrack">
        <v-icon>pause</v-icon>
      </v-btn></div>
      
      <v-btn outline fab small color="red darken-4" @click="skipTrack('next')">
        <v-icon>skip_next</v-icon>
      </v-btn>
      <v-spacer></v-spacer>
      <v-btn flat icon @click="toggleMute">
        <template v-if="!this.muted">
          <v-icon color="red darken-4" v-if="this.volume >= 0.5">volume_up</v-icon>
          <v-icon color="red darken-4" v-else-if="this.volume > 0">volume_down</v-icon>
          <v-icon color="red darken-4" v-else>volume_mute</v-icon>
        </template>
        <v-icon v-show="this.muted">volume_off</v-icon>
      </v-btn>
      <v-slider color="red darken-4" v-model="volume" @input="updateVolume(volume)" max="1" step="0.1"></v-slider>
     
      <v-spacer></v-spacer>
      <v-btn flat icon @click="toggleLoop">
        <v-icon color="red darken-4" v-if="this.loop">repeat_one</v-icon>
        <v-icon color="blue-grey" v-else>repeat_one</v-icon>
      </v-btn>
      <v-btn flat icon @click="toggleShuffle">
        <v-icon color="red darken-4" v-if="this.shuffle">shuffle</v-icon>
        <v-icon color="blue-grey" v-else>shuffle</v-icon>
      </v-btn>
    </v-toolbar>
    
  </div>
</template>

<script>
  export default {
    props: {
      loop: Boolean,
      shuffle: Boolean,
      progress: Number
    },
    data () {
      return {
        volume: 0.5,
        muted: false,
        isPlaying: false,
        count: 0
      }
    },
    computed: {
      trackProgress () {
        return this.progress * 100
      },
     

    },
    created: function () {
      Howler.volume(this.volume)
    },
    methods: {

progressCount(num){
    return +(Math.round(num + "e+2")  + "e-2");
},
      playTrack(index){
        this.$emit('playtrack', index)
        this.isPlaying = true;
      },
      pauseTrack(){
        this.$emit('pausetrack')
        this.isPlaying = false;
      },
      stopTrack(){
        this.$emit('stoptrack')
        this.isPlaying = false;
      },
      skipTrack (direction) {
          this.$emit('skiptrack', direction)
          this.isPlaying = true;
      },
      updateVolume (volume) {
        Howler.volume(volume)
      },
      toggleMute () {
        Howler.mute(!this.muted)
        this.muted = !this.muted
      },
      toggleLoop () {
        this.$emit('toggleloop', !this.loop)
      },
      toggleShuffle () {
        this.$emit('toggleshuffle', !this.shuffle)
        
      },
      updateSeek (event) {
        let el = document.querySelector(".progress-linear__bar"),
            mousePos = event.offsetX,
            elWidth = el.clientWidth,
            percents = (mousePos / elWidth) * 100
        this.$emit('updateseek', percents)
        this.isPlaying = true;
      }
    } 
  }
</script>