--// Cache
local loadstring, game, getgenv, setclipboard = loadstring, game, getgenv, setclipboard

--// Loaded check
if getgenv().Aimbot then return end

--// Load Aimbot V2 (Raw)
loadstring(game:HttpGet("https://raw.githubusercontent.com/Exunys/Aimbot-V2/main/Resources/Scripts/Raw%20Main.lua"))()

--// Variables
local Aimbot = getgenv().Aimbot
local Settings, FOVSettings, Functions = Aimbot.Settings, Aimbot.FOVSettings, Aimbot.Functions
local Library = loadstring(game:GetObjects("rbxassetid://7657867786")[1].Source)()

local Parts = {
    "Head", "HumanoidRootPart", "Torso", "Left Arm", "Right Arm", "Left Leg", "Right Leg",
    "LeftHand", "RightHand", "LeftLowerArm", "RightLowerArm", "LeftUpperArm", "RightUpperArm",
    "LeftFoot", "LeftLowerLeg", "UpperTorso", "LeftUpperLeg", "RightFoot", "RightLowerLeg",
    "LowerTorso", "RightUpperLeg"
}

--// UI Principal
Library.UnloadCallback = Functions.Exit

local MainFrame = Library:CreateWindow({
    Name = "Aimbot Universal",
    Themeable = {
        Image = "7059346386",
        Info = "Created By Pedrin031\nPowered by Pepsi's UI Library",
        Credit = false
    },
    Background = "",
    Theme = [[{"__Designer.Colors.section":"ADC7FF","__Designer.Colors.topGradient":"1B242F","__Designer.Settings.ShowHideKey":"Enum.KeyCode.RightShift","__Designer.Colors.otherElementText":"54637D","__Designer.Colors.hoveredOptionBottom":"38667D","__Designer.Background.ImageAssetID":"","__Designer.Colors.unhoveredOptionTop":"407495","__Designer.Colors.innerBorder":"2C4168","__Designer.Colors.unselectedOption":"4E6EA0","__Designer.Background.UseBackgroundImage":true,"__Designer.Files.WorkspaceFile":"Aimbot V2","__Designer.Colors.main":"23A0FF","__Designer.Colors.outerBorder":"162943","__Designer.Background.ImageColor":"FFFFFF","__Designer.Colors.tabText":"C9DFF1","__Designer.Colors.elementBorder":"111D26","__Designer.Colors.sectionBackground":"0E141C","__Designer.Colors.selectedOption":"558AC2","__Designer.Colors.background":"11182A","__Designer.Colors.bottomGradient":"202B42","__Designer.Background.ImageTransparency":95,"__Designer.Colors.hoveredOptionTop":"4885A0","__Designer.Colors.elementText":"7692B8","__Designer.Colors.unhoveredOptionBottom":"5471C4"}]]
})

local Tab = MainFrame:CreateTab({ Name = "Menu" })
local Section = Tab:CreateSection({ Name = "Configurações do Aimbot" })

--// Configurações principais
Section:AddToggle({ Name = "Enabled", Value = Settings.Enabled, Callback = function(n) Settings.Enabled = n end }).Default = Settings.Enabled
Section:AddToggle({ Name = "Toggle", Value = Settings.Toggle, Callback = function(n) Settings.Toggle = n end }).Default = Settings.Toggle

Settings.LockPart = Parts[1]
Section:AddDropdown({
    Name = "Lock Part",
    Value = Parts[1],
    Callback = function(n) Settings.LockPart = n end,
    List = Parts,
    Nothing = "Head"
}).Default = Parts[1]

Section:AddTextbox({ Name = "Hotkey", Value = Settings.TriggerKey, Callback = function(n) Settings.TriggerKey = n end }).Default = Settings.TriggerKey
Section:AddSlider({ Name = "Sensitivity", Value = Settings.Sensitivity, Callback = function(n) Settings.Sensitivity = n end, Min = 0, Max = 1, Decimals = 2 }).Default = Settings.Sensitivity

--// Checks
Section:AddToggle({ Name = "Team Check", Value = Settings.TeamCheck, Callback = function(n) Settings.TeamCheck = n end }).Default = Settings.TeamCheck
Section:AddToggle({ Name = "Wall Check", Value = Settings.WallCheck, Callback = function(n) Settings.WallCheck = n end }).Default = Settings.WallCheck
Section:AddToggle({ Name = "Alive Check", Value = Settings.AliveCheck, Callback = function(n) Settings.AliveCheck = n end }).Default = Settings.AliveCheck

--// Terceira pessoa
Section:AddToggle({ Name = "Enable Third Person", Value = Settings.ThirdPerson, Callback = function(n) Settings.ThirdPerson = n end }).Default = Settings.ThirdPerson
Section:AddSlider({ Name = "Third Person Sensitivity", Value = Settings.ThirdPersonSensitivity, Callback = function(n) Settings.ThirdPersonSensitivity = n end, Min = 0.1, Max = 5, Decimals = 1 }).Default = Settings.ThirdPersonSensitivity

--// FOV
Section:AddToggle({ Name = "FOV Enabled", Value = FOVSettings.Enabled, Callback = function(n) FOVSettings.Enabled = n end }).Default = FOVSettings.Enabled
Section:AddToggle({ Name = "FOV Visible", Value = FOVSettings.Visible, Callback = function(n) FOVSettings.Visible = n end }).Default = FOVSettings.Visible
Section:AddSlider({ Name = "FOV Amount", Value = FOVSettings.Amount, Callback = function(n) FOVSettings.Amount = n end, Min = 10, Max = 300 }).Default = FOVSettings.Amount
Section:AddToggle({ Name = "FOV Filled", Value = FOVSettings.Filled, Callback = function(n) FOVSettings.Filled = n end }).Default = FOVSettings.Filled
Section:AddSlider({ Name = "FOV Transparency", Value = FOVSettings.Transparency, Callback = function(n) FOVSettings.Transparency = n end, Min = 0, Max = 1, Decimal = 1 }).Default = FOVSettings.Transparency
Section:AddSlider({ Name = "FOV Sides", Value = FOVSettings.Sides, Callback = function(n) FOVSettings.Sides = n end, Min = 3, Max = 60 }).Default = FOVSettings.Sides
Section:AddSlider({ Name = "FOV Thickness", Value = FOVSettings.Thickness, Callback = function(n) FOVSettings.Thickness = n end, Min = 1, Max = 50 }).Default = FOVSettings.Thickness
Section:AddColorpicker({ Name = "FOV Color", Value = FOVSettings.Color, Callback = function(n) FOVSettings.Color = n end }).Default = FOVSettings.Color
Section:AddColorpicker({ Name = "Locked FOV Color", Value = FOVSettings.LockedColor, Callback = function(n) FOVSettings.LockedColor = n end }).Default = FOVSettings.LockedColor

--// Funções
Section:AddButton({ Name = "Reset Settings", Callback = function() Functions.ResetSettings() Library.ResetAll() end })
Section:AddButton({ Name = "Restart", Callback = Functions.Restart })
Section:AddButton({ Name = "Exit", Callback = function() Functions:Exit(); Library.Unload() end })
Section:AddButton({ Name = "Copiar Script Page", Callback = function() setclipboard("https://github.com/Exunys/Aimbot-V2") end })
Section:AddButton({ Name = "Copiar Discord", Callback = function() setclipboard("https://discord.gg/jfKVrrMx") end })
