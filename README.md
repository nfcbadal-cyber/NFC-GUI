# Professional GUI Framework - Complete Documentation

**Version:** 1.0  
**Platform:** Roblox (Lua)  
**Theme:** Black & Electric Blue (Modern Dark Mode)

---

## Table of Contents

1. [Overview](#overview)
2. [Installation & Setup](#installation--setup)
3. [Core Components](#core-components)
4. [Window Management](#window-management)
5. [Components Guide](#components-guide)
6. [Theme & Customization](#theme--customization)
7. [Examples](#examples)
8. [API Reference](#api-reference)
9. [Performance Optimization](#performance-optimization)
10. [GitHub Deployment](#github-deployment)

---

## Overview

The Professional GUI Framework is a modern, production-ready UI library for Roblox that provides:

- **Professional Aesthetics** – Black background with electric blue accents
- **Smooth Animations** – Tweened transitions for all interactive elements
- **Responsive Components** – Toggles, sliders, dropdowns, and sections
- **Draggable Windows** – Full window management with minimize/maximize
- **Tab System** – Organize content across multiple tabs
- **Zero Dependencies** – Pure Roblox Lua/API (no external libraries needed)

**Perfect for:** Admin panels, exploit GUIs, script management hubs, and modern game UIs.

---

## Installation & Setup

### Step 1: Load the Framework

Copy the entire framework into your Roblox script. The framework automatically creates a ScreenGui in the player's PlayerGui.

```lua
-- Load framework (paste entire code before creating UI)
local ProfessionalUI = loadstring(game:HttpGet("https://raw.githubusercontent.com/nfcbadal-cyber/NFC-GUI/main/Professional-GUI-Roblox"))()
-- ... [paste all framework code here]
```

### Step 2: Create Your First Window

```lua
local UI = ProfessionalUI:CreateWindow("MY AWESOME HUB", {
    Width = 700,
    Height = 450
})
```

### Step 3: Add Tabs

```lua
local mainTab = UI:CreateTab("Main", "rbxassetid://6023426920")
local settingsTab = UI:CreateTab("Settings", "rbxassetid://6023426923")
```

### Step 4: Add Components

```lua
ProfessionalUI:CreateToggle(mainTab, {
    Text = "Feature Enabled",
    Default = true,
    Y = 10,
    Callback = function(value)
        print("Toggled:", value)
    end
})
```

### Step 5: Setup Keybind

```lua
UserInputService.InputBegan:Connect(function(input)
    if input.KeyCode == Enum.KeyCode.RightShift then
        UI:Toggle()
    end
end)
```

---

## Core Components

### 1. **Window Management**

The main window serves as the container for all your UI elements. It includes:
- Draggable title bar
- Minimize/maximize functionality
- Smooth animations
- Professional drop shadow
- Minimize to icon system with pulsing animation

#### Window Properties

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `Width` | number | 600 | Window width in pixels |
| `Height` | number | 400 | Window height in pixels |
| `Title` | string | "Professional UI" | Window title text |

#### Window Methods

```lua
local window = ProfessionalUI:CreateWindow("Title", config)

window:Toggle()      -- Toggle minimize/maximize
window:Minimize()    -- Minimize window
window:Maximize()    -- Maximize window
window:CreateTab(name, iconAsset) -- Create new tab
```

---

## Window Management

### Creating a Window

```lua
local UI = ProfessionalUI:CreateWindow("ELITE HUB", {
    Width = 700,      -- Window width
    Height = 450      -- Window height
})
```

### Window Features

#### Draggable Title Bar
- Click and drag the title bar to move the window
- Smooth tweening during drag (buttery smooth feel)
- Visual feedback on drag

#### Minimize/Maximize System
- Click the minimize button (−) to hide window and show icon
- Icon pulses gently when minimized
- Click icon to restore window
- Icon is also draggable

#### Close Button
- Click the X button to completely destroy the window
- All connected listeners are cleaned up

### Minimize Animation Flow

```
Window visible → Click minimize → 
Smooth shrink animation → 
Window hidden + Icon appears (18px) → 
Icon pulses continuously
```

### Icon System

When minimized:
- Icon appears at 18px with rounded corners
- Background color matches theme accent with transparency
- Border stroke for definition
- Continuous pulse animation (18px → 22px)
- Click to restore (animates from icon size back to full window)

---

## Components Guide

### 1. **Toggle Component**

A smooth, animated switch for on/off states.

```lua
local toggle = ProfessionalUI:CreateToggle(parent, {
    Text = "Aimbot Enabled",
    Default = true,
    Y = 50,
    Callback = function(value)
        print("Aimbot is now:", value)
    end
})

-- Control the toggle programmatically
toggle:Set(false)
local state = toggle:Get()
```

**Features:**
- Animated knob movement (0.15s duration)
- Track color change on toggle (tertiary → accent)
- Hover effect on knob
- Customizable position (Y-axis)

**Visual States:**
- OFF: Gray track, white knob on left
- ON: Blue track, white knob on right
- HOVER: Knob highlights in blue

---

### 2. **Slider Component**

Smooth, interactive slider with value display and live feedback.

```lua
local slider = ProfessionalUI:CreateSlider(parent, {
    Text = "FOV Size",
    Min = 0,
    Max = 360,
    Default = 120,
    Increment = 5,      -- Snap to nearest 5
    Y = 100,
    Callback = function(value)
        print("FOV:", value)
    end
})

-- Control programmatically
slider:Set(180)
local currentValue = slider:Get()
```

**Features:**
- Real-time value display (top right)
- Draggable knob with snap-to-grid
- Smooth fill animation
- Large hitbox for easy interaction
- Knob expands on hover (16px → 20px)

**Interaction:**
- Click and drag knob
- Or click anywhere on track to jump to that position
- Value displays as you drag
- Callback fires on release

---

### 3. **Dropdown Component**

Smooth dropdown menu with animated list expansion.

```lua
local dropdown = ProfessionalUI:CreateDropdown(parent, {
    Text = "Hitbox Priority",
    Options = {"Head", "Torso", "Random", "Nearest"},
    Default = "Head",
    Y = 150,
    Callback = function(option)
        print("Selected:", option)
    end
})

-- Control programmatically
dropdown:Set("Torso")
local selected = dropdown:Get()
```

**Features:**
- Smooth list expansion animation (0.2s)
- Arrow rotates on open/close
- Options highlight on hover
- Click to select and auto-close
- Smooth size animation

**Visual Flow:**
```
Closed state (height 0) →
Click button →
List expands smoothly (0.2s) →
Arrow flips up
Click option →
List collapses (0.15s) →
Arrow flips down
```

---

### 4. **Section Divider**

Organizational divider with label for grouping related controls.

```lua
ProfessionalUI:CreateSection(parent, "COMBAT", 10)
-- Creates a section with "COMBAT" label and accent line
```

**Features:**
- Accent-colored line at bottom
- Bold section label
- Helps organize controls visually
- Fully transparent background

---

## Theme & Customization

### Default Theme (Black & Electric Blue)

```lua
local Theme = {
    Background = Color3.fromRGB(10, 10, 15),       -- Deep black
    Secondary = Color3.fromRGB(20, 20, 30),        -- Slightly lighter
    Tertiary = Color3.fromRGB(30, 30, 40),         -- Medium depth
    Accent = Color3.fromRGB(0, 160, 255),          -- Electric blue
    AccentDark = Color3.fromRGB(0, 120, 200),      -- Darker blue
    Text = Color3.fromRGB(255, 255, 255),          -- Pure white
    TextMuted = Color3.fromRGB(180, 180, 180),     -- Gray
    Success = Color3.fromRGB(80, 255, 120),        -- Green
    Error = Color3.fromRGB(255, 80, 80)            -- Red
}
```

### Customizing the Theme

To change the theme, modify the Theme table before creating UI elements:

```lua
Theme.Accent = Color3.fromRGB(255, 100, 0)        -- Change to orange
Theme.Background = Color3.fromRGB(20, 20, 20)     -- Slightly lighter black
```

### Corner Radius

All components use 12px rounded corners by default:

```lua
local CornerRadius = UDim.new(0, 12)  -- Customize here
```

---

## Examples

### Example 1: Basic Combat Hub

```lua
local UI = ProfessionalUI:CreateWindow("COMBAT HUB", {Width = 700, Height = 450})
local mainTab = UI:CreateTab("Main")

ProfessionalUI:CreateSection(mainTab, "AIM ASSIST", 10)
local y = 50

local aimbot = ProfessionalUI:CreateToggle(mainTab, {
    Text = "Aimbot",
    Default = false,
    Y = y,
    Callback = function(enabled)
        if enabled then
            print("Aimbot activated!")
        end
    end
})
y = y + 50

local fov = ProfessionalUI:CreateSlider(mainTab, {
    Text = "Field of View",
    Min = 10,
    Max = 180,
    Default = 45,
    Y = y,
    Callback = function(value)
        print("FOV changed to:", value)
    end
})
y = y + 60

local target = ProfessionalUI:CreateDropdown(mainTab, {
    Text = "Target Part",
    Options = {"Head", "Neck", "Chest", "Legs"},
    Default = "Head",
    Y = y,
    Callback = function(part)
        print("Targeting:", part)
    end
})

-- Keybind to toggle window
UserInputService.InputBegan:Connect(function(input)
    if input.KeyCode == Enum.KeyCode.RightShift then
        UI:Toggle()
    end
end)
```

### Example 2: Multi-Tab Settings Panel

```lua
local UI = ProfessionalUI:CreateWindow("SETTINGS", {Width = 800, Height = 500})

-- Create tabs
local generalTab = UI:CreateTab("General")
local visualsTab = UI:CreateTab("Visuals")
local advancedTab = UI:CreateTab("Advanced")

-- GENERAL TAB
ProfessionalUI:CreateSection(generalTab, "GENERAL", 10)
ProfessionalUI:CreateToggle(generalTab, {
    Text = "Enable Script",
    Default = true,
    Y = 50,
    Callback = function(v) print("Script:", v) end
})
ProfessionalUI:CreateSlider(generalTab, {
    Text = "Update Rate (ms)",
    Min = 10,
    Max = 1000,
    Default = 100,
    Y = 100,
    Callback = function(v) print("Update rate:", v) end
})

-- VISUALS TAB
ProfessionalUI:CreateSection(visualsTab, "DISPLAY", 10)
ProfessionalUI:CreateToggle(visualsTab, {
    Text = "Show Hitboxes",
    Default = false,
    Y = 50,
    Callback = function(v) print("Hitboxes:", v) end
})
ProfessionalUI:CreateDropdown(visualsTab, {
    Text = "Theme",
    Options = {"Dark", "Light", "Custom"},
    Default = "Dark",
    Y = 100,
    Callback = function(v) print("Theme:", v) end
})

-- ADVANCED TAB
ProfessionalUI:CreateSection(advancedTab, "ADVANCED", 10)
ProfessionalUI:CreateToggle(advancedTab, {
    Text = "Debug Mode",
    Default = false,
    Y = 50,
    Callback = function(v) print("Debug:", v) end
})
```

---

## API Reference

### ProfessionalUI Methods

#### `CreateWindow(title, config)`

Creates the main window container.

**Parameters:**
- `title` (string) – Window title
- `config` (table) – Configuration table
  - `Width` (number, default 600)
  - `Height` (number, default 400)

**Returns:** Window object with methods

**Example:**
```lua
local window = ProfessionalUI:CreateWindow("HUB", {Width: 700, Height: 450})
```

---

#### `CreateTab(name, iconAsset)`

Creates a new tab in the window.

**Parameters:**
- `name` (string) – Tab name
- `iconAsset` (string) – Optional Roblox image asset ID

**Returns:** ScrollingFrame for tab content

**Example:**
```lua
local tab = window:CreateTab("Settings", "rbxassetid://6023426923")
```

---

#### `CreateToggle(parent, config)`

Creates a toggle switch.

**Parameters:**
- `parent` (Frame) – Parent container
- `config` (table):
  - `Text` (string) – Label text
  - `Default` (bool, default false)
  - `Y` (number) – Y position offset
  - `Callback` (function) – Fired on toggle

**Returns:** Toggle object with `:Set(value)`, `:Get()`

**Example:**
```lua
local toggle = ProfessionalUI:CreateToggle(tab, {
    Text = "Enabled",
    Default = true,
    Y = 10,
    Callback = function(value) print(value) end
})
```

---

#### `CreateSlider(parent, config)`

Creates an interactive slider.

**Parameters:**
- `parent` (Frame) – Parent container
- `config` (table):
  - `Text` (string) – Label text
  - `Min` (number) – Minimum value
  - `Max` (number) – Maximum value
  - `Default` (number) – Initial value
  - `Increment` (number, default 1) – Snap-to-grid increment
  - `Y` (number) – Y position offset
  - `Callback` (function) – Fired on release

**Returns:** Slider object with `:Set(value)`, `:Get()`

**Example:**
```lua
local slider = ProfessionalUI:CreateSlider(tab, {
    Text = "Volume",
    Min = 0,
    Max = 100,
    Default = 50,
    Increment = 5,
    Y = 10,
    Callback = function(v) print("Volume:", v) end
})
```

---

#### `CreateDropdown(parent, config)`

Creates a dropdown menu.

**Parameters:**
- `parent` (Frame) – Parent container
- `config` (table):
  - `Text` (string) – Label text
  - `Options` (table) – Array of option strings
  - `Default` (string) – Initial selection
  - `Y` (number) – Y position offset
  - `Callback` (function) – Fired on selection

**Returns:** Dropdown object with `:Set(option)`, `:Get()`

**Example:**
```lua
local dropdown = ProfessionalUI:CreateDropdown(tab, {
    Text = "Quality",
    Options = {"Low", "Medium", "High", "Ultra"},
    Default = "High",
    Y = 10,
    Callback = function(opt) print("Quality:", opt) end
})
```

---

#### `CreateSection(parent, name, y)`

Creates a section divider with label.

**Parameters:**
- `parent` (Frame) – Parent container
- `name` (string) – Section label
- `y` (number) – Y position offset

**Returns:** Frame for organization

**Example:**
```lua
ProfessionalUI:CreateSection(tab, "SETTINGS", 10)
```

---

### Component Methods

All components return objects with standard methods:

```lua
local component = ProfessionalUI:CreateToggle(...)

-- Set value programmatically
component:Set(newValue)

-- Get current value
local value = component:Get()
```

---

## Performance Optimization

### Best Practices

1. **Reuse Components** – Don't recreate toggles/sliders; update them with `:Set()`

```lua
-- ❌ Bad: Creates new toggle every frame
game:GetService("RunService").Heartbeat:Connect(function()
    ProfessionalUI:CreateToggle(tab, {...})
end)

-- ✅ Good: Create once, update value
local toggle = ProfessionalUI:CreateToggle(tab, {...})
game:GetService("RunService").Heartbeat:Connect(function()
    toggle:Set(someValue)
end)
```

2. **Batch Operations** – Create all UI upfront, not dynamically

3. **Callback Optimization** – Keep callbacks light (no heavy loops)

```lua
-- ❌ Bad: Heavy processing in callback
ProfessionalUI:CreateSlider(tab, {
    Callback = function(v)
        for i = 1, 10000 do
            -- Heavy loop
        end
    end
})

-- ✅ Good: Lightweight callback, do work elsewhere
ProfessionalUI:CreateSlider(tab, {
    Callback = function(v)
        _G.targetValue = v
        -- Actual work handled in separate function
    end
})
```

---

## GitHub Deployment

### Option 1: Raw File Hosting (Recommended for Simple Scripts)

**Upload to GitHub:**

1. Create a repository: `RobloxGUIs` or `Professional-GUI-Framework`

2. Add file: `ProfessionalUI.lua` or `ProfessionalUI.rbxm`

3. Get raw URL:
   ```
   https://raw.githubusercontent.com/yourusername/RobloxGUIs/main/ProfessionalUI.lua
   ```

**Load in Your Script:**

```lua
local framework = loadstring(game:HttpGet("https://raw.githubusercontent.com/yourusername/RobloxGUIs/main/ProfessionalUI.lua"))()
local UI = framework:CreateWindow("HUB", {Width: 700, Height: 450})
```

### Option 2: Split Into Modules

**File Structure:**
```
RobloxGUIs/
├── ProfessionalUI.lua          -- Main framework
├── components/
│   ├── Toggle.lua
│   ├── Slider.lua
│   ├── Dropdown.lua
│   └── Window.lua
├── themes/
│   ├── DarkBlue.lua            -- Your theme
│   └── Themes.lua
└── README.md
```

**Example Module Loader:**

```lua
local modules = {
    framework = "https://raw.githubusercontent.com/.../ProfessionalUI.lua",
    theme = "https://raw.githubusercontent.com/.../themes/DarkBlue.lua"
}

local ProfessionalUI = loadstring(game:HttpGet(modules.framework))()
local Theme = loadstring(game:HttpGet(modules.theme))()
```

### Option 3: As a Module in ServerScriptService

If you're using Roblox Studio directly:

1. Insert a **ModuleScript** in **ServerScriptService**
2. Paste the entire framework code
3. Return the `ProfessionalUI` object at the end:

```lua
-- In ModuleScript
local ProfessionalUI = {}
-- ... all framework code ...
return ProfessionalUI
```

4. Use in a Script:

```lua
local ProfessionalUI = require(game:GetService("ServerScriptService"):WaitForChild("ProfessionalUI"))
local UI = ProfessionalUI:CreateWindow("HUB")
```

### GitHub Repository Setup

**README.md Template:**

```markdown
# Professional GUI Framework

A sleek, production-ready UI library for Roblox with modern black & electric blue theme.

## Quick Start

```lua
local framework = loadstring(game:HttpGet("https://raw.githubusercontent.com/yourusername/repo/main/ProfessionalUI.lua"))()
local UI = framework:CreateWindow("My Hub", {Width: 700, Height: 450})
local tab = UI:CreateTab("Main")
framework:CreateToggle(tab, {Text: "Enable", Callback: function(v) print(v) end})
```

## Features

- Draggable windows with minimize/maximize
- Smooth animations (0.15s tweens)
- Responsive components (toggles, sliders, dropdowns)
- Professional dark theme
- Tab system with ScrollingFrames

## Documentation

See [DOCUMENTATION.md](DOCUMENTATION.md) for full API reference.
```

### Best Practices for GitHub

1. **Always version your releases** – Use tags (v1.0, v1.1, etc.)

2. **Include a CHANGELOG** – Document breaking changes

3. **Keep raw file paths consistent** – Use `main` branch or specific release tags

4. **Add error handling** – Check if loadstring succeeds

```lua
local success, result = pcall(function()
    return loadstring(game:HttpGet("URL"))()
end)

if not success then
    warn("Failed to load framework:", result)
    return
end

local ProfessionalUI = result
```

---

## Troubleshooting

### Window Not Appearing

```lua
-- Check if PlayerGui exists
local player = game:GetService("Players").LocalPlayer
local playerGui = player:WaitForChild("PlayerGui")
print("PlayerGui found:", playerGui)
```

### Callbacks Not Firing

```lua
-- Ensure callback is a function
local toggle = ProfessionalUI:CreateToggle(tab, {
    Text = "Test",
    Callback = function(value)  -- Must be a function
        print("Toggled:", value)
    end
})
```

### Slider Not Dragging Smoothly

This is usually due to lag or high latency. The framework uses:
- `TweenService` for smooth movement
- `UserInputService` for immediate feedback
- `InputChanged` events for continuous tracking

If lagging, reduce animation duration:

```lua
local AnimationSpeed = 0.1  -- Reduce from 0.2
```

---

## License

This framework is provided as-is for personal and educational use in Roblox game development.

---

## Support & Contributions

For bugs, suggestions, or improvements:
1. Open a GitHub issue
2. Include reproduction steps
3. Specify Roblox platform (PC, Mobile, Console)

---

## Summary

The Professional GUI Framework provides everything needed for modern Roblox UI development:

✅ Complete window management  
✅ Smooth animations  
✅ Responsive components  
✅ Professional theming  
✅ Easy GitHub deployment  
✅ Zero external dependencies  

Get started in 5 minutes, scale to production-grade hubs.
