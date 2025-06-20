<script setup>
import { ref } from 'vue';

const inputStr = ref('');

function limpiarPantalla() {
  inputStr.value = '';
}

function actualizarPantalla(valor) {    // Actualiza la pantalla con el valor del boton presionado
  inputStr.value += valor;
}

function calcularResultado() {
  try {

    //porcentaje 
    if (inputStr.value.includes('%')) {
      const partes = inputStr.value.split('%');
      const porcentaje = parseFloat(partes[0]) / 100;
      const numero = parseFloat(partes[1]);
      inputStr.value = numero * porcentaje;
      return;
    }
    // Reemplazar el símbolo de división por el operador correcto
    const inputLimpio = inputStr.value.replace(/÷/g, '/');
    // Evaluar la expresión matemática
    const resultado = eval(inputLimpio);
    // Actualizar la pantalla con el resultado
    inputStr.value = resultado;
  } catch (error) {
    // Se mostrara mensaje de error si la expresión es inválida o hay error en el calculo 
    console.error('Error al calcular el resultado:', error);
    inputStr.value = 'Error';
  }
}

function borrarUltimoCaracter() {
  inputStr.value = inputStr.value.slice(0, -1);
}


function signoNegativo() {
  // Si la pantalla está vacía, se asigna un signo negativo por defecto
  if (inputStr.value === '') {
    inputStr.value = '-';
    return;
  }
  // Cambia el signo del número actual
  if (inputStr.value.startsWith('-')) {
    inputStr.value = inputStr.value.slice(1);
  } else {
    inputStr.value = '-' + inputStr.value;
  }
  //Asignar negativo al ultimo número ingresado
  const partes = inputStr.value.split(/([+\-*/])/);
  const ultimoNumero = partes[partes.length - 1];
  if (!isNaN(ultimoNumero)) {
    partes[partes.length - 1] = '-' + ultimoNumero;
    inputStr.value = partes.join('');
  }
}
</script>

<template>
<img class="nubes-horizonte" src="/src/assets/Ocean_8/2.png">
<img class="nubes-horizonte2" src="/src/assets/Ocean_8/3.png">
<img class="nubes-capas" src="/src/assets/Ocean_8/4.png">
<img class="nubes-capas1" src="/src/assets/nubes/2.67.png">
<img class="nubes-capas2" src="/src/assets/nubes/2.9.png">
<img class="nubes-capas3" src="/src/assets/nubes/2.1.png">
<section class="flex-container">
  <div class="general-screen">
    <h1 class="screen-numbers">{{ inputStr }}</h1>
  </div>
  <div class="botones">
    <button @click="limpiarPantalla" class="button-special">C</button>
    <button @click="signoNegativo" class="button-operador">+/-</button>
    <button @click="()=> actualizarPantalla('%')" class="button-operador">%</button>
    <button @click="()=> actualizarPantalla('÷')" class="button-operador">/</button>
    <button @click="()=> actualizarPantalla('7')" class="button">7</button>
    <button @click="()=> actualizarPantalla('8')" class="button">8</button>
    <button @click="()=> actualizarPantalla('9')" class="button">9</button>
    <button @click="()=> actualizarPantalla('*')" class="button-operador">X</button>
    <button @click="()=> actualizarPantalla('4')" class="button">4</button>
    <button @click="()=> actualizarPantalla('5')" class="button">5</button>
    <button @click="()=> actualizarPantalla('6')" class="button">6</button>
    <button @click="() => actualizarPantalla('-')" class="button-operador">-</button>
    <button @click="()=> actualizarPantalla('1')" class="button">1</button>
    <button @click="()=> actualizarPantalla('2')" class="button">2</button>
    <button @click="()=> actualizarPantalla('3')" class="button">3</button>
    <button @click="()=> actualizarPantalla('+')" class="button-operador">+</button>
    <button @click="borrarUltimoCaracter" class="button">DEL</button>
    <button @click="()=> actualizarPantalla('0')" class="button">0</button>
    <button @click="()=> actualizarPantalla('.')" class="button">.</button>
    <button @click="calcularResultado" class="button-operador">=</button>
  </div>
</section>
<h3 class="credits">made by @rgarzona1</h3>
</template>

<style scoped>



.flex-container {
  display: flex;
  flex-direction: column;
  margin: auto;   /* Centrar la caja en la pantalla */
  align-items: center;
  padding: 20px ;
  z-index: 20;

  /* Establecer un ancho y alto fijos para la calculadora */
  width: 650x;
  height: 450px;

  background-color: #91b0cc;
  justify-content: center;
  /* dejar la caja en el centro, fija*/
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  box-shadow: 
    inset -4px -4px #444258,  /* Sombra inferior-derecha (más pronunciada) */
    inset 4px 4px #f5f6fc;   /* Sombra superior-izquierda (más pronunciada) */
}

.general-screen {
  display: flex;
  height: 150px;
  width: 327px;
  background-color: #093a50;
  align-items: center;
  justify-content: end;
  border-radius: 5px;
  text-align: right;
  padding: 10px;
  font-size: 32px;
  margin-bottom: 20px;
  overflow: hidden;       /* Evita que el texto se desborde */
  box-sizing: border-box;  
  box-shadow: 
    inset 1px 1px #808080,    /* Sombra superior-izquierda oscura */
    inset -1px -1px #FFFFFF;   /* Sombra inferior-derecha clara */
  
}

/*Cuadricula de botones */

.botones {
  max-width: 320px;
  display: grid;
  grid-template-columns: repeat(4, 1fr);  
  gap: 10px;

}

.button {
  background-color: #b9d2d8;
  border: none;
  border-radius: 5px;
  padding: 20px;
  font-size: 24px;
  cursor: pointer;
  transition: background-color 0.3s ease;
  font-family: '04b30', sans-serif;
  font-size: large;
  color:#0e0d0d;
  box-shadow: 5px 5px 0px 0px rgb(4, 139, 133);
  -webkit-box-shadow: 5px 5px 0px 0px rgb(6, 102, 119);
  -moz-box-shadow: 5px 5px 0px 0px rgba(0,0,0,1);
}

/* Botones de operadores */

.button-operador {
  background-color: #819fa7;
  border: none;
  border-radius: 5px;
  padding: 20px;
  font-size: 24px;
  cursor: pointer;
  transition: background-color 0.3s ease;
  font-family: '04b30', sans-serif;
  font-size: large;
  color:#0e0d0d;
  box-shadow: 5px 5px 0px 0px rgb(4, 139, 133);
  -webkit-box-shadow: 5px 5px 0px 0px rgb(11, 59, 68);
  -moz-box-shadow: 5px 5px 0px 0px rgba(0,0,0,1);
}

/* Botón para limpiar la pantalla */
.button-special {
  background-color: #f5a03f;
  border: none;
  border-radius: 5px;
  padding: 20px;
  font-size: 24px;
  cursor: pointer;
  transition: background-color 0.3s ease;
  font-family: '04b30', sans-serif;
  font-size: large;
  color:#0e0d0d;
  box-shadow: 5px 5px 0px 0px rgb(4, 139, 133);
  -webkit-box-shadow: 5px 5px 0px 0px rgb(151, 92, 3);
  -moz-box-shadow: 5px 5px 0px 0px rgba(0,0,0,1);

}

.screen-numbers {
  color: #ffffff;
  font-size: large;
  font-family: 'PressStartReg', sans-serif;
}

.credits {
  position: absolute;
  bottom: 10px;
  right: 20px;
  color: #849df196;
  font-size: 14px;
  font-family: 'PressStartReg', sans-serif;
  z-index: 30; /* Asegura que el texto de créditos esté por encima de otros elementos */
  font-weight: lighter;
}

/* Animaciones */

@keyframes nube-lenta {
  0% { left: -200px; }
  100% { left: 110%; }
}

@keyframes nube-lenta2 {
  0% { transform:translateX(0); }
  100% { transform:translateX(110%); }
}

@keyframes nube-lenta3 {
  0% { transform:translateX(0); }
  100% { transform:translateX(110%); }
}

@keyframes inflar {
  0%   { transform: scale(1); }
  50%  { transform: scale(1.03); }
  100% { transform: scale(1); }
}

@keyframes flotar {
  0%   { transform: translatex(0); }
  50%  { transform: translateX(-5px); }
  100% { transform: translateX(0); }
}

/* Fuentes para botones y pantalla de calculadora */

@font-face {
  font-family: 'PressStartReg';
  src: url('./assets/fonts/PressStartReg.woff2') format('woff2');
}
@font-face {
  font-family: '04b30';
  src: url('./assets/fonts/04b30.woff2') format('woff2');
}

/* Estilos para las nubes y el fondo */

.nubes-capas {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 20;
}
.nubes-capas1 {
  position: absolute;
  top: -3;
  left: 50px;
  width: 30%;
  height: 30%;
  z-index: -1; 
  opacity: 0.8; /* Opacidad para dar un efecto de profundidad */
  animation: nube-lenta2 60s linear infinite;
}

.nubes-capas2 {
  position: absolute;
  top: 10px;
  right: 125px;
  width:20%;
  height: 20%;
  z-index: -1; 
  opacity: 0.5; /* Opacidad para dar un efecto de profundidad */
  animation: nube-lenta 60s linear infinite;
}

.nubes-capas3 {
  position: absolute;
  bottom: 50%;
  left: 50%;
  width: 20%;
  height: 20%;
  z-index: 1; 
  opacity: 0.6; /* Opacidad para dar un efecto de profundidad */
  animation: nube-lenta3 50s linear infinite;
}

.nubes-horizonte {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: -1; 
  animation: inflar 6s ease-in-out infinite; /* Animación de movimiento */

}
.nubes-horizonte2 {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 0; 
  animation: flotar 4s ease-in-out infinite; /* Animación de movimiento */
}
</style>
