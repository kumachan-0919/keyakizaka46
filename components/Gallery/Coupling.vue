<template>
    <v-content>
      <v-container>
            <v-row>
              <v-col v-for="(gallery, index) in GallerysCouplingArray" :key="index" cols="12" sm="6">
                <a :href="gallery.url" target="_blank">
                <v-img class="gallery-img" v-bind:src="gallery.src" :ripple="true" height="315px" width="560px"></v-img>
                </a>
                <span v-text="gallery.name"></span>
              </v-col>
            </v-row>
      </v-container>
    </v-content>
</template>

<script>
  import firebase from 'firebase'
  export default {
    data() {
      return {
        GallerysCouplingArray: [],
      }
    },
    created() {
      const that = this
      const gallerys = firebase.firestore().collection("galleryCoupling").orderBy("array", "asc")
      gallerys.get().then((snapshot) => {
        snapshot.forEach((doc) => {
          const gallerys = doc.data()
          that.GallerysCouplingArray = [
            ...that.GallerysCouplingArray,
            {
              name: gallerys.name,
              src: gallerys.src,
              array: gallerys.array,
              url: gallerys.url,
            },
          ]
        })
      })
    },
  }
</script>

<style>

</style>