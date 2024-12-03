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
  document.title = `${pageTitle} - Meu Crochê`
  currentPage.value = pageTitle
  localStorage.setItem('lastVisitedSection', sectionId)
}

onMounted(() => {
  const lastVisitedSection = localStorage.getItem('lastVisitedSection')
  if (lastVisitedSection) {
    scrollToSection(lastVisitedSection)
    currentPage.value = lastVisitedSection
    document.title = `${lastVisitedSection.charAt(0).toUpperCase() + lastVisitedSection.slice(1)
      } - Meu Crochê`
  } else {
    document.title = `Home - Meu Crochê`
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
  background-color: rgba(151, 60, 255, 0.06);
  border-bottom: 1px solid #973cff;
}
</style>
