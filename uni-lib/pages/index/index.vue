<template>
	<view class="content">
		<view class="btn">
			点击弹出popper
			<popper ref="popper1" />
		</view>
		<view class="btn">
			自定义宽度
			<popper ref="popper2" :width="300"/>
		</view>
		<view class="btn">
			自定义内容
			<popper ref="popper3" :width="300">
				<view class="btn">
					内容
				</view>
			</popper>
		</view>
		<view class="btn" @click="chooseImg">
			选择相册
		</view>
		<image v-for="(item, index) in imgPath" style="width: 50px; height: 50px;" :src="item"></image>
	</view>
</template>

<script>
	import popper from "../../compoments/popper/popper.vue";
	export default {
		data() {
			return {
				imgPath: []
			}
		},
		components: { popper }, 
		methods:{
			chooseImg(){
				uni.chooseFile({
					count: 10,
					type: 'all',
					success: res => {
						console.log(res.tempFilePaths, res.tempFiles);
						this.imgPath = res.tempFilePaths;
					},
					fail: err => {
						console.log(err);
					}
				})
			}
		}
	}
</script>

<style lang="less" scoped>
.content {
	display: flex;
	flex-direction: column;
	flex-grow: 1;
	align-items: center;
	height: 1000vh;
	gap:20px;
	.btn {
		position: relative;
		width: 120px;
		height: 40px;
		background-color: #007aff;
		border-radius: 40px;
		cursor: pointer;
		color:#fff;
		text-align: center;
		line-height: 40px;
		font-size: 12px;
	}
}
.popper-content {
	width: 40px;
	height: 40px;
	background-color: red;
}
</style>
