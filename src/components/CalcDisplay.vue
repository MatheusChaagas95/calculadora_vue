<script setup>
defineProps({ result: [Number, String] })
</script>

<template>
	<div class="calc-display">
		{{ result !== '' ? result : 0 }}
	</div>
</template>
<style scoped>
.calc-display {
	background: #32CD32;
	color: #000;
	font-size: 32px;
	text-align: right;
	padding: 14px;
	width: 100%;
	border-radius: 12px;
	font-weight: bold;
}
</style>