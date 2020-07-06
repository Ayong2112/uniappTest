<template>
    <view>
        <un-grid :grid-list=gridList :show-tip="true" :col="4"></un-grid>

    </view>
</template>

<script>
    import unGrid from '../../components/grid/grid'

    export default {
        components: {
            unGrid
        },
        data() {
            return {
				gridList: [	//格子数据列表
					{
						name: '健康码',
						imgUrl: '../../static/image/grid/qrCode.svg',
						tips: '',
                        path:'/pages/qrCode/qrCode'
					},

				],
			}
        },
        methods: {}
    }
</script>

<style lang="scss" scoped>
	image{
		width: 24px;
		height: 24px;
	}

</style>
