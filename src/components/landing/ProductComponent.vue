<template>
  <section class="product-container">
    <TitleSectionComponent :title="$t('product.sectionTitle')" />
    <div class="product-content">
      <!-- Título principal -->
      <h2 class="product-title">{{ $t('product.title') }}</h2>

      <!-- Tarjeta principal con información -->
      <div class="product-card">
        <div class="product-info">
          <h3 class="product-subtitle">
            {{ $t('product.subtitle') }}
          </h3>

          <p class="product-description">
            {{ $t('product.description') }}
          </p>

          <ul class="product-features">
            <li v-for="(feature, index) in productFeatures" :key="index" class="product-feature">
              <div class="feature-icon">
                <svg width="20" height="20" viewBox="0 0 20 20" fill="none" xmlns="http://www.w3.org/2000/svg">
                  <circle cx="10" cy="10" r="3" fill="currentColor"/>
                </svg>
              </div>
              <span>{{ feature }}</span>
            </li>
          </ul>
        </div>

        <div class="product-image">
          <img :src="truckImage" alt="Camión RedCarga" class="truck-image" />
        </div>
      </div>

    </div>
  </section>
</template>

<script setup lang="ts">
import { computed } from 'vue'
import { useI18n } from 'vue-i18n'

// Importar imágenes
import truckImage from '@/assets/images/camion.png'

const { t } = useI18n()

// Features list haciendo reactivo al idioma
const productFeatures = computed(() => [
  t('product.features.preventive'),
  t('product.features.corrective'),
  t('product.features.predictive'),
])
</script>

<style scoped>
.product-container {
  width: 100%;
  padding: 4em 0;
}

/* Banner principal */
.product-banner {
  width: 100%;
  display: flex;
  justify-content: center;
  padding: 3em 2em 2em;
}

.banner-image {
  max-width: 400px;
  width: 100%;
  height: auto;
  object-fit: contain;
}

/* Contenido principal */
.product-content {
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 70%;
  margin: 0 auto;
  padding: 2em 0 4em;
}

.product-title {
  background: linear-gradient(to right, var(--color-primary-1), var(--color-primary-2));
  -webkit-background-clip: text;
  background-clip: text;
  color: transparent;
  font-size: 2em;
  font-weight: 700;
  margin: 1em 0;
  text-align: center;
}

/* Tarjeta principal */
.product-card {
  display: flex;
  background: linear-gradient(to bottom, #f4dcdc, #f6eaea59, var(--color-background));
  border-radius: 16px;
  padding: 3rem;
  gap: 3rem;
  width: 100%;
}

.product-info {
  flex: 1;
  display: flex;
  flex-direction: column;
}

.product-subtitle {
  color: var(--color-primary-1);
  font-size: 1.3em;
  font-weight: 700;
  margin-bottom: 1.5rem;
}

.product-description {
  color: #555;
  font-size: 1em;
  line-height: 1.6;
  margin-bottom: 2rem;
}

.product-features {
  list-style: none;
  padding: 0;
  margin: 0;
}

.product-feature {
  display: flex;
  align-items: center;
  gap: 1rem;
  margin-bottom: 1rem;
  font-size: 0.95em;
}

.feature-icon {
  display: flex;
  align-items: center;
  justify-content: center;
  flex-shrink: 0;
  color: var(--color-primary-1);
}

.feature-icon svg {
  width: 20px;
  height: 20px;
}

.product-feature span {
  color: var(--color-primary-1);
  font-weight: 500;
}

.product-image {
  flex: 1;
  display: flex;
  align-items: center;
  justify-content: center;
}

.truck-image {
  max-width: 100%;
  height: auto;
  object-fit: contain;
  transition: transform 0.3s ease;
  cursor: pointer;
}

.truck-image:hover {
  animation: bounce 0.6s ease;
}

@keyframes bounce {
  0%, 100% {
    transform: translateY(0);
  }
  25% {
    transform: translateY(-15px);
  }
  50% {
    transform: translateY(-7px);
  }
  75% {
    transform: translateY(-10px);
  }
}

/* Responsive */
@media (max-width: 1024px) {
  .product-content {
    width: 85%;
  }
}

@media (max-width: 768px) {
  .product-content {
    width: 90%;
  }

  .banner-image {
    max-width: 300px;
  }

  .product-card {
    flex-direction: column;
    padding: 2rem;
    text-align: center;
  }

  .product-title {
    font-size: 1.5em;
  }

  .product-subtitle {
    font-size: 1.2em;
  }

  .product-description {
    font-size: 0.95em;
  }

  .product-features {
    display: flex;
    flex-direction: column;
    align-items: center;
  }
}

@media (max-width: 480px) {
  .product-banner {
    padding: 2em 1em 1em;
  }

  .banner-image {
    max-width: 250px;
  }

  .product-content {
    width: 95%;
  }

  .product-card {
    padding: 1.5rem;
  }
}
</style>
