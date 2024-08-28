local player = game.Players.LocalPlayer

-- Create a loading screen GUI
local loadingScreen = Instance.new("ScreenGui")
loadingScreen.Parent = player.PlayerGui

local loadingFrame = Instance.new("Frame")
loadingFrame.BackgroundColor3 = Color3.new(0, 0, 0)
loadingFrame.BackgroundTransparency = 0.5
loadingFrame.Size = UDim2.new(0, 200, 0, 100) -- Adjust the size to your liking
loadingFrame.Position = UDim2.new(0.5, -100, 0.5, -50) -- Center the frame
loadingFrame.AnchorPoint = Vector2.new(0.5, 0.5) -- Anchor the frame to the center
loadingFrame.Parent = loadingScreen

local loadingLabel = Instance.new("TextLabel")
loadingLabel.Text = "Loading..."
loadingLabel.Font = Enum.Font.SourceSans
loadingLabel.FontSize = Enum.FontSize.Size24
loadingLabel.TextColor3 = Color3.new(1, 1, 1)
loadingLabel.Parent = loadingFrame

-- Load the Luminosity UI library
local Luminosity = loadstring(game:HttpGet("https://raw.githubusercontent.com/iHavoc101/Genesis-Studios/main/UserInterface/Luminosity.lua", true))()

-- Wait for the UI library to load
wait(1)

-- Load the Key System 2 Lib
local KeySystem = loadstring(game:HttpGet("https://raw.githubusercontent.com/OopssSorry/KeySystem2Lib/main/KeySystem2Lib.lua", true))()

-- Initialize the Key System 2 Lib
KeySystem.Init()

-- Create a new key
local key = KeySystem.CreateKey("zz hub test", "ZZ Hub Test Key")

-- Add a key input field to the loading screen
local keyInputField = Instance.new("TextLabel")
keyInputField.Text = "Enter key:"
keyInputField.Font = Enum.Font.SourceSans
keyInputField.FontSize = Enum.FontSize.Size24
keyInputField.TextColor3 = Color3.new(1, 1, 1)
keyInputField.Parent = loadingFrame

local keyEntryField = Instance.new("TextBox")
keyEntryField.PlaceholderText = "Enter your key here..."
keyEntryField.Parent = loadingFrame

-- Add an event listener to the key entry field
[]
keyEntryField.FocusLost:Connect(function(enterPressed)
if enterPressed then
local enteredKey = keyEntryField.Text
if KeySystem.ValidateKey(key, enteredKey) then
-- Remove the loading screen
loadingScreen:Destroy()

-- Initialize the Luminosity UI library
Luminosity:SetTheme("Dark")
Luminosity:SetAccent(Color3.new(0, 255, 255))

-- Create a new window
local window = Luminosity:AddWindow("My UI")

-- Add a label to the window
local label = Luminosity:AddLabel("Hello, World!", window)

-- Add a button to the window
local button = Luminosity:AddButton("Click me!", window)

-- Add an event listener to the button
button.OnClickListener = function()
print("Button clicked!")
end
else
print("Invalid key!")
end
end
end)

