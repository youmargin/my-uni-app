<template>
	<view>
		
		<!-- 顶部选项卡 -->
		<scroll-view scroll-x :scroll-into-view="scrollInto" scroll-with-animation
		class="scroll-row border-bottom border-light-secondary">
			<view v-for="(item,index) in tabBars" :key="index" 
			class="scroll-row-item px-3 py-2 font-md" :id="'tab'+index"
			:class="tabIndex === index?'text-main font-lg font-weight-bold':''"
			@click="changeTab(index)">{{item.name}}</view>
		</scroll-view>
		
		
		<!-- <block v-for="(item,index) in list" :key="index"> -->
			<!-- 列表样式 -->
			<!-- <common-list :item="item" :index="index" @follow="follow" @doSupport="doSupport"></common-list> -->
			<!-- 全局分割线 -->
			<!-- <divider></divider> -->
		<!-- </block> -->
		
	</view>
</template>

<script>
	import commonList from '@/components/common/common-list.vue';
	export default {
		components: {
			commonList
		},
		data() {
			return {
				// 顶部选项卡
				scrollInto:"",
				tabIndex:0,
				tabBars: [{
				    name: '关注',
				}, {
				    name: '推荐',
				}, {
				    name: '体育',
				}, {
				    name: '热点',
				}, {
				    name: '财经',
				}, {
				    name: '娱乐',
				}, {
				    name: '军事',
				}, {
				    name: '历史',
				}, {
				    name: '本地',
				}],
				list:[
					{
						username:"昵称",
						userpic:"/static/default.jpg",
						newstime:"2019-10-20 下午04:30",
						isFollow:false,
						title:"我是标题",
						titlepic:"/static/demo/datapic/11.jpg",
						support:{
							type:"support", // 顶
							support_count:1,
							unsupport_count:2
						},
						comment_count:2,
						share_num:2
					},
					{
						username:"昵称",
						userpic:"/static/default.jpg",
						newstime:"2019-10-20 下午04:30",
						isFollow:false,
						title:"我是标题",
						titlepic:"",
						support:{
							type:"unsupport", // 踩
							support_count:1,
							unsupport_count:2
						},
						comment_count:2,
						share_num:2
					},
					{
						username:"昵称",
						userpic:"/static/default.jpg",
						newstime:"2019-10-20 下午04:30",
						isFollow:false,
						title:"我是标题",
						titlepic:"",
						support:{
							type:"", // 未操作
							support_count:1,
							unsupport_count:2
						},
						comment_count:2,
						share_num:2
					}
				]
			}
		},
		onLoad() {

		},
		methods: {
			// 切换选项
			changeTab(index){
				if (this.tabIndex === index) {
					return;
				}
				this.tabIndex = index
				// 滚动到指定元素
				this.scrollInto = 'tab'+index
			},
			// 关注
			follow(e){
				this.list[e].isFollow = true
				uni.showToast({ title: '关注成功' })
			},
			// 顶踩操作
			doSupport(e){
				// 拿到当前对象
				let item = this.list[e.index]
				let msg = e.type === 'support' ? '顶' : '踩'
				// 之前没有操作过
				if (item.support.type === '') {
					item.support[e.type+'_count']++
				} else if (item.support.type ==='support' && e.type === 'unsupport') {
					// 顶 - 1
					item.support.support_count--;
					// 踩 + 1
					item.support.unsupport_count++;
				} else if(item.support.type ==='unsupport' && e.type === 'support'){ 					// 之前踩了
					// 顶 + 1
					item.support.support_count++;
					// 踩 - 1
					item.support.unsupport_count--;
				}
				item.support.type = e.type
				uni.showToast({ title: msg + '成功' });
			}
		}
	}
</script>

<style>
scroll-view [style*="overflow"]::-webkit-scrollbar {  
  display: none;  
} 
</style>
