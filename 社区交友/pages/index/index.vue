<template>
  <view class="p-2">
    <!-- 顶部选项卡 -->
    <scroll-view scroll-x class="scroll-row shadow" style="100rpx;">
      <view class="scroll-row-item px-3 py-2 font-md" v-for="(item, index) in tabBars" :key="index"
        :class="tabIndex === index ? 'text-orange text-lg fontweight-bolder' : ''" @tap="changeTab(index)">
        {{ item.name }}
      </view>
    </scroll-view>

    <!-- 横向滑动的视图容器,对应上面的tabbar -->
    <swiper :duration="150" :current="tabIndex" :style="'height:' + scrollH + 'px;'" @change="onChangeTab">
      <swiper-item v-for="(item, index) in newsList" :key="index">
        <!-- 每个横向的swiper-item里,用纵向滚动视图容器来显示数据 -->
        <scroll-view scroll-y="true" :style="'height:' + scrollH + 'px;'" @scrolltolower="loadmore(index)">
		<template v-if="item.list.length > 0"> 
          <view class="p-2">
            <view v-for="(item2, index2) in item.list" :key="index2" class="mb-3">
				<!-- 通用列表组件 -->
              <common-list-item :item="item2" :index="index2" @follow="follow" @unFollow="unFollow"
                @doSupport="doSupport">
              </common-list-item>
              <divider></divider>
            </view>
			<loadmore :loadmore="item.loadmore"></loadmore>
          </view>
		  </template>
		  <template v-else>
		  	<nothing></nothing>
		  </template>
        </scroll-view>
      </swiper-item>
    </swiper>
  </view>
</template>

<script>
  import commonListItem from "@/components/common/common-list-item.vue"
  import loadmore from '@/components/common/loadmore.vue';
  export default {
    components: {
      commonListItem,
	  loadmore
    },
    data() {
      return {
        //列表高度
        scrollH: 600,
        tabIndex: 0,
        scrollInto:"",
        //顶部选项卡
        tabBars: [{
            name: '推荐'
          },
          {
            name: '体育'
          },
          {
            name: '热点'
          },
          {
            name: '财经'
          },
          {
            name: '娱乐'
          },
          {
            name: '军事'
          },
          {
            name: '历史'
          }
        ],
        newsList: []
      };
    },
    onLoad() {
        //异步获取系统信息
        let res = uni.getSystemInfo({
          success: res => {
            console.log(res);
            this.scrollH = res.windowHeight - uni.upx2px(100);
          }
        });
		this.getData();
      },
	  //点击导航栏搜索框
	  onNavigationBarSearchInputClicked() {
	  	uni.navigateTo({
	  		url: '../search/search'
	  	})
	  },
	   onNavigationBarButtonTap() {
	      console.log('跳转write')
	      uni.navigateTo({
	        url:'../write/write'
	      })
	    },
      methods: {
		loadmore(index) {
			console.log('loadmore')
			//获取当前列表
			let item = this.newsList[index]
			//判断是否处于可加载状态
			if (item.loadmore !== '上拉加载更多') {
				console.log('上拉加载更多')
				return;
			}
			//修改当前列表
			item.loadmore = '加载中...';
			//模拟数据请求
			setTimeout(() => {
				//加载数据
				item.list = [...item.list, ...item.list];
				//修改状态
				item.loadmore = '上拉加载更多';
			}, 2000);
		},
		//获取数据
		getData() {
			let arr = [];
			//生成数据
			for (let i = 0; i < this.tabBars.length - 1; i++) {
				//列表数据模板
				let obj = {
					//1.上拉加载2.加载中3.没有更多了
					loadmore: '上拉加载更多',
					list: [
						{											
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
						},
						{
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
							},
							{
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
					]
				};
				arr.push(obj);
			}
			//最后一个选项卡内容
			let empyObj = {
				list: []
			};
			arr.push(empyObj);
			this.newsList = arr;
		},
        follow(e) {
          console.log(e)
          let list = this.newsList[this.tabIndex].list;
          console.log(list)
          list[e].isFollow = true;
          uni.showToast({
            title: '关注成功'
          });
        },
    
        unFollow(e) {
          let list = this.newsList[this.tabIndex].list;
          list[e].isFollow = false;
          uni.showToast({
            title: '取消关注'
          });
        },
    
        doSupport(e) {
          console.log(e);
          let list = this.newsList[this.tabIndex].list;
          let item = list[e.index];
          //执行踩操作
          if (item.support.type === 'support' && e.type === 'unSupport') {
            //顶-1,踩+1
            item.support.unSupportCount++;
            item.support.supportCount--;
          } else if (item.support.type === 'unSupport' && e.type === 'support') {
            item.support.unSupportCount--;
            item.support.supportCount++;
          }
          item.support.type = e.type;
        },
        //切换选项卡
        changeTab(index) {
          if (this.tabIndex === index) {
            return;
          }
          // console.log(index);
          this.tabIndex = index;
          // console.log(this.tabIndex);
        },
        //监听滑动
        onChangeTab(e){
          this.changeTab(e.detail.current)
        },
      }
    };
    </script>
    
    <style lang="less" scoped>
    .scroll-row {
      width: 100%;
      white-space: nowrap;
    }
    
    .scroll-row-item {
      display: inline-block !important ;
    }
    </style>
