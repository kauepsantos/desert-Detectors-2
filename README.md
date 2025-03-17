-- Criando a interface gráfica
local ScreenGui = Instance.new("ScreenGui")
local MainFrame = Instance.new("Frame")
local UICornerMainFrame = Instance.new("UICorner")
local Title = Instance.new("TextLabel")
local ButtonESP = Instance.new("TextButton")
local ButtonGetMoney = Instance.new("TextButton")
local ButtonItemBom = Instance.new("TextButton")
local UICornerButton1 = Instance.new("UICorner")
local UICornerButton2 = Instance.new("UICorner")
local UICornerButton3 = Instance.new("UICorner")

-- Configurações do ScreenGui
ScreenGui.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui")

-- Configurações do MainFrame
MainFrame.Parent = ScreenGui
MainFrame.BackgroundColor3 = Color3.fromRGB(50, 50, 120)
MainFrame.Size = UDim2.new(0, 400, 0, 300)
MainFrame.Position = UDim2.new(0.5, -200, 0.5, -150)
MainFrame.Active = true
MainFrame.Draggable = true

-- Cantos arredondados para o MainFrame
UICornerMainFrame.CornerRadius = UDim.new(0, 15)
UICornerMainFrame.Parent = MainFrame

-- Configurações do Título
Title.Parent = MainFrame
Title.Text = "tubergamer (1.3)"
Title.Size = UDim2.new(1, 0, 0, 50)
Title.BackgroundColor3 = Color3.fromRGB(30, 30, 90)
Title.TextColor3 = Color3.fromRGB(255, 255, 255)
Title.Font = Enum.Font.SourceSansBold
Title.TextSize = 24

-- Configurações do botão "ESP (beta)"
ButtonESP.Parent = MainFrame
ButtonESP.Text = "ESP (beta)"
ButtonESP.Size = UDim2.new(0, 350, 0, 40)
ButtonESP.Position = UDim2.new(0.5, -175, 0.3, 0)
ButtonESP.BackgroundColor3 = Color3.fromRGB(50, 200, 50)
ButtonESP.TextColor3 = Color3.fromRGB(255, 255, 255)
ButtonESP.Font = Enum.Font.SourceSansBold
ButtonESP.TextSize = 18

-- Cantos arredondados para o botão "ESP (beta)"
UICornerButton1.CornerRadius = UDim.new(0, 15)
UICornerButton1.Parent = ButtonESP

-- Funcionalidade do botão "ESP (beta)"
ButtonESP.MouseButton1Click:Connect(function()
    _G.ShowLootNames = not _G.ShowLootNames

    local nameFolder = Instance.new("Folder")
    nameFolder.Name = "0x" .. tostring(math.random(10000, 99999))
    nameFolder.Parent = workspace

    local function createNameDisplay(loot)
        local billboard = Instance.new("BillboardGui")
        billboard.Adornee = loot
        billboard.Size = UDim2.new(4, 0, 1, 0)
        billboard.StudsOffset = Vector3.new(0, 3, 0)
        billboard.AlwaysOnTop = true
        billboard.Parent = loot

        local textLabel = Instance.new("TextLabel")
        textLabel.Size = UDim2.new(1, 0, 1, 0)
        textLabel.BackgroundTransparency = 1
        textLabel.Text = loot.Name
        textLabel.TextColor3 = Color3.new(1, 1, 1)
        textLabel.TextScaled = true
        textLabel.Font = Enum.Font.GothamBold
        textLabel.Parent = billboard
    end

    local function clearAll()
        for _, loot in ipairs(workspace.Loot:GetChildren()) do
            local billboard = loot:FindFirstChildWhichIsA("BillboardGui")
            if billboard then billboard:Destroy() end
        end
    end

    if _G.ShowLootNames then
        for _, loot in ipairs(workspace.Loot:GetChildren()) do
            if not loot:FindFirstChildWhichIsA("BillboardGui") then
                createNameDisplay(loot)
            end
        end
    else
        clearAll()
    end
end)

-- Configurações do botão "get money (1.2)"
ButtonGetMoney.Parent = MainFrame
ButtonGetMoney.Text = "get money (1.2)"
ButtonGetMoney.Size = UDim2.new(0, 350, 0, 40)
ButtonGetMoney.Position = UDim2.new(0.5, -175, 0.5, 0)
ButtonGetMoney.BackgroundColor3 = Color3.fromRGB(200, 50, 50)
ButtonGetMoney.TextColor3 = Color3.fromRGB(255, 255, 255)
ButtonGetMoney.Font = Enum.Font.SourceSansBold
ButtonGetMoney.TextSize = 18

-- Cantos arredondados para o botão "get money (1.2)"
UICornerButton2.CornerRadius = UDim.new(0, 15)
UICornerButton2.Parent = ButtonGetMoney

-- Criando uma variável de debounce para impedir múltiplos loops
local isRunning = false

-- Funcionalidade do botão "get money (1.2)"
ButtonGetMoney.MouseButton1Click:Connect(function()
    if isRunning then return end -- Evita múltiplas execuções
    isRunning = true

    while isRunning do
        local rs = game:GetService("ReplicatedStorage")
        local args = {
            [1] = {
                [1] = "Getting Settled",
                [2] = {
                    [1] = {
                        [1] = 0,
                        [2] = 0
                    },
                    [2] = "Any"
                },
                [3] = {
                    [1] = 1000 -- Ajustado para dar exatamente 1.000
                },
                [4] = "Found by @kylosilly on discord <3"
            }
        }
        rs:WaitForChild("Give_Quest"):FireServer(unpack(args))
        rs:WaitForChild("Win_Quest"):FireServer("Getting Settled")
        task.wait(0.05) -- Loop rápido
    end
end)

-- Funcionalidade para parar o loop ao clicar novamente
ButtonGetMoney.MouseButton2Click:Connect(function()
    isRunning = false -- Para o loop
end)

-- Configuração do botão "item bom (em construção)"
ButtonItemBom.Parent = MainFrame
ButtonItemBom.Text = "item bom (em construção)"
ButtonItemBom.Size = UDim2.new(0, 350, 0, 40)
ButtonItemBom.Position = UDim2.new(0.5, -175, 0.7, 0)
ButtonItemBom.BackgroundColor3 = Color3.fromRGB(70, 150, 200)
ButtonItemBom.TextColor3 = Color3.fromRGB(255, 255, 255)
ButtonItemBom.Font = Enum.Font.SourceSansBold
ButtonItemBom.TextSize = 18

-- Cantos arredondados para o botão "item bom (em construção)"
UICornerButton3.CornerRadius = UDim.new(0, 15)
UICornerButton3.Parent = ButtonItemBom
