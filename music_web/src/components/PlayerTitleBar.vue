<template>
  <v-system-bar window height="100">
    <v-menu offset-y transition="slide-y-transition">
      <v-btn flat small right slot="activator">
         <v-avatar size = "80" align-center>
      <v-img src="/public/android-chrome-512x512.png">
        
      </v-img>
      </v-avatar><v-spacer></v-spacer><div><h3 class="font-weight-light ma-2">DJ Sxhosana</h3></div>
      </v-btn>
      <v-list>
        <v-card class="ma-2" @click="dialog = true">
          <v-avatar size = "180" tile align-center>
      <v-img src="/public/android-chrome-512x512.png">
        
      </v-img>
      </v-avatar>
      <v-list>
        <template v-for="(item, i) in items">
          <v-divider v-if="item.divider" :key="i"></v-divider>
          <v-list-item v-else :key="item.title">
            <v-icon class="ma-2">{{ item.icon }}</v-icon>
            
            <v-list-item-title>{{ item.title }}</v-list-item-title>
          </v-list-item>
        </template>
      </v-list>
        </v-card>
        <v-dialog v-model="dialog" max-width="100" >
          <v-card>
            <v-card-title><h3 >Dj Sxhosana</h3></v-card-title>
            <v-card-text>Version 1.0.0</v-card-text>
            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn flat @click="dialog = false">OK</v-btn>
            </v-card-actions>
          </v-card>
        </v-dialog>
      </v-list>
    </v-menu>
    <v-spacer></v-spacer>
    Dj Sxhosana Latest Music Streaming
    <v-spacer></v-spacer>
   <v-icon ></v-icon>
    <v-icon></v-icon>
    <v-icon></v-icon>
  </v-system-bar>
</template>

<script>
  export default {
    data () {
      return {
        dialog: false,
        width: 300,
      items: [
        { icon: 'phone', title: '078 465 4691' },
        {divider: true},
       {icon: 'email', title: 'djsxhosana@gmail.com'}
      ],
      }
    },
    methods: {
    
    }
  }
</script>