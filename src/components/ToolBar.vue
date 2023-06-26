<script setup>
import { inject, ref, watch } from 'vue'
import Input from './Input.vue';
import Select from './Select.vue';
import Icon from './Icon.vue';
import Element from './Element.vue';

const state = inject('state');
const focusedElement = inject('focusedElement');
const heading1 = ref(null);
const paragraph = ref(null);
const button = ref(null);
const inputLabel = ref(null);
const input = ref(null);
const card = ref(null);
const cardHeading = ref(null);
const cardParagraph = ref(null);
const chip = ref(null);

function addSize() {
  state.sizes.push({
    name: state.sizes.length + 1,
    value: state.sizes.at(-1).value * state.multiplier,
  });
}

function deleteValue(index) {
  state.sizes.splice(index, 1);
}

function changeUnits(value, unit) {
  const v = parseFloat(value);
  if (isNaN(v)) {
    return value;
  }
  return unit === 'rem' ? `${v / 16}` : `${v * 16}`;
}

function updateStateUnits(units) {
  const updatedComponentsValues = state.components.map(component => {
    return Object.entries(component).reduce((acc, [cLabel, cValue]) => (
      {
        ...acc,
        [cLabel]: changeUnits(cValue, state.units)
      }
    ), {});
  });
  const updatedSizes = state.sizes.map(item => ({...item, value: changeUnits(item.value, state.units)}));

  state.sizes = updatedSizes;
  state.components = updatedComponentsValues;
  state.fontSize = changeUnits(state.fontSize, state.units);
}

watch(focusedElement, (elName) => {
  [heading1, paragraph, button, inputLabel, input, card, cardHeading, cardParagraph, chip].forEach(el => el.value.classList.remove('focused'));
  switch (elName) {
    case 'heading1':
      heading1.value.scrollIntoView({behavior: 'smooth'});
      heading1.value.classList.add('focused');
      break;
    case 'paragraph':
      paragraph.value.scrollIntoView({behavior: 'smooth'});
      paragraph.value.classList.add('focused');
      break;
    case 'button':
      button.value.scrollIntoView({behavior: 'smooth'});
      button.value.classList.add('focused');
      break;
    case 'inputLabel':
      inputLabel.value.scrollIntoView({behavior: 'smooth'});
      inputLabel.value.classList.add('focused');
      break;
    case 'input':
      input.value.scrollIntoView({behavior: 'smooth'});
      input.value.classList.add('focused');
      break;
    case 'card':
      card.value.scrollIntoView({behavior: 'smooth'});
      card.value.classList.add('focused');
      break;
    case 'cardHeading':
      cardHeading.value.scrollIntoView({behavior: 'smooth'});
      cardHeading.value.classList.add('focused');
      break;
    case 'cardParagraph':
      cardParagraph.value.scrollIntoView({behavior: 'smooth'});
      cardParagraph.value.classList.add('focused');
      break;
    case 'chip':
      chip.value.scrollIntoView({behavior: 'smooth'});
      chip.value.classList.add('focused');
      break;
  
    default:
      break;
  }
});
</script>

<template>
  <div id="dss-tool-bar">
    <small>Units</small>
    <Select :options="[{value: 'px'}, {value: 'rem'}]" v-model="state.units" @change="updateStateUnits(state.units)" />
    <div class="divider"></div>
    <small>Font size</small>
    <Input type="number" v-model="state.fontSize" :append="state.units" />
    <div class="divider"></div>
    <small>Identifier</small>
    <Input type="string" v-model="state.identifier" />
    <div class="divider"></div>
    <small>Multiplier</small>
    <Select :options="[{value: 1.5}]" v-model="state.multiplier" />
    <div class="divider"></div>
    <small>Base sizes</small>
    <div class="sizes-control-wrapper" v-for="(size, index) in state.sizes" :key="index">
      <Input type="number" v-model="size.value" />
      <button @click="deleteValue(index)">
        <Icon icon="trash" />
      </button>
    </div>
    <button class="add-size" @click="addSize"><Icon icon="plus" /> Add size</button>
    <div class="divider"></div>
    <div ref="heading1">
      <Element label="Heading 1" :options="state.sizes" v-model="state.components[0]"/>
    </div>
    <div class="divider"></div>
    <div ref="paragraph">
      <Element label="paragraph" :options="state.sizes" v-model="state.components[1]"/>
    </div>
    <div class="divider"></div>
    <div ref="button">
      <Element label="Button" :options="state.sizes" v-model="state.components[2]"/>
    </div>
    <div class="divider"></div>
    <div ref="inputLabel">
      <Element label="Input label" :options="state.sizes" v-model="state.components[3]"/>
    </div>
    <div class="divider"></div>
    <div ref="input">
      <Element label="Input" :options="state.sizes" v-model="state.components[4]"/>
    </div>
    <div class="divider"></div>
    <div ref="card">
      <Element label="Card" :options="state.sizes" v-model="state.components[5]"/>
    </div>
    <div class="divider"></div>
    <div ref="cardHeading">
      <Element label="Card heading" :options="state.sizes" v-model="state.components[6]"/>
    </div>
    <div class="divider"></div>
    <div ref="cardParagraph">
      <Element label="Card paragraph" :options="state.sizes" v-model="state.components[7]"/>
    </div>
    <div class="divider"></div>
    <div ref="chip">
      <Element label="Chip" :options="state.sizes" v-model="state.components[8]"/>
    </div>
  </div>
</template>

<style scoped>
  #dss-tool-bar {
    overflow-y: auto;
    padding: var(--space-6);
    border-right: 1px solid color-mix(in srgb, var(--color-primary) 90%, #ffffff);
  }

  #dss-tool-bar > div {
    transition: all 0.1s ease-in-out;
  }

  .sizes-control-wrapper {
    display: flex;
    align-items: center;
  }

  .sizes-control-wrapper > div {
    width: 100%;
  }

  button.add-size {
    margin-top: var(--space-4);
  }

  button.add-size .icon {
    margin-right: var(--space-2);
  }

  .focused {
    background: color-mix(in srgb, var(--color-primary) 95%, #ffffff);
    margin: calc(-1 * var(--space-4)) calc(-1 * var(--space-6));
    padding: var(--space-4) var(--space-6);
  }
</style>
