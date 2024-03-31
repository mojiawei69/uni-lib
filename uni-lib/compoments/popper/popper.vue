<template>
	<view class="popper-main" v-if="isshow" :style="{ top: top + 'px', left: left + 'px', width: r_width + 'px'}">
		<span></span>
		<slot></slot>
	</view>
</template>

<script>
	export default {
		data(){
			return {
				offset: 10,
				top: 0,
				left: 0,
				r_width: 0,
				isshow: false
			}
		},
		methods: {
			show(e) {
				this.isshow = true;
				document.addEventListener("click", this.hide, false);
				e.stopPropagation();
			},
			hide() {
				if(!this.$el || !this.$el.classList) return;
				this.$el.classList.add('fade-out');
				document.removeEventListener("click", this.hide);
				setTimeout(() => {
					this.$el.classList.remove('fade-out');
					this.isshow = false;
				}, 300);
			}
		},
		mounted() {
			const { width, height, top, bottom, left, right } = this.$parent.$el.getBoundingClientRect();
			this.$parent.$el.addEventListener("click", this.show, false);
			this.r_width = this.width ?? width;
			//默认正下方
			this.top = height + this.offset;
			this.left = - ( (this.r_width - width) / 2 );
		},
		props: {
			width: {
				type: Number
			}
		}
	}
</script>

<style lang="less" scoped>
.popper-main {
	position: absolute;
	min-height: 100px;
	border: 1px solid #d8d8d8;
	border-radius: 5px;
	box-shadow: 0px 0px 12px rgba(167, 167, 167, 0.7);
	animation: fade-in 300ms cubic-bezier(0.001, 0.02, 0.165, 1);
	transform-origin: top center;
	z-index: 10000;
	background-color: #fff;
	color: #000000;
	span {
		&::after {
			content: '';
			position: absolute;
			width: 10px;
			height: 10px;
			left: calc(50% - 5px);
			top: calc(sqrt(2) * -4.07px);
			border-style: solid;
			border-width: 1px;
			border-color: transparent;
			border-left-color: #d8d8d8;
			border-top-color: #d8d8d8;
			transform: rotate(45deg);
			background-color: #fff;
			border-radius: 2px;
		}
	}
}
.fade-out {
	animation: fade-out 300ms cubic-bezier(0.001, 0.02, 0.165, 1);
}
@keyframes fade-in {
	0% {
		opacity: 0;
		transform: scale(0);
	}
	100% {
		opacity: 1;
		transform: scale(1);
	}
}
@keyframes fade-out {
	0% {
		opacity: 1;
		transform: scale(1);
	}
	100% {
		opacity: 0;
		transform: scale(0);
	}
}
</style>