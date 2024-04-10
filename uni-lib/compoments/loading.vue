<template>
	<div>
		<div style="width: 200px; height: 200px;position: relative;">
			<div class="loading-main" :style="`transform: rotate(${value}deg)`"></div>
			<div style="width: 100%;height: 50%;background-color: #fff;z-index: 2;position: relative;"></div>
			<div class="loading-box">
				文字
			</div>
		</div>
		<svg>
			<defs>
			  <radialGradient
			    id="gradient"
			    cx="50%"
			    cy="50%"
			    r="60%"
			    fx="50%"
			    fy="50%"
			  >
			    <stop offset="30%" stop-color="#c1dfc4" />
			    <stop offset="100%" stop-color="#3cba92" />
			  </radialGradient>
			</defs>
			<circle cx="50" cy="50" r="30" stroke="url(#gradient)"></circle>
		</svg>
	</div>
</template>

<script>
	export default {
		props: {
			value: {
				type: Number,
				default: 0
			}
		}
	}
</script>

<style lang="less" scoped>

.loading-main {
	width: 200px;
	height: 100px;
	background-color: red;
	border-radius: 200px 200px 0 0 ;
	position: relative;
	display: flex;
	justify-content: center;
	align-items: center;
	transform-origin: 100px 100px;
	z-index: 1;
}
.loading-box {
	width: 180px;
	height: 180px;
	border-radius: 50%;
	background-color: #fff;
	position: absolute;
	top: 50%;
	left: 50%;
	transform: translate(-50%,-50%);
	z-index: 3;
	text-align: center;
	line-height: 160px;
}
svg {
	transform: rotate(90deg);
}
svg circle {
	stroke-width: 20px;
	fill: none;
	stroke-linecap: round;
	stroke-dasharray: 3.14 * 10;
	stroke-dashoffset: 3.14 * 10;
	
}
</style>