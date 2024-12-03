<script setup>
import '../css/rodape.css'

const enviarWhatsApp = () => {
  const linkWhatsApp = window.open(`https://api.whatsapp.com/send?phone=47999500994<`)

  formData.value = {
    nome: '',
    email: '',
    celular: '',
    tema: '',
    mensagem: '',
  }
}

const enviarEmail = () => {
  const mailtoLink = `mailto:sttirlley@gmail.com`

  window.open(mailtoLink)
}
</script>
<template>
  <footer>
    <div class="footer-contact">
      <p @click.prevent="enviarWhatsApp">+55 (47) 99950-0994</p>
      <p @click.prevent="enviarEmail">angelisgadotti@gmail.com</p>
    </div>
    <div class="footer-copyright">
      <p>COPYRIGHT © 2024 LÍGIA DE ANGELIS GADOTTI | ALL RIGHTS RESERVED</p>
    </div>
    <div class="footer-nada">
      <p></p>
    </div>
  </footer>
</template>