<template>
    <view>
		<block v-for="(item,index) in list" :key="index">
        <common-list :item="item" :index="index" @follow="follow1"></common-list>
		<divider></divider>
		</block>

    </view>
</template>

<script>
	import commonList from '@/components/common/common-list'
    export default {
		components:{
			commonList
		},
        data() {
            return {
                list: [
                    {
                        username: "昵称",
                        userpic: "/static/default.jpg",
                        newstime: "2019-10-20 下午04:30",
                        isFollow: false,
                        title: "我是标题1",
                        titlepic: "/static/demo/datapic/11.jpg",
                        support: {
                            type: "support",
                            support_count: 1,
                            unsupport_count: 2
                        },
                        comment_count: 2,
                        share_num: 2
                    },
                    {
                        username: "昵称",
                        userpic: "/static/default.jpg",
                        newstime: "2019-10-20 下午04:30",
                        isFollow: false,
                        title: "我是标题2",
                        titlepic: "",
                        support: {
                            type: "support",
                            support_count: 1,
                            unsupport_count: 2
                        },
                        comment_count: 2,
                        share_num: 2
                    }
                ]
            }
        },
        onLoad() {

        },
        methods: {
			// 关注
			follow1(e){
				console.log(e);
				this.list[e].isFollow = true
				uni.showToast({ title: '关注成功' })
			}
		}
    }
</script>

<style>

</style>
