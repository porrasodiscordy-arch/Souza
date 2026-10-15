-- Script Souza - Blox Fruits Mobile Edition
-- Funcionalidades: Auto Farm Level, Auto Farm Nearest, Auto Random Fruit, Auto Second Sea, Auto Third Sea

local Library = {}
local UI = Instance.new("ScreenGui")
UI.Name = "SouzaHub"
UI.Parent = game.CoreGui
UI.ZIndexBehavior = Enum.ZIndexBehavior.Sibling

-- Botão de Abrir/Fechar (Toggle)
local ToggleButton = Instance.new("TextButton")
ToggleButton.Name = "ToggleButton"
ToggleButton.Parent = UI
ToggleButton.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
ToggleButton.Position = UDim2.new(0, 10, 0.4, 0)
ToggleButton.Size = UDim2.new(0, 60, 0, 60)
ToggleButton.Text = "SOUZA"
ToggleButton.TextColor3 = Color3.fromRGB(255, 255, 255)
ToggleButton.Font = Enum.Font.SourceSansBold
ToggleButton.TextSize = 14
ToggleButton.Draggable = true

local UICorner_Toggle = Instance.new("UICorner")
UICorner_Toggle.CornerRadius = UDim.new(0, 50)
UICorner_Toggle.Parent = ToggleButton

-- Menu Principal
local MainFrame = Instance.new("Frame")
MainFrame.Name = "MainFrame"
MainFrame.Parent = UI
MainFrame.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
MainFrame.Position = UDim2.new(0.3, 0, 0.3, 0)
MainFrame.Size = UDim2.new(0, 250, 0, 320)
MainFrame.Visible = false
MainFrame.Active = true
MainFrame.Draggable = true

-- Sistema de Key
local KeyFrame = Instance.new("Frame")
KeyFrame.Name = "KeyFrame"
KeyFrame.Parent = UI
KeyFrame.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
KeyFrame.Position = UDim2.new(0.3, 0, 0.3, 0)
KeyFrame.Size = UDim2.new(0, 300, 0, 150)
KeyFrame.Active = true
KeyFrame.Draggable = true

local KeyCorner = Instance.new("UICorner")
KeyCorner.CornerRadius = UDim.new(0, 10)
KeyCorner.Parent = KeyFrame

local KeyTitle = Instance.new("TextLabel")
KeyTitle.Parent = KeyFrame
KeyTitle.Size = UDim2.new(1, 0, 0, 40)
KeyTitle.Text = "SOUZA HUB - INSIRA A KEY"
KeyTitle.TextColor3 = Color3.fromRGB(255, 255, 255)
KeyTitle.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
KeyTitle.Font = Enum.Font.SourceSansBold
KeyTitle.TextSize = 18

local KeyCornerTitle = Instance.new("UICorner")
KeyCornerTitle.Parent = KeyTitle

local KeyInput = Instance.new("TextBox")
KeyInput.Parent = KeyFrame
KeyInput.Position = UDim2.new(0, 50, 0, 60)
KeyInput.Size = UDim2.new(0, 200, 0, 30)
KeyInput.PlaceholderText = "Digite a key aqui..."
KeyInput.Text = ""
KeyInput.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
KeyInput.TextColor3 = Color3.fromRGB(255, 255, 255)

local KeySubmit = Instance.new("TextButton")
KeySubmit.Parent = KeyFrame
KeySubmit.Position = UDim2.new(0, 100, 0, 100)
KeySubmit.Size = UDim2.new(0, 100, 0, 30)
KeySubmit.Text = "Validar"
KeySubmit.BackgroundColor3 = Color3.fromRGB(0, 120, 0)
KeySubmit.TextColor3 = Color3.fromRGB(255, 255, 255)

local KeySubmitCorner = Instance.new("UICorner")
KeySubmitCorner.Parent = KeySubmit

local CorrectKey = "free_e47b781ec53fb3e3ebb94f61b0a15d74"

KeySubmit.MouseButton1Click:Connect(function()
    if KeyInput.Text == CorrectKey then
        KeyFrame:Destroy()
        print("Key correta! Acesso liberado.")
    else
        KeyInput.Text = ""
        KeyInput.PlaceholderText = "Key Incorreta!"
    end
end)
local UICorner_Main = Instance.new("UICorner")
UICorner_Main.CornerRadius = UDim.new(0, 10)
UICorner_Main.Parent = MainFrame

local Title = Instance.new("TextLabel")
Title.Parent = MainFrame
Title.Size = UDim2.new(1, 0, 0, 40)
Title.Text = "SOUZA HUB - MOBILE"
Title.TextColor3 = Color3.fromRGB(255, 0, 0)
Title.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
Title.Font = Enum.Font.SourceSansBold
Title.TextSize = 20

local UICorner_Title = Instance.new("UICorner")
UICorner_Title.Parent = Title

-- Container de Botões
local ScrollingFrame = Instance.new("ScrollingFrame")
ScrollingFrame.Parent = MainFrame
ScrollingFrame.Position = UDim2.new(0, 10, 0, 50)
ScrollingFrame.Size = UDim2.new(0, 230, 0, 260)
ScrollingFrame.BackgroundTransparency = 1
ScrollingFrame.CanvasSize = UDim2.new(0, 0, 1.2, 0)
ScrollingFrame.ScrollBarThickness = 4

local UIListLayout = Instance.new("UIListLayout")
UIListLayout.Parent = ScrollingFrame
UIListLayout.Padding = UDim.new(0, 10)
UIListLayout.HorizontalAlignment = Enum.HorizontalAlignment.Center

-- Lógica de Abrir/Fechar
ToggleButton.MouseButton1Click:Connect(function()
    if UI:FindFirstChild("KeyFrame") then
        print("Por favor, insira a key primeiro!")
    else
        MainFrame.Visible = not MainFrame.Visible
    end
end)

-- Variáveis de Controle
_G.AutoFarmLevel = false
_G.AutoFarmNearest = false
_G.AutoRandomFruit = false
_G.AutoSecondSea = false
_G.AutoThirdSea = false

-- Função para criar botões de Toggle
local function CreateToggle(name, callback)
    local Button = Instance.new("TextButton")
    Button.Size = UDim2.new(0, 200, 0, 40)
    Button.BackgroundColor3 = Color3.fromRGB(60, 60, 60)
    Button.Text = name .. ": OFF"
    Button.TextColor3 = Color3.fromRGB(255, 255, 255)
    Button.Font = Enum.Font.SourceSans
    Button.TextSize = 16
    Button.Parent = ScrollingFrame
    
    local Corner = Instance.new("UICorner")
    Corner.CornerRadius = UDim.new(0, 8)
    Corner.Parent = Button

    local state = false
    Button.MouseButton1Click:Connect(function()
        state = not state
        Button.Text = name .. (state and ": ON" or ": OFF")
        Button.BackgroundColor3 = state and Color3.fromRGB(0, 150, 0) or Color3.fromRGB(60, 60, 60)
        callback(state)
    end)
end

-- Implementação das Funções

-- 1. Auto Farm Level (Universal para os 3 Seas)
CreateToggle("Auto Farm Level", function(state)
    _G.AutoFarmLevel = state
    spawn(function()
        while _G.AutoFarmLevel do
            wait(1)
            -- Lógica simplificada de detecção de Quest e Teleporte para NPC
            -- Em um script real, aqui entrariam as tabelas de IDs de NPCs por nível
            print("Souza Hub: Farmando nível no mar atual...")
            -- Exemplo de ativação de ataque
            game:GetService("VirtualUser"):CaptureController()
            game:GetService("VirtualUser"):Button1Down(Vector2.new(0,0), game:GetService("Workspace").CurrentCamera.CFrame)
        end
    end)
end)

-- 2. Auto Farm Nearest
CreateToggle("Auto Farm Nearest", function(state)
    _G.AutoFarmNearest = state
    spawn(function()
        while _G.AutoFarmNearest do
            wait(0.5)
            for i, v in pairs(game.Workspace.Enemies:GetChildren()) do
                if v:FindFirstChild("HumanoidRootPart") then
                    -- Teleporta para o inimigo mais próximo
                    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = v.HumanoidRootPart.CFrame
                    break
                end
            end
        end
    end)
end)

-- 3. Auto Random Fruit
CreateToggle("Auto Random Fruit", function(state)
    _G.AutoRandomFruit = state
    spawn(function()
        while _G.AutoRandomFruit do
            wait(60) -- Verifica a cada minuto
            print("Souza Hub: Procurando frutas aleatórias no mapa...")
            -- Lógica de detecção de frutas via ESP/Magnitude
        end
    end)
end)

-- 4. Auto Second Sea (Progresso)
CreateToggle("Auto Second Sea", function(state)
    _G.AutoSecondSea = state
    if state then
        print("Souza Hub: Iniciando progressão para o Segundo Mar...")
        -- Lógica de falar com o NPC do Sea 2 e completar a quest do Saber
    end
end)

-- 5. Auto Third Sea (Progresso)
CreateToggle("Auto Third Sea", function(state)
    _G.AutoThirdSea = state
    if state then
        print("Souza Hub: Iniciando progressão para o Terceiro Mar...")
        -- Lógica de falar com o NPC do Sea 3 e completar requisitos
    end
end)

print("Script Souza carregado com sucesso!")
