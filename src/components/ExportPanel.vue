<template>
  <div class="export-panel">
    <h3>Export Palette</h3>
    
    <div class="export-format-selector">
      <label>
        <input type="radio" value="css" v-model="selectedFormat" />
        CSS Variables
      </label>
      <label>
        <input type="radio" value="scss" v-model="selectedFormat" />
        SCSS Variables
      </label>
      <label>
        <input type="radio" value="tailwind" v-model="selectedFormat" />
        Tailwind Config
      </label>
      <label>
        <input type="radio" value="json" v-model="selectedFormat" />
        JSON
      </label>
    </div>
    
    <div class="export-preview">
      <pre><code>{{ exportCode }}</code></pre>
    </div>
    
    <button class="copy-button" @click="copyExportCode">
      📋 Copy to Clipboard
    </button>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue';
import { copyToClipboard } from '../utils/colorUtils';

const props = defineProps({
  colors: {
    type: Array,
    required: true
  }
});

const emit = defineEmits(['notify']);

const selectedFormat = ref('css');

const exportCode = computed(() => {
  if (!props.colors || props.colors.length === 0) return '';
  
  switch (selectedFormat.value) {
    case 'css':
      return generateCSSVariables();
    case 'scss':
      return generateSCSSVariables();
    case 'tailwind':
      return generateTailwindConfig();
    case 'json':
      return generateJSON();
    default:
      return '';
  }
});

const generateCSSVariables = () => {
  let code = ':root {\n';
  props.colors.forEach((color, index) => {
    code += `  --color-${index + 1}: ${color.hex};\n`;
  });
  code += '}';
  return code;
};

const generateSCSSVariables = () => {
  let code = '';
  props.colors.forEach((color, index) => {
    code += `$color-${index + 1}: ${color.hex};\n`;
  });
  return code;
};

const generateTailwindConfig = () => {
  let code = 'module.exports = {\n  theme: {\n    extend: {\n      colors: {\n';
  props.colors.forEach((color, index) => {
    code += `        'palette-${index + 1}': '${color.hex}',\n`;
  });
  code += '      }\n    }\n  }\n}';
  return code;
};

const generateJSON = () => {
  const palette = {};
  props.colors.forEach((color, index) => {
    palette[`color${index + 1}`] = color.hex;
  });
  return JSON.stringify(palette, null, 2);
};

const copyExportCode = async () => {
  const success = await copyToClipboard(exportCode.value);
  if (success) {
    emit('notify', 'Export code copied to clipboard!');
  } else {
    emit('notify', 'Failed to copy code');
  }
};
</script>

<style scoped>
.export-panel {
  padding: 1.5rem;
  border: 1px solid #dee2e6;
  border-radius: 8px;
  background: white;
}

.export-panel h3 {
  margin-top: 0;
  margin-bottom: 1rem;
}

.export-format-selector {
  display: flex;
  gap: 1rem;
  margin-bottom: 1rem;
  flex-wrap: wrap;
}

.export-format-selector label {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  cursor: pointer;
}

.export-format-selector input[type="radio"] {
  cursor: pointer;
}

.export-preview {
  background: #f8f9fa;
  border: 1px solid #dee2e6;
  border-radius: 4px;
  padding: 1rem;
  margin-bottom: 1rem;
  max-height: 300px;
  overflow-y: auto;
}

.export-preview pre {
  margin: 0;
  font-family: 'Courier New', monospace;
  font-size: 0.9rem;
  white-space: pre-wrap;
  word-wrap: break-word;
}

.export-preview code {
  color: #212529;
}

.copy-button {
  width: 100%;
  padding: 0.75rem;
  background: #007bff;
  color: white;
  border: none;
  border-radius: 4px;
  font-size: 1rem;
  cursor: pointer;
  transition: background 0.2s;
}

.copy-button:hover {
  background: #0056b3;
}
</style>
