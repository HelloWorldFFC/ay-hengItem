
## 前言
简介：
1.横向工具栏，可自定义文字及提示字，传入list，直接引用，我的里面常用项
2.配置跳转页面直接跳转，直接配置微信客服，即可跳转

## 有疑问
微信搜索“慢慢向好”小程序，找客服反馈，相应问题。
				  

## 素材
[图片资源](https://pixabay.com)
## 示例项目可直接运行 
## 开始使用
下载源码解压，复制`/components` 下的组件至项目根目录的 `/components` 文件夹下

`index.vue`的`script`加入如下部分：
```
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
```


`index.vue`的`template`加入如下部分：
```
<view style="margin-top: 26upx;">
			<hengItem :list="tipList" @toDetailPage="toDetailPage_tip"></hengItem>
		</view>

```
 
 
引入阿里矢量图，复制示例源码`/style`下的`/iconfont.css`至项目根目录的`/style` 文件夹下，内容如下：
```
@font-face {font-family: "iconfont";
  src: url('//at.alicdn.com/t/font_1948714_yfb5fxewps.eot?t=1609912198024'); /* IE9 */
  src: url('//at.alicdn.com/t/font_1948714_yfb5fxewps.eot?t=1609912198024#iefix') format('embedded-opentype'), /* IE6-IE8 */
  url('data:application/x-font-woff2;charset=utf-8;base64,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') format('woff2'),
  url('//at.alicdn.com/t/font_1948714_yfb5fxewps.woff?t=1609912198024') format('woff'),
  url('//at.alicdn.com/t/font_1948714_yfb5fxewps.ttf?t=1609912198024') format('truetype'), /* chrome, firefox, opera, Safari, Android, iOS 4.2+ */
  url('//at.alicdn.com/t/font_1948714_yfb5fxewps.svg?t=1609912198024#iconfont') format('svg'); /* iOS 4.1- */
}

.iconfont {
  font-family: "iconfont" !important;
  font-size: 16px;
  font-style: normal;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

.icon-xuanzhong:before {
  content: "\e607";
}

.icon-weixuan:before {
  content: "\e65d";
}

.icon-time:before {
  content: "\e619";
}

.icon-you:before {
  content: "\e600";
}

.icon-shuazi:before {
  content: "\e62a";
}

.icon-shuazi1:before {
  content: "\e610";
}

.icon-baocun-tianchong:before {
  content: "\e82b";
}

.icon-chehui:before {
  content: "\e66b";
}

.icon-bianji-cuxiantiao-fill:before {
  content: "\e69e";
}

.icon-qingkong:before {
  content: "\e629";
}

.icon-yanse:before {
  content: "\e886";
}

.icon-beiwanglushili:before {
  content: "\e612";
}

.icon-shijian:before {
  content: "\e631";
}

.icon-icon-eye-open:before {
  content: "\e60c";
}

.icon-icon-eye-close:before {
  content: "\e60f";
}

.icon-icon-1:before {
  content: "\e6e0";
}

.icon-jisuan:before {
  content: "\e643";
}

.icon-tongji1:before {
  content: "\e61d";
}

.icon-shezhi:before {
  content: "\e654";
}

.icon-xiugai:before {
  content: "\e698";
}

.icon-liebiao:before {
  content: "\e611";
}

.icon-add:before {
  content: "\e604";
}

.icon-shenghuofuwu:before {
  content: "\e681";
}

.icon-jingqu:before {
  content: "\e61e";
}

.icon-dianhua:before {
  content: "\e76a";
}

.icon-xiaoxi:before {
  content: "\e79c";
}

.icon-zhoumomanmanzuo:before {
  content: "\e7d5";
}

.icon-sousuo:before {
  content: "\e62c";
}

.icon-collection-b:before {
  content: "\e60d";
}

.icon-daohangdizhi:before {
  content: "\e65f";
}

.icon-like-line:before {
  content: "\e634";
}

.icon-like-s:before {
  content: "\e635";
}

.icon-tubiaozhizuo-:before {
  content: "\e605";
}

.icon-shoucang:before {
  content: "\e6a7";
}

.icon-ziyuan1:before {
  content: "\e618";
}

.icon-back:before {
  content: "\e602";
}

.icon-wode1:before {
  content: "\e658";
}

.icon-fs-funding:before {
  content: "\e60e";
}

.icon-home:before {
  content: "\e63f";
}

.icon-gupiao:before {
  content: "\e614";
}

.icon-xiangzuo:before {
  content: "\e6b0";
}

.icon-xiangyou:before {
  content: "\e65a";
}


```

页面`App.vue` 引入`css`

```
<style >
	 /*每个页面公共css */
	    @import './style/iconfont.css';
</style>

```



 