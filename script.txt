-- This script should be run from the local player's perspective using JJSploit

local player = game.Players.LocalPlayer

-- Wait for the player's character to load
player.CharacterAdded:Wait()

-- Ensure the player has a Backpack
if player.Character and player.Character:FindFirstChild("Backpack") then
    local backpack = player.Backpack
    print(player.Name .. "'s Backpack contains:")

    -- Loop through all items in the Backpack
    for _, item in ipairs(backpack:GetChildren()) do
        if item:IsA("Tool") then
            print("  - " .. item.Name)  -- Print each tool name
        else
            print("  - " .. item.Name .. " (not a tool)")  -- Non-tool items
        end
    end
else
    print(player.Name .. " does not have a Backpack or Character!")
end
