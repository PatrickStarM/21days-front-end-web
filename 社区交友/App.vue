<script>
	export default {
		onLaunch: function() {
			console.log('App Launch')
		},
		onShow: function() {
			console.log('App Show')
		},
		onHide: function() {
			console.log('App Hide')
		}
	}
</script>

<style lang="less">
	/*每个页面公共css */
	@import url("@/common/index.less");
	@import url("@/common/icon.css");
	@import url("@/common/uni.css");
	@import url("@/common/animate.css");
	@import url("@/common/style.css");
</style>
