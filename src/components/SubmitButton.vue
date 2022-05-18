
<script>
export default {
	inheritAttrs: false,
	props: {
		label: {
			type: String,
			required: true,
		},

		theme: {
			type: String,
			required: false,
			default: 'prime',
			validator(value) {
				return ['prime', 'secondary'].includes(value);
			},
		},
	},
	emits: ['click'],
};
</script>

<template>
	<button
		class="submit-button btn btn-danger"
		:class="theme"
		@click="$emit('click', $event)"
        type="submit">
		{{ label }}
	</button>
</template>

