<template>
  <li class="list-group-item media" @click="onVideoSelect">
    <img class="mr-3" :src="thumbnailUrl" />
    <div class="media-body heading">
      {{ video.snippet.title }}
    </div>
  </li>
</template>

<script>
export default {
  // Name of component
  name: "VideoListItem ",

  // Props to expect
  props: {
    video: Object,
  },

  // Methods which are used in the template

  methods: {
    async onVideoSelect() {
      this.$emit("videoSelect", this.video);
    },
  },

  // refactoring functions to kinda destructuring (not mandatory - optional for readability)
  computed: {
    thumbnailUrl() {
      return this.video.snippet.thumbnails.default.url;
    },
  },
};
</script>

<style scoped>
li {
  display: flex;
  cursor: pointer;
}

li:hover {
  background-color: #eee;
}

.heading {
  margin: 2rem;
}
</style>
