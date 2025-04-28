-- Interface Gráfica Simples em Português
-- by GBzin 


local player = game.Players.LocalPlayer
local screenGui = Instance.new("ScreenGui", player.PlayerGui)
screenGui.Name = "PainelFarm"

local frame = Instance.new("Frame", screenGui)
frame.Size = UDim2.new(0, 200, 0, 220)
frame.Position = UDim2.new(0, 10, 0, 10)
frame.BackgroundColor3 = Color3.fromRGB(25, 25, 25)

local titulo = Instance.new("TextLabel", frame)
titulo.Size = UDim2.new(1, 0, 0, 30)
titulo.Text = "Painel de Farm"
titulo.TextColor3 = Color3.fromRGB(255, 255, 255)
titulo.BackgroundTransparency = 1
titulo.Font = Enum.Font.SourceSansBold
titulo.TextSize = 20

-- Botão Farm Inimigos
local botaoFarm = Instance.new("TextButton", frame)
botaoFarm.Size = UDim2.new(1, -20, 0, 40)
botaoFarm.Position = UDim2.new(0, 10, 0, 40)
botaoFarm.Text = "Farmar Inimigos"
botaoFarm.BackgroundColor3 = Color3.fromRGB(30, 144, 255)
botaoFarm.TextColor3 = Color3.fromRGB(255, 255, 255)
botaoFarm.Font = Enum.Font.SourceSansBold
botaoFarm.TextSize = 18

-- Botão Farm Baús
local botaoBaus = Instance.new("TextButton", frame)
botaoBaus.Size = UDim2.new(1, -20, 0, 40)
botaoBaus.Position = UDim2.new(0, 10, 0, 90)
botaoBaus.Text = "Coletar Baús"
botaoBaus.BackgroundColor3 = Color3.fromRGB(34, 139, 34)
botaoBaus.TextColor3 = Color3.fromRGB(255, 255, 255)
botaoBaus.Font = Enum.Font.SourceSansBold
botaoBaus.TextSize = 18

-- Botão Iniciar Quests
local botaoQuest = Instance.new("TextButton", frame)
botaoQuest.Size = UDim2.new(1, -20, 0, 40)
botaoQuest.Position = UDim2.new(0, 10, 0, 140)
botaoQuest.Text = "Iniciar Quest"
botaoQuest.BackgroundColor3 = Color3.fromRGB(218, 165, 32)
botaoQuest.TextColor3 = Color3.fromRGB(255, 255, 255)
botaoQuest.Font = Enum.Font.SourceSansBold
botaoQuest.TextSize = 18

-- Botão Fechar
local botaoFechar = Instance.new("TextButton", frame)
botaoFechar.Size = UDim2.new(1, -20, 0, 30)
botaoFechar.Position = UDim2.new(0, 10, 0, 190)
botaoFechar.Text = "Fechar Painel"
botaoFechar.BackgroundColor3 = Color3.fromRGB(178, 34, 34)
botaoFechar.TextColor3 = Color3.fromRGB(255, 255, 255)
botaoFechar.Font = Enum.Font.SourceSansBold
botaoFechar.TextSize = 16

-- Funções para os botões
botaoFarm.MouseButton1Click:Connect(function()
    print("Farm de Inimigos Ativado!")
    -- aqui você chama a função do farm de inimigos
end)

botaoBaus.MouseButton1Click:Connect(function()
    print("Farm de Baús Ativado!")
    -- aqui você chama a função do farm de baús
end)

botaoQuest.MouseButton1Click:Connect(function()
    print("Quest Iniciada!")
    -- aqui você chama a função de pegar quest
end)

botaoFechar.MouseButton1Click:Connect(function()
    screenGui:Destroy()
end)
