<template>
	<div class="datetime-picker" :style="{width: width}">
		<input 
			type="text" 
			:style="styleObj"
			:readonly="readonly"
			v-model="showValue"
			@click="show = !show">
		<div class="picker-wrap" v-show="show">
			<table class="date-picker">
				<thead>
					<tr class="date-picker">
						<th colspan="4">
							<span class="btn-prev" @click="yearClick(-1)">&lt;</span>
							<span class="show-year">{{now.getFullYear()}}</span>
							<span class="btn-next" @click="yearClick(1)">&gt;</span>
						</th>
						<th colspan="3">
							<span class="btn-prev" @click="monthClick(-1)">&lt;</span>
							<span class="show-month">{{months[now.getMonth()]}}</span>
							<span class="btn-next" @click="monthClick(1)">&gt;</span>
						</th>
					</tr>
					<tr class="date-days">
						<th v-for="day in days">{{ day }}</th>
					</tr>
				</thead>
				<tbody>
					<tr v-for="i in 6">
						<td v-for="j in 7"
							:class="date[i * 7 + j] && date[i * 7 + j].status"
							:date="date[i * 7 + j].date"
							@click="pickDate(i * 7 + j)">{{date[i * 7 + j] && date[i * 7 + j].text}}</td>
					</tr>
				</tbody>
			</table>
		</div>
	</div>
</template>

<script>
	export default {
		props: {
			width: {
				type: String,
				default: '238px'
			},
			readonly: {
				type: String,
				default: ''
			},
			format: {
				type: String,
				default: 'YYYY-MM-DD'
			},
			styleObj: {
				type: Object,
				default: null
			}
		},
		data () {
			return {
				show: false,
				showValue: '',
				days: ['Su', 'Mo', 'Tu', 'We', 'Th', 'Fr', 'Sa'],
				months: ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec'],
				date: [],
				now: new Date()
			}
		},
		watch: {
			now () {
				this.update();
			},
			show () {
				this.update();
			}
		},
		methods: {
			close () {
				this.show = false;
			},
			update () {
				let arr = [];
				let time = new Date(this.now);
				time.setMonth(time.getMonth(), 1);
			}
		}
	}
</script>

<style>
	
</style>