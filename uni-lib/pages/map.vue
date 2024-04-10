<template>
	<view>
		<map 
			:mapId="id"
			style="width: 100%; height: 600px;" 
			:latitude="latitude" 
			:longitude="longitude" 
			ref="amap"
			@markertap="markertap"
			:markers="covers"></map>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				id: 1, // 使用 marker点击事件 需要填写id
				title: 'map',
				latitude: 39.909,
				longitude: 116.39742,
				covers: [{
					id: 0,
					latitude: 39.909,
					longitude: 116.39742,
					iconPath: '../static/location.png',
					title: "title",
					
				}, {
					id: 1,
					latitude: 39.90,
					longitude: 116.39,
					iconPath: '../static/location.png',
					title: "title"
				}]
			}
		},
		methods: {
			markertap(e){
				this.longitude = e.detail.longitude;
				this.latitude = e.detail.latitude;
				console.log(this.$refs["amap"]);
			},
			
		},
		mounted() {
 
		}
	}
</script>

<style>

</style>