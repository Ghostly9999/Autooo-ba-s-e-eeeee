local tycoonLists = {
    [5142372758] = { -- Jogo 1
        "Spike", "Strong", "Stone", "Robotic", "Magic", "Web", "Dark", "Insanity", "Giant", "Storm"
    },
    [10065006658] = { -- Jogo 2
        "Frozen", "Nuclear", "Void", "Thunder", "Shadow", "Toxic", "Kong", "Mecha", "Magma", "Hyper"
    }
}

local allowedTycoons = tycoonLists[game.PlaceId] or {}

local Players = game:GetService("Players")
local LocalPlayer = Players.LocalPlayer
local RunService = game:GetService("RunService")

local touchinterest = {}
local firetouchinterest = firetouchinterest or function(part, part2, value)
    if part and part2 then
        if value == 0 then
            touchinterest[1] = part.CFrame
            part.CFrame = part2.CFrame
        else
            part.CFrame = touchinterest[1]
            touchinterest[1] = nil
        end
    end
end

-- Verifica se o jogador já possui uma base
local function PlayerHasBase()
    for _, tycoon in pairs(workspace.Tycoons:GetChildren()) do
        local ownerObject = tycoon:FindFirstChild("isim")
        if ownerObject and ownerObject.Value == LocalPlayer.Name then
            return true
        end
    end
    return false
end

-- Verifica se o tycoon está disponível
local function OwnerlessTycoon(name)
    local tycoon = workspace.Tycoons:FindFirstChild(name)
    local ownerObject = tycoon and tycoon:FindFirstChild("isim")
    return ownerObject and not Players:FindFirstChild(ownerObject.Value)
end

-- Tenta reivindicar um tycoon
local function ClaimTycoon(name)
    local tycoon = workspace.Tycoons:FindFirstChild(name)
    local claimDoor = tycoon and tycoon:FindFirstChild("Door")
    local root = LocalPlayer.Character and LocalPlayer.Character:FindFirstChild("HumanoidRootPart")
    if claimDoor and root then
        for _, v in pairs(claimDoor:GetChildren()) do
            if v:IsA("BasePart") then
                firetouchinterest(root, v, 0)
                firetouchinterest(root, v, 1)
            end
        end
    end
end

-- Busca e reivindica um tycoon disponível
local function FindAndClaimTycoon()
    for _, name in ipairs(allowedTycoons) do
        if PlayerHasBase() then
            return true
        end

        if OwnerlessTycoon(name) then
            for i = 1, 2 do
                ClaimTycoon(name)
                wait(0.1)

                local tycoon = workspace.Tycoons:FindFirstChild(name)
                local ownerObject = tycoon and tycoon:FindFirstChild("isim")

                if ownerObject and Players:FindFirstChild(ownerObject.Value) == LocalPlayer then
                    return true
                end
            end
        end
    end
    return false
end

-- Loop infinito para garantir que o jogador sempre tenha uma base
RunService.Heartbeat:Connect(function()
    local character = LocalPlayer.Character or LocalPlayer.CharacterAdded:Wait()
    local humanoid = character:FindFirstChild("Humanoid")

    if humanoid and humanoid.Health == 0 then
        LocalPlayer.CharacterAdded:Wait()
    end

    if not PlayerHasBase() then
        FindAndClaimTycoon()
    end
end)
