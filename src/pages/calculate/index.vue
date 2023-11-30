<template>
	<view>
		<form>
			<view class="form-title">收入</view>
			<view class="form-item">
				<view class="form-item-left">招商银行：</view>
				<input class="uni-input form-item-right" v-model="income.chinaMerchantsBank" placeholder="输入" />
			</view>
			<view class="form-item">
				<view class="form-item-left">兴业银行：</view>
				<input class="uni-input form-item-right" v-model="income.industrialBankOfChina" placeholder="输入" />
			</view>
			<view class="form-item">
				<view class="form-item-left">建设银行：</view>
				<input class="uni-input form-item-right" v-model="income.constructionBank" placeholder="输入" />
			</view>
			<view class="form-item">
				<view class="form-item-left">基金：</view>
				<input class="uni-input form-item-right" v-model="income.fund" placeholder="输入" />
			</view>
			<view class="form-item">
				<view class="form-item-left">现金：</view>
				<input class="uni-input form-item-right" v-model="income.cash" placeholder="输入" />
			</view>
			<view class="form-item">
				<view class="form-item-left">借款：</view>
				<input class="uni-input form-item-right" v-model="income.borrowMoney" placeholder="输入" />
			</view>
			<view class="form-item">
				<view class="form-item-plural-left">工资：</view>
				<input class="uni-input form-item-plural-middle" v-model="income.salary.salary" placeholder="输入" />
				&nbsp;×&nbsp;
				<input class="uni-input form-item-plural-right" v-model="income.salary.salaryCount" placeholder="输入" />
			</view>
			<view class="form-item">
				<view class="form-item-plural-left">公积金：</view>
				<input class="uni-input form-item-plural-middle" v-model="income.publicReserveFund.publicReserveFund" placeholder="输入" />
				&nbsp;×&nbsp;
				<input class="uni-input form-item-plural-right" v-model="income.publicReserveFund.publicReserveFundCount" placeholder="输入" />
			</view>
			<view class="form-item">
				<view class="form-item-left">年终奖：</view>
				<input class="uni-input form-item-right" v-model="income.yearEndBonus" placeholder="输入" />
			</view>
			<view class="form-item">
				<view class="form-item-left">其他：</view>
				<input class="uni-input form-item-right" v-model="income.other" placeholder="输入" />
			</view>

			<view class="form-title">支出</view>
			<view class="form-item">
				<view class="form-item-plural-left">贷款：</view>
				<input class="uni-input form-item-plural-middle" v-model="outcome.loan.loan" placeholder="输入" />
				&nbsp;×&nbsp;
				<input class="uni-input form-item-plural-right" v-model="outcome.loan.loanCount" placeholder="输入" />
			</view>
			<view class="form-item">
				<view class="form-item-plural-left">生活费1：</view>
				<input class="uni-input form-item-plural-middle" v-model="outcome.livingExpenses1.livingExpenses1" placeholder="输入" />
				&nbsp;×&nbsp;
				<input class="uni-input form-item-plural-right" v-model="outcome.livingExpenses1.livingExpenses1Count" placeholder="输入" />
			</view>
			<view class="form-item">
				<view class="form-item-plural-left">生活费2：</view>
				<input class="uni-input form-item-plural-middle" v-model="outcome.livingExpenses2.livingExpenses2" placeholder="输入" />
				&nbsp;×&nbsp;
				<input class="uni-input form-item-plural-right" v-model="outcome.livingExpenses2.livingExpenses2Count" placeholder="输入" />
			</view>
			<view class="form-item">
				<view class="form-item-left">彩礼：</view>
				<input class="uni-input form-item-right" v-model="outcome.betrothalGifts" placeholder="输入" />
			</view>
			<view class="form-item">
				<view class="form-item-left">手镯：</view>
				<input class="uni-input form-item-right" v-model="outcome.bracelet" placeholder="输入" />
			</view>
			<view class="form-item">
				<view class="form-item-plural-left">房租：</view>
				<input class="uni-input form-item-plural-middle" v-model="outcome.rent.rent" placeholder="输入" />
				&nbsp;×&nbsp;
				<input class="uni-input form-item-plural-right" v-model="outcome.rent.rentCount" placeholder="输入" />
			</view>
			<view class="form-item">
				<view class="form-item-left">其他：</view>
				<input class="uni-input form-item-right" v-model="outcome.other" placeholder="输入" />
			</view>

			<view class="form-title">结果</view>
			<view class="form-item">
				<view class="form-item-left">收入：</view>
				<view class="form-item-right">{{ incomeSum }}</view>
			</view>
			<view class="form-item">
				<view class="form-item-left">支出：</view>
				<view class="form-item-right">{{ outcomeSum }}</view>
			</view>
			<view class="form-item">
				<view class="form-item-left">余额：</view>
				<view class="form-item-right">{{ unfilledVacancies }}</view>
			</view>

		</form>
		<button type="primary" class="bottom-button" @click="submit">计算</button>
	</view>
</template>

<script>
export default {
	data() {
		return {
			incomeSum: 0,
			outcomeSum: 0,
			unfilledVacancies: 0,
			income: {
				chinaMerchantsBank: '55549.37',
				industrialBankOfChina: '0',
				constructionBank: '82.88',
				fund: '0',
				cash: '0',
				borrowMoney: '15000',
				salary: {
					salary: '12000',
					salaryCount: '3',
				},
				publicReserveFund: {
					publicReserveFund: '9000',
					publicReserveFundCount: '0',
				},
				yearEndBonus: '14000',
        other: '1800',
			},
			outcome: {
				loan: {
					loan: '6954.06',
					loanCount: '2',
				},
				livingExpenses1: {
					livingExpenses1: '2000',
					livingExpenses1Count: '0',
				},
				livingExpenses2: {
					livingExpenses2: '2800',
					livingExpenses2Count: '2',
				},
				betrothalGifts: '78000',
				bracelet: '0',
				rent: {
					rent: '7650',
					rentCount: '1',
				},
        other: '0',
			},
		};
	},
	onLoad() {
		this.submit();
	},
	methods: {
		submit() {
			this.incomeSum = this.sum(this.income);
			this.outcomeSum = this.sum(this.outcome);
			this.unfilledVacancies = this.incomeSum - this.outcomeSum;
		},
		sum(obj) {
			let re = 0;
			for (const key in obj) {
				if (obj[key] instanceof Object) {
					re = re + this.transNumber(obj[key][Object.keys(obj[key])[0]]) * this.transNumber(obj[key][Object.keys(obj[key])[1]]);
				} else {
					re = re + this.transNumber(obj[key]);
				}
			}
			return re;
		},
		transNumber(val) {
			if (!val) {
				return 0;
			}
			if (typeof val === 'string') {
				return Number(val);
			}
			return val;
		},
	},
}
</script>

<style>
.form-title {
	display: flex;
	align-items: center;
	padding: 4px 24px;
	border-left: 4px solid #1890ff;
	font-size: 1.1rem;
	font-weight: 700;
}
.form-item {
	display: flex;
	align-items: center;
	height: 48px;
}
.form-item-left {
	flex: 0 0 100px;
	text-align: right;
}
.form-item-right {
	flex: 1 1 auto;
}
.form-item-plural-left {
	width: 100px;
	text-align: right;
}
.form-item-plural-middle {
	width: 150px;
}
.form-item-plural-right {
	flex: 1;
}
.bottom-button {
	position: sticky;
	bottom: 0;
	width: 100%;
}
</style>
