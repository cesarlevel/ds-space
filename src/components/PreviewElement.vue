<script setup>
import {inject} from 'vue';
const focusedElement = inject('focusedElement');

function focusElement(el) {
  focusedElement.value = el;
}

const props = defineProps({
    block: {
        type: Object,
        default: () => {},
    },
    outline: {
        type: Boolean,
        default: false,
    },
    rounded: {
        type: Boolean,
        default: false,
    },
    unstyled: {
        type: Boolean,
        default: false,
    },
    inline: {
        type: Boolean,
        default: true,
    },
});
const state = inject('state');
</script>

<template>
    <div
      class="preview"
      @mouseover.prevent="focusElement(props.block.name)"
      :class="{'preview-outline': props.outline, 'preview-rounded': props.rounded, 'preview-unstyled': props.unstyled}"
      :style="{display: props.inline ? 'inline-block' : 'block', padding: `${props.block.vp}${state.units} ${props.block.hp}${state.units}`,fontSize: `${state.fontSize}${state.units}`, margin: `${props.block.mt}${state.units} ${props.block.mr}${state.units} ${props.block.mb}${state.units} ${props.block.ml}${state.units}`}">
      <slot></slot>
    </div>
</template>

<style scoped>
.preview {
  background: var(--color-accent);
  color: var(--color-primary);
}

.preview.preview-outline {
  border: 1px solid var(--color-accent);
  background: transparent;
  color: var(--color-accent);
}

.preview.preview-rounded {
  border-radius: 999px;
}

.preview.preview-unstyled {
  background: transparent;
  color: var(--color-accent);
}
</style>
