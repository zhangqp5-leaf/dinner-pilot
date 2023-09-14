<template>
	<view class="content">
    <view
      v-for="info in infoList"
      :key="info.title"
      class="pilot-info"
      @click="() => goDetail(info)"
    >{{ info.title }}</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
        infoList: [
          {
            title: '菜单',
            url: '../menu/index',
          },
          {
            title: '计算',
            url: '../calculate/index',
          },
        ],
			};
		},
		onLoad() {
      
		},
		methods: {
      goDetail(info) {
        uni.navigateTo({
          url: info.url,
        });
      },
		},
	};
</script>

<style>
	.content {
		display: flex;
		flex-direction: column;
    gap: 24px;
    /* width: 100%; */
    /* background-color: #eee; */
    padding: 24px 24px;
	}
  .pilot-info {
    height: 50vw;
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: rgb(250, 235, 215, 0.7);
    border-radius: 8%;
    font-size: x-large;
    /* color: bisque; */
    filter: blur(5);
  }

</style>
