<template>
    <li class="list-group-item media" @click="onVideoSelect"><img class="mr-3" :src="src"/> <div v-if="title" class="media-body">{{title}}</div></li>
</template>


<script>
export default {
    name: "VideoListItem",
    props: {
        video: Object
    },
    computed: {
        src() {
            return this.video.snippet.thumbnails.default.url
        },
        title() {
            return this.video.snippet.title
        }
    },
    methods: {
        onVideoSelect() {
            this.$emit("videoSelect", this.video)
        }
    }


}
</script>


<style scoped>
  li {
      display: flex;
      cursor: pointer;
  }

  li:hover {
      background-color: #eee;
  }
</style>