<template>
  <view class="p-2">
    <template v-if="searchList.length == 0">
      <!-- 搜索历史 -->
      <view class="py-2 text-md">搜索历史</view>
      <view class="flex flex-wrap">
        <view class="history-item" v-for="(item, index) in list" :key="index" @tap="tapSearchHistory(item)">{{ item }}</view>
      </view>
    </template>
    <template v-else>
      <view v-for="(item, index) in searchList" :key="index"><common-list-item :item="item" :index="index"></common-list-item></view>
    </template>
  </view>
</template>
<script>
  const demo = [{											
		nickname: '派大星',
		avatarUrl: '/static/img/me.jpg',
		publishTime: '2022-04-03 22:14:01',
		isFollow: false,
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
	}
  ];

import commonListItem from '@/components/common/common-list-item.vue';
export default {
  components: {
    commonListItem
  },
  data() {
    return {
      list: ['社区交友应用', 'UniApp指南', '从此学会搭讪', '生发秘诀', '多喝水', '小程序云开发', '前端工程化'],
      //搜索结果
      searchList: []
    };
  },
  //监听搜索框输入
  onNavigationBarSearchInputChanged(e) {
    console.log(e);
    this.searchTxt = e.text;
  },
  //监听点击导航栏搜索按钮
  onNavigationBarButtonTap(e) {
    console.log(e);
    //根据e.index确定点击了那个按钮
    this.searchEvent();
  },
  methods: {
    //点击搜索历史
    tapSearchHistory(txt) {
      this.searchTxt = txt;
      this.searchEvent();
    },
    //搜索事件
    searchEvent() {
      //收起盘
      uni.hideKeyboard();
      //loading
      uni.showLoading({
        title: '加载...',
        mask: false
      });
      //请求搜索
      setTimeout(() => {
        this.searchList = demo;
        uni.hideLoading();
      }, 1000);
    }
  }
};
</script>

<style lang="less" scoped>
@import (reference) '@/common/index.less';
.history-item {
  .border;
  .border-orange;
  .rounded;
  .text-sm;
  .text-base;
  .mr-2;
  .my-1;
  .px-2;
}
</style>