-- 👁️ Transparent ESP by 9QQASU
local Players = game:GetService("Players")
local LocalPlayer = Players.LocalPlayer

-- ✅ ฟังก์ชันสร้าง ESP แบบใส
local function applyTransparentESP(player)
    local function onChar(char)
        if not char:FindFirstChild("ESP") then
            local esp = Instance.new("Highlight")
            esp.Name = "ESP"
            esp.FillColor = Color3.fromRGB(0, 255, 255) -- สีฟ้าใส
            esp.FillTransparency = 0.8 -- ใสมาก
            esp.OutlineColor = Color3.fromRGB(255, 255, 255)
            esp.OutlineTransparency = 0.3
            esp.Adornee = char
            esp.Parent = char
        end
    end
    if player.Character then onChar(player.Character) end
    player.CharacterAdded:Connect(onChar)
end

-- ✅ ฟังก์ชันลบ ESP
local function removeESP(player)
    if player.Character and player.Character:FindFirstChild("ESP") then
        player.Character.ESP:Destroy()
    end
end

-- ✅ สร้าง ESP สำหรับทุกคน
for _, player in pairs(Players:GetPlayers()) do
    if player ~= LocalPlayer then
        applyTransparentESP(player)
    end
end

-- ✅ รองรับผู้เล่นใหม่
Players.PlayerAdded:Connect(function(player)
    player.CharacterAdded:Connect(function()
        applyTransparentESP(player)
    end)
end)
