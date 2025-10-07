<template>
  <header class="navbar">
    <a
      href="#home"
      class="navbar__logo"
      aria-label="Inicio - Logo RedCarga"
      @click.prevent="scrollToSection('home')"
    >
      <img src="@/assets/images/logo1.png" alt="Logo RedCarga" />
      <h1 class="navbar__logo-text">RedCarga</h1>
    </a>

    <v-icon name="fc-globe" />
    <nav
      class="navbar__nav"
      :class="{ 'navbar__nav--mobile': isMobileMenuOpen }"
      aria-label="Navegación principal"
    >
      <ul role="menubar">
        <li v-for="item in navItems" :key="item.text" role="none">
          <a
            :href="item.href"
            role="menuitem"
            :aria-current="item.isActive ? 'page' : undefined"
            :class="{ active: item.isActive }"
            @click.prevent="scrollToSection(item.href.substring(1))"
          >
            {{ item.text }}
          </a>
        </li>
      </ul>

      <div class="navbar__mobile-footer">
        <div class="navbar__language navbar__language--mobile">
          <template v-for="(lang, index) in languages" :key="lang.code">
            <button
              type="button"
              :aria-pressed="lang.isActive"
              :lang="lang.code"
              :class="{ active: lang.isActive }"
              @click="handleLanguageChange(lang.code)"
            >
              {{ lang.text }}
            </button>
            <span v-if="index < languages.length - 1" aria-hidden="true">|</span>
          </template>
        </div>

        <div class="navbar__buttons navbar__buttons--mobile">
          <InteractiveComponent
            tag="a"
            :href="androidDownloadConfig.href"
            variant="primary"
            :aria-label="androidDownloadConfig.ariaLabel"
            @click="androidDownloadConfig.onClick"
          >
            <svg class="button-icon" width="20" height="20" viewBox="0 0 24 24" fill="currentColor">
              <path d="M17.6 9.48l1.84-3.18c.16-.31.04-.69-.26-.85-.29-.15-.65-.06-.83.22l-1.88 3.24a11.43 11.43 0 0 0-8.94 0L5.65 5.67c-.19-.28-.54-.37-.83-.22-.3.16-.42.54-.26.85l1.84 3.18C2.92 11.03 1 14.22 1 17.8h22c0-3.58-1.92-6.77-5.4-8.32zM7 15.25c-.69 0-1.25-.56-1.25-1.25s.56-1.25 1.25-1.25 1.25.56 1.25 1.25-.56 1.25-1.25 1.25zm10 0c-.69 0-1.25-.56-1.25-1.25s.56-1.25 1.25-1.25 1.25.56 1.25 1.25-.56 1.25-1.25 1.25z"/>
            </svg>
            {{ androidDownloadConfig.text }}
          </InteractiveComponent>

          <InteractiveComponent
            tag="a"
            :href="iosDownloadConfig.href"
            variant="secondary"
            :aria-label="iosDownloadConfig.ariaLabel"
            @click="iosDownloadConfig.onClick"
          >
            <svg class="button-icon" width="20" height="20" viewBox="0 0 24 24" fill="currentColor">
              <path d="M17.05 20.28c-.98.95-2.05.8-3.08.35-1.09-.46-2.09-.48-3.24 0-1.44.62-2.2.44-3.06-.35C2.79 15.25 3.51 7.59 9.05 7.31c1.35.07 2.29.74 3.08.8 1.18-.24 2.31-.93 3.57-.84 1.51.12 2.65.72 3.4 1.8-3.12 1.87-2.38 5.98.48 7.13-.57 1.5-1.31 2.99-2.54 4.09l.01-.01zM12.03 7.25c-.15-2.23 1.66-4.07 3.74-4.25.29 2.58-2.34 4.5-3.74 4.25z"/>
            </svg>
            {{ iosDownloadConfig.text }}
          </InteractiveComponent>
        </div>
      </div>
    </nav>

    <div
      class="navbar__language navbar__language--desktop"
      role="navigation"
      aria-label="Selector de idioma"
    >
      <template v-for="(lang, index) in languages" :key="lang.code">
        <button
          type="button"
          :aria-pressed="lang.isActive"
          :lang="lang.code"
          :class="{ active: lang.isActive }"
          @click="handleLanguageChange(lang.code)"
        >
          {{ lang.text }}
        </button>
        <span v-if="index < languages.length - 1" aria-hidden="true">|</span>
      </template>
    </div>

    <div
      class="navbar__buttons navbar__buttons--desktop"
      role="navigation"
      aria-label="Descargar aplicación"
    >
      <InteractiveComponent
        tag="a"
        :href="androidDownloadConfig.href"
        variant="primary"
        :aria-label="androidDownloadConfig.ariaLabel"
        @click="androidDownloadConfig.onClick"
      >
        <svg class="button-icon" width="20" height="20" viewBox="0 0 24 24" fill="currentColor">
          <path d="M17.6 9.48l1.84-3.18c.16-.31.04-.69-.26-.85-.29-.15-.65-.06-.83.22l-1.88 3.24a11.43 11.43 0 0 0-8.94 0L5.65 5.67c-.19-.28-.54-.37-.83-.22-.3.16-.42.54-.26.85l1.84 3.18C2.92 11.03 1 14.22 1 17.8h22c0-3.58-1.92-6.77-5.4-8.32zM7 15.25c-.69 0-1.25-.56-1.25-1.25s.56-1.25 1.25-1.25 1.25.56 1.25 1.25-.56 1.25-1.25 1.25zm10 0c-.69 0-1.25-.56-1.25-1.25s.56-1.25 1.25-1.25 1.25.56 1.25 1.25-.56 1.25-1.25 1.25z"/>
        </svg>
        {{ androidDownloadConfig.text }}
      </InteractiveComponent>

      <InteractiveComponent
        tag="a"
        :href="iosDownloadConfig.href"
        variant="secondary"
        :aria-label="iosDownloadConfig.ariaLabel"
        @click="iosDownloadConfig.onClick"
      >
        <svg class="button-icon" width="20" height="20" viewBox="0 0 24 24" fill="currentColor">
          <path d="M17.05 20.28c-.98.95-2.05.8-3.08.35-1.09-.46-2.09-.48-3.24 0-1.44.62-2.2.44-3.06-.35C2.79 15.25 3.51 7.59 9.05 7.31c1.35.07 2.29.74 3.08.8 1.18-.24 2.31-.93 3.57-.84 1.51.12 2.65.72 3.4 1.8-3.12 1.87-2.38 5.98.48 7.13-.57 1.5-1.31 2.99-2.54 4.09l.01-.01zM12.03 7.25c-.15-2.23 1.66-4.07 3.74-4.25.29 2.58-2.34 4.5-3.74 4.25z"/>
        </svg>
        {{ iosDownloadConfig.text }}
      </InteractiveComponent>
    </div>

    <button
      class="navbar__hamburger"
      :class="{ 'is-active': isMobileMenuOpen }"
      aria-label="Menú principal"
      aria-expanded="false"
      @click="toggleMobileMenu"
    >
      <span class="navbar__hamburger-line"></span>
      <span class="navbar__hamburger-line"></span>
      <span class="navbar__hamburger-line"></span>
    </button>

    <div v-if="isMobileMenuOpen" class="navbar__overlay" @click="isMobileMenuOpen = false"></div>
  </header>
</template>

<script setup lang="ts">
import { ref, watch, onMounted, onBeforeUnmount } from 'vue'
import { useI18n } from 'vue-i18n'
import InteractiveComponent from './InteractiveComponent.vue'
import type { NavItem, Language, ButtonConfig } from '@/types/navbar.types'

const { t, locale } = useI18n()

const navItems = ref<NavItem[]>([
  { text: t('navbar.home'), href: '#home', isActive: true },
  { text: t('navbar.product'), href: '#producto', isActive: false },
  { text: t('navbar.benefits'), href: '#beneficios', isActive: false },
  { text: t('navbar.plans'), href: '#planes', isActive: false },
  { text: t('navbar.faq'), href: '#faq', isActive: false },
])

const languages = ref<Language[]>([
  { code: 'es', text: 'ES', isActive: locale.value === 'es' },
  { code: 'en', text: 'EN', isActive: locale.value === 'en' },
])

const isMobileMenuOpen = ref(false)
const isProgrammaticScrolling = ref(false)

const toggleMobileMenu = () => {
  isMobileMenuOpen.value = !isMobileMenuOpen.value
  document.body.style.overflow = isMobileMenuOpen.value ? 'hidden' : ''
}

const scrollToSection = (sectionId: string) => {
  const section = document.getElementById(sectionId)
  if (section) {
    isMobileMenuOpen.value = false
    document.body.style.overflow = ''

    navItems.value = navItems.value.map((item) => ({
      ...item,
      isActive: item.href === `#${sectionId}`,
    }))

    isProgrammaticScrolling.value = true

    section.scrollIntoView({
      behavior: 'smooth',
      block: 'start',
    })

    setTimeout(() => {
      isProgrammaticScrolling.value = false
    }, 1000)
  }
}

let observer: IntersectionObserver

onMounted(() => {
  observer = new IntersectionObserver(
    (entries) => {
      if (isProgrammaticScrolling.value) return

      entries.forEach((entry) => {
        if (entry.isIntersecting) {
          const sectionId = entry.target.id

          navItems.value = navItems.value.map((item) => ({
            ...item,
            isActive: item.href === `#${sectionId}`,
          }))
        }
      })
    },
    {
      threshold: 0.3,
      rootMargin: '-80px 0px 0px 0px',
    },
  )

  // Observar todas las secciones
  const sections = ['home', 'producto', 'beneficios', 'planes', 'faq']
  sections.forEach((sectionId) => {
    const section = document.getElementById(sectionId)
    if (section) {
      observer.observe(section)
    }
  })

  // Manejar navegación por hash en la URL al cargar
  if (window.location.hash) {
    const sectionId = window.location.hash.substring(1)
    setTimeout(() => scrollToSection(sectionId), 500)
  }
})

onBeforeUnmount(() => {
  // Desconectar el observer al desmontar
  if (observer) {
    observer.disconnect()
  }
})

const handleLanguageChange = (code: string) => {
  locale.value = code

  languages.value = languages.value.map((lang) => ({
    ...lang,
    isActive: lang.code === code,
  }))

  localStorage.setItem('userLanguage', code)
}

watch(locale, () => {
  navItems.value = [
    { text: t('navbar.home'), href: '#home', isActive: navItems.value[0].isActive },
    { text: t('navbar.product'), href: '#producto', isActive: navItems.value[1].isActive },
    { text: t('navbar.benefits'), href: '#beneficios', isActive: navItems.value[2].isActive },
    { text: t('navbar.plans'), href: '#planes', isActive: navItems.value[3].isActive },
    { text: t('navbar.faq'), href: '#faq', isActive: navItems.value[4].isActive },
  ]

  androidDownloadConfig.value = {
    ...androidDownloadConfig.value,
    text: t('navbar.downloadAndroid'),
    ariaLabel: t('navbar.downloadAndroidAriaLabel'),
  }

  iosDownloadConfig.value = {
    ...iosDownloadConfig.value,
    text: t('navbar.downloadIOS'),
    ariaLabel: t('navbar.downloadIOSAriaLabel'),
  }
})

const androidDownloadConfig = ref<ButtonConfig>({
  text: t('navbar.downloadAndroid'),
  href: 'https://play.google.com/store',
  ariaLabel: t('navbar.downloadAndroidAriaLabel'),
  onClick: () => {
    console.log('Descargando app para Android')
    isMobileMenuOpen.value = false
  },
})

const iosDownloadConfig = ref<ButtonConfig>({
  text: t('navbar.downloadIOS'),
  href: 'https://www.apple.com/app-store/',
  ariaLabel: t('navbar.downloadIOSAriaLabel'),
  onClick: () => {
    console.log('Descargando app para iOS')
    isMobileMenuOpen.value = false
  },
})
</script>

<style scoped>
.navbar {
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: space-between;
  background-color: var(--color-background);
  padding: 2em 0;
  position: sticky;
  top: 0;
  left: 0;
  z-index: 100;
}

.navbar__logo {
  display: flex;
  align-items: center;
}

.navbar__logo img {
  height: 45px;
  width: auto;
  transition: transform 0.1s ease;
  &:hover {
    transform: scale(1.05);
  }
}
.navbar__logo h1 {
  font-size: 1.3em;
  font-weight: 700;
  color: var(--color-primary-1);
  margin-left: 1em;
}

.navbar__nav {
  background-color: var(--color-gray-light);
  border-radius: 30px;
  padding: 5px;
  padding: 0.5em 2em;
  box-shadow: 0 2px 5px 1px rgba(0, 0, 0, 0.155);
}

.navbar__nav ul {
  display: flex;
  gap: 1em;
}

.navbar__nav li {
  list-style: none;
}

.navbar__nav a {
  display: block;
  padding: 0.6em 2em;
  color: var(--color-primary-1);
  font-size: 0.83em;
  font-weight: 400;
  border-radius: 25px;
  transition:
    background-color 0.5s ease,
    transform 0.15s ease;
}

.navbar__nav a.active {
  background: linear-gradient(to bottom, var(--color-primary-1), var(--color-primary-2));
  color: var(--color-white);
}

.navbar__nav a:hover {
  background-color: rgba(0, 0, 0, 0.05);
  transform: scale(1.05);
}

.navbar__language {
  display: flex;
  align-items: center;
}

.navbar__language button {
  cursor: pointer;
  background: none;
  border: none;
  cursor: pointer;
  font-size: 0.9rem;
  padding: 5px 8px;
  color: var(--color-primary-1);
  opacity: 0.8;
  transition: transform 0.1s ease;
  &:hover {
    transform: scale(1.05);
  }
}

.navbar__language button.active {
  opacity: 1;
  color: var(--color-primary-1);
  font-weight: 700;
}

.navbar__language span {
  margin: 0 5px;
  color: var(--color-text);
  opacity: 0.3;
}

.navbar__buttons {
  display: flex;
  gap: 15px;
  align-items: center;
}

.navbar__buttons :deep(.button-icon) {
  margin-right: 8px;
  vertical-align: middle;
}

.navbar__hamburger {
  display: none;
  flex-direction: column;
  justify-content: space-between;
  width: 30px;
  height: 22px;
  background: transparent;
  border: none;
  cursor: pointer;
  padding: 0;
  z-index: 30;
}

.navbar__hamburger-line {
  display: block;
  width: 100%;
  height: 3px;
  border-radius: 3px;
  background: var(--color-primary-1);
  transition: all 0.3s ease-in-out;
}

.navbar__hamburger.is-active .navbar__hamburger-line:nth-child(1) {
  transform: translateY(9.5px) rotate(45deg);
}

.navbar__hamburger.is-active .navbar__hamburger-line:nth-child(2) {
  opacity: 0;
}

.navbar__hamburger.is-active .navbar__hamburger-line:nth-child(3) {
  transform: translateY(-9.5px) rotate(-45deg);
}

.navbar__mobile-footer {
  display: none;
}

.navbar__overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  z-index: 20;
}

@media (max-width: 1517px) {
  .navbar__logo-text {
    display: none;
  }
}

@media (max-width: 1370px) {
  .navbar {
    padding: 1.5em 0;
  }

  .navbar__hamburger {
    display: flex;
  }

  .navbar__nav {
    position: fixed;
    top: 0;
    right: -300px;
    width: 280px;
    height: 100vh;
    background-color: var(--color-background);
    border-radius: 0;
    box-shadow: -5px 0 15px rgba(0, 0, 0, 0.1);
    transition: right 0.3s ease-in-out;
    z-index: 25;
    padding: 5em 1.5em 2em;
    overflow-y: auto;
  }

  .navbar__nav--mobile {
    right: 0;
  }

  .navbar__nav ul {
    flex-direction: column;
    gap: 0.7em;
  }

  .navbar__nav a {
    padding: 0.8em 1.5em;
    font-size: 1em;
    text-align: center;
  }

  .navbar__language--desktop,
  .navbar__buttons--desktop {
    display: none;
  }

  .navbar__mobile-footer {
    display: flex;
    flex-direction: column;
    align-items: center;
    margin-top: 2.5em;
    gap: 1.5em;
  }

  .navbar__language--mobile {
    justify-content: center;
    margin-bottom: 0.5em;
  }

  .navbar__buttons--mobile {
    flex-direction: column;
    width: 100%;
    gap: 10px;
  }

  .navbar__buttons--mobile :deep(a),
  .navbar__buttons--mobile :deep(button) {
    width: 100%;
    text-align: center;
  }
}
</style>
