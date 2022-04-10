<template>
	<view>
		<view class="info-wrapper">
			<image :src="item.avatarUrl" lazy-load class="avatar" @tap="openSpace"></image>
			<view class="flex-1">
				<view class="text-md">{{item.nickname}}</view>
				<view class="publish-time">{{item.publishTime}}</view>
			</view>
			<view  v-if="!item.isFollow" class="follow-btn animated fast"  hover-class="fadeIn" @tap="follow">
				关注
			</view>
			<view class="unfollow-btn animated fast" v-else hover-class="fadeIn" @tap="unFollow">
				已关注
			</view>
		</view>

		<view class="text-lg my-1 py-1" @tap="openDetail">
			{{item.title}}
		</view>

		<!-- 图片 -->
		<image v-if="item.thumbnail" :src="item.thumbnail" class="thumbnail"></image>

		<!-- 图标 -->
		<view class="flex align-center">
			<!-- 顶d -->
			<view class="icon-wrapper animated fast" hover-class="jello text-orange" @tap="doSupport('support')"
				:class="item.support.type === 'support' ? 'support-active':''">
				<text class="iconfont icon-dianzan2 mr-2"></text>
				<text>{{item.support.supportCount}}</text>
			</view>
			<!-- 踩 -->
			<view class="icon-wrapper animated fast" hover-class="jello text-orange" @tap="doSupport('unSupport')"
				:class="item.support.type === 'unSupport' ? 'support-active':''">
				<text class="iconfont icon-cai mr-2"></text>
				<text>{{item.support.unSupportCount}}</text>
			</view>
			<view class="icon-wrapper animated fast" hover-class="jello" @top="openDetail">
				<text class="iconfont icon-pinglun2 mr-2"></text>
				<text>{{item.commentCount}}</text>
			</view>
			<view class="icon-wrapper animated fast " hover-class="jello" @top="openDetail">
				<text class="iconfont icon-fenxiang mr-2"></text>
				<text>{{item.shareCount}}</text>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		name: "common-list-item",
		props: {
			item: Object,
			index: Number
		},
		methods: {
			//打开个人空间
			openSpace() {
				uni.showToast({
					title: "打开个人空间",
					duration: 1000
				})
			},
			//关注
			follow() {
				this.$emit('follow', this.index)
			},
			//取关
			unFollow() {
				this.$emit('unFollow', this.index)
			},
			//打开详情页
			openDetail() {
				uni.showToast({
					title: "打开详情页",
					duration: 1000
				})
			},
			//顶踩操作
			doSupport(type) {
				this.$emit('doSupport', {
					type,
					index: this.index
				})
			}
		}
	}
</script>

<style lang="less" scoped>
	@import (reference) '@/common/index.less';

	.info-wrapper {
		.flex;
		.items-center;
		.justify-center;
	}
	
	.avatar {
		.w-10;
		.h-10;
		.rounded-full;
		.mr-2;
	}

	.thumbnail {
		.h-35;
		.w-full;
		.rounded-md;

	}

	.publish-time {
		.text-sm;
		color: #9d9589;
	}

	.follow-btn {
		.w-9;
		.h-5;
		.flex;
		.items-center;
		.justify-center;
		.rounded-md;
		.text-white;
		.bg-orange;
	}
	.unfollow-btn {
		.w-9;
		.h-5;
		.flex;
		.items-center;
		.justify-center;
		.rounded-md;
		.text-orange;
		.border-orange;
	}

	.icon-wrapper {
		.flex;
		.items-center;
		.justify-center;
		.flex-1
	}

	.support-active {
		.text-orange;
	}
</style>
