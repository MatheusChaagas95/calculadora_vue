<script setup>
const props = defineProps({
	num1: String,
	num2: String,
	operation: String,
	activeField: String
})
//defineEmits() é uma função do Vue 3 (Composition API) usada dentro de <script setup> para declarar os eventos que o componente pode emitir para o componente pai.
//Quando você usa v-model com uma prop personalizada, o Vue espera um evento chamado update:<nome> para atualizar o valor no pai.

const emit = defineEmits(['update:num1', 'update:num2', 'update:operation', 'update:activeField']) //Este componente pode emitir eventos para atualizar as seguintes props no pai: num1, num2, operation, e activeField.

function focus(field) {
	emit('update:activeField', field)
}

// Recebe um parâmetro field — que será 'num1' ou 'num2', por exemplo.
// Dispara (emite) um evento chamado 'update:activeField' para o componente pai.
// Envia o valor de field como o novo valor de activeField no componente pai.
//Essa função é usada para mudar o campo ativo da calculadora
// ou seja, dizer se o usuário está digitando no primeiro número (num1) ou no segundo (num2).
//Mas como o campo ativo (activeField) é controlado pelo componente pai,
// o componente filho não altera diretamente — ele emite um evento e deixa o pai atualizar.

//:value="props.num1" → mostra o valor de num1 (passado pelo pai como prop).
// @input → quando o usuário digita, emite o evento update:num1 com o novo valor, para atualizar o estado no pai.
// @focus="focus('num1')" → quando o input é selecionado, ativa o campo num1 chamando a função focus, que emite update:activeField.
//:class="{ active: props.activeField === 'num1' }" → se o campo ativo for num1, adiciona a classe active para destacar o input visualmente.

//:value="props.operation" → mostra qual operação está selecionada.
//@change → quando o usuário muda a operação, emite update:operation com o novo valor.
//Isso atualiza o estado da operação no componente pai.

//        Elemento	      |      	      Função                        |    Emite evento     |
//   Input num1	          |  Digitar primeiro número	                |  update:num1        |
//   Input num2  	      |  Digitar segundo número	                    |  update:num2        |
//   Select operação	  |  Escolher operação matemática	            |  update:operation   |
//   Focus nos inputs	  |  Define campo ativo (activeField)	        |  update:activeField |
//   Class active	      |  Adiciona destaque visual ao input ativo	|        —            |

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
