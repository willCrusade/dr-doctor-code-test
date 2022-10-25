<template>
	<div
		class="form-input input-text"
		:class="{'has-description': description }"
	>
		<label
			v-if="label"
			class="block font-bold"
		>
			{{ label }}
			<span v-if="required" class="required">*</span>
		</label>

		<span
			v-if="description"
			class="input-description block text-sm mb-2"
		>
            {{ description }}
        </span>

		<input
			type="date"
			:min="min"
			:name="name"
			class="border rounded w-full px-4 py-2"
			:disabled="disabled"
			:placeholder="placeholder"
			:required="required"
			:aria-required="required"
			:class="{
                valid: isValid,
                invalid: isInvalid
            }"
			@input="$emit('update:modelValue', $event.target.value)"
		/>
	</div>

</template>

<script>
export default {
	name: "DateInput",
	props: {
		value: {
			type: [String, Number],
			default: ''
		},
		name: {
			type: String,
			required: true
		},
		min: {
			type: Number,
			default: 0
		},
		placeholder: {
			type: String,
			default: ''
		},
		label: {
			type: String,
			default: ''
		},
		description: {
			type: String,
			default: ''
		},
		required: {
			type: Boolean,
		},
		disabled: {
			type: Boolean,
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
.input-description {
	color: $color-grey;
}

input {
	border-color: $color-grey;
}
.valid {
	border-color: $color-success;
}

.invalid {
	border-color: $color-error;
}
</style>
