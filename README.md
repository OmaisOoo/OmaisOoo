local Sounds = {
    Screamer = "rbxassetid://9121609859", -- grito de terror
    Jumpscare = "rbxassetid://8934125122", -- susto forte
    Breathing = "rbxassetid://183763512", -- respiração assustadora
    Static = "rbxassetid://9121628917", -- estática de rádio tensa
    DeepBoom = "rbxassetid://138186576", -- batida grave de tensão
}

local Players = game:GetService("Players")
local LocalPlayer = Players.LocalPlayer

-- Interface simples (Delta mobile)
local gui = Instance.new("ScreenGui", LocalPlayer:WaitForChild("PlayerGui"))
gui.Name = "SoundTerrorUI"
gui.ResetOnSpawn = false

local yOffset = 10
for name, soundId in pairs(Sounds) do
    local btn = Instance.new("TextButton", gui)
    btn.Size = UDim2.new(0, 160, 0, 40)
    btn.Position = UDim2.new(0, 10, 0, yOffset)
    btn.Text = "Play: " .. name
    btn.BackgroundColor3 = Color3.fromRGB(40, 0, 0)
    btn.TextColor3 = Color3.new(1, 1, 1)
    btn.TextScaled = true

    btn.MouseButton1Click:Connect(function()
        local sound = Instance.new("Sound")
        sound.SoundId = soundId
        sound.Volume = 5
        sound.Looped = false
        sound.Parent = workspace
        sound:Play()
        game:GetService("Debris"):AddItem(sound, 10) -- remove após 10s
    end)

    yOffset = yOffset + 50
end
