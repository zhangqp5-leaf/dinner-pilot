<template>
	<view class="content">
    <view class="fix-title">
      <input
        class="uni-input"
        confirm-type="search"
        @input="changeInputValue"
        placeholder="请输入菜名搜索"
      />
      <view class="tabs">
        <view
          v-for="tab in tabOptions"
          :key="tab.value"
          class="tab"
          :class="activeKey === tab.value ? 'active-tab' : ''"
          @click="() => changeTab(tab.value)"
        >
          {{ tab.label }}
        </view>
      </view>
    </view>
    <view
      v-for="item in list"
      class="list-item"
      @click="() => showMethod(item)"
    >
      {{ item.dishName }}
    </view>
    <view>
			<uni-popup ref="bottomPopup" background-color="#fff">
				<view class="popup-content">
          <view><img :src="selectedDish.url" alt="" style="width: 100%;"></view>
          <view class="popup-title">{{ selectedDish.dishName }}</view>
          <view>
            <text :style="{fontWeight: 600}">食材：</text>
            {{ selectedDish.ingredients }}
          </view>
          <view
            v-for="step in selectedDish.steps"
            :key="step"
          >
            <uni-icons type="forward" size="14" color="pink"></uni-icons>
            {{ step }}
          </view>
        </view>
			</uni-popup>
		</view>
	</view>
</template>

<script>
  import {dishList} from '../../utils/const';
	export default {
		data() {
			return {
        list: [],
        tabOptions: [
          {
            value: 'all',
            label: '全部',
          },
          {
            value: '1',
            label: '肉类',
          },
          {
            value: '2',
            label: '素菜',
          },
          {
            value: '3',
            label: '主食',
          },
        ],
        activeKey: 'all',
        inputValue: '',
        selectedDish: {},
			};
		},
		onLoad() {
      this.list = dishList;
		},
		methods: {
      showMethod(item) {
        console.log(item.steps);
        this.selectedDish = item;
        this.$refs.bottomPopup.open('bottom');
      },
      changeInputValue(e) {
        this.inputValue = e.detail.value;
        this.list = dishList.filter(i => {
          if (this.activeKey === 'all') {
            return true;
          } else {
            return i.type === this.activeKey;
          }
        }).filter(i => i.dishName.includes(this.inputValue));
      },
      changeTab(val) {
        this.activeKey = val;
        if (val === 'all') {
          this.list = dishList.filter(i => i.dishName.includes(this.inputValue));
        } else {
          this.list = dishList.filter(i => i.type === val).filter(i => i.dishName.includes(this.inputValue));
        }
      },
		},
	};
</script>

<style>
	.content {
		display: flex;
		flex-direction: column;
    gap: 12px;
    width: 100%;
    background-color: #eee;
	}

  .fix-title {
    display: flex;
		flex-direction: column;
    gap: 12px;
    width: 100%;
    position: sticky;
    top: 44px;
    background-color: #eee;
  }

  .uni-input {
    padding: 8px 16px;
    margin: 8px 8px 0 8px;
    background-color: #fff;
    border-radius: 8px;
  }

  .tabs {
    display: flex;
    background-color: #fff;
  }
  .tab {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 25%;
    height: 42px;
  }
  .active-tab {
    background-color: pink;
  }

  .popup-content {
    max-height: 50vh;
    padding: 16px;
    display: flex;
    flex-direction: column;
    gap: 16px;
    overflow: auto;
  }
  .popup-title {
    font-size: 18px;
    font-weight: 700;
  }

  .list-item {
    padding: 12px 16px;
    cursor: pointer;
    background-color: #fff;
  }

	.logo {
		height: 200rpx;
		width: 200rpx;
		margin-top: 200rpx;
		margin-left: auto;
		margin-right: auto;
		margin-bottom: 50rpx;
	}

	.text-area {
		display: flex;
		justify-content: center;
	}

	.title {
		font-size: 36rpx;
		color: #8f8f94;
	}
</style>
