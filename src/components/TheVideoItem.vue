<template>
  <a class="mb-7 group">
    <VideoItemThumbnail :index="index" />
    <VideoItemInfo :index="index" />
  </a>
</template>

<script>
import VideoItemThumbnail from './VideoItemThumbnail.vue';
import VideoItemInfo from './VideoItemInfo.vue';
export default {
  components: { VideoItemInfo, VideoItemThumbnail },
  props: ['index'],
  name: 'TheVideoItem',
};
</script>

<style scoped></style>
