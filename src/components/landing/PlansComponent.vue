<template>
  <section class="plans-section">
    <TitleSectionComponent :title="$t('plans.title')" />
    <div class="plans-container">

      <div class="plans-grid">
        <!-- Plan Gratuito -->
        <div class="plan-card-container">
          <PlanItemComponent
            :title="freePlan.title"
            :subtitle="freePlan.subtitle"
            :price="freePlanPrice"
            :features="freePlan.features"
            :actionText="actionText"
          />
        </div>

        <!-- Plan Premium -->
        <div class="plan-wrapper plan-wrapper--featured">
          <PlanItemComponent
            :title="premiumPlan.title"
            :subtitle="premiumPlan.subtitle"
            :price="premiumPlanPrice"
            :period="t('plans.time.monthly')"
            :features="premiumPlan.features"
            :actionText="actionText"
            :isDark="true"
          />
        </div>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
import { computed } from 'vue'
import { useI18n } from 'vue-i18n'
import TitleSectionComponent from '@/components/common/TitleSectionComponent.vue'
import PlanItemComponent from '@/components/common/PlanItemComponent.vue'
import { formatPrice } from '@/utils/formatPrice'

const { t } = useI18n()
const actionText = computed(() => t('plans.cta'))

const freePlan = computed(() => ({
  title: t('plans.free.title'),
  subtitle: t('plans.free.subtitle'),
  features: [
    t('plans.free.features.0'),
    t('plans.free.features.1'),
    t('plans.free.features.2'),
    t('plans.free.features.3'),
    t('plans.free.features.4'),
    t('plans.free.features.5'),
  ],
}))

const premiumPlan = computed(() => ({
  title: t('plans.premium.title'),
  subtitle: t('plans.premium.subtitle'),
  features: [
    t('plans.premium.features.0'),
    t('plans.premium.features.1'),
    t('plans.premium.features.2'),
    t('plans.premium.features.3'),
    t('plans.premium.features.4'),
    t('plans.premium.features.5'),
    t('plans.premium.features.6'),
  ],
}))

const freePlanPrice = computed(() => formatPrice(0))
const premiumPlanPrice = computed(() => formatPrice(20))
</script>

<style scoped>
.plans-section {
  padding: 4em 0;
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
}
.plans-title {
  background: linear-gradient(to right, var(--color-primary-1), var(--color-primary-2));
  background-clip: text;
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  font-size: 1.6em;
  font-weight: 700;
}

.plans-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 2em;
  background-color: #ff803718;
  margin-top: 2em;
  border-radius: 1em;
  width: 100%;
  max-width: 1200px;
  box-shadow: 0 10px 30px rgba(138, 112, 214, 0.1);
}

.plan-card-container {
  position: relative;
}

.plans-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 40px;
  width: 100%;
  max-width: 900px;
  margin: 0 auto;
  padding: 3em;
}

/* Wrappers para cada plan */
.plan-wrapper {
  position: relative;
}

.plan-wrapper--featured {
  position: relative;
  z-index: 2;
}

/* Responsive ajustes */
@media (max-width: 1200px) {
  .plans-grid {
    gap: 25px;
  }

  .plans-container {
    margin: 2em 1em;
    width: calc(100% - 2em);
  }
}

@media (max-width: 900px) {
  .plans-section {
    padding: 3em 0;
  }

  .plans-grid {
    display: flex;
    flex-direction: column;
    gap: 30px;
    width: 90%;
    max-width: 450px;
    margin: 0 auto;
    align-items: center;
  }

  .plan-card-container,
  .plan-wrapper--featured {
    width: 100%;
    display: flex;
    justify-content: center;
  }

  .plan-wrapper--featured {
    order: -1;
  }
}

@media (max-width: 767px) {
  .plans-section {
    padding: 2em 0;
  }

  .plans-grid {
    width: 95%;
    max-width: 380px;
    gap: 30px;
  }
}

@media (max-width: 480px) {
  .plans-section {
    padding: 2em 0;
  }

  .plans-container {
    padding: 1.5em 1em;
    border-radius: 0.8em;
  }

  .plans-title {
    font-size: 1.4em;
    text-align: center;
  }

  .plans-grid {
    gap: 25px;
    max-width: 340px;
  }
}

@media (max-width: 360px) {
  .plans-container {
    padding: 1.2em 0.8em;
  }

  .plans-grid {
    max-width: 300px;
  }
}
</style>
