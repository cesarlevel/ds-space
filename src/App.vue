<script setup>
import ToolBar from './components/ToolBar.vue';
import Preview from './components/Preview.vue';
import { reactive, provide, computed, ref, watch } from 'vue';

const state = reactive({
  identifier: 'dss',
  multiplier: 1.5,
  units: 'px',
  fontSize: '16',
  sizes: [
    { name: '0', value: '0' },
    { name: '1', value: '2' },
    { name: '2', value: '4' },
    { name: '3', value: '8' },
    { name: '4', value: '12' },
    { name: '5', value: '16' },
    { name: '6', value: '20' },
    { name: '7', value: '32' },
  ],
  components: [
    {
      name: 'heading1',
      vp: '0',
      hp: '0',
      mt: '0',
      mr: '0',
      mb: '12',
      ml: '0',
    },
    {
      name: 'paragraph',
      vp: '0',
      hp: '0',
      mt: '0',
      mr: '0',
      mb: '20',
      ml: '0',
    },
    {
      name: 'button',
      vp: '8',
      hp: '12',
      mt: '0',
      mr: '0',
      mb: '0',
      ml: '0',
    },
    {
      name: 'inputLabel',
      vp: '0',
      hp: '0',
      mt: '0',
      mr: '0',
      mb: '4',
      ml: '0',
    },
    {
      name: 'input',
      vp: '8',
      hp: '12',
      mt: '0',
      mr: '0',
      mb: '0',
      ml: '0',
    },
    {
      name: 'card',
      vp: '20',
      hp: '20',
      mt: '0',
      mr: '0',
      mb: '0',
      ml: '0',
    },
    {
      name: 'cardHeading',
      vp: '0',
      hp: '0',
      mt: '0',
      mr: '0',
      mb: '12',
      ml: '0',
    },
    {
      name: 'cardParagraph',
      vp: '0',
      hp: '0',
      mt: '0',
      mr: '0',
      mb: '20',
      ml: '0',
    },
    {
      name: 'chip',
      vp: '2',
      hp: '12',
      mt: '0',
      mr: '8',
      mb: '0',
      ml: '0',
    }
  ],

});

const focusedElement = ref(null);

provide('state', state);
provide('focusedElement', focusedElement);
</script>

<template>
  <ToolBar />
  <Preview />
</template>

<style scoped>
</style>
