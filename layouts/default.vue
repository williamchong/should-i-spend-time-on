<template>
  <div>
    <slot />
  </div>
</template>

<script setup lang="ts">
import { useI18n } from 'vue-i18n'
const { t } = useI18n()

const i18nHead = useLocaleHead()
useHead({
  htmlAttrs: {
    lang: i18nHead.value.htmlAttrs!.lang
  },
  link: [...(i18nHead.value.link || [])],
  meta: [...(i18nHead.value.meta || [])],
  script: [
    {
      type: 'application/ld+json',
      children: JSON.stringify({
        '@context': 'https://schema.org',
        '@type': 'WebApplication',
        name: t('title'),
        description: t('description'),
        url: 'https://shouldispendtimeon.work',
        applicationCategory: 'UtilityApplication',
        operatingSystem: 'Web',
        offers: {
          '@type': 'Offer',
          price: '0',
          priceCurrency: 'USD',
          availability: 'https://schema.org/InStock'
        },
        author: {
          '@type': 'Person',
          name: 'William Chong',
          url: 'https://blog.williamchong.cloud'
        },
        potentialAction: {
          '@type': 'UseAction',
          target: 'https://shouldispendtimeon.work'
        }
      })
    }
  ]
})
useSeoMeta({
  title: t('title'),
  description: t('description'),
  ogTitle: t('title'),
  ogDescription: t('description'),
  ogImage: 'https://shouldispendtimeon.work/images/cover.jpg',
  ogType: 'website',
})
</script>
