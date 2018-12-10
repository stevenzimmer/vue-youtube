<!-- Video list Child -->
<template>
	<ul class="list-group">
		<VideoListItem
			@videoSelect="onVideoSelect"
			v-for="video in videos"
			:video="video"
			:key="video.etag"
		>
		</VideoListItem>
	</ul>
</template>

<script>
import VideoListItem from './VideoListItem';

export default {
	name: 'VideoList',
	components: {
		VideoListItem
	},
	props: {
		videos: Array
	},
	methods: {
		onVideoSelect( video ) {
			this.$emit('videoSelect', video );
		}
	}
}
</script>