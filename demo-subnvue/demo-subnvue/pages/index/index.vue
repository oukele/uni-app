<template>
	<view class="container">
		<view style="background-color: #0A98D5;
					 text-align: center;
					 line-height: 600rpx;
					 height: 600rpx;
					 margin-bottom: 20rpx;">
			Hello,word - {{ childParams }}
		</view>
		<button @click="openWindows('one')">点击打开子窗体1</button>
		<button @click="openWindows('two')">点击打开子窗体2</button>
		<button @click="openWindows('three')">点击打开子窗体3</button>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
				childParams: '(⊙o⊙)…'
			}
		},
		onLoad() {
			const vm = this;
			// 接收信息的页面(子窗体向父窗体传递参数)
			uni.$on('hello-popup', (data) => {
				switch( data.type ){
					case '1':
						vm.childParams = data.param;
					break;
					case '2':
						vm.childParams = data.param;
					break;
					case '3':
						vm.childParams = data.param;
					break;
					// .... 
				}
			});
			
		},
		methods: {
			openWindows(param) {
				
				let content = '';
				if( param == 'one' ){
					content = '啦啦'
				}else if( param == 'two' ){
					content = '德玛'
				}else if( param == 'three' ){
					content = '西亚'
				}else{
					content = '(⊙o⊙)…'
				}
				
				// 缩写法
				//uni.getSubNVueById('popup').show();
				
				// 对子窗体添加一些自定义的配置
				// 通过 ID 获取 subNVues 原生子窗体的实例
				const subNVue = uni.getSubNVueById('popup');
				
				// 向子窗体传递参数
				uni.$emit('hello-popup',{
					type: param,
					content: content
				})
				
				// 1:子窗体从顶部进入（动画效果）, 2:显示原生子窗体的动画持续时间
				subNVue.show('slide-out-top',250);
			}
		}
	}
</script>

<style>
	.container {
		padding: 20px;
		font-size: 14px;
		line-height: 24px;
	}
</style>
