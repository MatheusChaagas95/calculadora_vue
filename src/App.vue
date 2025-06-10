<script setup>
import { ref, computed } from 'vue'
import CalcInputs from './components/CalcInputs.vue'
import CalcButtons from './components/CalcButtons.vue'
import CalcDisplay from './components/CalcDisplay.vue'

const num1 = ref('')
const num2 = ref('')
const operation = ref('+')
const activeField = ref('num1')  //O ref é uma função do Vue que cria uma referência reativa a um valor. Isso significa que, se o valor mudar, o Vue vai reagir a essa mudança e atualizar a interface automaticamente (se necessário).
//Você está criando uma variável reativa chamada activeField, que começa com o valor 'num1'.
// Provavelmente, isso está sendo usado para controlar qual campo está ativo (por exemplo, em um formulário com dois campos, num1 e num2).
// Quando o usuário interage com um dos campos, você pode atualizar activeField.value para refletir o novo campo ativo.

const result = computed(() => { // Está criando uma constante reativa chamada result.
	//O valor de result será automaticamente calculado sempre que num1, num2 ou operation mudarem
	const a = parseFloat(num1.value) //Está convertendo os valores reativos num1.value e num2.value de string para número com parseFloat.
	const b = parseFloat(num2.value)
	if (isNaN(a) || isNaN(b)) return '' //Se a ou b não forem números válidos (por exemplo, se o campo estiver vazio), retorna uma string vazia.
	//Isso evita erros na hora de calcular.
	switch (operation.value) {  //Verifica o valor da operação atual (+, -, *, /), que também é uma variável reativa (operation deve ter sido criada com ref()).
		case '+': return a + b //Faz o cálculo matemático com base na operação selecionada , no caso soma.
		case '-': return a - b //Faz o cálculo matemático com base na operação selecionada, no caso subtração.
		case '*': return a * b //Faz o cálculo matemático com base na operação selecionada , no caso multiplicação.
		case '/': return b !== 0 ? a / b : 'Erro: divisão por zero' //Se for divisão (/) e b for 0, retorna uma mensagem de erro para evitar divisão por zero.
		default: return 'Operação inválida' //Se o símbolo da operação for diferente dos previstos, retorna uma mensagem de erro.
	}
})

function append(digit) {
	if (activeField.value === 'num1') { //Quando você usa ref, o valor real fica dentro de uma propriedade .value
		num1.value += digit // "Quando o campo ativo for o num1, adicione o dígito a num1.
	} else {
		num2.value += digit //Caso contrário, adicione a num2."
	}
}

// activeField: é uma ref que guarda o nome do campo atualmente ativo ('num1' ou 'num2').
// num1 e num2: também são refs e guardam os valores dos campos numéricos.
// digit: provavelmente é uma string com um número, como '1', '5' etc., que está sendo "digitado" pelo usuário (como num botão de calculadora).

function clearAll() {  	// Essa função ela reseta sua calculadora para o estado inicial.
	num1.value = ''   	//num1.value = '' → limpa o primeiro número
	num2.value = '' 	//num2.value = '' → limpa o segundo número
	operation.value = '+' //operation.value = '+' → define a operação como adição por padrão
	activeField.value = 'num1' //activeField.value = 'num1' → define que o primeiro campo (num1) está ativo para começar a digitar
}
</script>

<template>
	<div class="container">
		<div class="calc-wrapper">
			<h1>Calculadora Aritmética</h1>
			<CalcInputs v-model:num1="num1" v-model:num2="num2" v-model:operation="operation" :activeField="activeField"
				@update:activeField="val => activeField = val" />
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
