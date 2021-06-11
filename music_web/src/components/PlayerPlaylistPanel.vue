<template>
  <v-card height="330" :class="{playlist}">
    <v-list>
      <v-list-tile 
        v-for="(track, index) in playlist" 
        :key="track.title"
        v-show="track.display"
        :class="[{selected: track === selectedTrack}, {even: index % 2 == 0}]">
        <v-list-tile-content @click="selectTrack(track)" @dblclick="playTrack()">
          <v-list-tile-title>{{ index | numbers }} {{ track.artist }} - {{ track.title }}</v-list-tile-title>
          <v-list-tile-title><button class="black--text" outline fab small color="white darken-4" @click="downloadWithVueResource">Download</button></v-list-tile-title>
        </v-list-tile-content>
           
    
        {{ track.howl.duration() | minutes }}
      </v-list-tile>
    </v-list>
  </v-card>
</template>

<script>
  export default {
    props: {
      playlist: Array,
      selectedTrack: Object
    },
    data(){
return{
 url:'https://78.media.tumblr.com/tumblr_m39nv7PcCU1r326q7o1_500.png'
}  
    },
    methods: {
      selectTrack (track) {
        this.$emit('selecttrack', track)
      },
      playTrack(index) {
        this.$emit('playtrack', index)
      },
       forceFileDownload(response){
      const url = window.URL.createObjectURL(new Blob([response.data]))
      const link = document.createElement('a')
      link.href = url
      link.setAttribute('download', 'file.png') //or any other extension
      document.body.appendChild(link)

      link.click()
    },
    
    downloadWithVueResource() {
      
      this.$http({
        method: 'get',
        url: this.url,
        responseType: 'arraybuffer'
      })
      .then(response => {
        this.forceFileDownload(response)  
      })
      .catch(() => console.log('error occured'))
      
    },
    } 
  }
</script>

<style scoped>
  .selected {
    background-color:  rgba(117, 46, 13, 0.979) !important;
  }
  .even {
    background-color: #505050
  }
  .playlist {
    overflow: auto
  }
</style>