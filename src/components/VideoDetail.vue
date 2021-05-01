<template>
  <!--v-if is the if statement (or vue directive) to check whether the video exists or not. 
  It works on falsy an truthy values -->
  <div v-if="video" class="col-md-8">
    <div class="embed-responsive embed-responsive-16by9">
      <iframe class="embed-responsive-item" :src="videoUrl" />
    </div>

    <div class="details">
      <h4>
        {{ video.snippet.title }}
      </h4>

      <p>
        {{ video.snippet.description }}
      </p>
    </div>
  </div>
</template>

<script>
export default {
  // Name of the component
  name: "VideoDetail",

  // The props, this component has received
  props: {
    video: Object,
  },

  // Computed functions (optional) for code readability
  computed: {
    videoUrl() {
      return `https://www.youtube.com/embed/${this.video.id.videoid}`;
    },
  },
};
</script>

<style scoped>
.details {
  margin-top: 0.625rem;
  padding: 0.625rem;
  border: 1px solid #ddd;
  border-radius: 4px;
}
</style>
