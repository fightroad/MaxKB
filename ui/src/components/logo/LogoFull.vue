<template>
  <img v-if="theme.themeInfo?.loginLogo" :src="fileURL" alt="" height="45px" class="mr-8" />
  <div v-else class="logo-full">
    <LogoIcon :height="height" />
    <span class="logo-brand ml-8" :class="!isDefaultTheme ? 'is-custom' : ''">Agent</span>
  </div>
</template>
<script setup lang="ts">
import { computed } from 'vue'
import useStore from '@/stores'
import LogoIcon from './LogoIcon.vue'
defineOptions({ name: 'LogoFull' })

defineProps({
  height: {
    type: String,
    default: '36px',
  },
})
const { theme } = useStore()
const isDefaultTheme = computed(() => {
  return theme.isDefaultTheme()
})

const fileURL = computed(() => {
  if (theme.themeInfo) {
    if (typeof theme.themeInfo?.loginLogo === 'string') {
      return theme.themeInfo?.loginLogo
    } else {
      return URL.createObjectURL(theme.themeInfo?.loginLogo)
    }
  } else {
    return ''
  }
})
</script>
<style lang="scss" scoped>
.logo-full {
  display: inline-flex;
  align-items: center;
  .logo-brand {
    font-size: 20px;
    font-weight: 700;
    line-height: 1;
    letter-spacing: 0.02em;
    background: linear-gradient(180deg, #3370ff 0%, #7f3bf5 100%);
    -webkit-background-clip: text;
    background-clip: text;
    color: transparent;
    &.is-custom {
      background: none;
      -webkit-background-clip: unset;
      background-clip: unset;
      color: var(--el-color-primary);
    }
  }
}
</style>
