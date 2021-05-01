<template>
  <div class="container">
    <!--Emitting a function i.e. the child will ask the parent to trigger something 
    ("termChange" in our case) and the App component here will trigger the neccessary function) -->
    <SearchBar @termChange="onTermChange" />

    <div class="row">
      <!-- The selected video, :video is the prop -->
      <VideoDetail :video="selectedVideo" />

      <!-- PASSING PROP TO THE CHILD COMPONENT
         The one in quotes below is "kindof state", the first one is the prop name (our defined) 
         @onVideoSelect is the event emitted by the child component here  (VideoList) 
    -->
      <VideoList :videos="videos" @videoSelect="onVideoSelect" />
    </div>
  </div>
</template>

<script>
import axios from "axios";

// Child Components
import SearchBar from "./components/SearchBar";
import VideoList from "./components/VideoList";
import VideoDetail from "./components/VideoDetail";

// Youtube API_KEY
const API_KEY = "AIzaSyBcgcyxW_vD8ZrEPaa2S55_XG3uCDbfbew";

export default {
  // File Name
  name: "App",

  // Different components to render in this component (have to do this before using them)
  components: {
    SearchBar,
    VideoList,
    VideoDetail,
  },

  // Kind of state
  data() {
    // Inital values
    return {
      videos: [],
      selectedVideo: null,
    };
  },

  // Methods in this component
  methods: {
    async onVideoSelect(video) {
      this.selectedVideo = video;
    },

    // Triggered after any change in the search bar
    async onTermChange(searchTerm) {
      const response = await axios.get(
        `https://www.googleapis.com/youtube/v3/search`,
        {
          params: {
            key: API_KEY,
            type: "video",
            part: "snippet",
            q: searchTerm,
          },
        }
      );
      // console.log(response.data);

      /* Assign videos here (in the "kindof state")
       * This will cause the App (and all it's child components) to rerender
       */
      this.videos = response.data.items;
    },
  },
};
</script>
