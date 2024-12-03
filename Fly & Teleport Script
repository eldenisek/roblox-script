local ScreenGui = Instance.new("ScreenGui")
local MainFrame = Instance.new("Frame")
local TitleLabel = Instance.new("TextLabel")
local FlySection = Instance.new("Frame")
local TeleportSection = Instance.new("Frame")
local FlyButton = Instance.new("TextButton")
local SpeedLabel = Instance.new("TextLabel")
local SpeedInput = Instance.new("TextBox")
local Dropdown = Instance.new("TextButton") 
local DropdownList = Instance.new("Frame") 
local RefreshButton = Instance.new("TextButton") 
local TeleportButton = Instance.new("TextButton") 

ScreenGui.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui")
MainFrame.Parent = ScreenGui
MainFrame.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
MainFrame.Size = UDim2.new(0, 250, 0, 170)
MainFrame.Position = UDim2.new(0.5, -150, 0.5, -200)
MainFrame.Active = true
MainFrame.Draggable = true
MainFrame.BorderSizePixel = 0
TitleLabel.Parent = MainFrame
TitleLabel.Text = "Fly & Teleport Script"
TitleLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
TitleLabel.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
TitleLabel.Size = UDim2.new(1, 0, 0.2, 0)
TitleLabel.Font = Enum.Font.SourceSansBold
TitleLabel.TextSize = 20
TitleLabel.BorderSizePixel = 0

-- Fly
FlySection.Parent = MainFrame
FlySection.Size = UDim2.new(0, 200, 0, 30)
FlySection.Position = UDim2.new(0, 5, 0.2, 5) 
FlySection.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
FlySection.BackgroundTransparency = 1  
FlySection.BorderSizePixel = 0

FlyButton.Parent = FlySection
FlyButton.Text = "Fly"
FlyButton.Size = UDim2.new(0, 100, 0, 30)  
FlyButton.Position = UDim2.new(0, 10, 0.5, -15)  
FlyButton.BackgroundColor3 = Color3.fromRGB(30, 30, 30)  
FlyButton.TextColor3 = Color3.fromRGB(255, 255, 255)  
FlyButton.Font = Enum.Font.SourceSans
FlyButton.TextSize = 16

SpeedInput.Parent = FlySection
SpeedInput.Text = "1"
SpeedInput.Size = UDim2.new(0, 100, 0, 30)  
SpeedInput.Position = UDim2.new(0, 120, 0.5, -15) 
SpeedInput.BackgroundColor3 = Color3.fromRGB(30, 30, 30) 
SpeedInput.TextColor3 = Color3.fromRGB(255, 255, 255)  
SpeedInput.Font = Enum.Font.SourceSans
SpeedInput.TextSize = 14

local flying = false
local bodyVelocity
local bodyGyro
local moveDirection = Vector3.zero
local normalSpeed = 16 
local speed = normalSpeed
local UserInputService = game:GetService("UserInputService")
local Camera = game.Workspace.CurrentCamera

FlyButton.MouseButton1Click:Connect(function()
    if flying then
        flying = false
        if bodyVelocity then
            bodyVelocity:Destroy()
        end
        if bodyGyro then
            bodyGyro:Destroy()
        end
        FlyButton.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
        FlyButton.TextColor3 = Color3.fromRGB(255, 255, 255)
        FlyButton.Text = "Fly"
    else
        flying = true
        bodyVelocity = Instance.new("BodyVelocity")
        bodyGyro = Instance.new("BodyGyro")
        
        bodyVelocity.MaxForce = Vector3.new(400000, 400000, 400000)
        bodyVelocity.Velocity = Vector3.zero
        bodyVelocity.Parent = game.Players.LocalPlayer.Character:WaitForChild("HumanoidRootPart")
        
        bodyGyro.MaxTorque = Vector3.new(400000, 400000, 400000)
        bodyGyro.CFrame = game.Players.LocalPlayer.Character:WaitForChild("HumanoidRootPart").CFrame
        bodyGyro.Parent = game.Players.LocalPlayer.Character:WaitForChild("HumanoidRootPart")
        
        
        FlyButton.BackgroundColor3 = Color3.fromRGB(255, 0, 0) 
        FlyButton.TextColor3 = Color3.fromRGB(255, 255, 25)  
        FlyButton.Text = "Fly" 
    end
end)

UserInputService.InputBegan:Connect(function(input, gameProcessed)
    if gameProcessed or not flying then return end
    if input.KeyCode == Enum.KeyCode.W then
        moveDirection = moveDirection + Vector3.new(0, 0, -1)
    elseif input.KeyCode == Enum.KeyCode.S then
        moveDirection = moveDirection + Vector3.new(0, 0, 1)
    elseif input.KeyCode == Enum.KeyCode.A then
        moveDirection = moveDirection + Vector3.new(-1, 0, 0)
    elseif input.KeyCode == Enum.KeyCode.D then
        moveDirection = moveDirection + Vector3.new(1, 0, 0)
    end
end)
UserInputService.InputEnded:Connect(function(input, gameProcessed)
    if gameProcessed or not flying then return end
    if input.KeyCode == Enum.KeyCode.W then
        moveDirection = moveDirection - Vector3.new(0, 0, -1)
    elseif input.KeyCode == Enum.KeyCode.S then
        moveDirection = moveDirection - Vector3.new(0, 0, 1)
    elseif input.KeyCode == Enum.KeyCode.A then
        moveDirection = moveDirection - Vector3.new(-1, 0, 0)
    elseif input.KeyCode == Enum.KeyCode.D then
        moveDirection = moveDirection - Vector3.new(1, 0, 0)
    end
end)

game:GetService("RunService").RenderStepped:Connect(function()
    if flying and bodyVelocity then
        local character = game.Players.LocalPlayer.Character
        if character and character:FindFirstChild("HumanoidRootPart") then
            local rootPart = character.HumanoidRootPart
 
            bodyVelocity.Velocity = (Camera.CFrame.LookVector * -moveDirection.Z + Camera.CFrame.RightVector * moveDirection.X) * speed

            bodyGyro.CFrame = CFrame.new(rootPart.Position, rootPart.Position + Camera.CFrame.LookVector)
        end
    end
end)

SpeedInput.FocusLost:Connect(function()
    local newSpeed = tonumber(SpeedInput.Text)
    if newSpeed and newSpeed >= 1 and newSpeed <= 50 then
      
        speed = normalSpeed * (newSpeed)  
    else
        SpeedInput.Text = tostring(speed / normalSpeed)  
    end
end)
--  Teleport
TeleportSection.Parent = MainFrame
TeleportSection.Size = UDim2.new(0, 200, 0, 100)
TeleportSection.Position = UDim2.new(0, 5, 0.45, 0)  
TeleportSection.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
TeleportSection.BackgroundTransparency = 1 
TeleportSection.BorderSizePixel = 0

DropdownList.Parent = TeleportSection
DropdownList.Size = UDim2.new(0, 100, 0, 100)
DropdownList.Position = UDim2.new(0, 120, 0.6, 0)
DropdownList.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
DropdownList.Visible = false
DropdownList.BorderSizePixel = 0
DropdownList.ClipsDescendants = true

TeleportButton.Parent = TeleportSection
TeleportButton.Text = "Teleport"
TeleportButton.Size = UDim2.new(0, 100, 0, 30)
TeleportButton.Position = UDim2.new(0, 10, 0.2, 0) 
TeleportButton.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
TeleportButton.TextColor3 = Color3.fromRGB(255, 255, 255)
TeleportButton.Font = Enum.Font.SourceSans
TeleportButton.TextSize = 16

Dropdown.Parent = TeleportSection
Dropdown.Text = "Select Player"
Dropdown.Size = UDim2.new(0, 100, 0, 30)
Dropdown.Position = UDim2.new(0, 120, 0.2, 0)  
Dropdown.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
Dropdown.TextColor3 = Color3.fromRGB(255, 255, 255)
Dropdown.Font = Enum.Font.SourceSans
Dropdown.TextSize = 14

RefreshButton.Parent = TeleportSection
RefreshButton.Text = "Refresh Players"
RefreshButton.Size = UDim2.new(0, 100, 0, 30)
RefreshButton.Position = UDim2.new(0, 10, 0.6, 0) 
RefreshButton.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
RefreshButton.TextColor3 = Color3.fromRGB(255, 255, 255)
RefreshButton.Font = Enum.Font.SourceSans
RefreshButton.TextSize = 14

local function refreshPlayerList()
    for _, child in ipairs(DropdownList:GetChildren()) do
        if child:IsA("TextButton") then child:Destroy() end
    end
    for _, player in ipairs(game.Players:GetPlayers()) do
        local playerButton = Instance.new("TextButton")
        playerButton.Parent = DropdownList
        playerButton.Text = player.Name
        playerButton.Size = UDim2.new(1, 0, 0, 20)
        playerButton.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
        playerButton.TextColor3 = Color3.fromRGB(255, 255, 255)
        playerButton.Font = Enum.Font.SourceSans
        playerButton.TextSize = 14
        playerButton.MouseButton1Click:Connect(function()
            Dropdown.Text = player.Name
            DropdownList.Visible = false
        end)
    end
end

RefreshButton.MouseButton1Click:Connect(refreshPlayerList)
Dropdown.MouseButton1Click:Connect(function()
    DropdownList.Visible = not DropdownList.Visible
end)

TeleportButton.MouseButton1Click:Connect(function()
    local targetPlayerName = Dropdown.Text
    local targetPlayer = game.Players:FindFirstChild(targetPlayerName)
    if targetPlayer and targetPlayer.Character and targetPlayer.Character:FindFirstChild("HumanoidRootPart") then
        game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = targetPlayer.Character.HumanoidRootPart.CFrame
    else
        warn("Player not found or does not have a character!")
    end
end)

refreshPlayerList()
