<script setup>
import CabecalhoComp from './components/CabecalhoComp.vue'
import RodapeComp from './components/RodapeComp.vue'
import HomeView from './views/HomeView.vue'
import { onMounted, onUnmounted, ref } from 'vue'
const addBorderOnScroll = () => {
  const handleScroll = () => {
    const scrollPosition = window.scrollY || document.documentElement.scrollTop

    if (scrollPosition > 0) {
      document.body.classList.add('with-border')
    } else {
      document.body.classList.remove('with-border')
    }
  }

  onMounted(() => {
    window.addEventListener('scroll', handleScroll)
  })

  onUnmounted(() => {
    window.removeEventListener('scroll', handleScroll)
  })
}
addBorderOnScroll()

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

onMounted(() => {
  const lastVisitedSection = localStorage.getItem('lastVisitedSection')
  if (lastVisitedSection) {
    scrollToSection(lastVisitedSection)
    currentPage.value = lastVisitedSection
    document.title = `${lastVisitedSection.charAt(0).toUpperCase() + lastVisitedSection.slice(1)
      } - Algodão Doce Crochês`
  } else {
    document.title = `Home - Algodão Doce Crochês`
    currentPage.value = 'home'
  }
})
</script>

<template>
  <CabecalhoComp />
  <HomeView />
  <RodapeComp />
</template>
<style>
.with-border header {
  background-color: rgba(131, 94, 94, 0.06);
  border-bottom: 1px solid rgb(131, 94, 94);
}
</style>
