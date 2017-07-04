<template>
	<div class="reg-form">
		<div class="g-form">
			<div class="g-form-line" v-for="(formLine, index) in formData">
				<span class="g-form-label">
					{{ formLine.label }}
				</span>
				<div class="g-form-input">
					<input type="text" name="formLine.name" :placeholder="formLine.holder" v-model="formLine.value" v-if="index === 0">
					<input type="password" name="formLine.name" :placeholder="formLine.holder" v-model="formLine.value" v-else>
				</div>
				<span class="g-form-error">
					{{ formLine.error }}
				</span>
			</div>
			<div class="g-form-line">
				<div class="g-form-btn">
					<a class="button" @click="onRegister">注册</a>
				</div>
			</div>
			<p>{{ errorText }}</p>
		</div>
	</div>
</template>

<script>
	export default {
		data () {
			return {
				formData: [
					{	
						label: '用户名',
						name: 'user',
						holder: '请输入用户名',
						value: '',
						error: ''
					},
					{	
						label: '密码',
						name: 'pwd',
						holder: '请输入密码',
						value: '',
						error: ''
					},
					{
						label: '确认密码',
						name: 'confirm_pwd',
						holder: '请确认密码 ',
						value: '',
						error: ''
					}
				],
				errorText: ''
			}
		},
		watch: {
			formData:{
				handler:(val,oldVal) => {
					if (!/@/g.test(val[0].value)) {
						val[0].error = '不包含@'
					} else {
						val[0].error = ''
					}
					if(val[1].value != '' && !/^\w{1,6}$/g.test(val[1].value)) {
						val[1].error = '密码不是1-6位';
					} else {
						val[1].error = '';
					}
					if(val[2].value != '' && val[2].value !== val[1].value) {
						val[2].error = '密码输入不一致';
					} else {
						val[2].error = '';
					}
				},
				deep: true
			}
		},
		methods: {
			onRegister () {
				if(this.formData[0].error !== '' || this.formData[1].error !== '' || this.formData[2].error !== '') {
					this.errorText = '部分选项未通过'
				} else {
					this.errorText = '';
					alert('注册成功');
					this.$emit('has-reg');
				}
			}
		}
	}
</script>

<style>
	
</style>