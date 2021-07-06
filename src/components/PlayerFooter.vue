<template>
  <v-system-bar window>
    <v-menu offset-y transition="slide-y-transition">
      <div flat small right slot="activator">
        <v-icon></v-icon> djsxhosana
      </div>
     
    </v-menu>
    <v-spacer></v-spacer>
   
    <v-spacer></v-spacer>
    <div >
      <v-icon></v-icon>
    </div>
    
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
  }
</script>
