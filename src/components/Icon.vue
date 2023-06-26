<script setup>
import { onMounted } from 'vue';
const props = defineProps({
    icon: {
        type: String,
        default: null,
    },
    color: {
        type: String,
        default: null,
    },
    stopPropagation: {
        type: Boolean,
        default: false,
    },
});

const emit = defineEmits(['click'])

const sprites = `
    <!-- Vertical space -->
    <svg xmlns="http://www.w3.org/2000/svg">
        <symbol id="icon-vertical-space">
            <svg xmlns="http://www.w3.org/2000/svg" width="15" height="15"><path fill-rule="evenodd" d="M14 13v1H1v-1h13Zm-3-9v7H4V4h7Zm-1 1H5v5h5V5Zm4-4v1H1V1h13Z"/></svg>
        </symbol>
    </svg>

    <!-- Horizontal space -->
    <svg xmlns="http://www.w3.org/2000/svg">
        <symbol id="icon-horizontal-space">
            <svg xmlns="http://www.w3.org/2000/svg" width="15" height="15"><path fill-rule="evenodd" d="M2 1v13H1V1h1Zm12 0v13h-1V1h1Zm-3 3v7H4V4h7Zm-1 1H5v5h5V5Z"/></svg>
        </symbol>
    </svg>

    <!-- Trash -->
    <svg xmlns="http://www.w3.org/2000/svg">
        <symbol id="icon-trash">            
            <svg xmlns="http://www.w3.org/2000/svg" width="15" height="15"><path fill-rule="evenodd" d="M10 3h3v1h-1v10H3V4H2V3h3V1h5v2Zm1 1H4v9h1V5h1v8h1V5h1v8h1V5h1v8h1V4ZM9 2H6v1h3V2Z"/></svg>
        </symbol>
    </svg>

    <!-- Margin top -->
    <svg xmlns="http://www.w3.org/2000/svg">
        <symbol id="icon-m-t">            
            <svg xmlns="http://www.w3.org/2000/svg" width="15" height="15"><path fill-rule="nonzero" d="M14 13v1H1v-1h13ZM6 4H5V3h1V2h1V1h1v1h1v1H8v9H7V3H6v1Zm6 1v1h-1V5h1ZM4 5v1H3V5h1Zm7-1v1h-1V4h1ZM5 4v1H4V4h1Zm5-1v1H9V3h1Z"/></svg>
        </symbol>
    </svg>

    <!-- Margin right -->
    <svg xmlns="http://www.w3.org/2000/svg">
        <symbol id="icon-m-r">                        
            <svg xmlns="http://www.w3.org/2000/svg" width="15" height="15"><path fill-rule="nonzero" d="M2 1v13H1V1h1Zm8 10v1H9v-1h1Zm1-1v1h-1v-1h1Zm1-1v1h-1V9h1Zm1-3v1h1v1h-1v1h-1V8H3V7h9V6h1Zm-1-1v1h-1V5h1Zm-1-1v1h-1V4h1Zm-1-1v1H9V3h1Z"/></svg>
        </symbol>
    </svg>

    <!-- Margin bottom -->
    <svg xmlns="http://www.w3.org/2000/svg">
        <symbol id="icon-m-b">            
            <svg xmlns="http://www.w3.org/2000/svg" width="15" height="15"><path fill-rule="nonzero" d="M8 3v9h1v1H8v1H7v-1H6v-1h1V3h1Zm2 8v1H9v-1h1Zm-4 0v1H5v-1h1Zm5-1v1h-1v-1h1Zm-6 0v1H4v-1h1Zm7-1v1h-1V9h1ZM4 9v1H3V9h1Zm10-8v1H1V1h13Z"/></svg>
        </symbol>
    </svg>

    <!-- Maring left -->
    <svg xmlns="http://www.w3.org/2000/svg">
        <symbol id="icon-m-l">            
            <svg xmlns="http://www.w3.org/2000/svg" width="15" height="15"><path fill-rule="nonzero" d="M14 1v13h-1V1h1ZM6 11v1H5v-1h1Zm-1-1v1H4v-1h1ZM4 9v1H3V9h1ZM3 6v1h9v1H3v1H2V8H1V7h1V6h1Zm1-1v1H3V5h1Zm1-1v1H4V4h1Zm1-1v1H5V3h1Z"/></svg>
        </symbol>
    </svg>

    <!-- Caret down -->
    <svg xmlns="http://www.w3.org/2000/svg">
        <symbol id="icon-c-d">            
            <svg xmlns="http://www.w3.org/2000/svg" width="15" height="15"><path fill-rule="nonzero" d="M8 9v1H7V9h1Zm1-1v1H8V8h1ZM7 8v1H6V8h1Zm3-1v1H9V7h1ZM6 7v1H5V7h1Zm5-1v1h-1V6h1ZM5 6v1H4V6h1Z"/></svg>
        </symbol>
    </svg>

    <!-- Plus -->
    <svg xmlns="http://www.w3.org/2000/svg">
        <symbol id="icon-plus">
            <svg xmlns="http://www.w3.org/2000/svg" width="15" height="15"><path fill-rule="evenodd" d="M8 3v4h4v1H8v4H7V8H3V7h4V3h1Z"/></svg>
        </symbol>
    </svg>
`;

function bubbleClick(evt) {
    if (props.stopPropagation) {
        evt.stopPropagation();
    }
    emit('click', evt);
}

onMounted(() => {
    if (!document.getElementById('icon-vertical-space')) {
      const spritesDiv = document.createElement('div');
      spritesDiv.style.display = 'none';
      spritesDiv.innerHTML = sprites;
      document.body.appendChild(spritesDiv);
    }
});

</script>

<template>
  <svg
    class="icon"
    @click="bubbleClick"
  >
    <use
      :xlink:href="`#icon-${props.icon}`"
      xmlns:xlink="http://www.w3.org/1999/xlink"
    ></use>
  </svg>
</template>

<style scoped>
.icon {
    width: 15px;
    height: 15px;
    fill: #ffffff;
    pointer-events: none;
}
</style>
