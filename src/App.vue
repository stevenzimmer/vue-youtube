<!-- Parent Template -->
<template>
	<div class="container">
		<!-- Child Components -->
		<SearchBar
			@termChange="onTermChange"
		>
		</SearchBar>
		<div class="row">
			<div class="col-sm-8">
				<div class="row">
					<VideoDetail
						:video="selectedVideo"
					>
					</VideoDetail>
				</div>
			</div>
			<div class="col-sm-4">
				<div class="row">
					<VideoList
						@videoSelect="onVideoSelect"
						:videos="videos"
					>
					</VideoList>
				</div>
			</div>

		</div>
	</div>
</template>

<script>
import axios from 'axios';
import SearchBar from './components/SearchBar';
import VideoList from './components/VideoList';
import VideoDetail from './components/VideoDetail';

const API_KEY = 'AIzaSyAltP6LoCBcgdYA2ZKLZ9RIewvrxhvcbyU';

export default {
	name: 'App',
	components: {
		SearchBar: SearchBar,
		VideoList: VideoList,
		VideoDetail: VideoDetail
	},
	data() {
		return {
			selectedVideo: null,
			videos: []
		};
	},
	methods: {
		onVideoSelect( video ) {
			this.selectedVideo = video;
		},
		onTermChange( searchTerm ) {
			axios
				.get('https://www.googleapis.com/youtube/v3/search', {
					params: {
						key: API_KEY,
						type: 'video',
						part: 'snippet',
						q: searchTerm
					}
				})
				.then( response => {
					this.videos = response.data.items
				})
				.catch( e => {
					return e;
				});
		}

	}
};
</script>