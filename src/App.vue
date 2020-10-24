<template>
  <div class="container">
    <SearchBar @termChange="onTermChange"></SearchBar>
    <div class="row">
    <VideoDetail  :video="selectedVideo"></VideoDetail>
    <VideoList :videos="videos" @viedoSelect="onVideoSelect"></VideoList>
    </div>

    
  </div>
</template>


<script>
    import SearchBar from "./components/SearchBar";
    import VideoList from "./components/VideoList";
    import VideoDetail from "./components/VideoDeatail"
    import axios from "axios";
    const API_KEY = "AIzaSyDC6_gW8TAMVEGbkuTTxrwTumOE8ri96fM";

    export default {
         name: "App",
         components: {
             SearchBar,
             VideoList,
             VideoDetail
             },
          data() {
              return {
                  videos:[],
                  selectedVideo: null
              }
          },   
         methods: {
             onTermChange(term) {
                 axios.get("https://www.googleapis.com/youtube/v3/search", {
                     params: {
                         key: API_KEY,
                         type: 'video',
                         part: 'snippet',
                         q: term,
                     }
                 }).then((data) => {
                     this.videos = data.data.items;
                    //  console.log(data.data)
                 }).catch(err => console.log(err))
             },
             onVideoSelect(video) {
                 this.selectedVideo = video;
             }
         }    
    };
</script>

