<template>
	<view>
		<uni-nav-bar statusBar backgroundColor="#ffcc80" color="#ffffff" title="动态"></uni-nav-bar>
		
		<scroll-view scroll-y class="mt-1" >
			<!-- 轮播图 -->
			<swiper class="px-2" indicator-active-color="#ffcc80" indicator-color="#fff3e0" :indicator-dots="true" :autoplay="true" :interval="3000" :duration="1000">
				<block v-for="(item,index) in topic.swiper" :key="index">
					<swiper-item>
						<image class="w-full rounded" :src="item.src" mode="aspectFill" lazy-load></image>
					</swiper-item>
				</block>
			</swiper>
			
			<!-- 热门分类 -->
			<hot-topic :nav="topic.nav"></hot-topic>
			
			<!-- 最近更新 -->
			<view class="px-2">
				<view class="text-lg mb-1">最近更新</view>
				<block v-for="(item,index) in topic.list" :key="index">
					<topic-list-item :item="item" :index="index"></topic-list-item>
				</block>
			</view>
		</scroll-view>
	</view>
</template>

<script>
	import uniNavBar from "@/components/uni/uni-nav-bar/uni-nav-bar.vue";
	import hotTopic from "@/components/common/hot-topic.vue";
	import topicListItem from "@/components/common/topic-list-item.vue";
	
	export default {
		components:{
			uniNavBar,
			hotTopic,
			topicListItem
		},
		data() {
			return {
				swiperheight:600,
				topic: {
					swiper: [{
						src: "/static/img/banner1.jpg"
					},
					{
						src: "/static/img/banner3.jpg"
					},
					{
						src: "/static/img/banner4.jpg"
					}
				],
				nav: [{
						name: "最新"
					},
					{
						name: "游戏"
					},
					{
						name: "打卡"
					},
					{
						name: "情感"
					},
					{
						name: "故事"
					},
					{
						name: "喜爱"
					},
				],
				list: [
					{
						id: 1,
						titlePic: "/static/img/1.jpeg",
						title: "君子之交，其淡如水",
						desc: "语出《庄子》：“君子之交淡若水，小人之交甘若醴；君子淡以亲，小人甘以绝。”",
						totalNum: 50,
						todayNum: 10
					},
					{
						id: 2,
						titlePic: "/static/img/2.jpeg",
						title: "芝兰当路，不得不锄",
						desc: "明万历年间，文坛领袖、兵部左侍郎汪道昆在巡视蓟辽军事设施时，不听汇报不察实情，却与当地文人吟诗作赋。当时的蓟辽总兵戚继光，把这个情况上报了首辅张居正。回京后，汪道昆给皇上呈报了一份妙笔生花、行文优美的散文奏章。首辅张居正阅之，愤然写下“芝兰当道，不得不除”，罢免了其官职。",
						totalNum: 50,
						todayNum: 10
					},
					{
						id: 3,
						titlePic: "/static/img/3.jpeg",
						title: "不驰于空想，不骛于虚声",
						desc: "这是李大钊先生的名言，意思是：不能空想，不行动；更不能去追求一些虚幻的东西。",
						totalNum: 50,
						todayNum: 10
					},
					{
						id: 4,
						titlePic: "/static/img/4.jpeg",
						title: "大人不华，君子务实",
						desc: "出自王充《潜夫论》，意思是：卓越的人不追求虚有其表 ，有修养有名望的人致力于实际。人民日报写评论时，曾用过这句话做标题，强调务实的重要性。",
						totalNum: 50,
						todayNum: 10
					},
					{
						id: 5,
						titlePic: "/static/img/5.jpeg",
						title: "守真志满，逐物意移",
						desc: "出自《千字文》，意思是：坚守内心的情怀，志向会饱满；追逐外在物质，内心的意志就会转移。",
						totalNum: 50,
						todayNum: 10
					},
					{
						id: 6,
						titlePic: "/static/img/6.jpeg",
						title: "似兰斯馨，如松之盛",
						desc: "出自《千字文》，意思是：像兰花一样散发馨香，如松柏一般青翠茂盛。",
						totalNum: 50,
						todayNum: 10
					},	
				]	
				}				
			};
		},
		onLoad() {},
		methods: {
			gotoDetail(index) {
				uni.navigateTo({
					url: "../topic-detail/topic-detail"
				})
			}
		}
	}
	
</script>

<style scoped>
	.topic-swiper {
		padding: 0 20upx 20upx 20upx; 
	}
	
	.topic-swiper image {
		width: 100%;
		border-radius: 10upx;
	}
	
	.topic-new {
		padding: 20upx;
	}
	
	.topic-new>view:first-child {
		padding-bottom: 5upx;
		font-size: 32upx;
	}
</style>