<template>
    <div class="cardUsuario">
        <div class="card text-center align-items-center">
            <img :src="imagenUsuario" alt="">
            <p>{{ nombre }}</p>
            <form @submit.prevent="enviarMsg">
                <div class=" d-flex flex-column">
                    <input class="input-group my-2" type="color" name="" id="" v-model="colorFondo">
                    <textarea class="form-control my-2" name="" id="" v-model="textoChat" @keyup.enter="enviarMsg"></textarea>
                    <button class="btn btn-secondary">Enviar</button>
                </div>
            </form>
        </div>
    </div>
</template>

<script>
export default {
    name:'CardUsuario',
    props:{
        imagenUsuario: String,
        nombre: String,
        alineacion: String,
        showUserName: Boolean
    },
    data(){
        return{
            colorFondo:'#9ee2ff',
            textoChat:'',
            
        }
    },
    methods:{
        enviarMsg: function(){
            let mensaje = {
                autor: this.nombre,
                color: this.colorFondo,
                texto: this.textoChat,
                alineacion: this.alineacion,
                showUserName: this.showUserName
            }
            if(this.textoChat.length > 0 && this.textoChat != "\n"){
                this.$emit('enviarChat', mensaje)
            }
                this.textoChat= ''
           
            
        }
    }
}
</script>

<style scoped>
.cardUsuario{
    padding: 15px 12%;
}
.card{
    width: 200px;
    height: 370px;
}
.card img{
    width: 150px;
    border-radius: 120px;
    padding: 12px;
}
</style>