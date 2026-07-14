# FireballVFXClient

local UserInputService = game:GetService("UserInputService")
local Players = game:GetService("Players")
local ReplicatedStorage = game:GetService("ReplicatedStorage")

local player = Players.LocalPlayer
local fireballVFX = ReplicatedStorage:WaitForChild("FireballVFX")

local function hasFireballEquipped()
	local character = player.Character
	if not character then return false end
	for _, tool in ipairs(character:GetChildren()) do
		if tool:IsA("Tool") and tool.Name == "FIREBALL" then
			return true
		end
	end
	return false
end

UserInputService.InputBegan:Connect(function(input, gameProcessed)
	if gameProcessed then return end
	if input.KeyCode == Enum.KeyCode.Z then
		if hasFireballEquipped() then
			fireballVFX:FireServer()
		end
	end
end)
