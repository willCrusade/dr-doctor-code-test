<template>
	<div
		class="form-input input-radio"
	>
		<label :for="value">
			<input
				:id="value"
				type="radio"
				:name="name"
				:required="required"
				:aria-required="required"
				:value="value"
				:checked="checked"
				:class="{
		            valid: isValid,
		            invalid: isInvalid
		        }"
				@input="$emit('update:modelValue', value)"
			/>

			<div class="radio-info">
			<span class="radio-label">
				{{ label }}
			</span>

				<span class="radio-value">
				{{ value }}
			</span>
			</div>
		</label>



	</div>
</template>

<script>
export default {
	name: "RadioInput",
	props: {
		name: {
			type: String,
			required: true
		},
		required: {
			type: Boolean,
		},
		label: {
			type: String
		},
		checked: {
			type: Boolean,
			required: true
		},
		value: {
			type: String
		},
		valid: {
			type: Boolean,
			default: null
		}
	},
	emits: ['update:modelValue'],
	computed: {
		isValid() {
			return this.valid !== null && this.valid
		},
		isInvalid() {
			return this.valid !== null && !this.valid
		}
	}
}
</script>

<style lang="scss" scoped>
.input-radio {
	display: flex;
	background: rgba($color-primary, .1);
	border: 2px solid $color-primary;
	border-radius: 5px;
	padding: .3rem .5rem .5rem;
	cursor: pointer;

	// hacky for code test time limitations,  assuming 3
	flex-basis: 33%;
	margin-right: .4rem;

	input {
		margin-bottom: 0;
		margin-right: .4rem;
	}

	label {
		display: flex;
		align-items: center;
		margin: 0;
	}

	.radio-info {
		display: flex;
		flex-direction: column;
		color: $color-primary;

		.radio-label {
			font-weight: 400;
			font-size: .9rem;
		}

		.radio-value {
			font-weight: 600;
			font-size: .7rem;
		}
	}
}

</style>
