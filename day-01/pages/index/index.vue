<template>
	<view class="content">
		<!-- 清晰的模板和语义化 -->
		<view class="card">
			<h2 class="text-neutral">透明主色背景，阴影</h2>
		</view>

		<view class="btn bg-warning animated fast" hover-class="rotateInUpLeft">
			我是warning颜色的按钮
		</view>
		
		<view class="btn bg-success animated fast" hover-class="slideInLeft">
			我是success颜色的按钮
		</view>
		
		<view class="btn bg-primary animated fast" hover-class="fadeIn">
			我是primary颜色的按钮
		</view>

		<view class="iconfont icon-a-jiaren1x icon-wrapper animated" hover-class="bounceIn">
			{{title}}
		</view>
		
		<view class="flex">
			<view class="block-1" v-for="count in 3">
				{{count}}
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				title: 'Hello,这里是地球'
			}
		},
		onLoad() {

		},
		methods: {

		}
	}
</script>

<style scoped lang="less">
	/** 在style标签下重新引入基础less样式库 **/
	@import (reference) '@/common/index.less';

	/** mixin样式库，使得设计更统一 **/
	.content {
		.p-2;
		.text-center;
	}

	.card {
		.p-5;
		.bg-primary;
		.bg-opacity-20;
		.my-5;
		.rounded-2xl;
		.shadow-lg;
	}

	.btn {
		.px-5;
		.py-3;
		.mb-5;
		.rounded-full;
		.text-white;
		.font-bold;
		.text-2xl;
		.shadow-lg
	}

	.icon-wrapper {
		.text-3xl;
		.text-success;
		.m-5;
		.p-3;
		.border;
		.border-accent;
	}
	
	.block-1 {
		.w-25;
		.h-20;
		.mr-1;
		.my-1;
		.rounded;
		.bg-accent;
		.bg-opacity-100;
	}
</style>