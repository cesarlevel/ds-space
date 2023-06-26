<script setup>
import Icon from './Icon.vue';
import {watch} from 'vue';

const props = defineProps({
    modelValue: String,
    label: String,
    icon: {
        type: String,
        default: null,
    },
    options: {
        type: Array,
        default: () => [],
    },
});

const emit = defineEmits(['update:modelValue']);
</script>

<template>
  <div class="select-wrapper">
    <label v-if="props.label">Label</label>
    <Icon class="select-icon" :icon="icon"/>
    <select :value="modelValue" @input="$emit('update:modelValue', $event.target.value)" :class="props.icon ? 'has-icon' : ''">
        <option :value="item.value" v-for="item in props.options">{{item.value}}</option>
    </select>
    <Icon class="caret-icon" icon="c-d"/>
  </div>
</template>

<style scoped>
.select-wrapper {
    position: relative;
}

.select-icon, 
.caret-icon {
    position: absolute;
    top: 50%;
    left: var(--space-3);
    transform: translateY(-50%);
}

.caret-icon {
    left: calc(100% - 23px);
}

select {
    padding: var(--space-3) var(--space-4);
    width: 100%;
    background: transparent;
    border: none;
    box-shadow: inset 0 0 0 1px rgba(255, 255, 255, 0);
    box-sizing: border-box;
    transition: all 300ms cubic-bezier(0.075, 0.82, 0.165, 1);
    -webkit-appearance: none;
    -moz-appearance: none;
    -ms-appearance: none;
    -o-appearance: none;
    appearance: none;
}

select.has-icon {
    padding-left: var(--space-7);
}

select:hover {
    box-shadow: inset 0 0 0 1px rgba(255, 255, 255, 0.2);
}

select:focus {
    outline: none;
    box-shadow: inset 0 0 0 1px rgba(255, 255, 255, 0.5);
}
</style>
