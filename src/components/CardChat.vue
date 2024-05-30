<template>
    <div class="cardChat overflow-y-auto"  ref="chatContainer">
        <h5 class="text-center py-3">Chat</h5>
        <div v-for="(message, index) in formattedMessages" :key="index" :style="{ textAlign: message.alineacion }"
            class="d-flex flex-column">
            <label class="fs-6" v-if="message.showUserName">{{ message.autor }}</label>
            <div class="py-1">
                <span :style="{ backgroundColor: message.color }" class="fs-5 rounded inline-block" id="cajaTexto">{{ message.texto }}</span>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'CardChat',
    props: ['mensajes'],
    watch: { 
        mensajes() { 
            this.$nextTick(() => { 
                this.$refs.chatContainer.scrollTop = this.$refs.chatContainer.scrollHeight; });
             } 
    },
    computed: {
    formattedMessages() {
      return this.mensajes.map((message, index) => {
        if (index === 0) {
          message.showUserName = true;
        } else {
          const previousMessage = this.mensajes[index - 1];
          message.showUserName = message.autor !== previousMessage.autor;
        }
        return message;
      });
    }
  }

}
</script>

<style>
.cardChat {
    background-color: bisque;
    height: 50vh;
    margin: 15px 0;
}

#cajaTexto {
    padding: 2px 12px;
    animation-name: opacidad;
    animation-duration: 0.9s;
}

@keyframes opacidad{
    from {opacity: 0;}
    to {opacity: 100;}
}
</style>