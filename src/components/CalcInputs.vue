<script setup>
const props = defineProps({
	num1: String,
	num2: String,
	operation: String,
	activeField: String
})

const emit = defineEmits(['update:num1', 'update:num2', 'update:operation', 'update:activeField'])

function focus(field) {
	emit('update:activeField', field)
}
</script>

<template>
	<div class="calc-inputs">
		<input
		class="input-btn"
		:class="{ active: props.activeField === 'num1' }"
		:value="props.num1"
		@focus="focus('num1')"
		@input="e => emit('update:num1', e.target.value)"
		placeholder="Num 1"
		/>
		<select
		class="input-btn"
		:value="props.operation"
		@change="e => emit('update:operation', e.target.value)"
		>
		<option value="+">+</option>
		<option value="-">-</option>
		<option value="*">*</option>
		<option value="/">/</option>
		</select>
		<input
		class="input-btn"
		:class="{ active: props.activeField === 'num2' }"
		:value="props.num2"
		@focus="focus('num2')"
		@input="e => emit('update:num2', e.target.value)"
		placeholder="Num 2"
		/>
	</div>
</template>
<style scoped>
.input-btn {
	font-size: 16px;
	padding: 12px;
	border: none;
	margin: 4px;
	border-radius: 6px;
	background: #eee;
	box-sizing: border-box;
	text-align: center;
	font-weight: bold;
}

select.input-btn {
	cursor: pointer;
}

</style>
