<script setup lang="ts">
import { ref } from 'vue'

const nombre = ref('')
const apellido = ref ('')
const edad = ref()
const numero = ref('')
const genero = ref('')
const otrog = ref('')
const formularioEnviado = ref(false);

/*errores*/
const error = ref(false)
const errorAp = ref (true)
const ApLargo = ref (false)
const NLargo = ref (false)

const checkValidation = () =>{
    if(nombre.value.length > 18){
            NLargo.value = true
        }
        else{
            NLargo.value = false
        }
    }
const validationApellido = () =>{
    const nombreSinEspacios = nombre.value.replace(/\s/g, '');
    errorAp.value = nombreSinEspacios === apellido.value.replace(/\s/g, '')
    if(nombre.value == ''){
        errorAp.value = false        
    }
    if(apellido.value.length >18){
        ApLargo.value = true
    }
    else{
        ApLargo.value = false
    }
}
const checkedad = () =>{
    if(edad.value >= 60 || edad.value < 1){
        error.value = true
    }
    else{
        error.value = false
    }
}

const checkTel = () =>{
    if (numero.value.toString().length >= 10) {
        numero.value = numero.value.toString().slice(0, 10);
    }
}
const enviarFormulario = () => {
    formularioEnviado.value = true;
    alert("Formulario enviado")
    window.location.reload()
}
</script>

<template>
    <div class="formulario">
        <h2>Este es el formulario!</h2>
        <h3>Por favor, ingresa tu nombre</h3>
        <input :input="checkValidation()" type="text" v-model="nombre" required>
        <span :class="{'NLargo': NLargo}" v-if="NLargo">El nombre es muy largo</span>

        <h3>Ahora, ingresa tu apellido</h3>
        <input :input="validationApellido()" type="text" v-model="apellido" required>
        <span :class="{'errorAp': errorAp}" v-if="errorAp">El apellido debe ser diferente al nombre</span>
        <span :class="{'ApLargo': ApLargo}" v-if="ApLargo">El apellido es muy largo</span>

        <h3>Por favor, ingresa tu edad</h3> 
        <input :input="checkedad()" type="number" v-model="edad" required>
        <span :class="{'error': error}" v-if="error">La edad debe ser mayor a 1 y menor a 60 </span>

        <h3>Ingresa tu numero telefónico</h3>
        <input :input="checkTel()" type="number" v-model="numero" required>

        <h3>Genero</h3>
        <select v-model="genero" id="generoS" required  >
            <option value="Femenino">Femenino</option>
            <option value="Masculino">Masculino</option>
            <option value="Otro">Otro</option>
        </select>
        <input v-if="genero == 'Otro'" type="text" v-model="otrog" placeholder="Especificar otro genero" class="otro">
        <button @click="enviarFormulario">Enviar Formulario</button>
    </div>
</template>

<style>
    .formulario{
        width: 500px;
        height: 360px;
    }
    .errorAp, .ApLargo, .errorte, .NLargo, .tel{
        color: red;
    }
    input{
        width: 60%;
        height: 28px;
        border-radius: 50px;
        border: none;
        background-color: cadetblue;
    }
.otro{
    margin-top: 10px;
    width: 60%;
}
    span{
        width: 100%;
        display: block;
    }
    select{
        width: 60%;
        height: 25px;
        border-radius: 100px;
        border: none;
        background-color: cadetblue;
    }

    option{
        font-size: 15px;
        text-align: center;
    }
    h3{
        font-size: 13px;
    }
    button{
        display: flex;
        width: 100px;
        border-radius: 20px;
        border: none;
        margin-top: 20px;
        margin-left: 40%;
        margin-bottom: 40px;
}
button:hover{
    cursor: pointer;
    background-color: cornflowerblue;
}
</style>