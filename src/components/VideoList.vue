<template>
  <ul class="list-group cols-md-4">
    <!-- This will create only one list item,but we need to loop through all -->
    <!-- <VideoListItem :video="video" /> -->

    <!-- This will render the item for every item on the list, 
         :video is the prop (: is shorthand to v-bind),
         @videoSelect is the event emitted from the child (VideoListItem) component
         :key has to be unique (mandatory + improves rerendering performance) -->
    <VideoListItem
      v-for="video in videos"
      :video="video"
      :key="video.etag"
      @videoSelect="onVideoSelect"
    />
  </ul>
</template>

<script>
// Child component
import VideoListItem from "./VideoListItem";

export default {
  // Name of component
  name: "VideoList",

  // Child component it will display
  components: {
    VideoListItem,
  },

  // Methods to use in this template
  methods: {
    // This will be triggered when the child emits (refer line 14)
    async onVideoSelect(video) {
      this.$emit("videoSelect", video);
    },
  },

  // List of props the component should expect (with types that are optional)
  props: {
    videos: Array,
  },
};
</script>

<style lang=""></style>
