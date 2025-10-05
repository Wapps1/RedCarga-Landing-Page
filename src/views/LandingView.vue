<template>
  <div class="landing-view">
    <NavbarComponent v-show="isVisible" class="fade-enter fade-enter-active" />
    <section id="home" v-show="isVisible" class="fade-enter fade-enter-active delay-1">
      <HeroComponent />
    </section>
    <section id="producto" v-show="isVisible" class="fade-enter fade-enter-active delay-2">
      <ProductComponent />
    </section>
    <section id="beneficios" v-show="isVisible" class="fade-enter fade-enter-active delay-3">
      <BenefitsComponent />
    </section>
    <section id="planes" v-show="isVisible" class="fade-enter fade-enter-active delay-4">
      <PlansComponent />
    </section>
    <!-- <section v-show="isVisible" class="fade-enter fade-enter-active delay-2">
      <ProductVideoComponent />
    </section>
    <section v-show="isVisible" class="fade-enter fade-enter-active delay-2">
      <TeamVideoComponent />
    </section> -->
    <section id="faq" v-show="isVisible" class="fade-enter fade-enter-active delay-5">
      <FAQComponent />
    </section>
    <FooterComponent v-show="isVisible" class="fade-enter fade-enter-active delay-5" />
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue'
import NavbarComponent from '@/components/common/NavbarComponent.vue'
import HeroComponent from '@/components/landing/HeroComponent.vue'
import ProductComponent from '@/components/landing/ProductComponent.vue'
// import ProductVideoComponent from '@/components/landing/ProductVideoComponent.vue'
// import TeamVideoComponent from '@/components/landing/TeamVideoComponent.vue'
import BenefitsComponent from '@/components/landing/BenefitsComponent.vue'
import PlansComponent from '@/components/landing/PlansComponent.vue'
import FAQComponent from '@/components/landing/FAQComponent.vue'
import FooterComponent from '@/components/common/FooterComponent.vue'

const isVisible = ref(false)

onMounted(() => {
  // Pequeño retraso para asegurar que las animaciones se activen
  setTimeout(() => {
    isVisible.value = true
  }, 100)
})
</script>

<style scoped>
.landing-view {
  background: var(--color-background);
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: start;
  min-height: 100vh;
  width: 100%;
  padding: 0 8%;
  scroll-behavior: smooth;
}

section {
  width: 100%;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  scroll-margin-top: 100px; /* Ajusta esto según la altura de tu navbar */
  padding: 4rem 0;
}

/* Mejora la estética en dispositivos pequeños */
@media (max-width: 768px) {
  section {
    min-height: 80vh;
    scroll-margin-top: 80px;
    padding: 2rem 0;
  }
}
</style>
