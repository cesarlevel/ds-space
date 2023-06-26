<script setup>
import Icon from './Icon.vue';

const props = defineProps({
    modelValue: String,
    label: String,
    append: String,
    icon: {
        type: String,
        default: null,
    },
    type: {
        type: String,
        default: 'text',
    },
    min: String,
    max: String,
    step: {
        type: String,
        default: '1',
    },
});

defineEmits(['update:modelValue']);
</script>

<template>
  <div class="input-wrapper">
    <label v-if="props.label">Label</label>
    <Icon class="input-icon" :icon="icon"/>
    <input
        :class="props.icon ? 'has-icon' : ''"
        :value="modelValue"
        :min="props.min"
        :max="props.max"
        :step="props.step" 
        @input="$emit('update:modelValue', $event.target.value)"
        :type="props.type">
    <span class="input-append">{{ props.append }}</span>
  </div>
</template>

<style scoped>
.input-wrapper {
    position: relative;
}

.input-icon {
    position: absolute;
    top: 50%;
    left: var(--space-3);
    transform: translateY(-50%);
}

.input-append {
    position: absolute;
    top: 50%;
    right: var(--space-7);
    text-transform: uppercase;
    font-size: var(--font-size-sm);
    line-height: 1;
    transform: translateY(-50%);
    opacity: 0.5;
}

input {
    padding: var(--space-3) var(--space-4);
    width: 100%;
    background: transparent;
    box-shadow: inset 0 0 0 1px rgba(255, 255, 255, 0);
    border: none;
    box-sizing: border-box;
    transition: all 200ms cubic-bezier(0.075, 0.82, 0.165, 1);
}

input.has-icon {
    padding-left: var(--space-7);
}

input:hover {
    box-shadow: inset 0 0 0 1px rgba(255, 255, 255, 0.2);
}

input:focus {
    outline: none;
    box-shadow: inset 0 0 0 1px rgba(255, 255, 255, 0.5);
}
</style>
