<template>
	<view class="qrCodeWrap">
		<!-- 顶部-->
		<view class="header">
			<view class="backLeft"><view class="iconfont iconzuo"></view></view>
			<view>电子健康码</view>
			<view class="rightIcon">
				<view class="iconfont iconmore"></view>
				<view class="shu"></view>
				<view class="iconfont iconyuandian"></view>
			</view>
		</view>
		<!-- 中间部分 -->
		<view class="content">
	<!-- 		<view class="backgroundImg">
				<image src="../../static/image/qrcode/sdh.jpg" mode=""></image>
				<image src="../../static/image/qrcode/sdh.jpg" mode=""></image>
				<image src="../../static/image/qrcode/sdh.jpg" mode=""></image>
				<image src="../../static/image/qrcode/sdh.jpg" mode=""></image>
				<image src="../../static/image/qrcode/sdh.jpg" mode=""></image>
			</view> -->
			<view class="contentWrap">
				<!-- 顶部 -->
				<view class="content_header">
					<view class="iconfont iconai-connection"></view>
					<view class="content_header_title">电子健康通行码</view>
				</view>
				<!-- 日期 -->
				<view class="dateTime">
					<view>{{ nowDate.date }}</view>
					<view>{{ nowDate.time }}</view>
				</view>
				<!-- 二维码 -->
				<view class="qrimg-i" @click="refreshCode">
					<tki-qrcode
						v-if="ifShow"
						cid="qrcode1"
						ref="qrcode"
						:val="val"
						:size="size"
						:unit="unit"
						:background="background"
						:foreground="foreground"
						:pdground="pdground"
						:icon="icon"
						:iconSize="iconsize"
						:lv="lv"
						:onval="onval"
						:loadMake="loadMake"
						:usingComponents="true"
						@result="qrR"
					/>
				</view>
				<view class="refresh">点击二维码刷新</view>
				<view class="fullName">*飞</view>
				<!-- <view class="poetry">不经一番彻骨寒，怎得梅花扑鼻香</view> -->
				<!-- <view class="container">
					<view class="qrimg">
					</view>
					<view class="uni-padding-wrap"><view class="uni-title">请输入要生成的二维码内容</view></view>
					<view class="uni-list"><input class="uni-input" placeholder="请输入要生成的二维码内容" v-model="val" /></view>
					<view class="uni-padding-wrap uni-common-mt"><view class="uni-title">设置二维码大小</view></view>
					<view class="body-view"><slider :value="size" @change="sliderchange" min="50" max="500" show-value /></view>
					<view class="uni-padding-wrap">
						<view class="btns">
							<button type="primary" @tap="selectIcon">选择二维码图标</button>
							<button type="primary" @tap="creatQrcode">生成二维码</button>
							<button type="primary" @tap="saveQrcode">保存到图库</button>
							<button type="warn" @tap="clearQrcode">清除二维码</button>
							<button type="warn" @tap="ifQrcode">显示隐藏二维码</button>
						</view>
					</view>
				</view> -->
			</view>
			<view class="bottom">数据来源：国家政务服务平台及本省公共管理机构</view>
		</view>
	</view>
</template>

<script>
import tkiQrcode from '@/components/tki-qrcode/tki-qrcode.vue';
export default {
	components: { tkiQrcode },
	data() {
		return {
			ifShow: true,
			val: '这里是扫码扫出来的值1122', // 要生成的二维码值
			size: 220, // 二维码大小
			unit: 'rpx', // 单位
			background: '#FFFFFF', // 背景色
			foreground: '#008001', // 前景色
			pdground: '#008001', // 角标色
			icon: '', // 二维码图标
			iconsize: 40, // 二维码图标大小
			lv: 3, // 二维码容错级别 ， 一般不用设置，默认就行
			onval: false, // val值变化时自动重新生成二维码
			loadMake: true, // 组件加载完成后自动生成二维码
			src: '', // 二维码生成后的图片地址或base64
			// ↑ 二维码部分
			timer: null,
			nowDate: {
				date: '',
				time: ''
			}
		};
	},
	methods: {
		// 获取当前年月日
		getMonthDay() {
			let _this = this;
			this.timer = setInterval(() => {
				let nd = new Date();
				let Y = nd.getFullYear();
				let M = nd.getMonth() + 1;
				let D = nd.getDate();
				let H = nd.getHours();
				let m = nd.getMinutes();
				let s = nd.getSeconds();
				H = H < 10 ? `0${H}` : H;
				m = m < 10 ? `0${m}` : m;
				s = s < 10 ? `0${s}` : s;
				_this.nowDate.date = `${M}月${D}日`;
				_this.nowDate.time = `${H}:${m}:${s}`;
			}, 1000);
		},

		randomWord(randomFlag, min, max) {
			// randomFlag-是否任意长度 min-任意长度最小位[固定位数] max-任意长度最大位
			// 生成3-32位随机串：randomWord(true, 3, 32)
			// 生成43位随机串：randomWord(false, 43)
			var str = '',
				range = min,
				arr = [
					'0',
					'1',
					'2',
					'3',
					'4',
					'5',
					'6',
					'7',
					'8',
					'9',
					'a',
					'b',
					'c',
					'd',
					'e',
					'f',
					'g',
					'h',
					'i',
					'j',
					'k',
					'l',
					'm',
					'n',
					'o',
					'p',
					'q',
					'r',
					's',
					't',
					'u',
					'v',
					'w',
					'x',
					'y',
					'z',
					'A',
					'B',
					'C',
					'D',
					'E',
					'F',
					'G',
					'H',
					'I',
					'J',
					'K',
					'L',
					'M',
					'N',
					'O',
					'P',
					'Q',
					'R',
					'S',
					'T',
					'U',
					'V',
					'W',
					'X',
					'Y',
					'Z'
				];

			// 随机产生
			if (randomFlag) {
				range = Math.round(Math.random() * (max - min)) + min;
			}
			for (var i = 0; i < range; i++) {
				let pos = Math.round(Math.random() * (arr.length - 1));
				str += arr[pos];
			}
			return str;
		},
		// 刷新二维码
		refreshCode() {
			this.val = this.randomWord(false, 32);
			this.creatQrcode();
		},
		// ↓ 二维码事件
		sliderchange(e) {
			this.size = e.detail.value;
		},
		creatQrcode() {
			this.$refs.qrcode._makeCode();
		},
		saveQrcode() {
			this.$refs.qrcode._saveCode();
		},
		qrR(res) {
			this.src = res;
		},
		clearQrcode() {
			this.$refs.qrcode._clearCode();
			this.val = '';
		},
		ifQrcode() {
			this.ifShow = !this.ifShow;
		},
		selectIcon() {
			let that = this;
			uni.chooseImage({
				count: 1, //默认9
				sizeType: ['original', 'compressed'], //可以指定是原图还是压缩图，默认二者都有
				sourceType: ['album'], //从相册选择
				success: function(res) {
					that.icon = res.tempFilePaths[0];
					setTimeout(() => {
						that.creatQrcode();
					}, 100);
					// console.log(res.tempFilePaths);
				}
			});
		}
	},
	created() {
		this.getMonthDay();
	},
	beforeDestroy() {
		if (this.timer) {
			clearInterval(this.timer);
		}
	}
};
</script>

<style lang="scss" scoped>
@import '../../static/iconfont/iconfont.css';
.qrCodeWrap {
	.header {
		height: 48px;
		line-height: 48px;
		font-size: 16px;
		font-weight: 100;
		.backLeft {
			margin: 0 10px;
			.iconzuo {
				font-size: 24px;
			}
		}
		.rightIcon {
			float: right;
			border: 1px solid rgb(223, 223, 223);
			border-radius: 20px;
			height: 30px;
			width: 100px;
			margin: 10px 8px 0 0;
			.iconfont {
				font-size: 22px;
				margin: 0 13px;
				line-height: 30px;
			}
			.shu {
				width: 0;
				margin-top: 4px;
				height: 20px;
				border-left: 1px solid rgb(223, 223, 223);
			}
		}
		.rightIcon > view {
			float: left;
		}
	}
	.header > view {
		float: left;
	}
	.content {
		height: calc(100vh - 48px);
		background-color: rgb(0, 128, 1);
		overflow: hidden;
		.contentWrap {
			width: 86%;
			height: 460px;
			background: #ffffff;
			margin: 14% 7% 0;
			border-radius: 10px;
			text-align: center;
			.content_header > view {
				float: left;
			}
			.content_header {
				height: 60px;
				line-height: 60px;
				background-color: rgb(230, 229, 227);
				border-radius: 10px 10px 0 0;
				.iconfont {
					color: rgb(121, 121, 121);
					font-size: 22px;
					margin-left: 10px;
				}
				.content_header_title {
					font-size: 16px;
				}
			}
			.dateTime {
				font-size: 30px;
				font-weight: 800;
				line-height: 34px;
			}
			.refresh {
				color: #838489;
				font-size: 14px;
			}
			.fullName {
				margin-top: 20px;
				font-size: 18px;
				font-weight: 800;
			}
			.poetry {
				margin-top: 10px;
				font-size: 18px;
				font-weight: 600;
			}
		}
		.bottom{
			width: 100%;
			position: fixed;
			bottom: 30px;
			font-size: 14px;
			color: #FFFFFF;
			text-align: center;
		}
		// 图片
		.backgroundImg {
			position: relative;
			image {
				position: absolute;
				width: 70px;
				height: 60px;
			}
			image:nth-of-type(1){
				top: 50px;
				left: 20px;
			}
		}
	
	}
}
</style>
