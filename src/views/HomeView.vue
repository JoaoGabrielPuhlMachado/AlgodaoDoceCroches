<script setup lang="ts">
import '../css/base.css'
import '../css/home.css'
import '../css/fotos.css'
import '../css/contato.css'

import { ref } from 'vue'

const scrollToSection = (sectionId) => {
  const targetElement = document.getElementById(sectionId)
  if (targetElement) {
    targetElement.scrollIntoView({ behavior: 'smooth' })
  }
}

const handleLinkClick = (e: Event, sectionId: string, pageTitle: string) => {
  e.preventDefault()
  scrollToSection(sectionId)
  document.title = `${pageTitle} - Algodão Doce Crochês`
}

const formData = ref({
  nome: '',
  email: '',
  celular: '',
  tema: '',
  mensagem: '',
})

const enviarWhatsApp = () => {
  const linkWhatsApp = window.open(
    `https://api.whatsapp.com/send?phone=47999500994&text=${encodeURIComponent(
      formData.value.mensagem,
    )}`,
  )

  formData.value = {
    nome: '',
    email: '',
    celular: '',
    tema: '',
    mensagem: '',
  }
}
</script>
<template>
  <div id="home" class="container-home">
    <div class="home-titulo">
      <h1>Bem-Vindo ao Algodão Doce Crochês</h1>
      <h3>
        Aqui fazemos amigurimis a pronta entrega ou sob-medida.
      </h3>
    </div>
    <div class="home-contato">
      <a href="#" class="btn-contato" @click="handleLinkClick($event, 'contato', 'Contato')">
        Contato
      </a>
    </div>
  </div>
  <div id="fotos" class="container-fotos">
    <div class="fotos-titulo">
      <h1>Alguns Trabalhos Feitos Por Mim</h1>
    </div>
    <div class="fotos-div">
      <img class="foto" src="../css/img/PolvoHumorBravo.jpg" alt="foto" />
      <img class="foto" src="../css/img/PolvoHumorFeliz.jpg" alt="foto" />
      <img class="foto" src="../css/img/UrsoJardineiro.jpg" alt="foto" />
      <img class="foto" src="../css/img/UrsinhoCachecol.jpg" alt="foto" />
      <img class="foto" src="../css/img/UrsoRosa.jpg" alt="foto" />
      <img class="foto" src="../css/img/GatinhoCoração.jpg" alt="foto" />
      <img class="foto" src="../css/img/ChaveiroGatinho.jpg" alt="foto" />
      <img class="foto" src="../css/img/ChaveiroSorvete.jpg" alt="foto" />
      <img class="foto" src="../css/img/Elefante.jpg" alt="foto" />
      <img class="foto" src="../css/img/Dinossauro.jpg" alt="foto" />
    </div>
  </div>
  <div id="contato" class="container-contato">
    <div class="contato-titulo">
      <h1>Entre em contato comigo e faça seu pedido agora mesmo!</h1>
    </div>
    <form>
      <div class="contato-input">
        <textarea v-model="formData.mensagem" placeholder="Mensagem" class="input-contato" type="text" />
      </div>
      <div class="container-botao">
        <button @click.prevent="enviarWhatsApp" class="contato-botao">Enviar Mensagem</button>
      </div>
    </form>
  </div>
</template>
