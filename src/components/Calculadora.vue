<template>
<div class="calculadora">
	<div class="display"> {{valorCorrente || '0'}} </div>
	<div @click="limpar" class="botao"> C </div>
	<div @click="sinal" class="botao"> +/- </div>
	<div @click="porcentagem" class="botao"> % </div>
	<div @click="dividir" class="botao operadores"> ÷ </div>
	<div @click="juntarNumeros('7')" class="botao"> 7 </div>
	<div @click="juntarNumeros('8')" class="botao"> 8 </div>
	<div @click="juntarNumeros('9')" class="botao"> 9 </div>
	<div @click="multiplicar" class="botao operadores"> x </div>
	<div @click="juntarNumeros('4')" class="botao"> 4 </div>
	<div @click="juntarNumeros('5')" class="botao"> 5 </div>
	<div @click="juntarNumeros('6')" class="botao"> 6 </div>
	<div @click="subtrair" class="botao operadores"> - </div>
	<div @click="juntarNumeros('1')" class="botao"> 1 </div>
	<div @click="juntarNumeros('2')" class="botao"> 2 </div>
	<div @click="juntarNumeros('3')" class="botao"> 3 </div>
	<div @click="somar" class="botao operadores"> + </div>
	<div @click="juntarNumeros('0')" class="botao zero"> 0 </div>
	<div @click="ponto" class="botao"> . </div>
	<div @click="resultado" class="botao"> = </div>
</div>
</template>

<script>
	export default {
		data() {
			return {
				valorCorrente: '',
				numeroAnterior: null,
				operador: null,
				operadorClicado: false,
			};
		},
		methods: {
			limpar() {
				this.valorCorrente = '';
				console.log("FOI")
			},

			sinal() {
				this.valorCorrente = this.valorCorrente.charAt(0) === '-'
				? this.valorCorrente.slice(1)
				: `-${this.valorCorrente}`;
			},

			juntarNumeros(numero) {
				if (this.operadorClicado) {
					this.valorCorrente = '';
					this.operadorClicado = false;
				}

				this.valorCorrente = `${this.valorCorrente}${numero}`;
			},

			porcentagem() {
				this.valorCorrente = `${parseFloat(this.valorCorrente) / 100}`;
			},
		
			ponto() {
				if (this.valorCorrente.indexOf('.') === -1) {
					this.juntarNumeros('.');
				}
			},

			setarValor() {
				this.numeroAnterior = this.valorCorrente;
				this.operadorClicado = true;
			},
			
			resultado() {
				this.valorCorrente = `${this.operador(
					parseFloat(this.numeroAnterior),
					parseFloat(this.valorCorrente),
				)}`;
      			this.numeroAnterior = null;
			},

			dividir() {
				this.operador = (num1, num2) => num1 / num2;
      			this.setarValor();
			},

			multiplicar() {
				this.operador = (num1, num2) => num1 * num2;
				this.setarValor();
			},

			subtrair() {
				this.operador = (num1, num2) => num1 - num2;
				this.setarValor();
			},

			somar() {
				this.operador = (num1, num2) => num1 + num2;
				this.setarValor();
			},
		}
	};
</script>

<style scoped>
	.calculadora {
		margin: 0 auto;
		width: 350px;
		font-size: 40px;
		display: grid;
		grid-template-columns: repeat(4, 1fr);
		grid-auto-rows: minmax(50px, auto);
	}
	.display {
		grid-column: 1 / 5;
		background-color: #333;
		color: white;
	}
	.zero {
		grid-column: 1 / 3;
	}
	.botao {
		background-color: #f2f2f2;
		border: 1px solid #999;
		cursor: pointer;
	}
	.operadores {
		background-color: orange;
		color: white;
	}
</style>