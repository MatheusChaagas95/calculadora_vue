<script setup>
import { ref, computed } from 'vue'
import CalcInputs from './components/CalcInputs.vue'
import CalcButtons from './components/CalcButtons.vue'
import CalcDisplay from './components/CalcDisplay.vue'

const num1 = ref('')
const num2 = ref('')
const operation = ref('+')
const activeField = ref('num1')

const result = computed(() => {
	const a = parseFloat(num1.value)
	const b = parseFloat(num2.value)
	if (isNaN(a) || isNaN(b)) return ''
	switch (operation.value) {
		case '+': return a + b
		case '-': return a - b
		case '*': return a * b
		case '/': return b !== 0 ? a / b : 'Erro: divisão por zero'
		default: return 'Operação inválida'
	}
})

function append(digit) {
	if (activeField.value === 'num1') {
		num1.value += digit
	} else {
		num2.value += digit
	}
	}

	function clearAll() {
	num1.value = ''
	num2.value = ''
	operation.value = '+'
	activeField.value = 'num1'
	}
	</script>

	<template>
	<div class="container">
		<div class="calc-wrapper">
		<h1>Calculadora Aritmética</h1>
		<CalcInputs
			v-model:num1="num1"
			v-model:num2="num2"
			v-model:operation="operation"
			:activeField="activeField"
			@update:activeField="val => activeField = val"
		/>
		<CalcButtons @append="append" @clearAll="clearAll" />
		<CalcDisplay :result="result" />
		</div>
	</div>
</template>
<style scoped>
.container {
	max-width: 100%;
	padding: 20px;
	display: flex;
	justify-content: center;
	text-align: center;
}

.calc-wrapper {
	width: 300px;
	background: #1e1e1e;
	padding: 20px;
	border-radius: 20px;
	display: flex;
	flex-direction: column;
	align-items: center;
	box-shadow: 0 0 10px rgba(0, 0, 0, 0.4);
}

h1 {
	color: #fff;
	font-size: 22px;
	margin-bottom: 20px;
}

</style>
