-- LocalScript for the UI and Backpack listing using JJSploit

local player = game.Players.LocalPlayer
local screenGui = Instance.new("ScreenGui")
screenGui.Parent = player:WaitForChild("PlayerGui")

-- Create a button
local button = Instance.new("TextButton")
button.Size = UDim2.new(0, 200, 0, 50)  -- Button size
button.Position = UDim2.new(0.5, -100, 0.5, -25)  -- Center the button
button.Text = "Show Backpack"
button.Parent = screenGui

-- Function to show the Backpack contents when button is clicked
local function showBackpack()
    -- Wait for the character to be loaded
    if player.Character and player.Character:FindFirstChild("Backpack") then
        local backpack = player.Backpack  -- Access the local player's Backpack
        print(player.Name .. "'s Backpack contains:")

        -- Loop through all items in the Backpack
        for _, item in ipairs(backpack:GetChildren()) do
            -- Check if the item is a Tool
            if item:IsA("Tool") then
                print("  - Tool: " .. item.Name)
            else
                print("  - " .. item.Name .. " (not a tool)")  -- Non-tool items
            end
        end
    else
        print(player.Name .. " does not have a Backpack or Character!")
    end
end

-- Connect button click to the showBackpack function
button.MouseButton1Click:Connect(showBackpack)

-- Optional: Add a little animation (Tweening) for the button appearance
local TweenService = game:GetService("TweenService")
local goal = {BackgroundColor3 = Color3.fromRGB(0, 255, 0)}  -- Change color on click
local tweenInfo = TweenInfo.new(0.5, Enum.EasingStyle.Bounce, Enum.EasingDirection.Out)
local tween = TweenService:Create(button, tweenInfo, goal)

button.MouseButton1Click:Connect(function()
    tween:Play()
end)
