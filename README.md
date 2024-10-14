-- Create the ScreenGui
local screenGui = Instance.new("ScreenGui")
screenGui.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui")

-- Create the Frame
local frame = Instance.new("Frame")
frame.Size = UDim2.new(0.3, 0, 0.5, 0)
frame.Position = UDim2.new(0.35, 0, 0.25, 0)
frame.BackgroundColor3 = Color3.new(0.1, 0.1, 0.1)
frame.Parent = screenGui

-- Create the TextLabel
local textLabel = Instance.new("TextLabel")
textLabel.Size = UDim2.new(1, 0, 0.2, 0)
textLabel.Position = UDim2.new(0, 0, 0, 0)
textLabel.BackgroundTransparency = 1
textLabel.Text = "Ruazu Hub"
textLabel.TextColor3 = Color3.new(1, 1, 1)
textLabel.Font = Enum.Font.SourceSansBold
textLabel.TextScaled = true
textLabel.Parent = frame

-- Function to create buttons
local function createButton(name, position)
    local button = Instance.new("TextButton")
    button.Size = UDim2.new(0.8, 0, 0.1, 0)
    button.Position = position
    button.BackgroundColor3 = Color3.new(0.2, 0.2, 0.8)
    button.Text = name
    button.TextColor3 = Color3.new(1, 1, 1)
    button.Font = Enum.Font.SourceSansBold
    button.TextScaled = true
    button.Parent = frame
    return button
end

-- Function to stop farming, collecting or hunting
local function stopActions()
    autoFarming = false
    autoCollecting = false
    autoHunting = false
end

-- Auto Farm Function
local autoFarming = false
local function autoFarm()
    if autoFarming then
        autoFarming = false
        return
    end
    autoFarming = true
    spawn(function()
        while autoFarming do
            for _, npc in pairs(game.Workspace.NPCs:GetChildren()) do
                if npc:FindFirstChild("Humanoid") and autoFarming then
                    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = npc.HumanoidRootPart.CFrame
                    -- Attack logic
                    print("Farming " .. npc.Name)
                end
            end
            wait(0.1)
        end
    end)
end

-- Auto Item Function
local autoCollecting = false
local function autoItem()
    if autoCollecting then
        autoCollecting = false
        return
    end
    autoCollecting = true
    spawn(function()
        while autoCollecting do
            for _, item in pairs(game.Workspace.Items:GetChildren()) do
                game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = item.CFrame
                -- Item pickup logic
                print("Picking up " .. item.Name)
            end
            wait(0.1)
        end
    end)
end

-- Auto Bounty Function
local autoHunting = false
local function autoBounty()
    if autoHunting then
        autoHunting = false
        return
    end
    autoHunting = true
    spawn(function()
        while autoHunting do
            for _, player in pairs(game.Players:GetPlayers()) do
                if player ~= game.Players.LocalPlayer and autoHunting then
                    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = player.Character.HumanoidRootPart.CFrame
                    -- Attack logic
                    print("Hunting " .. player.Name)
                end
            end
            wait(0.1)
        end
    end)
end

-- Create Auto Farm Button
local autoFarmButton = createButton("Auto Farm", UDim2.new(0.1, 0, 0.3, 0))
autoFarmButton.MouseButton1Click:Connect(autoFarm)
autoFarmButton.MouseButton2Click:Connect(stopActions) -- Stop on right click

-- Create Auto Item Button
local autoItemButton = createButton("Auto Item", UDim2.new(0.1, 0, 0.5, 0))
autoItemButton.MouseButton1Click:Connect(autoItem)
autoItemButton.MouseButton2Click:Connect(stopActions) -- Stop on right click

-- Create Auto Bounty Button
local autoBountyButton = createButton("Auto Bounty", UDim2.new(0.1, 0, 0.7, 0))
autoBountyButton.MouseButton1Click:Connect(autoBounty)
autoBountyButton.MouseButton2Click:Connect(stopActions) -- Stop on right click
