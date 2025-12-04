if game.CoreGui:FindFirstChild("MeuHub") then
    game.CoreGui.MeuHub:Destroy()
end

local P = game:GetService("Players")
local VU = game:GetService("VirtualUser")
local LP = P.LocalPlayer
local RSV = game:GetService("RunService")
local TS = game:GetService("TweenService") 
local GS = game:GetService("GuiService") 
local RS = game:GetService("ReplicatedStorage") 

-- Caminho da Pasta Zones
local ZFP = workspace:FindFirstChild("Gameplay")
    and workspace.Gameplay:FindFirstChild("Static")
    and workspace.Gameplay.Static:FindFirstChild("Zones")

-- GUI principal (Criação do Hub)
local G = Instance.new("ScreenGui")
G.Name = "MeuHub"
G.IgnoreGuiInset = true
G.Parent = game.CoreGui

-- Hub principal Frame
local MF = Instance.new("Frame")
MF.Size = UDim2.new(0,560,0,340)
MF.Position = UDim2.new(0.5,-280,0.5,-170)
MF.BackgroundColor3 = Color3.fromRGB(20,20,20)
MF.Active = true 
MF.Draggable = true 
MF.Visible = false 
MF.Parent = G
Instance.new("UICorner",MF).CornerRadius = UDim.new(0,24)

-- Bola de abrir (movível)
local OB = Instance.new("TextButton")
OB.Size = UDim2.new(0,54,0,54)
OB.Position = UDim2.new(0,24,0,100)
OB.BackgroundColor3 = Color3.fromRGB(30,30,30)
OB.Text = "CSX"
OB.TextSize = 18
OB.Font = Enum.Font.GothamBold
OB.TextColor3 = Color3.fromRGB(0, 150, 255)
OB.AutoButtonColor = false
OB.Parent = G
Instance.new("UICorner",OB).CornerRadius = UDim.new(1,0)
Instance.new("UIStroke",OB).Thickness = 2
OB.Active = true
OB.Draggable = true

-- LÓGICA DE ABRIR/FECHAR O HUB
OB.MouseButton1Click:Connect(function()
    MF.Visible = not MF.Visible
end)
------------------------------------

-- Borda animada
local aB = Instance.new("UIStroke")
aB.Thickness = 2
aB.Color = Color3.fromRGB(255,255,255)
aB.Transparency = 0.3
aB.ApplyStrokeMode = Enum.ApplyStrokeMode.Border
aB.Parent = MF

local T = 0
RSV.RenderStepped:Connect(function(dt)
    T += dt * 1.5
    local s = (math.sin(T) + 1)/2
    aB.Color = Color3.fromRGB(
        255 * s,
        255 * s,
        255 * s
    )
    aB.Transparency = 0.15 + 0.25 * (1-s)
end)

-- Título 
local tF = Instance.new("Frame")
tF.Size = UDim2.new(1,-20,0,30)
tF.Position = UDim2.new(0,10,0,8)
tF.BackgroundTransparency = 1
tF.Parent = MF
local cI = Instance.new("ImageLabel")
cI.Size = UDim2.new(0, 28, 0, 28) 
cI.Position = UDim2.new(0, 0, 0, 1) 
cI.BackgroundTransparency = 1
cI.Image = "rbxassetid://13426724036" 
cI.ImageColor3 = Color3.fromRGB(255, 255, 255)
cI.Parent = tF
local T_L = Instance.new("TextLabel")
T_L.Size = UDim2.new(1,-35,1,0)
T_L.Position = UDim2.new(0,35,0,0)
T_L.BackgroundTransparency = 1
T_L.Font = Enum.Font.GothamBold
T_L.Text = "Clicker Simulador X"
T_L.TextSize = 22
T_L.TextColor3 = Color3.fromRGB(255,255,255)
T_L.TextXAlignment = Enum.TextXAlignment.Left
T_L.Parent = tF

-- Data de Atualização (Canto Superior Direito)
local uD = Instance.new("TextLabel")
uD.Size = UDim2.new(0, 120, 0, 18) 
uD.Position = UDim2.new(1, -160, 0, 6) 
uD.BackgroundTransparency = 1
uD.Font = Enum.Font.Gotham
uD.Text = "Atualizado 4/12/2025 (v5)" 
uD.TextSize = 14 
uD.TextColor3 = Color3.fromRGB(150, 150, 150) 
uD.TextXAlignment = Enum.TextXAlignment.Right
uD.Parent = MF

-- Criador byfelipe 
local cL = Instance.new("TextLabel")
cL.Size = UDim2.new(0, 120, 0, 18) 
cL.Position = UDim2.new(1, -160, 0, 21) 
cL.BackgroundTransparency = 1
cL.Font = Enum.Font.Gotham
cL.Text = "Criador byfelipe" 
cL.TextSize = 12 
cL.TextColor3 = Color3.fromRGB(100, 100, 100) 
cL.TextXAlignment = Enum.TextXAlignment.Right
cL.Parent = MF

-- Botão de Bloqueio/Cadeado 
local iL = false
local lB = Instance.new("TextButton")
local LC = Color3.fromRGB(40, 40, 40) 
lB.Size = UDim2.new(0, 28, 0, 18) 
lB.Position = UDim2.new(0, 250, 0, 10) 
lB.BackgroundColor3 = LC
lB.Text = "🔓" 
lB.TextSize = 18
lB.Font = Enum.Font.Gotham
lB.TextColor3 = Color3.fromRGB(255, 255, 255)
lB.AutoButtonColor = false
lB.Parent = MF
Instance.new("UICorner", lB).CornerRadius = UDim.new(0, 5)

lB.MouseButton1Click:Connect(function()
    iL = not iL
    
    if iL then
        MF.Active = true 
        MF.Draggable = false 
        lB.Text = "🔒" 
        lB.BackgroundColor3 = LC 
        print("Hub Bloqueado: Posição fixa. Botões INTERATIVOS.")
    else
        MF.Active = true
        MF.Draggable = true
        lB.Text = "🔓" 
        lB.BackgroundColor3 = LC 
        print("Hub Desbloqueado: Pode ser movido e interagido.")
    end
end)


-- Separador e Tabs 
local S = Instance.new("Frame")
S.Size = UDim2.new(1,-20,0,2)
S.Position = UDim2.new(0,10,0,38)
S.BackgroundColor3 = Color3.fromRGB(60,60,60)
S.BorderSizePixel = 0
S.Parent = MF
local tH = Instance.new("Frame")
tH.Size = UDim2.new(0,545,0,32) 
tH.Position = UDim2.new(0,10,0,48)
tH.BackgroundTransparency = 1
tH.Parent = MF

local TSZ = UDim2.new(0,100,0,28)

-- FUNÇÃO makeTab 
local function mT(name, icon, x)
    local btn = Instance.new("TextButton")
    btn.Name = name .. "Tab"
    btn.Size = TSZ
    btn.Position = UDim2.new(0,x,0,0)
    btn.BackgroundColor3 = Color3.fromRGB(40,40,40)
    btn.BorderSizePixel = 0
    btn.AutoButtonColor = false
    btn.Font = Enum.Font.GothamSemibold
    btn.Text = icon .. " " .. name 
    btn.TextSize = 16
    btn.TextColor3 = Color3.fromRGB(255,255,255)
    btn.Parent = tH
    Instance.new("UICorner",btn).CornerRadius = UDim.new(0,10)
    return btn
end

-- Definição de Animação de Clique 
local TCI = TweenInfo.new(0.08, Enum.EasingStyle.Sine, Enum.EasingDirection.Out)
local SF = 0.95 

-- Posições das abas 
local mTab     = mT("Main",      "🏠", 0)
local tTab = mT("Teleport",  "🗺️", 110)
local mTab2 = mT("Machines",  "⚙️", 220)
local eTab     = mT("Eggs",      "🥚", 330) 
local sTab = mT("Settings",  "🛠️", 440) 

local lT = Instance.new("Frame")
lT.Size = UDim2.new(1,-20,0,1)
lT.Position = UDim2.new(0,10,0,84)
lT.BackgroundColor3 = Color3.fromRGB(60,60,60)
lT.BorderSizePixel = 0
lT.Parent = MF

-- FUNÇÃO makeArea 
local function mA(initialCanvasY)
    local f = Instance.new("ScrollingFrame")
    f.Size = UDim2.new(1,-40,1,-96)
    f.Position = UDim2.new(0,20,0,90)
    f.BackgroundTransparency = 1
    f.Visible = false
    f.Parent = MF
    f.ScrollBarThickness = 6
    f.CanvasSize = UDim2.new(0,0, 0, initialCanvasY or 300) 
    f.Active = true
    return f
end

local mArea     = mA(350) 
local tArea = mA(600) 
local mArea2 = mA(300) 
local eArea     = mA(300) 
local sArea = mA(400) 

local TS_L = {
    Main      = mTab,
    Teleport  = tTab,
    Machines  = mTab2,
    Eggs      = eTab,      
    Settings  = sTab
}

local AS_L = {
    Main      = mArea,
    Teleport  = tArea, 
    Machines  = mArea2,
    Eggs      = eArea,     
    Settings  = sArea 
}

-- Lógica de clique nas abas
for tabName, tB in pairs(TS_L) do
    local oS = tB.Size
    local cS = UDim2.new(0, oS.X.Offset * SF, 0, oS.Y.Offset * SF)
    
    tB.MouseButton1Click:Connect(function()
        
        if iL then 
            print("Hub Bloqueado: Posição fixa, mas botões interativos.")
        end
        
        -- 1. ANIMAÇÃO
        TS:Create(tB, TCI, {Size = cS}):Play()

        task.wait(0.08)

        -- 3. ANIMAÇÃO: Retorna ao tamanho original
        TS:Create(tB, TCI, {Size = oS}):Play()

        -- 4. Troca de abas (Lógica principal)
        for _, area in pairs(AS_L) do
            area.Visible = false
        end
        for _, button in pairs(TS_L) do
            button.BackgroundColor3 = Color3.fromRGB(40,40,40)
        end
        
        if AS_L[tabName] then
            AS_L[tabName].Visible = true
        end
        tB.BackgroundColor3 = Color3.fromRGB(50,50,50)
    end)
end

-- Garante que o Main seja a aba inicial
mTab.BackgroundColor3 = Color3.fromRGB(50,50,50)
mArea.Visible = true

----------------------------------------------------------------
-- FUNÇÕES DE TOGGLE E BOTÃO
----------------------------------------------------------------

local function cT(p_F, l_T, yP, c_F)
    local tB_R = Instance.new("Frame")
    tB_R.Size = UDim2.new(0,307,0,44)
    tB_R.Position = UDim2.new(0, 0, 0, yP)
    tB_R.BackgroundColor3 = Color3.fromRGB(31,31,31)
    tB_R.BorderSizePixel = 0
    tB_R.Parent = p_F
    Instance.new("UICorner",tB_R).CornerRadius = UDim.new(0,16)

    local tL = Instance.new("TextLabel")
    tL.Size = UDim2.new(0.7,0,1,0)
    tL.Position = UDim2.new(0,14,0,0)
    tL.BackgroundTransparency = 1
    tL.Font = Enum.Font.Gotham
    tL.Text = l_T
    tL.TextSize = 18
    tL.TextXAlignment = Enum.TextXAlignment.Left
    tL.TextColor3 = Color3.fromRGB(255,255,255)
    tL.Parent = tB_R

    local tB = Instance.new("TextButton")
    tB.Size = UDim2.new(0,48,0,22)
    tB.Position = UDim2.new(1,-70,0.5,-11)
    tB.BackgroundColor3 = Color3.fromRGB(60,60,60)
    tB.AutoButtonColor = false
    tB.Text = ""
    tB.Parent = tB_R
    Instance.new("UICorner",tB).CornerRadius = UDim.new(1,0)

    local SW = Instance.new("Frame")
    SW.Size = UDim2.new(0,18,0,18)
    SW.Position = UDim2.new(0,2,0.5,-9)
    SW.BackgroundColor3 = Color3.fromRGB(200,30,30)
    SW.Parent = tB
    Instance.new("UICorner",SW).CornerRadius = UDim.new(1,0)
    
    local EN = false
    
    local function sT(state)
        EN = state
        if state then
            tB.BackgroundColor3 = Color3.fromRGB(50,170,50)
            SW.Position = UDim2.new(1,-20,0.5,-9)
            SW.BackgroundColor3 = Color3.fromRGB(50,220,70)
        else
            tB.BackgroundColor3 = Color3.fromRGB(60,60,60)
            SW.Position = UDim2.new(0,2,0.5,-9)
            SW.BackgroundColor3 = Color3.fromRGB(200,30,30)
        end
        c_F(state)
    end
    
    sT(false)

    tB.MouseButton1Click:Connect(function()
        sT(not EN)
    end)
    return tB_R
end

-- CRIAÇÃO DO BOTÃO ESTILIZADO 
local function cSB(p_F, l_T, yP, c_F, b_C)
    local DGC = Color3.fromRGB(31, 31, 31) 
    
    local bB = Instance.new("TextButton")
    bB.Size = UDim2.new(0,307,0,44)
    bB.Position = UDim2.new(0, 0, 0, yP) 
    bB.BackgroundColor3 = b_C or DGC 
    bB.BorderSizePixel = 0
    bB.AutoButtonColor = true 
    bB.Font = Enum.Font.Gotham
    bB.Text = l_T
    bB.TextSize = 18
    bB.TextColor3 = Color3.fromRGB(255, 255, 255) 
    bB.Parent = p_F
    Instance.new("UICorner",bB).CornerRadius = UDim.new(0,16)
    
    bB.MouseButton1Click:Connect(function()
        c_F() 
    end)
    return bB
end

-- Lógicas de Farm
local aAC
local bFC
local sCF
local iBF = false 

-- Lógica para o Anti AFK
local function aAC_CB(state)
    if aAC then aAC:Disconnect(); aAC = nil end
    if state then 
        aAC = LP.Idled:Connect(function()
            VU:CaptureController()
            VU:ClickButton2(Vector2.new()) 
            print("Anti AFK: Simulação de clique executada.")
        end)
    end
end

-- Função auxiliar para Auto Farm Boss
local function gACP()
    local bF = workspace:FindFirstChild("Gameplay")
        and workspace.Gameplay:FindFirstChild("Dynamic")
        and workspace.Gameplay.Dynamic:FindFirstChild("Bosses")
    if not bF then return {} end

    local C = {}
    for _, obj in ipairs(bF:GetChildren()) do
        if obj:IsA("BasePart") and (string.find(obj.Name, "Combo_", 1, true) or string.find(obj.Name, "Hitbox", 1, true)) then
            table.insert(C, obj)
        end
        if obj:IsA("Model") then
            local hB = obj:FindFirstChild("Hitbox")
            if hB and hB:IsA("BasePart") then table.insert(C, hB) end
        end
    end
    return C
end

-- Lógica para o Auto Farm Boss
local function aFB_CB(state)
    iBF = state
    
    if bFC then
        task.cancel(bFC)
        bFC = nil
    end

    local C = LP.Character or LP.CharacterAdded:Wait()
    local HR = C:FindFirstChild("HumanoidRootPart")
    
    if not state then
        if HR and sCF then
            HR.CFrame = sCF
        end
        return
    end

    if HR then
        sCF = HR.CFrame
    end

    bFC = task.spawn(function()
        while iBF and HR do
            
            local Cmb = gACP()
            
            if #Cmb > 0 then
                local tC = Cmb[1] 
                
                if tC and tC.Parent then
                    local OF = tC.CFrame.LookVector * -5 
                    HR.CFrame = tC.CFrame + Vector3.new(0, 1.5, 0) + OF
                    
                    while iBF and tC.Parent do
                        task.wait(0.1) 
                    end
                end

                if HR and sCF then
                    HR.CFrame = sCF
                end
            end
            
            task.wait(1) 
        end
        
        if HR and sCF then
            HR.CFrame = sCF
        end
    end)
end

-- Lógica de Teleporte (Ilhas)
local function tTI(iFN)
    local iF = workspace:FindFirstChild("Islands") or workspace:FindFirstChild("island")
    if not iF then warn("Pasta principal 'Islands' ou 'island' não encontrada no Workspace."); return end
    
    local iM = iF:FindFirstChild(iFN)
    if not iM then
        local fN = string.gsub(iFN, "zone", "_island")
        iM = iF:FindFirstChild(fN)
        if not iM then warn("Tentativas de encontrar a Ilha '" .. iFN .. "' falharam."); return end
    end

    local TT = iM:FindFirstChild("Origin") or iM:FindFirstChild("origin")
    if not TT then TT = iM:FindFirstChildOfClass("BasePart") end
    if not TT and iM:IsA("Model") and iM.PrimaryPart then TT = iM.PrimaryPart end

    local C = LP.Character
    local HR = C and C:FindFirstChild("HumanoidRootPart")

    if HR and TT and TT:IsA("BasePart") then
        HR.CFrame = TT.CFrame + Vector3.new(0, 5, 0)
        print("Teleporte para: " .. iM.Name .. " executado com sucesso.")
    else
        warn("Ponto de teleporte para '" .. iM.Name .. "' não é válido ou não foi encontrado.")
    end
end

-- Lógica de Teleporte (Spawn)
local function tTS()
    local sT = workspace:FindFirstChild("SpawnLocation") 
        or workspace:FindFirstChild("Spawn") 
        or workspace:FindFirstChildOfClass("SpawnPoint")

    local C = LP.Character
    local HR = C and C:FindFirstChild("HumanoidRootPart")

    if HR and sT and sT:IsA("BasePart") then
        HR.CFrame = sT.CFrame + Vector3.new(0, 5, 0)
        print("Teleporte para Spawn executado com sucesso.")
    else
        warn("Ponto de teleporte para Spawn não encontrado ou não é válido.")
    end
end

-- Lógica Fly 
local iF = false
local fC
local function tF()
    iF = not iF
    
    local C = LP.Character
    local HR = C and C:FindFirstChild("HumanoidRootPart")
    local H = C and C:FindFirstChildOfClass("Humanoid")

    if not HR or not H then 
        warn("Personagem ou HumanoidRootPart não encontrados.")
        iF = false 
        return 
    end

    if iF then
        H.PlatformStand = true 
        HR.Anchored = true
        HR.CanCollide = false
        print("Fly Ativado. Use as teclas de movimento para 'voar'.")
        
        fC = RSV.RenderStepped:Connect(function()
            local mV = Vector3.new(
                LP.Humanoid.MoveDirection.X,
                LP.Humanoid.MoveDirection.Y,
                LP.Humanoid.MoveDirection.Z
            ) * 1.5 
            
            HR.CFrame = HR.CFrame * CFrame.new(mV)
        end)
    else
        if fC then fC:Disconnect() end
        H.PlatformStand = false
        HR.Anchored = false
        HR.CanCollide = true
        print("Fly Desativado.")
    end
end

-- Lógica de injeção do Infinity Yield
local function iIY()
    local S_S, E = pcall(function()
        loadstring(game:HttpGet("https://raw.githubusercontent.com/EdgeIY/infinite-yield/master/source"))()
    end)
    
    if S_S then
        print("Infinity Yield Injetado com Sucesso! Procure por sua interface na tela.")
    else
        warn("Falha ao Injetar Infinity Yield: " .. tostring(E) .. ". O módulo pode não estar disponível ou o executor não suporta httpget/loadstring.")
    end
end

-- Lógica de Teleporte (Ovos)
local function tTIO(oN, pCN, oI) 
    print("--- Tentativa de Teleporte Indexado ---")
    
    local C = nil
    local fO = {}
    
    -- 1. ENCONTRAR O CONTÊINER
    if pCN == "RestockingShops" then
        local G_P = workspace:FindFirstChild("Gameplay") 
        local S_T = G_P and G_P:FindFirstChild("Static") 
        local R_S = S_T and S_T:FindFirstChild("RestockingShops") 
        
        if R_S then
            C = R_S
        else
            warn("STATUS 1/3: FALHA ao encontrar 'RestockingShops'.")
            return
        end
    else
        local fC = workspace:FindFirstChild(pCN, true)
        if fC then
            C = fC
        else
            warn("Contêiner não encontrado. Retornando.")
            return
        end
    end
    
    -- 2. ENCONTRAR TODAS AS INSTÂNCIAS COM O NOME CORRETO
    for _, child in ipairs(C:GetChildren()) do
        if child.Name == oN then
            table.insert(fO, child)
        end
    end
    
    if #fO < oI then
        warn("STATUS 2/3: FALHA! Objeto no índice " .. oI .. " NÃO encontrado (Total de objetos: " .. #fO .. ").")
        return
    end

    local tO = fO[oI]
    
    local C_ = LP.Character
    local HR_ = C_ and C_:FindFirstChild("HumanoidRootPart")

    if HR_ and tO then
        local tCF = nil 
        
        -- 3. DETERMINAR O CFRAME CORRETO (CORRIGIDO)
        if tO:IsA("Model") then
            if tO.PrimaryPart then
                tCF = tO.PrimaryPart.CFrame
            else
                local S_, P_ = pcall(tO.GetPivot, tO)
                if S_ then tCF = P_ end
            end
        elseif tO:IsA("BasePart") then
            tCF = tO.CFrame
        end

        if tCF then
            if typeof(tCF) == "CFrame" then
                HR_.CFrame = tCF + Vector3.new(0, 5, 0)
                print("Teleporte para: " .. tO.Name .. " em '" .. C.Name .. "' EXECUTADO com sucesso.")
            else
                 warn("Teleporte cancelado: Pivot/CFrame não é um CFrame válido.")
            end
        else
            warn("Teleporte cancelado: Não foi possível determinar um CFrame válido.")
        end
    else
        warn("Teleporte cancelado: Personagem (HumanoidRootPart) não encontrado.")
    end
end

-- FUNÇÃO PRINCIPAL DE POPULAÇÃO DAS ABAS
local function pTA()
    for _, child in pairs(tArea:GetChildren()) do child:Destroy() end

    local yP = 6
    local bS = 50
    
    -- 1. SEÇÃO SPAWN
    local sL = Instance.new("TextLabel")
    sL.Name = "SpawnLabel"
    sL.Size = UDim2.new(0,260,0,22); sL.Position = UDim2.new(0,0,0,yP)
    sL.BackgroundTransparency = 1; sL.Font = Enum.Font.GothamSemibold
    sL.Text = "Spawn"; sL.TextSize = 18
    sL.TextXAlignment = Enum.TextXAlignment.Left; sL.TextColor3 = Color3.fromRGB(220,220,220)
    sL.Parent = tArea
    yP += 24 

    cSB(tArea, "Teleport Início", yP, tTS)
    yP += bS 

    -- 2. SEÇÃO ILHAS
    local iL = Instance.new("TextLabel")
    iL.Name = "IslandLabel"
    iL.Size = UDim2.new(0,260,0,22); iL.Position = UDim2.new(0,0,0,yP)
    iL.BackgroundTransparency = 1; iL.Font = Enum.Font.GothamSemibold
    iL.Text = "Teleporte de Ilhas"; iL.TextSize = 18
    iL.TextXAlignment = Enum.TextXAlignment.Left; iL.TextColor3 = Color3.fromRGB(220,220,220)
    iL.Parent = tArea
    yP += 24
    
    local iO = {
        {"Nature Island", "naturezone"}, {"Desert Island", "desertzone"},  
        {"Volcano Island", "volcanozone"}, {"Water Island", "waterzone"},
        {"Ice Island", "icezone"}, {"Cloud Island", "cloudzone"},
        {"Cosmic Island", "cosmic_island"},  {"Boss Island", "bosszone"}, 
    }

    for _, iD in ipairs(iO) do
        cSB(tArea, iD[1], yP, function()
            tTI(iD[2])
        end)
        yP += bS
    end

    tArea.CanvasSize = UDim2.new(0,0, 0, math.max(tArea.AbsoluteSize.Y, yP + 10))
end

local function pMA()
    for _, child in pairs(mArea2:GetChildren()) do child:Destroy() end

    local mL = Instance.new("TextLabel")
    mL.Name = "MachineLabel"
    mL.Size = UDim2.new(0,260,0,22); mL.Position = UDim2.new(0,0,0,6)
    mL.BackgroundTransparency = 1; mL.Font = Enum.Font.GothamSemibold
    mL.Text = "Máquinas e Daycare"; mL.TextSize = 18
    mL.TextXAlignment = Enum.TextXAlignment.Left; mL.TextColor3 = Color3.fromRGB(220,220,220)
    mL.Parent = mArea2

    local yP = 30
    local bS = 50 
    
    local function cSMB(mN, D, yPos)
        local function tTM()
            local tO = ZFP and ZFP:FindFirstChild(mN) 

            local tP = tO
            if tO and (tO:IsA("Model") or tO:IsA("Folder")) then
                tP = tO:FindFirstChildOfClass("BasePart")
            end
            
            local C = LP.Character
            local HR = C and C:FindFirstChild("HumanoidRootPart")

            if tP and HR and tP:IsA("BasePart") then
                HR.CFrame = tP.CFrame + Vector3.new(0, 5, 0)
            else
                print("Objeto da máquina '" .. mN .. "' não encontrado ou não é uma BasePart válida para teleporte.")
            end
        end
        cSB(mArea2, D, yPos, tTM)
    end
    
    cSMB("GoldMachine", "Gold Machine", yP); yP += bS
    cSMB("RainbowMachine", "Rainbow Machine", yP); yP += bS
    cSMB("CosmicMachine", "Cosmic Machine", yP); yP += bS
    cSMB("Daycare", "Daycare", yP); yP += bS
    
    mArea2.CanvasSize = UDim2.new(0,0, 0, math.max(mArea2.AbsoluteSize.Y, yP + 10))
end

local function pEA()
    for _, child in pairs(eArea:GetChildren()) do child:Destroy() end
    
    local yP = 6
    local bS = 50 

    local mL = Instance.new("TextLabel")
    mL.Name = "MysteriousLabel"
    mL.Size = UDim2.new(0,260,0,22); mL.Position = UDim2.new(0,0,0,yP)
    mL.BackgroundTransparency = 1; mL.Font = Enum.Font.GothamSemibold
    mL.Text = "Teleporte de Ovos Restock";
    mL.TextSize = 18
    mL.TextXAlignment = Enum.TextXAlignment.Left; mL.TextColor3 = Color3.fromRGB(220,220,220)
    mL.Parent = eArea
    yP += 24

    local D_C = Color3.fromRGB(31, 31, 31) 

    local function cREB(I)
        local eN = "Restocking_Egg" 
        local cN = "RestockingShops" 
        
        cSB(eArea, "Egg Restocking " .. I, yP, function() 
            tTIO(eN, cN, I) 
        end, D_C) 
        yP += bS
    end

    cREB(1)
    cREB(2)
    cREB(3)
    cREB(4)
    
    eArea.CanvasSize = UDim2.new(0,0, 0, math.max(eArea.AbsoluteSize.Y, yP + 10))
end

local function pSA()
    for _, child in pairs(sArea:GetChildren()) do child:Destroy() end
    
    local yP_S = 6
    local bS = 50

    local cL = Instance.new("TextLabel")
    cL.Size = UDim2.new(0,260,0,22); cL.Position = UDim2.new(0,0,0,yP_S)
    cL.BackgroundTransparency = 1; cL.Font = Enum.Font.GothamSemibold
    cL.Text = "Configs"; cL.TextSize = 18
    cL.TextXAlignment = Enum.TextXAlignment.Left; cL.TextColor3 = Color3.fromRGB(220,220,220)
    cL.Parent = sArea
    yP_S = 30

    -- 1. Anti AFK
    cT(sArea, "Anti AFK", yP_S, aAC_CB); yP_S += bS

    -- 2. Fly PC e Mobile 
    local D_C = Color3.fromRGB(31, 31, 31)
    cSB(sArea, "Fly PC e Mobile", yP_S, tF, D_C); yP_S += bS

    -- 3. Infinity Yield (BOTÃO DE INJEÇÃO)
    cSB(sArea, "Infinity Yield (Inject)", yP_S, iIY); yP_S += bS

    -- Label Misc
    yP_S += 10
    local mL = Instance.new("TextLabel")
    mL.Size = UDim2.new(0,260,0,22); mL.Position = UDim2.new(0,0,0,yP_S) 
    mL.BackgroundTransparency = 1; mL.Font = Enum.Font.GothamSemibold
    mL.Text = "Misc"; mL.TextSize = 18
    mL.TextXAlignment = Enum.TextXAlignment.Left; mL.TextColor3 = Color3.fromRGB(220,220,220)
    mL.Parent = sArea
    yP_S += 24

    -- 4. Delete Hub
    local RC = Color3.fromRGB(200, 30, 30)
    cSB(sArea, "Delete Hub", yP_S, function()
        local h = game.CoreGui:FindFirstChild("MeuHub")
        if h then
            h:Destroy()
            print("Hub 'MeuHub' excluído com sucesso.")
        end
    end, RC); yP_S += bS

    sArea.CanvasSize = UDim2.new(0,0, 0, math.max(sArea.AbsoluteSize.Y, yP_S + 10))
end


--==============================================================
-- INICIALIZAÇÃO DE CONTEÚDO
--==============================================================

-- SEÇÃO MAIN AREA (Auto Farm Boss e Evento)
local yPM = 6
local bS = 50

-- 1. Seção Auto Farm
local aFL = Instance.new("TextLabel")
aFL.Size = UDim2.new(0,260,0,22); aFL.Position = UDim2.new(0,0,0,yPM)
aFL.BackgroundTransparency = 1; aFL.Font = Enum.Font.GothamSemibold
aFL.Text = "Auto Farm"; aFL.TextSize = 18
aFL.TextXAlignment = Enum.TextXAlignment.Left; aFL.TextColor3 = Color3.fromRGB(220,220,220)
aFL.Parent = mArea
yPM = 30

-- Toggle: Auto Farm Boss
cT(mArea, "Auto Farm Boss", yPM, aFB_CB); yPM += bS

-- 2. Seção Evento 
yPM += 10 
local eL = Instance.new("TextLabel")
eL.Size = UDim2.new(0,260,0,22); eL.Position = UDim2.new(0,0,0,yPM)
eL.BackgroundTransparency = 1; eL.Font = Enum.Font.GothamSemibold
eL.Text = "Evento"; eL.TextSize = 18
eL.TextXAlignment = Enum.TextXAlignment.Left; eL.TextColor3 = Color3.fromRGB(220,220,220)
eL.Parent = mArea
yPM += 24

local G_C = Color3.fromRGB(31, 31, 31) 
cSB(mArea, "🔒 Em breve", yPM, function() 
    print("Botão 'Em breve' clicado. Nenhuma função ativa associada.")
end, G_C); yPM += bS

mArea.CanvasSize = UDim2.new(0,0, 0, math.max(mArea.AbsoluteSize.Y, yPM + 10))


pTA()
pMA()
pEA() 
pSA()
