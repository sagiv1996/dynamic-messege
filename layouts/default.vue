<template lang="pug">
  v-app
    v-main(class= "info")
      v-container( fill-height class="justify-center" )  
        nuxt 
    v-btn( @click="openSetting" bottom left absolute icon dark   )
      v-icon fas fa-cog
        
          

</template>

<script>
export default {
  methods:{
    openSetting(){

    }
  }
}
</script>