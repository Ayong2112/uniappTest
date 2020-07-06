<template>
	<view>
		<view class="header">
			<view class="header_image"><image src="../../static/image/tabbar/4.jpg"></image></view>
			<view class="header_name">
				<view>哇咔咔</view>
				<view>wakaka</view>
			</view>
		</view>
		<view class='content'>
			<view>账号信息</view>
			<view>关于我们</view>
			<view>设置</view>
		</view>
	</view>
</template>

<script>
export default {
	data() {
		return {};
	},
	methods: {}
};
</script>

<style lang="scss">
.header {
	height: 100px;
	background: #007aff;
	& > view {
		float: left;
	}

	.header_image {
		height: 100px;
		vertical-align: top;
	}
	image {
		margin: 10px;
		width: 80px;
		height: 80px;
		border-radius: 3px;
	}
	.header_name {
		font-size: 24px;
		margin-top: 30px;
		margin-left: 10px;
	}
	.header_name > view:last-child {
		color: #333333;
		margin-top: 5px;
		font-size: 16px;
	}
}
.content{
	&>view{
		border-bottom: 1px solid #007AFF;
	}
}
</style>
