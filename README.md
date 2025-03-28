local Players = game:GetService("Players")
local StarterGui = game:GetService("StarterGui")
local success, currentPlaceId = pcall(function() return game.PlaceId end)
if not success then currentPlaceId = nil end

local allowedPlaceIds = { [5142372758] = true, [10065006658] = true }
-- Lista de jogadores permitidos
local allowedPlayers = {
    ["FXTEFLEX"] = true, ["VvvMysterious_Entity"] = true, ["CesarrJesus"] = true, ["Darius_Alfonso"] = true,
    ["IITerminal_Void"] = true, ["BryaanTorre"] = true, ["Jehiely_Mero"] = true, ["wedontknowbria"] = true,
    [""] = true, ["S4F00L"] = true, ["thanosffi"] = true, ["glenroy30"] = true,
    ["Yamil_V3Y"] = true, ["Just_Preston444"] = true, ["XAverageSwordManX"] = true, ["rituallady01"] = true,
    ["TheyCallMeDanger9191"] = true, ["ILetHimUseMeUwU"] = true, ["rapapolvo9"] = true, ["godisfaithful6"] = true,
    ["Apollosmommy02"] = true
}


local function copyToClipboard(text)
    setclipboard(text)
end

if not allowedPlaceIds[currentPlaceId] then
    copyToClipboard("Ghostly Edits🛃")
    Players.LocalPlayer:Kick("Game Not Found/010101010101/")
    return
end

if not allowedPlayers[Players.LocalPlayer.Name] then
    copyToClipboard("Ghostly Edits🛃")
    Players.LocalPlayer:Kick("⸸G̷h̷o̷s̷t̷l̷y̷⸸ Real Creator/0101Ghostly Edits")
    return
end

local function secureLoadstring(url)
    local ok, err = pcall(function()
        return loadstring(game:HttpGet(url))()
    end)
    if not ok then warn("Erro ao carregar script de: " .. url .. "\nErro: " .. tostring(err)) end
end

local playerName = Players.LocalPlayer.Name
local imageId = "rbxassetid://98338389851088"

StarterGui:SetCore("SendNotification", {
    Title = "Welcome",
    Text = "Welcome " .. playerName,
    Icon = imageId,
    Duration = 5
})

copyToClipboard("Ghostly Edits🛃")

local ScreenGui = Instance.new("ScreenGui", game.CoreGui)
ScreenGui.Name = "GhostlyHubPro"

local Frame = Instance.new("Frame", ScreenGui)
Frame.Size = UDim2.new(0.35, 0, 0.4, 0)
Frame.Position = UDim2.new(0.325, 0, 0.3, 0)
Frame.BackgroundColor3 = Color3.fromRGB(25, 25, 25)
Frame.BorderSizePixel = 0
Frame.Visible = false

local UICorner = Instance.new("UICorner", Frame)
UICorner.CornerRadius = UDim.new(0, 10)

local UIStroke = Instance.new("UIStroke", Frame)
UIStroke.Thickness = 4

task.spawn(function()
    while true do
        UIStroke.Color = Color3.new(1, 0, 0)
        task.wait(0.5)
        UIStroke.Color = Color3.new(0, 0, 1)
        task.wait(0.5)
    end
end)

local UIGridLayout = Instance.new("UIGridLayout", Frame)
UIGridLayout.CellSize = UDim2.new(0.25, -5, 0.25, -5)
UIGridLayout.CellPadding = UDim2.new(0, 5, 0, 5)
UIGridLayout.FillDirectionMaxCells = 4

local buttons = {
    Page1 = {
        {"GET TOOLS", "https://raw.githubusercontent.com/Ghostly9999/Gets-toolss/refs/heads/main/README.md"},
        {"RESPAWN", "https://raw.githubusercontent.com/Ghostly9999/e-Oh-RESPAWN-ne-vida/refs/heads/main/README.md"},
        {"AUTO BASE SPT", "https://raw.githubusercontent.com/Ghostly9999/Baseeeeeeeese/refs/heads/main/README.md"},
        {"HIT BOX", "https://raw.githubusercontent.com/Ghostly9999/Hit-boxis-/refs/heads/main/README.md"},
        {"NO COOLDOWN", "https://raw.githubusercontent.com/Ghostly9999/No-cooldown-82299229/refs/heads/main/README.md"},
        {"ANTI CHAT SPY", "https://pastebin.com/raw/ECZP85Ud"},
        {"CHAT SPY", "https://rawscripts.net/raw/Universal-Script-Chat-spy-20280"},
        {"ANTI BANG", "https://rawscripts.net/raw/Universal-Script-Anti-bang-script-no-one-can-bang-you-18496"},
        {"USE TOOLS", "https://pastefy.app/vxu5jGb0/raw"},
        {"GET BASE MPT", "https://pastefy.app/TVWnH7bn/raw"},
        {"AUTO BUY", "https://pastebin.com/raw/QUHsSNCS"},
        {"ANTI LAG", "https://raw.githubusercontent.com/Ghostly9999/Anti-lag-/refs/heads/main/README.md"},
        {"HEX SHIELD", "https://raw.githubusercontent.com/Ghostly9999/Auraaa/refs/heads/main/README.md"},
        {"NOCLIP", "https://pastefy.app/8Nqj67eP/raw"},
        {"LOOP BRING", "https://raw.githubusercontent.com/Ghostly9999/Loopbringbbbbbb/refs/heads/main/README.md"},
        {"PAG 2", nil}
    },
    Page2 = {
        {"Float v1", "https://pastefy.app/XPHen0MY/raw"},
        {"Reach v3", "https://raw.githubusercontent.com/Ghostly9999/Reachh/refs/heads/main/README.md"},
        {"Aura SPT", "https://pastebin.com/raw/bCDQwE8A"},
        {"Aura SPT 2", "https://pastebin.com/raw/PDb4vqec"},
        {"reach V2 SPT", "https://pastebin.com/raw/JBgVCKrc"},
        {"SPEED/JUMP", "https://raw.githubusercontent.com/Ghostly9999/Speed-Jump/refs/heads/main/README.md"},
        {"INFINITY YIELD", "https://raw.githubusercontent.com/EdgeIY/infiniteyield/master/source"},
        {"BEAST MODE", "https://pastebin.com/raw/tJybmgTs"},
        {"USE TOOLS 2", "https://pastefy.app/UYA1eBRX/raw"},
        {"PAG 1", nil}
    }
}

local currentPage = "Page1"

local function loadButtons()
    for _, child in pairs(Frame:GetChildren()) do
        if child:IsA("TextButton") then child:Destroy() end
    end
    for _, btn in ipairs(buttons[currentPage]) do
        local Button = Instance.new("TextButton", Frame)
        Button.Text = btn[1]
        Button.Size = UDim2.new(0, 100, 0, 40)
        Button.TextColor3 = Color3.fromRGB(255, 255, 255)
        Button.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
        Button.BorderSizePixel = 2
        Button.BorderColor3 = Color3.fromRGB(150, 150, 150)

        local ButtonCorner = Instance.new("UICorner", Button)
        ButtonCorner.CornerRadius = UDim.new(0, 10)

        Button.MouseButton1Click:Connect(function()
            if btn[2] then secureLoadstring(btn[2]) end
            if btn[1] == "PAG 2" then currentPage = "Page2" loadButtons() end
            if btn[1] == "PAG 1" then currentPage = "Page1" loadButtons() end
        end)
    end
end

loadButtons()

local ToggleButton = Instance.new("TextButton", ScreenGui)
ToggleButton.Text = "Ativar"
ToggleButton.Position = UDim2.new(0.95, -110, 0, 10)
ToggleButton.Size = UDim2.new(0, 100, 0, 40)
ToggleButton.TextColor3 = Color3.fromRGB(255, 255, 255)
ToggleButton.BackgroundColor3 = Color3.fromRGB(50, 50, 50)

local ToggleCorner = Instance.new("UICorner", ToggleButton)
ToggleCorner.CornerRadius = UDim.new(0, 10)

ToggleButton.MouseButton1Click:Connect(function()
    Frame.Visible = not Frame.Visible
    ToggleButton.Text = Frame.Visible and "Desativar" or "Ativar"
end)

Frame.Visible = true
