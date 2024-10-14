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

-- Create Auto Farm Button
local autoFarmButton = createButton("Auto Farm", UDim2.new(0.1, 0, 0.3, 0))
autoFarmButton.MouseButton1Click:Connect(function()
    while wait(0.1) do  -- Fast auto farm
        -- Auto farm script here
        print("Auto farming...")
    end
end)

-- Create Auto Item Button
local autoItemButton = createButton("Auto Item", UDim2.new(0.1, 0, 0.5, 0))
autoItemButton.MouseButton1Click:Connect(function()
    -- Auto item script here
    print("Auto collecting items...")
end)

-- Create Auto Bounty Button
local autoBountyButton = createButton("Auto Bounty", UDim2.new(0.1, 0, 0.7, 0))
autoBountyButton.MouseButton1Click:Connect(function()
    -- Auto bounty script here
    print("Auto bounty hunting...")
end)
