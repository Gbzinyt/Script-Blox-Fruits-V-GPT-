--// Criação do HAB (GUI)
local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name = "MenuPrincipal"
ScreenGui.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui")

local Frame = Instance.new("Frame")
Frame.Size = UDim2.new(0, 300, 0, 400)
Frame.Position = UDim2.new(0.5, -150, 0.5, -200)
Frame.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
Frame.BorderSizePixel = 0
Frame.Parent = ScreenGui

--// Título
local Titulo = Instance.new("TextLabel")
Titulo.Text = "Menu de Funções"
Titulo.Size = UDim2.new(1, 0, 0, 40)
Titulo.BackgroundColor3 = Color3.fromRGB(60, 60, 60)
Titulo.TextColor3 = Color3.fromRGB(255, 255, 255)
Titulo.Font = Enum.Font.SourceSansBold
Titulo.TextSize = 22
Titulo.Parent = Frame

-- Função para criar botões
function CriarBotao(nome, posY, callback)
    local Botao = Instance.new("TextButton")
    Botao.Text = nome
    Botao.Size = UDim2.new(0, 280, 0, 40)
    Botao.Position = UDim2.new(0, 10, 0, posY)
    Botao.BackgroundColor3 = Color3.fromRGB(70, 70, 70)
    Botao.TextColor3 = Color3.fromRGB(255, 255, 255)
    Botao.Font = Enum.Font.SourceSans
    Botao.TextSize = 20
    Botao.Parent = Frame

    Botao.MouseButton1Click:Connect(callback)
end

-- Variáveis de controle
local fovAtivo = false
local espAtivo = false
local verAtravés = false
local autoKillAtivo = false
local atravessarAtivo = false

-- Funções

-- FOV
function AtivarFOV()
    fovAtivo = not fovAtivo
    if fovAtivo then
        local Circle = Drawing.new("Circle")
        Circle.Color = Color3.fromRGB(0, 255, 0)
        Circle.Thickness = 2
        Circle.NumSides = 100
        Circle.Radius = 150
        Circle.Filled = false
        Circle.Transparency = 0.8
        Circle.Visible = true

        game:GetService("RunService").RenderStepped:Connect(function()
            if fovAtivo then
                Circle.Position = Vector2.new(workspace.CurrentCamera.ViewportSize.X/2, workspace.CurrentCamera.ViewportSize.Y/2)
            else
                Circle.Visible = false
            end
        end)
    end
end

-- ESP (Nome sobre os inimigos)
function AtivarESP()
    espAtivo = not espAtivo
    while espAtivo do
        for _, player in pairs(game.Players:GetPlayers()) do
            if player ~= game.Players.LocalPlayer and player.Character and player.Character:FindFirstChild("Head") and not player.Character.Head:FindFirstChild("ESPLabel") then
                local Billboard = Instance.new("BillboardGui", player.Character.Head)
                Billboard.Name = "ESPLabel"
                Billboard.Size = UDim2.new(0, 100, 0, 30)
                Billboard.AlwaysOnTop = true

                local Texto = Instance.new("TextLabel", Billboard)
                Texto.Text = player.Name
                Texto.Size = UDim2.new(1, 0, 1, 0)
                Texto.BackgroundTransparency = 1
                Texto.TextColor3 = Color3.fromRGB(255, 0, 0)
                Texto.TextScaled = true
            end
        end
        wait(1)
    end
end

-- Ver de trás das paredes (WallHack)
function AtivarVerAtravés()
    verAtravés = not verAtravés
    for _, obj in pairs(workspace:GetDescendants()) do
        if obj:IsA("BasePart") and obj.Transparency < 1 and obj.CanCollide == true then
            if verAtravés then
                obj.LocalTransparencyModifier = 0.5
            else
                obj.LocalTransparencyModifier = 0
            end
        end
    end
end

-- Auto-Kill
function AtivarAutoKill()
    autoKillAtivo = not autoKillAtivo
    while autoKillAtivo do
        for _, player in pairs(game.Players:GetPlayers()) do
            if player ~= game.Players.LocalPlayer and player.Character and player.Character:FindFirstChild("Humanoid") and player.Character.Humanoid.Health > 0 then
                local args = {
                    [1] = player.Character.Humanoid
                }
                game.ReplicatedStorage.Remotes.KillPlayer:FireServer(unpack(args))
            end
        end
        wait(0.5)
    end
end

-- Atravessar paredes (NoClip)
function AtivarAtravessar()
    atravessarAtivo = not atravessarAtivo
    game:GetService("RunService").Stepped:Connect(function()
        if atravessarAtivo then
            for _, v in pairs(game.Players.LocalPlayer.Character:GetDescendants()) do
                if v:IsA("BasePart") then
                    v.CanCollide = false
                end
            end
        end
    end)
end

-- Ant-Ban (obfuscado básico e ocultação local)
pcall(function()
    local mt = getrawmetatable(game)
    setreadonly(mt, false)
    local oldNamecall = mt.__namecall

    mt.__namecall = newcclosure(function(self, ...)
        local metodo = getnamecallmethod()
        if metodo == "Kick" then
            return nil
        end
        return oldNamecall(self, ...)
    end)
end)

-- Criar os botões no HAB
CriarBotao("Ativar FOV", 50, AtivarFOV)
CriarBotao("Ativar ESP", 100, AtivarESP)
CriarBotao("Ver Através das Paredes", 150, AtivarVerAtravés)
CriarBotao("Auto-Kill", 200, AtivarAutoKill)
CriarBotao("Atravessar Paredes", 250, AtivarAtravessar)

-- Créditos
local Credito = Instance.new("TextLabel")
Credito.Text = "by Gabriel | 2025"
Credito.Size = UDim2.new(1, 0, 0, 30)
Credito.Position = UDim2.new(0, 0, 1, -30)
Credito.BackgroundTransparency = 1
Credito.TextColor3 = Color3.fromRGB(180, 180, 180)
Credito.Font = Enum.Font.SourceSansItalic
Credito.TextSize = 16
Credito.Parent = Frame
