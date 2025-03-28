local tycoonLists = {
    [5142372758] = { -- Jogo 1 (Nova ordem de prioridade)
        "Robotic", "Magic", "Storm", "Stone", "Spike", "Strong", "Web", "Dark", "Insanity", "Giant"
    }
}

local allowedTycoons = tycoonLists[game.PlaceId] or {}

local Players = game:GetService("Players")
local LocalPlayer = Players.LocalPlayer
local RunService = game:GetService("RunService")

local function WaitForTycoons()
    while not workspace:FindFirstChild("Tycoons") do
        wait(1) -- Aguarda a estrutura carregar
    end
end

local function WaitForCharacter()
    if not LocalPlayer.Character or not LocalPlayer.Character:FindFirstChild("HumanoidRootPart") then
        LocalPlayer.CharacterAdded:Wait()
        repeat wait() until LocalPlayer.Character and LocalPlayer.Character:FindFirstChild("HumanoidRootPart")
    end
end

local function PlayerHasBase()
    for _, tycoon in pairs(workspace.Tycoons:GetChildren()) do
        local ownerObject = tycoon:FindFirstChild("isim")
        if ownerObject and ownerObject.Value == LocalPlayer.Name then
            return true
        end
    end
    return false
end

local function OwnerlessTycoon(name)
    local tycoon = workspace.Tycoons:FindFirstChild(name)
    local ownerObject = tycoon and tycoon:FindFirstChild("isim")
    return ownerObject and not Players:FindFirstChild(ownerObject.Value)
end

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

local function FindAndClaimTycoon()
    if game.PlaceId ~= 5142372758 then
        return -- Se não estiver no lugar certo, não faz nada
    end

    for _, name in ipairs(allowedTycoons) do
        if PlayerHasBase() then return end
        if OwnerlessTycoon(name) then
            ClaimTycoon(name)

            local tycoon = workspace.Tycoons:FindFirstChild(name)
            local ownerObject = tycoon and tycoon:FindFirstChild("isim")

            if ownerObject and ownerObject.Value == LocalPlayer.Name then
                return
            end
        end
    end
end

RunService.Heartbeat:Connect(function()
    if game.PlaceId == 5142372758 then
        WaitForTycoons()
        WaitForCharacter()

        if not PlayerHasBase() then
            FindAndClaimTycoon()
        end
    end
end)
