<script setup lang="ts">
import { RouterView } from 'vue-router'
import { ConfigProvider } from 'ant-design-vue'
</script>

<template>
  <ConfigProvider
    :theme="{
      token: { colorPrimary: '#00AEEF', borderRadius: 8 },
      components: {
        Button: {
          // design team can modify these
          colorPrimary: '#050833',
          colorPrimaryHover: '#050833B3',
          colorLinkActive: '#050833B3',
          colorLinkHover: '#050833B3',
          colorPrimaryActive: '#050833B3',
          algorithm: false,
        },
        Input: {
          colorPrimary: '#050833',
          colorPrimaryHover: '#050833B3',
        },
      },
    }"
  >
    <RouterView />
  </ConfigProvider>
</template>
