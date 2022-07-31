<template>
    <div class="container">
        <!-- v-on:termChange="onTermChange" -->
        <SearchBar @termChange="onTermChange"></SearchBar>
        <!-- v-bind:videos="videos" -->
        <div class="row">
            <VideoDetail :video="selectedVideo">
            </VideoDetail>
            <VideoList :videos="videos" @videoSelect="onVideoSelect">
            </VideoList>
        </div>
    </div> 
</template>

<script>
    import axios from 'axios';
    import SearchBar from './components/SearchBar';
    import VideoList from './components/VideoList';
    import VideoDetail from './components/VideoDetail'
    const API_KEY = 'AIzaSyBtg7wP9NS3zp9cx8rnmvXkv_edBdNytdI';
    export default{
        name: "App",
        components: { 
            SearchBar,
            VideoList,
            VideoDetail,
        },
        data() {
            return { videos: [], selectedVideo: null };
        },
        methods: {
            onVideoSelect(video) {
                this.selectedVideo = video;
            },
            onTermChange(serachTerm){
                axios.get('https://www.googleapis.com/youtube/v3/search',{
                   params:{
                    key:API_KEY,
                    type: 'video',
                    part: 'snippet',
                    q: serachTerm
                   } 
                }).then( response => {
                    this.videos = response.data.items;
                })
            }
        }
    }; 
</script>