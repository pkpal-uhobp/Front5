<template>
  <div class="advanced-view">
    <h1>Advanced Palette Tools</h1>
    
    <div class="advanced-controls">
      <div class="control-section">
        <h3>Generate from Base Color</h3>
        <div class="base-color-controls">
          <input 
            type="color" 
            v-model="baseColor" 
            class="color-picker"
          />
          <input 
            type="text" 
            v-model="baseColor" 
            placeholder="#000000"
            class="color-input"
          />
        </div>
        
        <div class="palette-type-selector">
          <label>Palette Type:</label>
          <select v-model="paletteType">
            <option value="analogous">Analogous</option>
            <option value="monochromatic">Monochromatic</option>
            <option value="triadic">Triadic</option>
            <option value="complementary">Complementary</option>
          </select>
        </div>
        
        <button @click="generateFromBase" class="action-button">
          Generate from Base Color
        </button>
      </div>
      
      <div class="control-section">
        <h3>Generate by Mood</h3>
        <div class="mood-selector">
          <button 
            v-for="mood in moods" 
            :key="mood.value"
            @click="generateByMood(mood.value)"
            :class="['mood-button', mood.value]"
          >
            {{ mood.icon }} {{ mood.label }}
          </button>
        </div>
      </div>
    </div>
    
    <div class="palette-display">
      <ColorCard 
        v-for="color in colors"
        :key="color.id"
        :color="color"
        :display-format="displayFormat"
        @copy="handleCopy"
        @toggle-lock="toggleLock"
      />
    </div>
    
    <div class="tools-grid">
      <AccessibilityChecker :colors="colors" />
      <ExportPanel :colors="colors" @notify="showNotification" />
    </div>
    
    <div class="library-section">
      <SavedPalettes 
        :current-colors="colors" 
        @load="loadPalette"
        @notify="showNotification"
      />
    </div>
    
    <Notification :message="notification" />
  </div>
</template>

<script setup>
import { ref } from 'vue';
import ColorCard from '../components/ColorCard.vue';
import AccessibilityChecker from '../components/AccessibilityChecker.vue';
import ExportPanel from '../components/ExportPanel.vue';
import SavedPalettes from '../components/SavedPalettes.vue';
import Notification from '../components/Notification.vue';
import {
  generateAnalogousPalette,
  generateMonochromaticPalette,
  generateTriadicPalette,
  generateComplementaryPalette,
  generateMoodPalette,
  generateRandomPalette,
  copyToClipboard
} from '../utils/colorUtils';

const colors = ref(generateRandomPalette(5));
const baseColor = ref('#3498db');
const paletteType = ref('analogous');
const displayFormat = ref('HEX');
const notification = ref('');

const moods = [
  { value: 'calm', label: 'Calm', icon: '🌊' },
  { value: 'energetic', label: 'Energetic', icon: '⚡' },
  { value: 'professional', label: 'Professional', icon: '💼' }
];

const generateFromBase = () => {
  let newPalette;
  
  switch (paletteType.value) {
    case 'analogous':
      newPalette = generateAnalogousPalette(baseColor.value, 5);
      break;
    case 'monochromatic':
      newPalette = generateMonochromaticPalette(baseColor.value, 5);
      break;
    case 'triadic':
      newPalette = generateTriadicPalette(baseColor.value);
      break;
    case 'complementary':
      newPalette = generateComplementaryPalette(baseColor.value);
      break;
    default:
      newPalette = generateRandomPalette(5);
  }
  
  colors.value = newPalette;
  showNotification(`Generated ${paletteType.value} palette!`);
};

const generateByMood = (mood) => {
  colors.value = generateMoodPalette(mood, 5);
  showNotification(`Generated ${mood} palette!`);
};

const handleCopy = async (colorValue) => {
  const success = await copyToClipboard(colorValue);
  if (success) {
    notification.value = `Copied ${colorValue} to clipboard!`;
    setTimeout(() => {
      notification.value = '';
    }, 100);
  }
};

const toggleLock = (colorId) => {
  const color = colors.value.find(c => c.id === colorId);
  if (color) {
    color.locked = !color.locked;
  }
};

const loadPalette = (paletteColors) => {
  colors.value = JSON.parse(JSON.stringify(paletteColors));
};

const showNotification = (message) => {
  notification.value = message;
  setTimeout(() => {
    notification.value = '';
  }, 100);
};
</script>

<style scoped>
.advanced-view {
  max-width: 1200px;
  margin: 0 auto;
  padding: 2rem;
}

.advanced-view h1 {
  text-align: center;
  margin-bottom: 2rem;
  color: #212529;
}

.advanced-controls {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 1.5rem;
  margin-bottom: 2rem;
}

.control-section {
  padding: 1.5rem;
  background: white;
  border: 1px solid #dee2e6;
  border-radius: 8px;
}

.control-section h3 {
  margin-top: 0;
  margin-bottom: 1rem;
}

.base-color-controls {
  display: flex;
  gap: 1rem;
  margin-bottom: 1rem;
}

.color-picker {
  width: 80px;
  height: 40px;
  border: 1px solid #ced4da;
  border-radius: 4px;
  cursor: pointer;
}

.color-input {
  flex: 1;
  padding: 0.5rem;
  border: 1px solid #ced4da;
  border-radius: 4px;
  font-family: monospace;
}

.palette-type-selector {
  margin-bottom: 1rem;
}

.palette-type-selector label {
  display: block;
  margin-bottom: 0.5rem;
  font-weight: 500;
}

.palette-type-selector select {
  width: 100%;
  padding: 0.5rem;
  border: 1px solid #ced4da;
  border-radius: 4px;
}

.action-button {
  width: 100%;
  padding: 0.75rem;
  background: #007bff;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 1rem;
  transition: background 0.2s;
}

.action-button:hover {
  background: #0056b3;
}

.mood-selector {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
}

.mood-button {
  padding: 0.75rem;
  border: 2px solid;
  border-radius: 4px;
  cursor: pointer;
  font-size: 1rem;
  transition: all 0.2s;
}

.mood-button.calm {
  background: #e3f2fd;
  border-color: #2196f3;
  color: #1565c0;
}

.mood-button.calm:hover {
  background: #2196f3;
  color: white;
}

.mood-button.energetic {
  background: #ffebee;
  border-color: #f44336;
  color: #c62828;
}

.mood-button.energetic:hover {
  background: #f44336;
  color: white;
}

.mood-button.professional {
  background: #f3e5f5;
  border-color: #9c27b0;
  color: #6a1b9a;
}

.mood-button.professional:hover {
  background: #9c27b0;
  color: white;
}

.palette-display {
  display: flex;
  gap: 0.5rem;
  margin-bottom: 2rem;
  border-radius: 8px;
  overflow: hidden;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
}

.tools-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(400px, 1fr));
  gap: 1.5rem;
  margin-bottom: 2rem;
}

.library-section {
  margin-top: 2rem;
}
</style>
