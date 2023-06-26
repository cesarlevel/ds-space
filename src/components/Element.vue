<script setup>
import Select from './Select.vue';

const props = defineProps({
    modelValue: String,
    label: String,
    options: {
        type: Array,
        default: () => [],
    },
});

const emit = defineEmits(['update:modelValue']);
</script>

<template>
  <div class="element-wrapper">
    <small>{{ props.label }}</small>
    <div class="element-padding-wrapper">
        <Select icon="vertical-space" :options="props.options" v-model="modelValue.vp" @input="$emit('update:modelValue.vp', $event.target.value)" />
        <Select icon="horizontal-space" :options="props.options" v-model="modelValue.hp" @input="$emit('update:modelValue.hp', $event.target.value)" />
    </div>
    <div class="element-margin-wrapper">
        <Select icon="m-r" :options="props.options" v-model="modelValue.mr" @input="$emit('update:modelValue.mr', $event.target.value)" />
        <Select icon="m-b" :options="props.options" v-model="modelValue.mb" @input="$emit('update:modelValue.mb', $event.target.value)" />
    </div>
  </div>
</template>

<style scoped>
.element-padding-wrapper,
.element-margin-wrapper  {
    display: flex;
    align-items: center;
}

.element-wrapper h3 {
    margin-bottom: var(--space-3);
}

.element-padding-wrapper > *,
.element-margin-wrapper > * {
    flex: 1 0 auto;
}
</style>
