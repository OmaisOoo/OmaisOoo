local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local LocalPlayer = Players.LocalPlayer
local Character = LocalPlayer.Character or LocalPlayer.CharacterAdded:Wait()

-- Noclip ativado por padrão = false
local noclip = false

-- Invisible ativado por padrão = false
local invisible = false

-- Função de Noclip
RunService.Stepped:Connect(function()
    if noclip and Character then
        for _, part in pairs(Character:GetDescendants()) do
            if part:IsA("BasePart") and part.CanCollide == true then
                part.CanCollide = false
            end
        end
    end
end)

-- Função de invisibilidade
local function setInvisible(state)
    if not Character then return end
    for _, part in pairs(Character:GetDescendants()) do
        if part:IsA("BasePart") and part.Name ~= "HumanoidRootPart" then
            part.Transparency = state and 1 or 0
        elseif part:IsA("Decal") then
            part.Transparency = state and 1 or 0
        end
    end
end

-- Interface simples para Delta (Mobile friendly)
local gui = Instance.new("ScreenGui", LocalPlayer:WaitForChild("PlayerGui"))
gui.ResetOnSpawn = false
gui.Name = "BrookhavenMod"

local function createButton(text, position, callback)
    local btn = Instance.new("TextButton", gui)
    btn.Size = UDim2.new(0, 140, 0, 40)
    btn.Position = position
    btn.Text = text
    btn.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
    btn.TextColor3 = Color3.new(1, 1, 1)
    btn.TextScaled = true
    btn.MouseButton1Click:Connect(callback)
    return btn
end

-- Botão Noclip
createButton("Toggle Noclip", UDim2.new(0, 10, 0, 10), function()
    noclip = not noclip
end)

-- Botão Invisível
createButton("Toggle Invisível", UDim2.new(0, 10, 0, 60), function()
    invisible = not invisible
    setInvisible(invisible)
end)
