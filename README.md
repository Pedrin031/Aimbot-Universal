--// Cache
local loadstring, game, getgenv, setclipboard = loadstring, game, getgenv, setclipboard

--// Loaded check
if getgenv().Aimbot then return end

--// Load Aimbot V2 (Raw)
loadstring(game:HttpGet("https://raw.githubusercontent.com/Exunys/Aimbot-V2/main/Resources/Scripts/Raw%20Main.lua"))()

--// Variables
local Aimbot = getgenv().Aimbot
local Settings, FOVSettings, Functions = Aimbot.Settings, Aimbot.FOVSettings, Aimbot.Functions

local Library = loadstring(game:GetObjects("rbxassetid://7657867786")[1].Source)() -- Pepsi's UI Library

-- Criar Janela
local MainFrame = Library:CreateWindow({
    Name = "Aimbot Universal",
    Themeable = {
        Image = "7059346386",
        Info = "Created By Pedrin031",
        Credit = false
    },
    Background = "",
    Theme = [[{"__Designer.Colors.section":"ADC7FF","__Designer.Colors.topGradient":"1B242F","__Designer.Settings.ShowHideKey":"Enum.KeyCode.RightShift","__Designer.Colors.otherElementText":"54637D","__Designer.Colors.hoveredOptionBottom":"38667D","__Designer.Background.ImageAssetID":"","__Designer.Colors.unhoveredOptionTop":"407495","__Designer.Colors.innerBorder":"2C4168","__Designer.Colors.unselectedOption":"4E6EA0","__Designer.Background.UseBackgroundImage":true,"__Designer.Files.WorkspaceFile":"Aimbot Universal","__Designer.Colors.main":"23A0FF","__Designer.Colors.outerBorder":"162943","__Designer.Background.ImageColor":"FFFFFF","__Designer.Colors.tabText":"C9DFF1","__Designer.Colors.elementBorder":"111D26","__Designer.Colors.sectionBackground":"0E141C","__Designer.Colors.selectedOption":"558AC2","__Designer.Colors.background":"11182A","__Designer.Colors.bottomGradient":"202B42","__Designer.Background.ImageTransparency":95,"__Designer.Colors.hoveredOptionTop":"4885A0","__Designer.Colors.elementText":"7692B8","__Designer.Colors.unhoveredOptionBottom":"5471C4"}]]
})

-- Criar uma única aba com todas as opções visíveis
local Section = MainFrame:CreateTab({ Name = "Aimbot Settings" }):CreateSection({ Name = "Configurações" })

-- Lista de partes possíveis para lock
local Parts = {"Head", "HumanoidRootPart", "Torso", "Left Arm", "Right Arm", "Left Leg", "Right Leg", "LeftHand", "RightHand", "LeftLowerArm", "RightLowerArm", "LeftUpperArm", "RightUpperArm", "LeftFoot", "LeftLowerLeg", "UpperTorso", "LeftUpperLeg", "RightFoot", "RightLowerLeg", "LowerTorso", "RightUpperLeg"}

-- Opções principais
Section:AddToggle({ Name = "Enabled", Value = Settings.Enabled, Callback = function(v) Settings.Enabled = v end }).Default = Settings.Enabled
Section:AddToggle({ Name = "Toggle", Value = Settings.Toggle, Callback = function(v) Settings.Toggle = v end }).Default = Settings.Toggle
Settings.LockPart = Parts[1]
Section:AddDropdown({ Name = "Lock Part", Value = Parts[1], List = Parts, Callback = function(v) Settings.LockPart = v end, Nothing = "Head" }).Default = Parts[1]
Section:AddTextbox({ Name = "Hotkey", Value = Settings.TriggerKey, Callback = function(v) Settings.TriggerKey = v end }).Default = Settings.TriggerKey
Section:AddSlider({ Name = "Sensitivity", Value = Settings.Sensitivity, Min = 0, Max = 1, Decimals = 2, Callback = function(v) Settings.Sensitivity = v end }).Default = Settings.Sensitivity

-- Checks
Section:AddToggle({ Name = "Team Check", Value = Settings.TeamCheck, Callback = function(v) Settings.TeamCheck = v end }).Default = Settings.TeamCheck
Section:AddToggle({ Name = "Wall Check", Value = Settings.WallCheck, Callback = function(v) Settings.WallCheck = v end }).Default = Settings.WallCheck
Section:AddToggle({ Name = "Alive Check", Value = Settings.AliveCheck, Callback = function(v) Settings.AliveCheck = v end }).Default = Settings.AliveCheck

-- Terceira Pessoa
Section:AddToggle({ Name = "Enable Third Person", Value = Settings.ThirdPerson, Callback = function(v) Settings.ThirdPerson = v end }).Default = Settings.ThirdPerson
Section:AddSlider({ Name = "Third Person Sensitivity", Value = Settings.ThirdPersonSensitivity, Min = 0.1, Max = 5, Decimals = 1, Callback = function(v) Settings.ThirdPersonSensitivity = v end }).Default = Settings.ThirdPersonSensitivity

-- FOV Settings
Section:AddToggle({ Name = "FOV Enabled", Value = FOVSettings.Enabled, Callback = function(v) FOVSettings.Enabled = v end }).Default = FOVSettings.Enabled
Section:AddToggle({ Name = "FOV Visible", Value = FOVSettings.Visible, Callback = function(v) FOVSettings.Visible = v end }).Default = FOVSettings.Visible
Section:AddSlider({ Name = "FOV Amount", Value = FOVSettings.Amount, Min = 10, Max = 300, Callback = function(v) FOVSettings.Amount = v end }).Default = FOVSettings.Amount
Section:AddToggle({ Name = "FOV Filled", Value = FOVSettings.Filled, Callback = function(v) FOVSettings.Filled = v end }).Default = FOVSettings.Filled
Section:AddSlider({ Name = "FOV Transparency", Value = FOVSettings.Transparency, Min = 0, Max = 1, Decimal = 1, Callback = function(v) FOVSettings.Transparency = v end }).Default = FOVSettings.Transparency
Section:AddSlider({ Name = "FOV Sides", Value = FOVSettings.Sides, Min = 3, Max = 60, Callback = function(v) FOVSettings.Sides = v end }).Default = FOVSettings.Sides
Section:AddSlider({ Name = "FOV Thickness", Value = FOVSettings.Thickness, Min = 1, Max = 50, Callback = function(v) FOVSettings.Thickness = v end }).Default = FOVSettings.Thickness
Section:AddColorpicker({ Name = "FOV Color", Value = FOVSettings.Color, Callback = function(v) FOVSettings.Color = v end }).Default = FOVSettings.Color
Section:AddColorpicker({ Name = "FOV Locked Color", Value = FOVSettings.LockedColor, Callback = function(v) FOVSettings.LockedColor = v end }).Default = FOVSettings.LockedColor

-- Botões extras
Section:AddButton({ Name = "Reset Settings", Callback = function() Functions.ResetSettings(); Library.ResetAll() end })
Section:AddButton({ Name = "Restart", Callback = Functions.Restart })
Section:AddButton({ Name = "Exit", Callback = function() Functions:Exit(); Library.Unload() end })
Section:AddButton({ Name = "Copiar Script Page", Callback = function() setclipboard("https://github.com/Exunys/Aimbot-V2") end })
Section:AddButton({ Name = "Copiar Discord", Callback = function() setclipboard("https://discord.gg/jfKVrrMx") end })

-- Crédit
