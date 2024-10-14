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

-- Teleport Function
local function teleportTo(target)
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = target.CFrame
end

-- Auto Farm Function
local function autoFarm()
    spawn(function()
        while wait(0.1) do  -- Fast auto farm
            for _, npc in pairs(game.Workspace.NPCs:GetChildren()) do
                if npc:FindFirstChild("Humanoid") then
                    teleportTo(npc.HumanoidRootPart)
                    -- Attack logic
                    print("Farming " .. npc.Name)
                end
            end
        end
    end)
end

-- Auto Item Function
local function autoItem()
    spawn(function()
        while wait(0.1) do
            for _, item in pairs(game.Workspace.Items:GetChildren()) do
                teleportTo(item)
                -- Item pickup logic
                print("Picking up " .. item.Name)
            end
        end
    end)
end

-- Auto Bounty Function
local function autoBounty()
    spawn(function()
        while wait(0.1) do
            for _, player in pairs(game.Players:GetPlayers()) do
                if player ~= game.Players.LocalPlayer then
                    teleportTo(player.Character.HumanoidRootPart)
                    -- Attack logic
                    print("Hunting " .. player.Name)
                end
            end
        end
    end)
end

-- Create Auto Farm Button
local autoFarmButton = createButton("Auto Farm", UDim2.new(0.1, 0, 0.3, 0))
autoFarmButton.MouseButton1Click:Connect(autoFarm)

-- Create Auto Item Button
local autoItemButton = createButton("Auto Item", UDim2.new(0.1, 0, 0.5, 0))
autoItemButton.MouseButton1Click:Connect(autoItem)

-- Create Auto Bounty Button
local autoBountyButton = createButton("Auto Bounty", UDim2.new(0.1, 0, 0.7, 0))
autoBountyButton.MouseButton1Click:Connect(autoBounty)
