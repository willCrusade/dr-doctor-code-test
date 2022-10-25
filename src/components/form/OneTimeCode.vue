<template>
	<div class="form-input input-one-time-code flex">
		
		<input
			type="text"
			class="border rounded"
			maxlength="1"
			:disabled="isLoading"
			v-model="code[0]"
			@input="next"
		/>

		<input
			type="text"
			class="border rounded"
			maxlength="1"
			:disabled="isLoading"
			v-model="code[1]"
			@input="next"
		/>

		<input
			type="text"
			class="border rounded"
			maxlength="1"
			:disabled="isLoading"
			v-model="code[2]"
			@input="next"
		/>

		<input
			type="text"
			class="border rounded"
			maxlength="1"
			:disabled="isLoading"
			v-model="code[3]"
		/>
	</div>

</template>

<script>
export default {
	name: "TextInput",
	data() {
		return {
			code: [],
			isLoading: false,
		}
	},
	methods: {
		onSuccess() {
			alert('code accepted ( no time to do UI )')
		},
		onError() {
			alert('code rejected ( no time to do UI )')
			this.code = [];
		},
		next(e) {
			e.target.nextSibling.focus()
		},
		handleCode() {
			this.isLoading = true;

			setTimeout(() => {
				if(this.code.join('') === '0000'){
					this.onSuccess();
				} else {
					this.onError()
				}
				this.isLoading = false;
			}, 500)
		}
	},
	watch: {
		code: {
			deep: true,

			handler() {
				if(this.code.length === 4) {
					this.handleCode();
				}
			}
		},
	},
}
</script>

<style lang="scss" scoped>
.input-one-time-code {
	margin-top: 2rem;

	input {
		width: 40px;
		margin-right: .4rem;

	}
}
</style>
