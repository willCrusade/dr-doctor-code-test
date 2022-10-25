<template>
	<form @submit.prevent>
		<slot name="description"></slot>

		<slot name="fields"></slot>

		<slot name="submit"></slot>
	</form>
</template>
<script>

export default {
	name: 'FormHandler',
	props: {
		formData: {
			type: Object,
		},
	},
	data() {
		return {

		}
	},
}

</script>
<style scoped lang="scss">

</style>