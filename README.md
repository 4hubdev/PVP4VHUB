local Players = game:GetService("Players")
local TweenService = game:GetService("TweenService")
local lp = Players.LocalPlayer
local pgui = lp:WaitForChild("PlayerGui")

-- Nettoyage des anciens GUIs
for _, old in pairs(pgui:GetChildren()) do
    if old.Name == "4vHubPVP" then old:Destroy() end
end

-- Interface Principale
local sg = Instance.new("ScreenGui", pgui)
sg.Name = "4vHubPVP"
sg.ResetOnSpawn = false 

-- Frame Principale
local mainFrame = Instance.new("Frame", sg)
mainFrame.Size = UDim2.new(0, 380, 0, 290)
mainFrame.Position = UDim2.new(0.5, -190, 0.5, -145)
mainFrame.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
mainFrame.BorderSizePixel = 0
mainFrame.Active = true
mainFrame.Draggable = true
mainFrame.ClipsDescendants = true

local mainCorner = Instance.new("UICorner", mainFrame)
mainCorner.CornerRadius = UDim.new(0, 15)

local mainStroke = Instance.new("UIStroke", mainFrame)
mainStroke.Color = Color3.fromRGB(255, 50, 50)
mainStroke.Thickness = 3

-- Header avec dégradé rouge/noir
local header = Instance.new("Frame", mainFrame)
header.Size = UDim2.new(1, 0, 0, 55)
header.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
header.BorderSizePixel = 0

local headerCorner = Instance.new("UICorner", header)
headerCorner.CornerRadius = UDim.new(0, 15)

local gradient = Instance.new("UIGradient", header)
gradient.Color = ColorSequence.new{
    ColorSequenceKeypoint.new(0, Color3.fromRGB(255, 0, 0)),
    ColorSequenceKeypoint.new(0.5, Color3.fromRGB(150, 0, 0)),
    ColorSequenceKeypoint.new(1, Color3.fromRGB(50, 0, 0))
}
gradient.Rotation = 90

-- Icône PVP
local pvpIcon = Instance.new("TextLabel", header)
pvpIcon.Size = UDim2.new(0, 50, 0, 50)
pvpIcon.Position = UDim2.new(0, 5, 0, 2.5)
pvpIcon.BackgroundTransparency = 1
pvpIcon.Text = "⚔️"
pvpIcon.TextColor3 = Color3.fromRGB(255, 255, 255)
pvpIcon.Font = Enum.Font.GothamBold
pvpIcon.TextSize = 32

-- Titre
local title = Instance.new("TextLabel", header)
title.Size = UDim2.new(1, -120, 1, 0)
title.Position = UDim2.new(0, 55, 0, 0)
title.BackgroundTransparency = 1
title.Text = "4V HUB PVP"
title.TextColor3 = Color3.fromRGB(255, 255, 255)
title.Font = Enum.Font.GothamBold
title.TextSize = 26
title.TextXAlignment = Enum.TextXAlignment.Left

-- Variable pour l'état de réduction
local isMinimized = false

-- Bouton Réduire/Agrandir
local minimizeBtn = Instance.new("TextButton", header)
minimizeBtn.Size = UDim2.new(0, 40, 0, 40)
minimizeBtn.Position = UDim2.new(1, -90, 0, 7.5)
minimizeBtn.BackgroundColor3 = Color3.fromRGB(255, 150, 0)
minimizeBtn.Text = "—"
minimizeBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
minimizeBtn.Font = Enum.Font.GothamBold
minimizeBtn.TextSize = 22

local minimizeBtnCorner = Instance.new("UICorner", minimizeBtn)
minimizeBtnCorner.CornerRadius = UDim.new(0, 8)

-- Bouton Fermer
local closeBtn = Instance.new("TextButton", header)
closeBtn.Size = UDim2.new(0, 40, 0, 40)
closeBtn.Position = UDim2.new(1, -45, 0, 7.5)
closeBtn.BackgroundColor3 = Color3.fromRGB(255, 50, 50)
closeBtn.Text = "X"
closeBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
closeBtn.Font = Enum.Font.GothamBold
closeBtn.TextSize = 20

local closeBtnCorner = Instance.new("UICorner", closeBtn)
closeBtnCorner.CornerRadius = UDim.new(0, 8)

closeBtn.MouseButton1Click:Connect(function()
    local tweenInfo = TweenInfo.new(0.3, Enum.EasingStyle.Back, Enum.EasingDirection.In)
    local tween = TweenService:Create(mainFrame, tweenInfo, {Size = UDim2.new(0, 0, 0, 0)})
    tween:Play()
    tween.Completed:Connect(function()
        sg:Destroy()
    end)
end)

-- Container pour les boutons (caché quand réduit)
local container = Instance.new("Frame", mainFrame)
container.Size = UDim2.new(1, -20, 1, -75)
container.Position = UDim2.new(0, 10, 0, 65)
container.BackgroundTransparency = 1

-- Fonction pour créer un bouton
local function createButton(name, icon, description, position, callback)
    local btnFrame = Instance.new("Frame", container)
    btnFrame.Size = UDim2.new(1, 0, 0, 60)
    btnFrame.Position = position
    btnFrame.BackgroundColor3 = Color3.fromRGB(35, 35, 35)
    btnFrame.BorderSizePixel = 0
    
    local btnCorner = Instance.new("UICorner", btnFrame)
    btnCorner.CornerRadius = UDim.new(0, 12)
    
    local btnStroke = Instance.new("UIStroke", btnFrame)
    btnStroke.Color = Color3.fromRGB(255, 50, 50)
    btnStroke.Thickness = 2
    
    local btn = Instance.new("TextButton", btnFrame)
    btn.Size = UDim2.new(1, 0, 1, 0)
    btn.BackgroundTransparency = 1
    btn.Text = ""
    
    local iconLabel = Instance.new("TextLabel", btn)
    iconLabel.Size = UDim2.new(0, 50, 1, 0)
    iconLabel.Position = UDim2.new(0, 10, 0, 0)
    iconLabel.BackgroundTransparency = 1
    iconLabel.Text = icon
    iconLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
    iconLabel.Font = Enum.Font.GothamBold
    iconLabel.TextSize = 28
    
    local textLabel = Instance.new("TextLabel", btn)
    textLabel.Size = UDim2.new(1, -70, 0, 25)
    textLabel.Position = UDim2.new(0, 60, 0, 8)
    textLabel.BackgroundTransparency = 1
    textLabel.Text = name
    textLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
    textLabel.Font = Enum.Font.GothamBold
    textLabel.TextSize = 18
    textLabel.TextXAlignment = Enum.TextXAlignment.Left
    
    -- Description en petit
    if description then
        local descLabel = Instance.new("TextLabel", btn)
        descLabel.Size = UDim2.new(1, -70, 0, 20)
        descLabel.Position = UDim2.new(0, 60, 0, 32)
        descLabel.BackgroundTransparency = 1
        descLabel.Text = description
        descLabel.TextColor3 = Color3.fromRGB(150, 150, 150)
        descLabel.Font = Enum.Font.Gotham
        descLabel.TextSize = 11
        descLabel.TextXAlignment = Enum.TextXAlignment.Left
    end
    
    btn.MouseButton1Click:Connect(function()
        callback(btnFrame, btnStroke, textLabel)
    end)
    
    -- Effet hover
    btn.MouseEnter:Connect(function()
        btnFrame.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
        btnStroke.Color = Color3.fromRGB(255, 100, 100)
    end)
    
    btn.MouseLeave:Connect(function()
        btnFrame.BackgroundColor3 = Color3.fromRGB(35, 35, 35)
        btnStroke.Color = Color3.fromRGB(255, 50, 50)
    end)
    
    return btnFrame
end

-- Bouton 1: Auto Bat
createButton("AUTO BAT", "🏏", nil, UDim2.new(0, 0, 0, 0), function(frame, stroke, textLabel)
    local success, err = pcall(function()
        loadstring(game:HttpGet("https://pandadevelopment.net/virtual/file/bf7fbb5f9e5d3cf5"))()
    end)
    
    if success then
        textLabel.Text = "AUTO BAT ✅"
        textLabel.TextColor3 = Color3.fromRGB(0, 255, 120)
        stroke.Color = Color3.fromRGB(0, 255, 120)
        wait(2)
        textLabel.Text = "AUTO BAT"
        textLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
        stroke.Color = Color3.fromRGB(255, 50, 50)
    else
        textLabel.Text = "AUTO BAT ❌"
        textLabel.TextColor3 = Color3.fromRGB(255, 50, 50)
        wait(2)
        textLabel.Text = "AUTO BAT"
        textLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
    end
end)

-- Bouton 2: Speed Boost
createButton("SPEED BOOST", "🚀", nil, UDim2.new(0, 0, 0, 70), function(frame, stroke, textLabel)
    local success, err = pcall(function()
        loadstring(game:HttpGet("https://monlua-protector.vercel.app/raw/deaf66d32110b98505c2c3eabb58e687"))()
    end)
    
    if success then
        textLabel.Text = "SPEED BOOST ✅"
        textLabel.TextColor3 = Color3.fromRGB(0, 255, 120)
        stroke.Color = Color3.fromRGB(0, 255, 120)
        wait(2)
        textLabel.Text = "SPEED BOOST"
        textLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
        stroke.Color = Color3.fromRGB(255, 50, 50)
    else
        textLabel.Text = "SPEED BOOST ❌"
        textLabel.TextColor3 = Color3.fromRGB(255, 50, 50)
        wait(2)
        textLabel.Text = "SPEED BOOST"
        textLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
    end
end)

-- Bouton 3: Nameless
createButton("NAMELESS", "👤", "Auto Grab • Anti Ragdoll", UDim2.new(0, 0, 0, 140), function(frame, stroke, textLabel)
    local success, err = pcall(function()
        loadstring(game:HttpGet("https://raw.githubusercontent.com/ily123950/Vulkan/refs/heads/main/Tr"))()
    end)
    
    if success then
        textLabel.Text = "NAMELESS ✅"
        textLabel.TextColor3 = Color3.fromRGB(0, 255, 120)
        stroke.Color = Color3.fromRGB(0, 255, 120)
        wait(2)
        textLabel.Text = "NAMELESS"
        textLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
        stroke.Color = Color3.fromRGB(255, 50, 50)
    else
        textLabel.Text = "NAMELESS ❌"
        textLabel.TextColor3 = Color3.fromRGB(255, 50, 50)
        wait(2)
        textLabel.Text = "NAMELESS"
        textLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
    end
end)

-- Fonction Réduire/Agrandir avec animation
minimizeBtn.MouseButton1Click:Connect(function()
    isMinimized = not isMinimized
    
    local tweenInfo = TweenInfo.new(0.4, Enum.EasingStyle.Quint, Enum.EasingDirection.Out)
    
    if isMinimized then
        -- Réduire
        minimizeBtn.Text = "+"
        container.Visible = false
        local tween = TweenService:Create(mainFrame, tweenInfo, {
            Size = UDim2.new(0, 200, 0, 55)
        })
        tween:Play()
    else
        -- Agrandir
        minimizeBtn.Text = "—"
        local tween = TweenService:Create(mainFrame, tweenInfo, {
            Size = UDim2.new(0, 380, 0, 290)
        })
        tween:Play()
        tween.Completed:Connect(function()
            container.Visible = true
        end)
    end
end)

-- Animation d'entrée
mainFrame.Size = UDim2.new(0, 0, 0, 0)
local tweenInfo = TweenInfo.new(0.5, Enum.EasingStyle.Back, Enum.EasingDirection.Out)
local tween = TweenService:Create(mainFrame, tweenInfo, {Size = UDim2.new(0, 380, 0, 290)})
tween:Play()

print("⚔️ 4V HUB PVP chargé avec succès!")
