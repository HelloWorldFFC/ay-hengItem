<template>
	<view >
		<view style="margin-top: 26upx;">
			<hengItem :list="tipList" @toDetailPage="toDetailPage_tip"></hengItem>
		</view>
	</view>
</template>

<script>
	import hengItem from '@/components/ay-hengItem/hengItem.vue';
	export default {
		components: {
			hengItem,

		},
		data() {
			return {
				themeColor : '#33CCCC',
				tipList: [{
							img: 'https://cdn.pixabay.com/photo/2021/01/01/19/33/marshmallows-5879707__340.jpg',
							name: '上传凭证',
							// toPageUrl: '/pagesShow/upload/upload_img'
						},
						{
							img: 'https://cdn.pixabay.com/photo/2021/01/01/14/07/chapel-5878656__340.jpg',
							name: '客服',
							isKefu: true,
						},
						{
							img: 'https://cdn.pixabay.com/photo/2015/05/15/14/38/telephone-booth-768610__340.jpg',
							name: '关于我们',
						},
						{
							img: 'https://cdn.pixabay.com/photo/2016/12/19/08/39/mobile-phone-1917737__340.jpg',
							name: '设置',
						},
				
					],
				
			}
		},
		onLoad() {
			let that = this;

		},

		methods: {
			toDetailPage_tip(e) {
				let that = this;
				let list = e.list;
				
				let item = e.item;
			
				if (item.toPageUrl) {
					uni.navigateTo({
						url: item.toPageUrl
					})
					return;
				}
				// #ifdef MP-WEIXIN
				if(item.isKefu){
					return;
				}
				// #endif
				let list_img = [];
				list.forEach(item => {
					list_img.push(item.img)
				});
				let idx = e.curIndex;
				if (list_img && list_img.length > 0) {
					uni.previewImage({
						current: list_img[idx],
						urls: list_img,
						indicator: "number",
						loop: true,
					});
				}
			},
		}
	}
</script>

<style lang="scss">
</style>
