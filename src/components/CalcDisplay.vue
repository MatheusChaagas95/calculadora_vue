<script setup>
defineProps({ result: [Number, String] }) //Define que este componente espera receber uma propriedade chamada result.
//Essa result pode ser um número (ex: 42) ou uma string (ex: 'Erro: divisão por zero').
//Isso significa que o componente pai vai passar o valor de result para esse componente filho.
// Mostra o conteúdo da result na tela.
// Mas com uma verificação:
// result !== '' ? result : 0
// Se result não for uma string vazia, ele mostra o valor de result.
// Caso contrário, mostra 0 (o valor padrão no visor)
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