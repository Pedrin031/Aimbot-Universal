--// Cache
local loadstring, game, getgenv, setclipboard = loadstring, game, getgenv, setclipboard

--// Failsafe para recarregar
if not getgenv().Aimbot then
    loadstring(game:HttpGet("https://raw.githubusercontent.com/Exunys/Aimbot-V2/main/Resources/Scripts/Raw%20Main.lua"))()
end

--// Referência
local Aimbot = getgenv().Aimbot
local Settings, FOVSettings, Functions = Aimbot.Settings, Aimbot.FOVSettings, Aimbot.Functions

local Library = loadstring(game:GetObjects("rbxassetid://7657867786")[1].Source)()

local Parts = {"Head", "HumanoidRootPart", "Torso", "Left Arm", "Right Arm", "Left Leg", "Right Leg", "LeftHand", "RightHand", "LeftLowerArm", "RightLowerArm", "LeftUpperArm", "RightUpperArm", "LeftFoot", "LeftLowerLeg", "UpperTorso", "LeftUpperLeg", "RightFoot", "RightLowerLeg", "LowerTorso", "RightUpperLeg"}

Library.UnloadCallback = Functions.Exit

--// Criar janela principal
local MainFrame = Library:CreateWindow({
    Name = "Aimbot Universal",
    Themeable = {
        Image = "7059346386",
        Info = "Made by Exunys\nPowered by Pepsi's UI Library",
        Credit = false
    },
    Background = "",
    Theme = [[{"__Designer.Colors.section":"ADC7FF","__Designer.Colors.topGradient":"1B242F","__Designer.Settings.ShowHideKey":"Enum.KeyCode.RightShift","__Designer.Colors.otherElementText":"54637D","__Designer.Colors.hoveredOptionBottom":"38667D","__Designer.Background.ImageAssetID":"","__Designer.Colors.unhoveredOptionTop":"407495","__Designer.Colors.innerBorder":"2C4168","__Designer.Colors.unselectedOption":"4E6EA0","__Designer.Background.UseBackgroundImage":true,"__Designer.Files.WorkspaceFile":"Aimbot Universal","__Designer.Colors.main":"23A0FF","__Designer.Colors.outerBorder":"162943","__Designer.Background.ImageColor":"FFFFFF","__Designer.Colors.tabText":"C9DFF1","__Designer.Colors.elementBorder":"111D26","__Designer.Colors.sectionBackground":"0E141C","__Designer.Colors.selectedOption":"558AC2","__Designer.Colors.background":"11182A","__Designer.Colors.bottomGradient":"202B42","__Designer.Background.ImageTransparency":95,"__Designer.Colors.hoveredOptionTop":"4885A0","__Designer.Colors.elementText":"7692B8","__Designer.Colors.unhoveredOptionBottom":"5471C4"}]]
})

-- Tabs
local SettingsTab = MainFrame:CreateTab({Name = "Settings"})
local FOVSettingsTab = MainFrame:CreateTab({Name = "FOV Settings"})
local FunctionsTab = MainFrame:CreateTab({Name = "Functions"})

-- Sections
local Values = SettingsTab:CreateSection({Name = "Values"})
local Checks = SettingsTab:CreateSection({Name = "Checks"})
local ThirdPerson = SettingsTab:CreateSection({Name = "Third Person"})

local FOV_Values = FOVSettingsTab:CreateSection({Name = "Values"})
local FOV_Appearance = FOVSettingsTab:CreateSection({Name = "Appearance"})

local FunctionsSection = FunctionsTab:CreateSection({Name = "Functions"})

-- Settings / Values
Values:AddToggle({
    Name = "Enabled",
    Value = Settings.Enabled,
    Callback = function(v) Settings.Enabled = v end
}).Default = Settings.Enabled

Values:AddToggle({
    Name = "Toggle",
    Value = Settings.Toggle,
    Callback = function(v) Settings.Toggle = v end
}).Default = Settings.Toggle

Settings.LockPart = Parts[1]
Values:AddDropdown({
    Name = "Lock Part",
    Value = Parts[1],
    Callback = function(v) Settings.LockPart = v end,
    List = Parts,
    Nothing = "Head"
}).Default = Parts[1]

Values:AddTextbox({
    Name = "Hotkey",
    Value = Settings.TriggerKey,
    Callback = function(v) Settings.TriggerKey = v end
}).Default = Settings.TriggerKey

Values:AddSlider({
    Name = "Sensitivity",
    Value = Settings.Sensitivity,
    Callback = function(v) Settings.Sensitivity = v end,
    Min = 0,
    Max = 1,
    Decimals = 2
}).Default = Settings.Sensitivity

-- Settings / Checks
Checks:AddToggle({
    Name = "Team Check",
    Value = Settings.TeamCheck,
    Callback = function(v) Settings.TeamCheck = v end
}).Default = Settings.TeamCheck

Checks:AddToggle({
    Name = "Wall Check",
    Value = Settings.WallCheck,
    Callback = function(v) Settings.WallCheck = v end
}).Default = Settings.WallCheck

Checks:AddToggle({
    Name = "Alive Check",
    Value = Settings.AliveCheck,
    Callback = function(v) Settings.AliveCheck = v end
}).Default = Settings.AliveCheck

-- Settings / Third Person
ThirdPerson:AddToggle({
    Name = "Enable Third Person",
    Value = Settings.ThirdPerson,
    Callback = function(v) Settings.ThirdPerson = v end
}).Default = Settings.ThirdPerson

ThirdPerson:AddSlider({
    Name = "Sensitivity",
    Value = Settings.ThirdPersonSensitivity,
    Callback = function(v) Settings.ThirdPersonSensitivity = v end,
    Min = 0.1,
    Max = 5,
    Decimals = 1
}).Default = Settings.ThirdPersonSensitivity

-- FOV Settings / Values
FOV_Values:AddToggle({
    Name = "Enabled",
    Value = FOVSettings.Enabled,
    Callback = function(v) FOVSettings.Enabled = v end
}).Default = FOVSettings.Enabled

FOV_Values:AddToggle({
    Name = "Visible",
    Value = FOVSettings.Visible,
    Callback = function(v) FOVSettings.Visible = v end
}).Default = FOVSettings.Visible

FOV_Values:AddSlider({
    Name = "Amount",
    Value = FOVSettings.Amount,
    Callback = function(v) FOVSettings.Amount = v end,
    Min = 10,
    Max = 300
}).Default = FOVSettings.Amount

-- FOV Settings / Appearance
FOV_Appearance:AddToggle({
    Name = "Filled",
    Value = FOVSettings.Filled,
    Callback = function(v) FOVSettings.Filled = v end
}).Default = FOVSettings.Filled

FOV_Appearance:AddSlider({
    Name = "Transparency",
    Value = FOVSettings.Transparency,
    Callback = function(v) FOVSettings.Transparency = v end,
    Min = 0,
    Max = 1,
    Decimal = 1
}).Default = FOVSettings.Transparency

FOV_Appearance:AddSlider({
    Name = "Sides",
    Value = FOVSettings.Sides,
    Callback = function(v) FOVSettings.Sides = v end,
    Min = 3,
    Max = 60
}).Default = FOVSettings.Sides

FOV_Appearance:AddSlider({
    Name = "Thickness",
    Value = FOVSettings.Thickness,
    Callback = function(v) FOVSettings.Thickness = v end,
    Min = 1,
    Max = 50
}).Default = FOVSettings.Thickness

FOV_Appearance:AddColorpicker({
    Name = "Color",
    Value = FOVSettings.Color,
    Callback = function(v) FOVSettings.Color = v end
}).Default = FOVSettings.Color

FOV_Appearance:AddColorpicker({
    Name = "Locked Color",
    Value = FOVSettings.LockedColor,
    Callback = function(v) FOVSettings.LockedColor = v end
}).Default = FOVSettings.LockedColor

-- Functions
FunctionsSection:AddButton({
    Name = "Reset Settings",
    Callback = function()
        Functions.ResetSettings()
        Library.ResetAll()
    end
})

FunctionsSection:AddButton({
    Name = "Restart",
    Callback = Functions.Restart
})

FunctionsSection:AddButton({
    Name = "Exit",
    Callback = function()
        Functions:Exit()
        Library.Unload()
    end
})

FunctionsSection:AddButton({
    Name = "Copiar Discord",
    Callback = function()
        setclipboard("https://discord.gg/jfKVrrMx")
    end
})

FunctionsSection:AddLabel("Created By Pedrin031")

-- Failsafe para manter o Aimbot sempre ativo
task.spawn(function()
    while task.wait(10) do
        if not getgenv().Aimbot or not getgenv().Aimbot.Settings then
            warn("[Failsafe] Recarregando Aimbot...")
            loadstring(game:HttpGet("https://raw.githubusercontent.com/Exunys/Aimbot-V2/main/Resources/Scripts/Raw%20Main.lua"))()
        end
    end
end)

-- Tecla de emergência: P recarrega o menu
game:GetService("UserInputService").InputBegan:Connect(function(input, gp)
    if not gp and input.KeyCode == Enum.KeyCode.P then
        loadstring(game:HttpGet("https://raw.githubusercontent.com/Exunys/Aimbot-V2/main/Resources/Scripts/Raw%20Main.lua"))()
    end
end)
