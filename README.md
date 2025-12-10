# 🎨 Color Palette Generator

An interactive Vue.js web application for creating, managing, and exporting color palettes. A useful tool for designers, developers, and anyone working with visual content.

![Basic Generator](https://github.com/user-attachments/assets/7c4194e6-3f55-4565-8ae6-87f2eea56711)

## 🚀 Features

### Practice 27: Basic Functionality

#### Palette Generation System
- **Random Palette Generation**: Generate 5 harmonious colors with a single click
- **Horizontal Color Display**: Colors displayed as cards in a horizontal strip
- **HEX Display**: Each color shows its HEX value (e.g., #FF6B6B)

#### Individual Color Management
- **Click to Copy**: Click on any color card to copy its HEX value to clipboard
- **Copy Notification**: Visual feedback when color is successfully copied
- **Lock Colors**: Pin favorite colors to keep them when generating new palettes

#### Basic Configuration Tools
- **Adjustable Count**: Choose between 3, 5, or 7 colors in your palette
- **Format Toggle**: Switch between HEX and RGB display formats
- **Local Storage**: Current palette automatically saved to localStorage

#### Simple Previewer
- **UI Preview**: See palette in mock interface elements (button, card, heading)
- **Light/Dark Mode**: Toggle background to test color contrast

### Practice 28: Advanced Features

![Advanced Tools](https://github.com/user-attachments/assets/592cee2a-4566-4eb6-9b6b-60f6abcb9c28)

#### Advanced Generation
- **Base Color Generation**: Generate palettes from a selected base color
- **Palette Types**:
  - Analogous: Colors adjacent on the color wheel
  - Monochromatic: Variations of a single hue
  - Triadic: Three colors equally spaced on the color wheel
  - Complementary: Opposite colors on the color wheel
- **Mood-Based Generation**:
  - 🌊 Calm: Blues and greens with lower saturation
  - ⚡ Energetic: Reds, oranges, and yellows with high saturation
  - 💼 Professional: Blues with moderate saturation

#### Analysis & Accessibility Tools
- **WCAG Contrast Checker**: Test contrast ratios between any two colors
- **Accessibility Levels**: Shows AA/AAA compliance for normal and large text
- **Visual Preview**: See selected color combinations in real-time
- **Recommendations**: Warnings when colors don't meet accessibility standards

#### Palette Library Management
- **Save Palettes**: Store palettes with custom names
- **Tagging System**: Add comma-separated tags for organization
- **Search & Filter**: Find palettes by name or tags
- **Favorites**: Mark palettes as favorites for quick access
- **Load & Edit**: Reload saved palettes for further editing
- **Delete**: Remove unwanted palettes

#### Export & Integration
- **Multiple Export Formats**:
  - CSS Variables: `:root` format for CSS
  - SCSS Variables: `$variable` format for Sass
  - Tailwind Config: Ready-to-use Tailwind configuration
  - JSON: Structured data format
- **One-Click Copy**: Copy generated code to clipboard
- **Real-time Preview**: See export code update as you modify palettes

## 🛠️ Technical Stack

- **Vue 3**: Using Composition API with `<script setup>`
- **Vue Router**: Navigation between Basic and Advanced views
- **Vite**: Fast development and build tool
- **Reactive State Management**: Using Vue's reactivity system
- **localStorage**: Persistent data storage
- **Modern CSS**: Scoped styles with transitions

## 📦 Installation

```bash
# Clone the repository
git clone <repository-url>
cd Front5

# Install dependencies
npm install

# Run development server
npm run dev

# Build for production
npm run build

# Preview production build
npm run preview
```

## 🎯 Usage

### Basic Generator Page

1. **Generate a Palette**: Click the "Generate Random Palette" button
2. **Adjust Settings**: Choose number of colors (3, 5, or 7) and format (HEX/RGB)
3. **Copy Colors**: Click on any color card to copy its value
4. **Lock Colors**: Click the lock icon to keep specific colors when regenerating
5. **Test UI**: View your palette applied to sample UI components
6. **Toggle Background**: Switch between light and dark backgrounds for contrast testing

### Advanced Tools Page

1. **Generate from Base Color**: 
   - Pick a base color using the color picker
   - Select a palette type (Analogous, Monochromatic, etc.)
   - Click "Generate from Base Color"

2. **Generate by Mood**:
   - Click one of the mood buttons (Calm, Energetic, Professional)
   - Palette automatically generates with appropriate color characteristics

3. **Check Accessibility**:
   - Select foreground and background colors from dropdowns
   - View contrast ratio and WCAG compliance levels
   - See visual preview of text on background

4. **Export Palette**:
   - Choose export format (CSS, SCSS, Tailwind, JSON)
   - Click "Copy to Clipboard" to use in your project

5. **Save & Manage Palettes**:
   - Enter a name and tags for your palette
   - Click "Save Current Palette"
   - Use search to find saved palettes
   - Load, favorite, or delete palettes as needed

## 🎨 Color Utility Functions

The application includes comprehensive color manipulation utilities:

- HSL to HEX conversion
- HEX to RGB conversion
- RGB to HSL conversion
- Contrast ratio calculation (WCAG 2.0)
- Relative luminance calculation
- Accessibility level determination

## 📱 Responsive Design

The application is fully responsive and works on:
- Desktop computers
- Tablets
- Mobile devices

## 🔒 Data Persistence

- Current palette saved to localStorage automatically
- Saved palettes persist across browser sessions
- No server required - all data stored locally

## 🌐 Browser Support

- Modern browsers (Chrome, Firefox, Safari, Edge)
- Requires JavaScript enabled
- Clipboard API support for copy functionality

## 📝 Project Structure

```
src/
├── components/
│   ├── ColorCard.vue           # Individual color display card
│   ├── PalettePreview.vue      # UI mockup preview
│   ├── Notification.vue        # Toast notifications
│   ├── AccessibilityChecker.vue # WCAG contrast checker
│   ├── ExportPanel.vue         # Export functionality
│   └── SavedPalettes.vue       # Palette library
├── views/
│   ├── Generator.vue           # Basic generator page
│   └── Advanced.vue            # Advanced tools page
├── router/
│   └── index.js                # Vue Router configuration
├── utils/
│   └── colorUtils.js           # Color manipulation utilities
├── App.vue                     # Main app component
├── main.js                     # App entry point
└── style.css                   # Global styles
```

## 🎓 Learning Objectives Covered

### Practice 27 (Basic)
✅ Vue 3 Composition API usage  
✅ Reactive state management  
✅ v-for, v-if, v-model directives  
✅ Computed properties  
✅ Event handling  
✅ localStorage integration  

### Practice 28 (Advanced)
✅ Vue Router implementation  
✅ Component props and emits  
✅ Custom v-model components  
✅ Watchers for reactive changes  
✅ Advanced color theory algorithms  
✅ WCAG accessibility standards  

## 🤝 Contributing

Feel free to submit issues and enhancement requests!

## 📄 License

This project is created for educational purposes.

## 👨‍💻 Author

Created as part of the Vue.js Color Palette Generator project - Practices 27 & 28.
