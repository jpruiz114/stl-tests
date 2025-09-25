# STL Viewer

A web-based 3D model viewer for STL files and other 3D formats, built with Three.js. This tool allows you to load, view, and interact with 3D models directly in your web browser.

**Live Demo**: [https://jeanpaulruizvallejo.com/stl-tests/](https://jeanpaulruizvallejo.com/stl-tests/)

## Features

### Core Functionality
- **STL File Support**: Load both ASCII and binary STL files
- **Interactive 3D Viewer**: Rotate, zoom, and pan around 3D models
- **Multiple View Modes**: Top, side, bottom, and diagonal camera angles
- **Material Options**: Toggle between solid and wireframe rendering
- **Auto-rotation**: Optional continuous rotation of the model

### Supported Formats
- **STL** (ASCII & Binary) - Primary format
- **OBJ** - Wavefront 3D object files
- **PLY** - Stanford Polygon Format
- **JSON** - Three.js JSON geometry format

### Interactive Controls
- **Mouse Controls**: 
  - Left-click and drag to rotate
  - Scroll wheel to zoom in/out
- **Touch Controls**: Full mobile device support
- **Button Controls**: 
  - Camera view presets (Top, Side, Bottom, Diagonal)
  - Zoom controls (+/-)
  - Rotation toggle (On/Off)
  - Material switching (Solid/Wireframe)

### Technical Features
- **WebGL Rendering**: Hardware-accelerated 3D graphics with Canvas fallback
- **Web Worker Support**: Non-blocking file parsing for better performance
- **Cross-browser Compatible**: Works on modern browsers with graceful degradation
- **Responsive Design**: Adapts to different screen sizes

## Getting Started

### Quick Setup
1. Clone or download this repository
2. Open `index.html` in a web browser
3. The demo will automatically load a sample STL file

### Loading Your Own Models
Currently, the viewer loads a predefined STL file (`models/Lego_Track_Curved_w_support.stl`). To load your own models:

1. Place your STL files in the `models/` directory
2. Update the file path in `index.html` around line 31:
   ```javascript
   url: "./models/your-model-name.stl"
   ```

## Project Structure

```
stl-tests/
├── index.html              # Main HTML file and UI
├── js/
│   ├── thingiview.js       # Main 3D viewer component
│   ├── thingiloader.js     # File loading and parsing logic
│   ├── binaryReader.js     # Binary file reading utility
│   ├── plane.js            # 3D plane geometry generator
│   ├── stats.js            # Performance statistics display
│   ├── Three.js            # Three.js 3D graphics library
│   └── jquery/             # jQuery library files
└── models/
    └── Lego_Track_Curved_w_support.stl  # Sample STL file
```

## Technical Details

### Dependencies
- **Three.js**: 3D graphics rendering library
- **jQuery 2.1.4**: DOM manipulation and AJAX requests
- **Custom Components**: 
  - `Thingiview`: Main viewer class
  - `Thingiloader`: File loading with Web Worker support
  - `BinaryReader`: Binary file parsing utility

### Browser Compatibility
- **Modern Browsers**: Chrome, Firefox, Safari, Edge (WebGL support)
- **Older Browsers**: Fallback to Canvas renderer
- **Mobile Devices**: Full touch control support

### Performance Optimizations
- Web Workers for non-blocking file parsing
- Vertex deduplication for memory efficiency
- Progressive loading with status updates
- Hardware-accelerated rendering when available

## Usage Examples

### Basic Usage
The viewer automatically initializes when the page loads:

```javascript
thingiView = new Thingiview("viewer");
thingiView.setObjectColor('#C0D8F0');
thingiView.initScene();
thingiView.loadSTLString(stlData);
```

### Customization Options
```javascript
// Set custom colors
thingiView.setObjectColor('#FF0000');        // Red model
thingiView.setBackgroundColor('#000000');    // Black background

// Control camera
thingiView.setCameraView('top');             // Top view
thingiView.setCameraZoom(10);                // Zoom in

// Toggle features
thingiView.setRotation(true);                // Enable auto-rotation
thingiView.setObjectMaterial('wireframe');   // Wireframe mode
thingiView.setShowPlane(false);              // Hide ground plane
```

## File Format Details

### STL Files
- **ASCII STL**: Text-based format with human-readable geometry data
- **Binary STL**: Compact binary format for faster loading
- **Auto-detection**: Automatically detects and handles both formats

### Other Formats
- **OBJ**: Supports vertices and faces (materials not implemented)
- **PLY**: Point cloud support with color information
- **JSON**: Three.js native geometry format

## Contributing

### Development Setup
1. Clone the repository
2. Use a local web server to serve files (required for AJAX requests)
3. Make changes to the JavaScript files
4. Test across different browsers and devices

### Architecture Notes
- `thingiview.js`: Core viewer logic, camera controls, rendering
- `thingiloader.js`: File parsing, format detection, Web Worker wrapper
- `binaryReader.js`: Low-level binary data reading utilities
- Worker pattern with fallback for browsers without Web Worker support

## License

This project appears to use components with various licenses:
- Three.js: MIT License
- jQuery: MIT License
- Stats.js: MIT License (by mrdoob)
- Custom components: Please verify licensing requirements

## Credits

- **Three.js**: [mrdoob](https://github.com/mrdoob) and contributors
- **Stats.js**: [mrdoob](https://github.com/mrdoob)
- **Binary Reader**: Originally by Jonas Raoni Soares Silva, refactored by [Vjeux](http://blog.vjeux.com/)
- **Plane Geometry**: Based on PaperVision3D implementation

---

**Note**: This is a client-side only application. All file processing happens in the browser, so your 3D models never leave your device.
