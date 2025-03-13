<script setup>
import { ref } from 'vue'
import '../css/cabecalho.css'

const currentPage = ref()

const scrollToTop = () => {
  window.scrollTo({
    top: 0,
    behavior: 'smooth',
  })
}

const scrollToSection = (sectionId) => {
  const targetElement = document.getElementById(sectionId)

  if (targetElement) {
    targetElement.scrollIntoView({ behavior: 'smooth' })
  }
}

const handleLinkClick = (e, sectionId, pageTitle) => {
  e.preventDefault()
  if (sectionId === 'home') {
    scrollToTop()
  } else {
    scrollToSection(sectionId)
  }
  document.title = `${pageTitle} - Algodão Doce Crochês`
  currentPage.value = pageTitle
  localStorage.setItem('lastVisitedSection', sectionId)
}
</script>
<template>
  <header>
    <ul>
      <li>
        <a href="#" @click="handleLinkClick($event, 'home', 'Home')">Home</a>
      </li>
      <li>
        <a href="#" @click="handleLinkClick($event, 'fotos', 'Fotos')">Fotos</a>
      </li>
      <li>
        <a href="#" @click="handleLinkClick($event, 'contato', 'Contato')">Contato</a>
      </li>
    </ul>
  </header>
</template>
