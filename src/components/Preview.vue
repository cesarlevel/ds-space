<script setup>
import { inject } from 'vue'
import PreviewElement from './PreviewElement.vue';

const state = inject('state');
</script>

<template>
  <div id="dss-preview">
    <h3>Space</h3>
    <table v-for="size in state.sizes">
      <colgroup>
        <col width="10%">
        <col width="50%">
      </colgroup>
      <tr>
        <td>
          <small>--{{ state.identifier }}-space-{{ size.name }} <span style="opacity: 0.4;">({{ `${size.value}${state.units}` }})</span></small>
        </td>
        <td>
          <div class="size-box" :style="{ width: `${size.value}${state.units}` }"></div>
        </td>
      </tr>
    </table>
    <div class="divider divider-l"></div>
    <div class="component-test">
      <PreviewElement :block="state.components[0]" unstyled :inline="false"><h1 style="margin-bottom: 0">Heading 1</h1></PreviewElement>
      <PreviewElement :block="state.components[1]" unstyled :inline="false">Lorem ipsum dolor sit amet, consectetur adipiscing elit. Integer mollis non felis at eleifend. Curabitur dignissim leo non lacinia pellentesque. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Integer mollis non felis at eleifend. Curabitur dignissim leo non lacinia pellentesque. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Integer mollis non felis at eleifend. Curabitur dignissim leo non lacinia pellentesque.</PreviewElement>
      <PreviewElement :block="state.components[1]" unstyled :inline="false">Lorem ipsum dolor sit amet, consectetur adipiscing elit. Integer mollis non felis at eleifend. Curabitur dignissim leo non lacinia pellentesque. Integer mollis non felis at eleifend. Curabitur dignissim leo non lacinia pellentesque.</PreviewElement>
      <PreviewElement :block="state.components[2]">Button</PreviewElement>
      <div class="divider divider-hidden"></div>
      <PreviewElement :block="state.components[3]" unstyled>Input label</PreviewElement>
      <PreviewElement :block="state.components[4]" outline :inline="false">Input</PreviewElement>
      <div class="divider divider-hidden"></div>
      <PreviewElement :block="state.components[5]" outline style="width: 50%;">
        <template #default>
          <PreviewElement :block="state.components[6]" unstyled><h3 style="margin-bottom: 0">Card</h3></PreviewElement>
          <PreviewElement :block="state.components[7]" unstyled>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Integer mollis non felis at eleifend. Curabitur dignissim leo non lacinia pellentesque.</PreviewElement>
          <PreviewElement :block="state.components[8]" rounded>Chip</PreviewElement>
          <PreviewElement :block="state.components[8]" rounded>Chip</PreviewElement>
          <PreviewElement :block="state.components[8]" rounded>Chip</PreviewElement>
          <div style="text-align: right;">
            <PreviewElement :block="state.components[2]">Button</PreviewElement>
          </div>
        </template>
      </PreviewElement>
    </div>
  </div>
</template>

<style scoped>
  #dss-preview {
    overflow-y: auto;
    background: color-mix(in srgb, var(--color-primary) 95%, #ffffff);
    padding: var(--space-7);
  }

  table {
    width: 100%;
  }

  .size-box {
    height: 10px;
    margin-left: 10px;
    border-radius: 999px;
    background: var(--color-accent);
  }

  .component-test {
    max-width: 900px;
    margin-inline: auto;
  }
</style>
