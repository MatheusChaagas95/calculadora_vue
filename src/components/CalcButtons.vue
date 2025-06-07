<script setup>
const emit = defineEmits(['append', 'clearAll'])
function press(digit) {
	emit('append', digit)
}
</script>
<template>
	<div class="input-btn-buttons">
		<button @click="press('7')">7</button>
		<button @click="press('8')">8</button>
		<button @click="press('9')">9</button>
		<button @click="press('4')">4</button>
		<button @click="press('5')">5</button>
		<button @click="press('6')">6</button>
		<button @click="press('1')">1</button>
		<button @click="press('2')">2</button>
		<button @click="press('3')">3</button>
		<button @click="emit('clearAll')">C</button>
		<button class="zero-btn" @click="press('0')">0</button>
	</div>
</template>
<style scoped>
.calc-inputs {
	display: grid;
	grid-template-columns: repeat(3, 1fr);
	gap: 10px;
	width: 100%;
	margin-bottom: 15px;
}

.input-btn-buttons {
	display: grid;
	grid-template-columns: repeat(3, 1fr);
	gap: 10px;
	width: 100%;
	justify-content: center;
	margin-bottom: 20px;
	margin-top: 20px;
}

.input-btn-buttons button {
	font-size: 22px;
	padding: 16px;
	border: none;
	border-radius: 8px;
	background-color: #ddd;
	cursor: pointer;
	font-weight: bold;
	transition: background-color 0.2s;
}

.input-btn-buttons button:hover {
	background-color: #bbb;
}

.zero-btn {
	grid-column: span 2;
}
</style>