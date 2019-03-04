<template>
	<view class="page">
		 <view>
                <scroll-view class="scroll-view_H" scroll-x="true" @scroll="scroll" scroll-left="120">
                    <view id="demo1" class="scroll-view-item_H uni-bg-red">A</view>
                    <view id="demo2" class="scroll-view-item_H uni-bg-green">B</view>
                    <view id="demo3" class="scroll-view-item_H uni-bg-blue">C</view>
                </scroll-view>
            </view>
		<view class="uni-product-list">
			<view class="uni-product" v-for="(product,index) in productList" :key="index">
				<view class="image-view">
					<image v-if="renderImage" class="uni-product-image" :src="product.image"></image>
				</view>
				<view class="uni-product-title">{{product.title}}</view>
				<view class="uni-product-price">
					<text class="uni-product-price-favour">￥{{product.originalPrice}}</text>
					<text class="uni-product-price-original">￥{{product.favourPrice}}</text>
					<text class="uni-product-tip">{{product.tip}}</text>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
export default {
    data() {
        return {
            title: 'product-list',
			productList: [],
            renderImage: false,
			
            scrollTop: 0,
            old: {
                scrollTop: 0
            }
        };
    },
    methods: {
        scroll: function(e) {
            console.log(e)
            this.old.scrollTop = e.detail.scrollTop
        },
        loadData(action = 'add') {
            const data = [
                {
                    image: 'https://img-cdn-qiniu.dcloud.net.cn/uploads/example/product1.jpg',
                    title: 'Apple iPhone X 256GB 深空灰色 移动联通电信4G手机',
                    originalPrice: 9999,
                    favourPrice: 8888,
                    tip: '自营'
                },
                {
                    image: 'https://img-cdn-qiniu.dcloud.net.cn/uploads/example/product2.jpg',
                    title: 'Apple iPad 平板电脑 2018年新款9.7英寸',
                    originalPrice: 3499,
                    favourPrice: 3399,
                    tip: '优惠'
                },
                {
                    image: 'https://img-cdn-qiniu.dcloud.net.cn/uploads/example/product3.jpg',
                    title: 'Apple MacBook Pro 13.3英寸笔记本电脑（2017款Core i5处理器/8GB内存/256GB硬盘 MupxT2CH/A）',
                    originalPrice: 12999,
                    favourPrice: 10688,
                    tip: '秒杀'
                },
                {
                    image: 'https://img-cdn-qiniu.dcloud.net.cn/uploads/example/product4.jpg',
                    title: 'Kindle Paperwhite电纸书阅读器 电子书墨水屏 6英寸wifi 黑色',
                    originalPrice: 999,
                    favourPrice: 958,
                    tip: '秒杀'
                },
                {
                    image: 'https://img-cdn-qiniu.dcloud.net.cn/uploads/example/product5.jpg',
                    title: '微软（Microsoft）新Surface Pro 二合一平板电脑笔记本 12.3英寸（i5 8G内存 256G存储）',
                    originalPrice: 8888,
                    favourPrice: 8288,
                    tip: '优惠'
                },
                {
                    image: 'https://img-cdn-qiniu.dcloud.net.cn/uploads/example/product6.jpg',
                    title: 'Apple Watch Series 3智能手表（GPS款 42毫米 深空灰色铝金属表壳 黑色运动型表带 MQL12CH/A）',
                    originalPrice: 2899,
                    favourPrice: 2799,
                    tip: '自营'
                }
            ];

            if (action === 'refresh') {
                this.productList = [];
            }

            data.forEach(item => {
                this.productList.push(item);
            });
        }
    },
    onLoad() {
        this.loadData();
        setTimeout(()=> {
            this.renderImage = true;
        }, 300);
    },
    onPullDownRefresh() {
        this.loadData('refresh');
        // 实际开发中通常是网络请求，加载完数据后就停止。这里仅做演示，加延迟为了体现出效果。
        setTimeout(() => {
            uni.stopPullDownRefresh();
        }, 2000);
    },
    onReachBottom() {
        this.loadData();
    }
};
</script>

<style>
	.scroll-Y {
		height: 300upx;
	}

	.scroll-view_H {
		white-space: nowrap;
		width: 100%;
	}

	.scroll-view-item {
		height: 300upx;
		line-height: 300upx;
		text-align: center;
		font-size: 36upx;
	}

	.scroll-view-item_H {
		display: inline-block;
		width: 100%;
		height: 300upx;
		line-height: 300upx;
		text-align: center;
		font-size: 36upx;
	}
</style>
