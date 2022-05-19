
<script>
export default {
	inheritAttrs: false,
	props: {
		label: {
			type: String,
			required: true,
		},
	},
	emits: ['click'],
};
</script>

<template>
	<button
		class="btn btn-danger"
		@click="$emit('click', $event)"
        type="submit">
		{{ label }}
	</button>
</template>

