<template>
	<view class="deposit-container">
    <view class="deposit-item">
      <input class="uni-input form-item-right" v-model="oldVacancies" placeholder="输入" />
    </view>
    <view class="deposit-item">
      <picker mode="date" :value="date" :start="startDate" :end="endDate" @change="bindDateChange">
        <view class="uni-input">{{date}}</view>
      </picker>
    </view>
    <view class="deposit-item">
      {{ newVacancies }}
    </view>
  </view>
</template>

<script>
import { depositFormatMap } from '../../utils/const';
export default {
  data() {
    const currentDate = this.getDate({
      format: true
    })
    return {
      date: currentDate,
      oldVacancies: 0,
      newVacancies: 0,
    }
  },
  computed: {
    startDate() {
      return this.getDate('');
    },
    endDate() {
      return this.getDate('end');
    }
  },
  methods: {
    bindDateChange: function(e) {
      console.log(e.detail.value);
      this.date = e.detail.value;
      this.getResult(e.detail.value);
    },
    getResult(date) {
      const _currentDate = this.getDate('');
      const [ oldYear, oldMonth, oldDay ] = _currentDate.split('-');
      const [ newYear, newMonth, newDay ] = date.split('-');
      const totalMonth = ( newYear - oldYear ) * 12 + ( newMonth - oldMonth );
      let res = 0;
      if (totalMonth === 0) {
        // 计算同月
        for (const _day of Object.keys(depositFormatMap[newMonth])) {
          if (_day > oldDay && _day <= newDay) {
            res += depositFormatMap[newMonth][_day];
          }
        }
      } else if (totalMonth === 1) {
        // 计算隔月
        for (const _day of Object.keys(depositFormatMap[oldMonth])) {
          if (_day > oldDay) {
            res += depositFormatMap[oldMonth][_day];
          }
        }
        for (const _day of Object.keys(depositFormatMap[newMonth])) {
          if (_day <= newDay) {
            res += depositFormatMap[newMonth][_day];
          }
        }
      } else {
        // 计算隔月加整月
        for (const _day of Object.keys(depositFormatMap[oldMonth])) {
          if (_day > oldDay) {
            res += depositFormatMap[oldMonth][_day];
          }
        }
        for (const _day of Object.keys(depositFormatMap[newMonth])) {
          if (_day <= newDay) {
            res += depositFormatMap[newMonth][_day];
          }
        }
        const monthArr = [];
        for (let i = 1; i < totalMonth; i++) {
          const _month = +oldMonth + i;
          monthArr.push(_month > 9 ? _month : '0' + _month);
        }
        console.log(monthArr);
        while(monthArr.length >= 12) {
          res += this.getSumYear(depositFormatMap);
          monthArr.splice(-12);
        }
        for (const _month of monthArr) {
          let temp = _month;
          if (typeof temp === 'number' && temp > 12) {
            temp = '0' + temp % 12;
          }
          res += this.getObjSum(depositFormatMap[temp]);
        }
      }
      this.newVacancies = Number(this.oldVacancies) + res;
    },
    getObjSum(obj) {
      return Object.values(obj).reduce((a, b) => a + b, 0);
    },
    getSumYear(obj) {
      let re = 0;
      for (const month of Object.values(obj)) {
        re = re + Object.values(month).reduce((a, b) => a + b, 0)
      }
      return re;
    },
    getDate(type) {
      const date = new Date();
      let year = date.getFullYear();
      let month = date.getMonth() + 1;
      let day = date.getDate();

      if (type === 'start') {
        year = year - 60;
      } else if (type === 'end') {
        year = year + 20;
      }
      month = month > 9 ? month : '0' + month;
      day = day > 9 ? day : '0' + day;
      return `${year}-${month}-${day}`;
    }
  }
}
</script>

<style>
.deposit-container {
  display: flex;
  flex-direction: column;
  gap: 16px;
  background-color: #eee;
  width: 100%;
}
.deposit-item {
  background-color: #fff;
  padding: 8px 16px;
}
</style>
