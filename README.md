# 3D Print Pattern Simulator

An interactive tool for visualizing and experimenting with 3D printing parameters, specifically designed for exploring extreme nozzle diameters and layer heights where the print pattern becomes an aesthetic element. **Now with G-code generation for actual printing!**

<img width="1420" height="1480" alt="image" src="https://github.com/user-attachments/assets/c0a94569-6f63-4d20-9a35-b088a421e772" />


## Overview

This simulator allows you to:
- Experiment with different nozzle diameters (0.2mm to 2.0mm)
- Test extreme layer heights (0.1mm to 3.0mm)
- Visualize various printing patterns (concentric, rectilinear, grid, honeycomb, spiral, Hilbert curve)
- Apply patterns to different geometric shapes
- See both the nozzle path and the actual extruded material volume
- **Generate production-ready G-code files for your 3D printer**
- **Configure printer-specific settings**

## Installation

### Requirements
- Python 3.6 or higher
- matplotlib
- numpy
- tkinter (usually included with Python)

### Setup
```bash
pip install matplotlib numpy
```

## Usage

### GUI Version with G-Code Export (RECOMMENDED)

```bash
python thicLayer.py.py
```

**Features:**
- ✨ Real-time parameter adjustment with sliders
- 🔄 Interactive 3D visualization you can rotate
- 🖨️ **G-code generation with printer configuration**
- ⚙️ **Built-in printer settings editor**
- 📂 **Load/save printer configurations**
- 💾 Export visualizations as images
- 📊 Status bar with helpful feedback
- 🎨 Scrollable interface for all controls

**Interface Layout:**
- **Left Panel**: All controls (scrollable)
  - Print parameters (nozzle, layer height, etc.)
  - Pattern and shape selection
  - Display options
  - Printer configuration section
  - G-code generation button
- **Right Panel**: 3D visualization
- **Bottom**: Status bar

**G-Code Features:**
- Load pre-configured printer profiles (Ender 3, Prusa, etc.)
- Edit all printer settings through GUI
- Save custom printer configurations
- Generate G-code with one click
- Automatic safety warnings

## Parameters Explained

### Nozzle Diameter
The diameter of the 3D printer nozzle. Larger nozzles allow faster printing and create more visible, sculptural layers. Typical range: 0.4mm (standard) to 1.5mm+ (artistic/structural).

### Layer Height
The vertical thickness of each layer. Extreme layer heights (0.5mm - 3.0mm) create highly visible, textured surfaces where the print pattern becomes a design element.

### Extrusion Width
The width of the extruded line. Usually 100-150% of nozzle diameter. Wider extrusion creates bolder, more pronounced patterns.

### Print Patterns

- **Concentric**: Follows the perimeter of the shape, creating rings
- **Rectilinear**: Straight lines that alternate direction each layer
- **Grid**: Perpendicular lines creating a grid structure
- **Honeycomb**: Hexagonal pattern, structurally efficient
- **Spiral**: Continuous spiral from center outward
- **Hilbert**: Space-filling Hilbert curve pattern

### Shapes

- **Cube**: Simple cubic form
- **Flat Square**: Single-layer square base (good for testing patterns)
- **Cylinder**: Circular form
- **Pyramid**: Tapered pyramid form
- **Vase**: Expanding vase shape

### Infill Density
Controls how densely the pattern fills the area (0-100%). Lower values create sparser, more open patterns. Higher values create denser patterns.

## Use Cases for Art/Design Education

### 1. Understanding Layer-Based Manufacturing
Students can visualize how 2D slices stack to create 3D forms, understanding the fundamental principle of additive manufacturing.

### 2. Exploring Pattern as Texture
With extreme layer heights, the toolpath becomes visible texture. Experiment with different patterns to create varied surface qualities.

### 3. Structural vs. Aesthetic Considerations
Compare how different patterns affect both structural properties and visual appearance.

### 4. Parametric Design Thinking
Adjust parameters to see immediate visual feedback, developing intuition for parametric design.

### 5. Digital Craft
Bridge digital code and physical making by understanding how parameters translate to physical results.

## Advanced Usage Examples

### Creating a Series of Pattern Comparisons

```bash
# Generate all patterns for comparison
for pattern in concentric rectilinear grid honeycomb hilbert spiral; do
  python 3d_print_simulator_cli.py --pattern $pattern --output pattern_${pattern}.png
done
```

### Exploring Extreme Parameters

```bash
# Ultra-thick layers (2mm) with large nozzle (1.8mm)
python 3d_print_simulator_cli.py --nozzle 1.8 --layer 2.0 --extrusion 2.5 --layers 8 --output extreme_thick.png

# Fine detail with small nozzle
python 3d_print_simulator_cli.py --nozzle 0.2 --layer 0.1 --extrusion 0.25 --layers 40 --infill 80 --output fine_detail.png
```

### Artistic Pattern Studies

```bash
# Dense spiral pattern
python 3d_print_simulator_cli.py --pattern spiral --shape flat_square --infill 100 --layer 0.8 --output art_spiral.png

# Sparse honeycomb structure
python 3d_print_simulator_cli.py --pattern honeycomb --infill 15 --layer 1.0 --output art_honeycomb.png
```

## Tips for Educational Use

1. **Start Simple**: Begin with default parameters and change one at a time to understand individual effects

2. **Compare Side by Side**: Generate multiple images with different parameters to discuss differences

3. **Physical Connection**: After simulating, try printing with similar parameters to connect digital and physical

4. **Pattern Recognition**: Have students predict what parameter changes will do before visualizing

5. **Design Intent**: Discuss how parameter choices affect both function and aesthetics

6. **Documentation**: Use the simulator to document design decisions and parameter explorations

## Technical Details

### Coordinate System
- Origin at center
- X, Y in horizontal plane
- Z vertical (build direction)
- Units in millimeters

### Visualization
- Green to purple color gradient represents layer progression
- Black lines show nozzle path (when enabled)
- Solid volumes show actual extruded material (when enabled)

### Performance Notes
- Higher layer counts increase computation time
- Complex patterns (honeycomb, Hilbert) are more computationally intensive
- Adjust DPI for quality vs. file size tradeoffs

## Troubleshooting

**Issue**: Visualization looks cluttered
- Solution: Reduce infill density or number of layers
- Try hiding nozzle path with `--no-path`

**Issue**: Pattern not visible
- Solution: Increase extrusion width and layer height
- Increase infill density

**Issue**: Slow generation
- Solution: Reduce number of layers or use simpler patterns
- Lower DPI for faster exports

## Extending the Simulator

The code is designed to be educational and extensible. Key areas for customization:

- Add new patterns in `generate_path_points()` method
- Create custom shapes
- Modify color schemes
- Add support for multi-material simulation
- Implement support structure visualization

## License

This tool is designed for educational use in art and design contexts.

## Credits

Created for interactive media, electronics, and programming education with a focus on making the 3D printing process visible and explorable.

# GUI User Guide - 3D Print Pattern Simulator

## Getting Started

### Launch the Application

```bash
python 3d_print_simulator_gui.py
```

The application window will open with:
- **Left panel**: Controls (scrollable)
- **Right panel**: 3D visualization
- **Bottom**: Status bar

## Interface Overview

### Main Controls Section

#### 1. Print Parameters
Adjust these sliders to change your print characteristics:

- **Nozzle Diameter** (0.2 - 2.0mm)
  - Controls the size of the nozzle opening
  - Larger = faster prints, more visible patterns
  - Start with 0.4mm (standard)

- **Layer Height** (0.1 - 3.0mm)
  - Vertical thickness of each layer
  - For artistic prints: 0.5 - 2.0mm
  - For standard prints: 0.2 - 0.4mm

- **Extrusion Width** (0.3 - 3.0mm)
  - Width of the extruded line
  - Usually 100-150% of nozzle diameter
  - Affects pattern visibility

- **Number of Layers** (5 - 50)
  - Total layers to simulate/print
  - Start small (10-15) for tests
  - More layers = taller object

- **Infill Density** (0 - 100%)
  - How densely the pattern fills space
  - 20-40% typical
  - Higher = stronger but slower

#### 2. Pattern Selection
Choose from six different patterns:
- **Concentric**: Follows the perimeter (organic look)
- **Rectilinear**: Parallel lines (classic 3D print look)
- **Grid**: Perpendicular lines (strong, structured)
- **Honeycomb**: Hexagonal pattern (efficient, beautiful)
- **Hilbert**: Space-filling curve (interesting texture)
- **Spiral**: Continuous spiral (decorative)

#### 3. Shape Selection
Choose the object shape:
- **Cube**: Simple cube form
- **Flat Square**: Single-layer square (great for testing)
- **Cylinder**: Round cylindrical form
- **Pyramid**: Tapered pyramid
- **Vase**: Expanding vase shape

#### 4. Display Options
Toggle what you see:
- ☑️ **Show Nozzle Path**: Black lines showing toolpath
- ☑️ **Show Extrusion Volume**: Colored 3D extrusions

### Visualization Controls

The 3D view shows your print with:
- **Color gradient**: Green (bottom) to purple (top) layers
- **Interactive rotation**: Click and drag to rotate view
- **Axes**: X, Y (horizontal), Z (vertical/build direction)

### Action Buttons

#### 🔄 Refresh Visualization
Manually updates the 3D view (also auto-updates when you change parameters)

#### 💾 Save Image
Export the current visualization as a PNG image:
1. Click the button
2. Choose location and filename
3. Image saved at 150 DPI

## G-Code Generation Features

### Printer Configuration

#### Current Config Display
Shows which printer profile is loaded (default: "Generic Printer")

#### 📂 Load Printer Config
Load a saved printer configuration:
1. Click "Load Printer Config"
2. Browse to a `.json` config file
3. Config loads automatically

**Included configs:**
- `printer_ender3.json` - Creality Ender 3
- `printer_prusa_mk3s.json` - Prusa i3 MK3S
- `printer_large_format.json` - Large format printer

#### ⚙️ Edit Printer Settings
Open the full settings editor:

**General Settings:**
- Printer Name
- Bed Size X, Y, Z (mm)

**Temperatures:**
- Nozzle Temperature (°C)
- Bed Temperature (°C)

**Filament:**
- Filament Diameter (1.75mm or 2.85mm)

**Retraction:**
- Retraction Distance (mm)
- Retraction Speed (mm/s)

**Speeds:**
- Travel Speed (mm/s) - non-printing moves
- Print Speed (mm/s) - printing moves
- First Layer Speed (mm/s) - slower for adhesion

**Other:**
- Z Offset
- Use Bed Leveling (checkbox)
- Bed Leveling Command (e.g., G29)
- Home Command (e.g., G28)
- Fan Speed (0-255)
- Enable Fan at Layer

**Usage:**
1. Click "Edit Printer Settings"
2. Modify values in the dialog
3. Click "Save" to apply
4. Settings saved to memory (not file)

#### 💾 Save Printer Config
Save your current settings:
1. Click "Save Printer Config"
2. Choose filename (e.g., `my_custom_printer.json`)
3. Settings saved as JSON file
4. Can reload anytime

### 🖨️ Generate G-Code

This is the main button for creating printable files!

**Steps:**
1. Set up your print parameters (nozzle, layers, pattern, etc.)
2. Load or configure your printer settings
3. Click "🖨️ Generate G-Code"
4. Choose save location and filename
5. G-code file is created

**Success Dialog Shows:**
- File location
- Number of G-code lines
- Number of layers
- Total print height
- Printer name
- Safety warning

**The G-code includes:**
- Printer initialization (homing, heating)
- Bed leveling (if configured)
- Nozzle priming
- Layer-by-layer toolpath
- Proper extrusion calculations
- Automatic retractions
- Print completion routine

## Typical Workflow

### For Visualization Only
1. Launch application
2. Adjust sliders to desired values
3. Select pattern and shape
4. View real-time 3D preview
5. Save image if desired

### For G-Code Generation
1. Launch application
2. Set print parameters (nozzle, layers, etc.)
3. Select pattern and shape
4. Preview in 3D visualization
5. Load appropriate printer config
6. (Optional) Edit printer settings
7. Generate G-code
8. Preview G-code in external viewer
9. Send to printer

### For Education/Experimentation
1. Start with default settings
2. Change ONE parameter at a time
3. Observe effects on visualization
4. Document interesting combinations
5. Generate G-code for physical tests
6. Compare digital vs. physical results

## Tips and Tricks

### Getting Good Results

**For Visualization:**
- Use "Show Extrusion Volume" for realistic appearance
- Hide "Show Nozzle Path" for cleaner images
- Adjust view angle by dragging in 3D window
- Save multiple angles for documentation

**For G-Code:**
- Always start with a test print (5-10 layers)
- Verify temperatures match your filament
- Check bed size matches your printer
- Preview G-code before printing (OctoPrint, etc.)
- Monitor first layer closely

**For Artistic Prints:**
- Use layer heights 0.5mm or higher
- Increase extrusion width for boldness
- Try spiral or honeycomb patterns
- Lower infill (20-40%) for visible patterns
- Use contrasting filament colors

**For Teaching:**
- Start with flat_square shape (simple)
- Compare same shape with different patterns
- Show effect of changing one parameter
- Generate series for side-by-side comparison
- Print and discuss physical vs. digital

### Keyboard Shortcuts

While focus is on the 3D view:
- **Click + Drag**: Rotate view
- **Right-click + Drag**: Pan view
- **Scroll**: Zoom in/out

### Performance

**If visualization is slow:**
- Reduce number of layers
- Use simpler patterns (concentric, rectilinear)
- Turn off "Show Extrusion Volume"
- Reduce infill density

**If G-code generation is slow:**
- This is normal for complex patterns
- Wait for status bar to show "Ready"
- Complex patterns = more G-code lines

## Troubleshooting

### "Config Not Found"
**Problem**: Trying to load non-existent config file
**Solution**: Check file path, use included configs as examples

### "Invalid Config"
**Problem**: Config file has incorrect JSON format
**Solution**: Use included configs as templates, check JSON syntax

### "Could not save config"
**Problem**: No write permission or invalid path
**Solution**: Save to your home directory or documents folder

### Visualization doesn't update
**Problem**: Parameters changed but view stays the same
**Solution**: Click "🔄 Refresh Visualization" button

### G-code generation takes long time
**Problem**: Many layers or complex pattern
**Solution**: This is normal - wait for status bar to show completion

### Application window too small
**Problem**: Can't see all controls
**Solution**: Maximize window, or scroll in left panel

### Can't find G-code file
**Problem**: Saved but don't know where
**Solution**: Check the path shown in success dialog, or save to desktop

## Safety Reminders

### Before Printing

⚠️ **CRITICAL**: Always preview G-code before sending to printer!

Use software like:
- OctoPrint
- Pronterface
- Simplify3D
- Online G-code viewers

### Check These Items

- [ ] Temperatures correct for your filament
- [ ] Bed size matches your printer
- [ ] First layer will stick (use adhesion aids)
- [ ] Print fits within bed boundaries
- [ ] All movements look correct in preview
- [ ] Emergency stop is accessible
- [ ] Printer will be supervised

### During Printing

- Monitor first layer closely (most critical!)
- Verify proper bed adhesion
- Check for stringing or oozing
- Listen for unusual sounds
- Be ready to emergency stop

### Material-Specific Temps

The default configs are for PLA. Adjust for other materials:

**PLA**: 190-220°C nozzle, 50-60°C bed
**PETG**: 230-250°C nozzle, 70-85°C bed
**ABS**: 230-260°C nozzle, 95-110°C bed
**TPU**: 210-230°C nozzle, 40-60°C bed

## Advanced Features

### Creating Custom Configs

1. Start with similar printer (Ender 3 for small printers, etc.)
2. Load that config
3. Click "Edit Printer Settings"
4. Modify all values for your printer
5. Click "Save"
6. Click "Save Printer Config" to create new file
7. Name it clearly (e.g., `my_ender3_modified.json`)

### Comparing Patterns

Generate multiple versions:
1. Set parameters
2. Choose pattern 1, generate G-code
3. Choose pattern 2, generate G-code
4. Compare files side-by-side
5. Print both for comparison

### Batch Generation Workflow

For systematic exploration:
1. Set base parameters
2. Generate and save G-code (pattern1_layer02.gcode)
3. Change one parameter
4. Generate and save (pattern1_layer04.gcode)
5. Continue varying parameters
6. Print series to document effects

## Examples

### Example 1: Quick Test Print
```
Pattern: Concentric
Shape: Flat Square
Layers: 5
Nozzle: 0.4mm
Layer Height: 0.2mm
Extrusion: 0.5mm
Infill: 20%
Printer: Ender 3
```
Result: Safe 1mm tall test square

### Example 2: Artistic Thick Layers
```
Pattern: Honeycomb
Shape: Cube
Layers: 12
Nozzle: 1.0mm
Layer Height: 0.8mm
Extrusion: 1.2mm
Infill: 40%
```
Result: Bold, visible honeycomb texture

### Example 3: Decorative Vase
```
Pattern: Spiral
Shape: Vase
Layers: 40
Nozzle: 0.4mm
Layer Height: 0.3mm
Extrusion: 0.5mm
Infill: 100%
```
Result: Continuous spiral vase form

## Resources

### Documentation
- `README.md` - Overview and installation
- `GCODE_GUIDE.md` - Comprehensive G-code reference
- `QUICK_REFERENCE.md` - One-page cheat sheet

### Example Files
- `printer_*.json` - Printer configuration examples
- `example_*.gcode` - Sample G-code outputs
- `example_*.png` - Sample visualizations

### External Tools
- **OctoPrint**: Web-based printer control and G-code preview
- **Pronterface**: Desktop 3D printer control
- **Cura**: Full-featured slicer (for comparison)
- **PrusaSlicer**: Another popular slicer

## Getting Help

### Check Status Bar
Bottom of window shows current operation status

### Error Messages
Dialog boxes explain what went wrong and suggest solutions

### Feedback
Test prints not working as expected?
- Review G-code in external viewer
- Check printer configuration values
- Verify temperatures for your filament
- Start with smaller test prints

## Version Information

This is the enhanced GUI version with G-code generation.
- Includes all visualization features
- Adds full G-code export
- Provides printer configuration management
- Offers settings editor interface

For command-line batch processing, see `3d_print_simulator_cli.py`
For simple visualization only, see `3d_print_simulator.py`

---

**Happy printing! 🎨🖨️**
