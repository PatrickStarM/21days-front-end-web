<template>
	<view>
		<!-- 话题介绍组件 -->
		<topic-info :item="topicInfo"></topic-info>
		
		<!-- 消息区 -->
		<divider></divider>
		<block v-for="count in 2">
			<view class="top">
				<text class="iconfont icon-xiaoxi1 text-orange text-lg font-weight-bolder pl-2 mx-2"></text>
				<text>【新人必读】uni-app实战 社区交友</text>
			</view>
			<divider></divider>
		</block>
		
		<!-- 列表 -->
		<view class="px-2">
			<block v-for="(item,index) in list" :key="index">
				<common-list-item :item="item" :index="index"></common-list-item>
				<divider></divider>
			</block>
		</view>
	</view>
</template>

<script>
	import topicInfo from "@/components/common/topic-info.vue";
	import commonListItem from "@/components/common/common-list-item.vue";
	const demo = [
		{
			nickname: '派大星',
			avatarUrl: '/static/img/me.jpg',
			publishTime: '2022-04-03 22:14:01',
			isFollow: true,
			title: '吾心吾行澄如明镜，所做所为皆为正义',
			thumbnail: '/static/img/banner1.jpg',
			support: {
				type: "support",
				supportCount: 6,
				unSupportCount: 6
			},
			commentCount: 66,
			shareCount: 66
		},
		{
			nickname: '狗狗祟祟',
			avatarUrl: '/static/img/avatar1.jpeg',
			publishTime: '2022-04-03 22:14:02',
			isFollow: false,
			title: '我来了',
			// thumbnail: '/static/img/banner2.jpg',
			thumbnail: '',
			support: {
				type: "support",
				supportCount: 7,
				unSupportCount: 7
			},
			commentCount: 77,
			shareCount: 77
		},
		{
			nickname: '暗中观察',
			avatarUrl: '/static/img/avatar2.jpeg',
			publishTime: '2022-04-03 22:14:03',
			isFollow: false,
			title: '我走了',
			thumbnail: '/static/img/banner3.jpg',
			support: {
				type: "support",
				supportCount: 8,
				unSupportCount: 8
			},
			commentCount: 88,
			shareCount: 88
		},
	]
	
	export default {
		components:{
			topicInfo,
			commonListItem
		},
		
		data() {
			return {
				topicInfo: {
					id: 0,
					titlePic: '',
					title: '',
					desc: '',
					totalNum: 0,
					todayNum: 0
				},
				list: demo
			};
		},
		onLoad(option) {
			console.log(option)
			this.topicInfo = JSON.parse(option.item)
			console.log(this.topicInfo)
		},
		methods: {
			
		}
	}
</script>

<style scoped lang="less">
	@import (reference) '@/common/index.less';
	
	.top {
		.h-10;
		line-height: 100rpx;
		.text-lg;
	}

</style>
