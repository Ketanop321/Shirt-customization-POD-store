# T-Shirt Customizer Documentation

## Project Overview

The T-Shirt Customizer is a React application built with Vite and Tailwind CSS that allows users to customize both the front and back of a t-shirt. Users can upload images, add text with various styling options, zoom and pan the t-shirt view, and save their customizations for later editing. The application features three different UI themes that can be switched using the Alt+Q keyboard shortcut.


### Project Structure

\`\`\`
tshirt-customizer/
├── public/
│   └── shirt-icon.png
├── src/
│   ├── App.jsx           # Main application component
│   ├── index.css         # Global styles and Tailwind imports
│   └── main.jsx          # Entry point
├── index.html            # HTML template
├── vite.config.js        # Vite configuration
├── tailwind.config.js    # Tailwind CSS configuration
├── postcss.config.js     # PostCSS configuration
├── package.json          # Dependencies and scripts
└── DOCUMENTATION.md      # This documentation file
\`\`\`

## Project Setup

### Prerequisites

- Node.js (v14.0.0 or higher)
- npm (v6.0.0 or higher)

### Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/yourusername/tshirt-customizer.git
   cd tshirt-customizer
   ```

2. Install dependencies:
   ```bash
   npm install
   ```

3. Start the development server:
   ```bash
   npm run dev
   ```

4. Build for production:
   ```bash
   npm run build
   ```

## Features

### 1. Front and Back Customization

- Toggle between front and back views
- Separate image uploads for front and back
- Separate text customization for front and back
- Independent positioning of text on front and back

### 2. Zoom and Pan Controls

- Zoom in and out of the t-shirt view
- Pan/move the t-shirt view to see different parts
- Reset zoom and pan to default
- Toggle between text positioning mode and pan mode

### 3. Body Profile Selection

- Height input (default: 180cm)
- Weight input (default: 80kg)
- Build dropdown (options: lean, regular, athletic, big; default: athletic)

### 4. Image Upload

- File upload button
- Drag and drop functionality
- Preview of uploaded image on the t-shirt (28% of page width)
- Smaller thumbnail preview in the upload area
- Remove image button



### 6. T-Shirt Customization

- Color selection (White, Black, Navy, Red, Green)
- Size selection (XS, S, M, L, XL, XXL)

### 7. Theme Switching

- Three distinct UI themes (Modern, Minimal, Vibrant)
- Alt+Q keyboard shortcut to switch themes
- Theme selector buttons

### 8. Saved Customizations

- Save customizations with automatic naming
- View list of saved customizations
- Load saved customizations for editing
- Delete saved customizations
- Create new designs

### 9. Form Validation

- Input validation for height and weight
- Text length and line count validation
- Required field validation

## Implementation Details

### Front and Back View Management

The application uses a state variable to track the current view and conditionally renders the appropriate content:

```jsx
const [currentView, setCurrentView] = useState('front')

// Computed values based on current view
const uploadedImage = currentView === 'front' ? frontImage : backImage
const setUploadedImage = currentView === 'front' ? setFrontImage : setBackImage
const textPosition = currentView === 'front' ? frontTextPosition : backTextPosition
const setTextPosition = currentView === 'front' ? setFrontTextPosition : setBackTextPosition
```

### Zoom and Pan Functionality

The application uses a combination of state variables and CSS transforms to implement zoom and pan functionality:

```jsx
const [zoomLevel, setZoomLevel] = useState(1)
const [panPosition, setPanPosition] = useState({ x: 0, y: 0 })
const [isPanning, setIsPanning] = useState(false)

// Zoom controls
const handleZoomIn = () => {
  setZoomLevel(prev => Math.min(prev + 0.1, 2))
}

const handleZoomOut = () => {
  setZoomLevel(prev => Math.max(prev - 0.1, 0.5))
}

// Pan controls
<Draggable
  position={panPosition}
  onStart={handlePanStart}
  onStop={handlePanStop}
  disabled={!isPanning}
>
  <div 
    style={{
      transform: `scale(${zoomLevel})`,
      transition: isPanning ? 'none' : 'transform 0.2s ease-out',
    }}
  >
    {/* T-shirt content */}
  </div>
</Draggable>
```



### Draggable Text

The application uses the `react-draggable` library to allow users to position text anywhere on the t-shirt:



### Saved Customizations

The application uses localStorage to persist saved customizations, including both front and back data:



## Challenges and Solutions

### 1. Managing Separate Front and Back State

**Challenge**: Keeping track of separate state for front and back views while maintaining a clean UI.

**Solution**: 
- Used a `currentView` state variable to toggle between front and back views
- Created computed values based on the current view to simplify the code
- Used separate state variables for front and back data (images, text positions, zoom levels, etc.)
- Created separate form instances for front and back data

### 2. Implementing Zoom and Pan Functionality

**Challenge**: Allowing users to zoom in/out and pan the t-shirt view while maintaining the ability to position text.

**Solution**:
- Used CSS transforms to implement zoom functionality
- Used react-draggable for pan functionality
- Added a toggle button to switch between text positioning mode and pan mode
- Disabled text dragging when in pan mode and vice versa

### 3. Saving and Loading Complex Customizations

**Challenge**: Persisting all customization data, including front and back views, zoom levels, and pan positions.

**Solution**:
- Stored all state variables in the saved customization object
- Used separate loading logic for front and back data
- Reset all state variables when creating a new design or loading a saved design

### 4. Maintaining UI Consistency

**Challenge**: Ensuring the UI remains consistent and intuitive when switching between front and back views.

**Solution**:
- Used clear visual indicators for the current view
- Showed/hid certain UI elements based on the current view
- Used consistent styling and layout for both views
- Added helpful tooltips and instructions

 0. **Template Designs**: Add pre-made template designs that users can customize.

## Conclusion

The T-Shirt Customizer is a feature-rich application that allows users to create personalized t-shirt designs with ease. It provides a user-friendly interface with front and back customization, zoom and pan functionality, drag-and-drop text positioning, and the ability to save and edit customizations. The application is built with modern web technologies and follows best practices for responsive design and user experience.