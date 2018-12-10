<template>
	<li class="list-group-item media" @click="onVideoSelect">
		<img :src="thumbnailURL" class="mr-3" />
		<div class="media-body">
			{{ videoTitle }}
		</div>

	</li>
</template>

<script>
	export default {
		name: 'VideoListItem',
		props: ['video'],
		computed: {
			videoTitle() {
				return this.video.snippet.title;
			},
			thumbnailURL() {
				return this.video.snippet.thumbnails.default.url;
			}
		},
		methods: {
			onVideoSelect() {
				this.$emit( 'videoSelect', this.video );
			}
		}
	}
</script>

<style scoped>
	li {
		display: flex;
		align-items: center;
		cursor: pointer;
	}

	li:hover {
		background-color: #eee;
	}
</style>