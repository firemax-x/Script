# Orion Library
This documentation is for the stable release of Orion Library.

## Booting the Library
```lua
local OrionLib = loadstring(game:HttpGet(('https://raw.githubusercontent.com/firemax-x/Script/refs/heads/main/Lib')))()
```



## Creating a Window
```lua
local Window = OrionLib:MakeWindow({Name = "Title of the library", HidePremium = false, SaveConfig = true, ConfigFolder = "OrionTest"})

--[[
Name = <string> - The name of the UI.
HidePremium = <bool> - Whether or not the user details shows Premium status or not.
SaveConfig = <bool> - Toggles the config saving in the UI.
ConfigFolder = <string> - The name of the folder where the configs are saved.
IntroEnabled = <bool> - Whether or not to show the intro animation.
IntroText = <string> - Text to show in the intro animation.
IntroIcon = <string> - URL to the image you want to use in the intro animation.
Icon = <string> - URL to the image you want displayed on the window.
CloseCallback = <function> - Function to execute when the window is closed.
]]
```



## Creating a Tab
```lua
local Tab = Window:MakeTab({
	Name = "Tab 1",
	Icon = "rbxassetid://4483345998",
	PremiumOnly = false
})

--[[
Name = <string> - The name of the tab.
Icon = <string> - The icon of the tab.
PremiumOnly = <bool> - Makes the tab accessible to Sirus Premium users only.
]]
```
## Creating a Section
```lua
local Section = Tab:AddSection({
	Name = "Section"
})

--[[
Name = <string> - The name of the section.
]]
```
You can add elements to sections the same way you would add them to a tab normally.

## Notifying the user
```lua
OrionLib:MakeNotification({
	Name = "Title!",
	Content = "Notification content... what will it say??",
	Image = "rbxassetid://4483345998",
	Time = 5
})

--[[
Title = <string> - The title of the notification.
Content = <string> - The content of the notification.
Image = <string> - The icon of the notification.
Time = <number> - The duration of the notfication.
]]
```



## Creating a Button
```lua
Tab:AddButton({
	Name = "Button!",
	Callback = function()
      		print("button pressed")
  	end    
})

--[[
Name = <string> - The name of the button.
Callback = <function> - The function of the button.
]]
```


## Creating a Checkbox toggle
```lua
Tab:AddToggle({
	Name = "This is a toggle!",
	Default = false,
	Callback = function(Value)
		print(Value)
	end    
})

--[[
Name = <string> - The name of the toggle.
Default = <bool> - The default value of the toggle.
Callback = <function> - The function of the toggle.
]]
```

### Changing the value of an existing Toggle
```lua
CoolToggle:Set(true)
```



## Creating a Color Picker
```lua
Tab:AddColorpicker({
	Name = "Colorpicker",
	Default = Color3.fromRGB(255, 0, 0),
	Callback = function(Value)
		print(Value)
	end	  
})

--[[
Name = <string> - The name of the colorpicker.
Default = <color3> - The default value of the colorpicker.
Callback = <function> - The function of the colorpicker.
]]
```

### Setting the color picker's value
```lua
ColorPicker:Set(Color3.fromRGB(255,255,255))
```


## Creating a Slider
```lua
Tab:AddSlider({
	Name = "Slider",
	Min = 0,
	Max = 20,
	Default = 5,
	Color = Color3.fromRGB(255,255,255),
	Increment = 1,
	ValueName = "bananas",
	Callback = function(Value)
		print(Value)
	end    
})

--[[
Name = <string> - The name of the slider.
Min = <number> - The minimal value of the slider.
Max = <number> - The maxium value of the slider.
Increment = <number> - How much the slider will change value when dragging.
Default = <number> - The default value of the slider.
ValueName = <string> - The text after the value number.
Callback = <function> - The function of the slider.
]]
```

### Change Slider Value
```lua
Slider:Set(2)
```
Make sure you make your slider a variable (local CoolSlider = Tab:AddSlider...) for this to work.


## Creating a Label
```lua
Tab:AddLabel("Label")
```

### Changing the value of an existing label
```lua
CoolLabel:Set("Label New!")
```


## Creating a Paragraph
```lua
Tab:AddParagraph("Paragraph","Paragraph Content")
```

### Changing an existing paragraph
```lua
CoolParagraph:Set("Paragraph New!", "New Paragraph Content!")
```


## Creating an Adaptive Input
```lua
Tab:AddTextbox({
	Name = "Textbox",
	Default = "default box input",
	TextDisappear = true,
	Callback = function(Value)
		print(Value)
	end	  
})

--[[
Name = <string> - The name of the textbox.
Default = <string> - The default value of the textbox.
TextDisappear = <bool> - Makes the text disappear in the textbox after losing focus.
Callback = <function> - The function of the textbox.
]]
```


## Creating a Keybind
```lua
Tab:AddBind({
	Name = "Bind",
	Default = Enum.KeyCode.E,
	Hold = false,
	Callback = function()
		print("press")
	end    
})

--[[
Name = <string> - The name of the bind.
Default = <keycode> - The default value of the bind.
Hold = <bool> - Makes the bind work like: Holding the key > The bind returns true, Not holding the key > Bind returns false.
Callback = <function> - The function of the bind.
]]
```

### Chaning the value of a bind
```lua
Bind:Set(Enum.KeyCode.E)
```


## Creating a Dropdown menu

### Basic Dropdown (Single Selection)
```lua
Tab:AddDropdown({
	Name = "Dropdown",
	Default = "",
	Options = {"Option1", "Option2", "Option3"},
	Callback = function(Value)
		print("Selected:", Value)
	end    
})
```

### Multi-Selection Dropdown
```lua
Tab:AddDropdown({
	Name = "Multi Dropdown", 
	Default = {},
	Multi = true,
	Options = {"Option1", "Option2", "Option3"},
	Callback = function(Value)
		-- Value is a table for multi dropdowns
		if type(Value) == "table" then
			print("Selected options:", table.concat(Value, ", "))
		end
	end    
})
```

### Searchable Dropdown
```lua
Tab:AddDropdown({
	Name = "Searchable Dropdown",
	Default = "",
	Options = {"Player1", "Player2", "Player3"},
	Searchable = true,
	Callback = function(Value)
		print("Selected:", Value)
	end    
})
```

### Player Dropdown (Auto-detects players and shows avatars)
```lua
Tab:AddDropdown({
	Name = "Select Player",
	Default = "",
	Options = {"PlayerName (DisplayName)", "Player2 (Display2)"},
	Callback = function(Value)
		local playerName = Value:match("^(.-) %(") or Value
		local player = game.Players:FindFirstChild(playerName)
		if player then
			print("Selected player:", player.Name)
		end
	end    
})
```

### Grouped Dropdown
```lua
Tab:AddDropdown({
	Name = "Grouped Dropdown",
	Default = "",
	Grouped = true,
	Options = {
		["Weapons"] = {"Sword", "Bow", "Staff"},
		["Tools"] = {"Hammer", "Pickaxe", "Shovel"}
	},
	Callback = function(Value)
		print("Selected:", Value)
	end    
})
```

**Parameters:**
```lua
--[[
Name = <string> - The name of the dropdown
Default = <string> | <table> - Default value ("" for single, {} for multi)
Options = <table> - The options in the dropdown
Multi = <boolean> - Enable multi-selection (default: false)
Searchable = <boolean> - Enable search functionality (default: false)  
Grouped = <boolean> - Enable grouped options (default: false)
Icons = <boolean> - Enable icon support (default: false)
MaxHeight = <number> - Maximum dropdown height in pixels (default: 200)
Callback = <function> - Function called when selection changes
Flag = <string> - Save flag for configuration
Save = <boolean> - Whether to save selection (default: false)
]]
```

## Managing Dropdown Options

### Adding new options to existing dropdown
```lua
Dropdown:Refresh(NewOptions, DeleteOld)
```
- `NewOptions` - Table of new options
- `DeleteOld` - Boolean: true = replace all options, false = add to existing

**Examples:**
```lua
-- Replace all options
Dropdown:Refresh({"NewOption1", "NewOption2"}, true)

-- Add to existing options  
Dropdown:Refresh({"AdditionalOption"}, false)
```

## Setting Dropdown Values

### Single Selection Dropdown
```lua
Dropdown:Set("option name")
```

### Multi-Selection Dropdown  
```lua
-- Set multiple selections
Dropdown:Set({"option1", "option2"})

-- Clear all selections
Dropdown:Set({})
```

### Avoiding Callback Loops
```lua
-- If your callback calls Set(), use a flag to prevent infinite loops:
local isResetting = false

Tab:AddDropdown({
	Name = "Dropdown",
	Default = "",
	Options = {"Option1", "Option2"},
	Callback = function(Value)
		if isResetting then return end
		
		if someCondition then
			isResetting = true
			Dropdown:Set("")  -- Reset without triggering callback loop
			isResetting = false
		end
	end
})
```

## Special Features

### Player Detection
The dropdown automatically detects player formats like `"PlayerName (DisplayName)"` and:
- Shows player avatars
- Displays username and display name separately  
- Uses enhanced player layout (60px height vs 28px standard)

### Search Functionality
When `Searchable = true`:
- Search box appears when dropdown is opened
- Filters options in real-time
- Supports searching display names and usernames for player dropdowns

# Finishing your script (REQUIRED)
The below function needs to be added at the end of your code.
```lua
OrionLib:Init()
```

### How flags work.
The flags feature in the ui may be confusing for some people. It serves the purpose of being the ID of an element in the config file, and makes accessing the value of an element anywhere in the code possible.
Below in an example of using flags.
```lua
Tab1:AddToggle({
    Name = "Toggle",
    Default = true,
    Save = true,
    Flag = "toggle"
})

print(OrionLib.Flags["toggle"].Value) -- prints the value of the toggle.
```
Flags only work with the toggle, slider, dropdown, bind, and colorpicker.

### Making your interface work with configs.
In order to make your interface use the configs function you first need to add the `SaveConfig` and `ConfigFolder` arguments to your window function. The explanation of these arguments in above.
Then you need to add the `Flag` and `Save` values to every toggle, slider, dropdown, bind, and colorpicker you want to include in the config file.
The `Flag = <string>` argument is the ID of an element in the config file.
The `Save = <bool>` argument includes the element in the config file.
Config files are made for every game the library is launched in.

## Destroying the Interface
```lua
OrionLib:Destroy()
```

## Combos

```lua
local OrionLib = loadstring(game:HttpGet(('https://raw.githubusercontent.com/firemax-x/Script/refs/heads/main/Lib')))()

local Window = OrionLib:MakeWindow({Name = "Test", IntroText = "Test", IntroIcon = "rbxassetid://134867074334684", HidePremium = false, SaveConfig = true, ConfigFolder = "Test", FreeMouse = true, SearchBar = ""})

local Tab = Window:MakeTab({
	Name = "Tab 1",
	Icon = "rbxassetid://4483345998",
	PremiumOnly = false
})

Tab:AddMouseModeDropdown()

Tab:AddSection({Name = ""})

Tab:AddToggle({
	Name = "This is a toggle!",
	Default = false,
	Callback = function(Value)
        
	end    
})
```
### This Can save u Alot Of time when ur Testing Stuff
