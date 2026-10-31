-- ============================================================
-- RD CHEATS VIP ULTIMATE v7.1 — CÓDIGO COMPLETO
-- F1=menu | F2=HUD | Y=update | V=voo | G=ghost | M=speed | B=TP
-- ============================================================

local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local UIS = game:GetService("UserInputService")
local HttpService = game:GetService("HttpService")
local Camera = workspace.CurrentCamera
local LP = Players.LocalPlayer

local C = {
    ESP1=false,ESP2=false,ESP3=false,ESP4=false,ESP5=false,ESP6=false,ESP7=false,ESP8=false,ESP9=false,ESP10=false,
    ESP11=false,ESP12=false,ESP13=false,ESP14=false,ESP15=false,ESP16=false,ESP17=false,ESP18=false,ESP19=false,ESP20=false,
    ESP21=false,ESP22=false,ESP23=false,ESP24=false,ESP25=false,ESP26=false,ESP27=false,ESP28=false,ESP29=false,ESP30=false,
    ESP31=false,ESP32=false,ESP33=false,ESP34=false,ESP35=false,ESP36=false,ESP37=false,ESP38=false,ESP39=false,ESP40=false,
    ESP41=false,ESP42=false,ESP43=false,ESP44=false,ESP45=false,ESP46=false,ESP47=false,ESP48=false,ESP49=false,ESP50=false,
    ESP51=false,ESP52=false,ESP53=false,ESP54=false,ESP55=false,ESP56=false,ESP57=false,ESP58=false,ESP59=false,ESP60=false,
    ESPChams=false, ESPArma=false,
    FiltroTime=true, FiltroDist=false, DistMax=500,
    RGBAtivo=false, RGBVel=1, RGBBri=1, Hue=0,
    CorBox=Color3.fromRGB(255,255,255), CorLinha=Color3.fromRGB(255,255,255),
    CorNome=Color3.fromRGB(255,255,255), CorEsq=Color3.fromRGB(255,255,255),
    CorChams=Color3.fromRGB(255,0,0), CorArma=Color3.fromRGB(255,200,0),
    CorDist=Color3.fromRGB(200,200,200), CorVida=Color3.fromRGB(0,255,0),
    Espessura=1, Transparencia=0.7, Tamanho=1,
    AimbotTipo="Camera", Aimbot=false, FOV=150, MostrarFOV=true,
    Suav=25, Parte="Head", Pred=0.15, AimDist=500,
    VisObrig=false, Cross=false, AimKey=Enum.KeyCode.E, AimToggle=false,
    Voo=false, VooVel=3, Noclip=false, Speed=false, SpeedVal=50, SJump=false,
    HUD=false,
    KeyMenu=Enum.KeyCode.F1, KeyHUD=Enum.KeyCode.F2,
    KeyUpd=Enum.KeyCode.Y, KeyVoo=Enum.KeyCode.V,
    KeyGhost=Enum.KeyCode.G, KeySpeed=Enum.KeyCode.M,
    KeyTP=Enum.KeyCode.B,
    MenuFundo=Color3.fromRGB(12,12,16), MenuAccent=Color3.fromRGB(220,35,50),
    MenuHeader=Color3.fromRGB(18,18,24), MenuCard=Color3.fromRGB(22,22,30),
    SilentAim=false, SilentFOV=150,
    HitboxExpander=false, HitboxSize=3,
    AutoParry=false, InfiniteYield=false,
    AntiStun=false, Freecam=false, FreecamSpeed=2,
    InstantKill=false, TeleportKill=false,
    RainbowESP=false, SpinBot=false, SpinSpeed=10,
    NoCooldown=false, AutoFarm=false,
    TeleportAll=false, FlingAll=false,
    SoundSpam=false, SoundId=0,
}

local D = {}
local MenuGui, FOVC, CrossD, vooC, bPos, bGyr
local t0 = tick()
local fpsH = {}
local fpsL, tempoL, alvoL

local function MesmoTime(p)
    if p == LP then return true end
    if LP.Team and p.Team and LP.Team == p.Team then return true end
    return false
end

local function ParteAlvo(ch)
    if not ch then return nil end
    local p = C.Parte
    if p=="Head" then return ch:FindFirstChild("Head")
    elseif p=="Neck" then return ch:FindFirstChild("Neck") or ch:FindFirstChild("UpperTorso") or ch:FindFirstChild("Torso")
    elseif p=="Chest" then return ch:FindFirstChild("UpperTorso") or ch:FindFirstChild("Torso")
    elseif p=="Hip" then return ch:FindFirstChild("LowerTorso") or ch:FindFirstChild("Torso") end
    return ch:FindFirstChild("Head")
end

local function CriarD(p)
    if p == LP or D[p] then return end
    local d = {}
    d.box2=Drawing.new("Square"); d.box2.Thickness=1; d.box2.Filled=false; d.box2.Visible=false
    d.box3=Drawing.new("Square"); d.box3.Thickness=1; d.box3.Filled=false; d.box3.Visible=false
    d.box4=Drawing.new("Square"); d.box4.Thickness=2; d.box4.Filled=false; d.box4.Visible=false
    d.box25=Drawing.new("Square"); d.box25.Thickness=2; d.box25.Filled=false; d.box25.Visible=false
    d.box28=Drawing.new("Square"); d.box28.Thickness=1; d.box28.Filled=false; d.box28.Visible=false
    d.box29=Drawing.new("Square"); d.box29.Thickness=3; d.box29.Filled=false; d.box29.Visible=false
    d.box30=Drawing.new("Square"); d.box30.Thickness=2; d.box30.Filled=false; d.box30.Visible=false
    d.boxP=Drawing.new("Square"); d.boxP.Thickness=1; d.boxP.Filled=true; d.boxP.Transparency=0.7; d.boxP.Visible=false
    d.boxG=Drawing.new("Square"); d.boxG.Thickness=1; d.boxG.Filled=true; d.boxG.Transparency=0.3; d.boxG.Visible=false
    d.linha1=Drawing.new("Line"); d.linha1.Thickness=1; d.linha1.Visible=false
    d.linha21=Drawing.new("Line"); d.linha21.Thickness=1; d.linha21.Visible=false
    d.linha22=Drawing.new("Line"); d.linha22.Thickness=1; d.linha22.Visible=false
    d.linha23=Drawing.new("Line"); d.linha23.Thickness=1; d.linha23.Visible=false
    d.linha24=Drawing.new("Line"); d.linha24.Thickness=1; d.linha24.Visible=false
    d.nome=Drawing.new("Text"); d.nome.Size=14; d.nome.Center=true; d.nome.Outline=true; d.nome.Visible=false
    d.nomeDist=Drawing.new("Text"); d.nomeDist.Size=13; d.nomeDist.Center=true; d.nomeDist.Outline=true; d.nomeDist.Visible=false
    d.nomeVida=Drawing.new("Text"); d.nomeVida.Size=13; d.nomeVida.Center=true; d.nomeVida.Outline=true; d.nomeVida.Visible=false
    d.nomeVidaDist=Drawing.new("Text"); d.nomeVidaDist.Size=12; d.nomeVidaDist.Center=true; d.nomeVidaDist.Outline=true; d.nomeVidaDist.Visible=false
    d.vidaN=Drawing.new("Text"); d.vidaN.Size=11; d.vidaN.Center=true; d.vidaN.Outline=true; d.vidaN.Visible=false
    d.vidaPct=Drawing.new("Text"); d.vidaPct.Size=11; d.vidaPct.Center=true; d.vidaPct.Outline=true; d.vidaPct.Visible=false
    d.dist=Drawing.new("Text"); d.dist.Size=12; d.dist.Center=true; d.dist.Outline=true; d.dist.Visible=false
    d.distM=Drawing.new("Text"); d.distM.Size=12; d.distM.Center=true; d.distM.Outline=true; d.distM.Visible=false
    d.arma=Drawing.new("Text"); d.arma.Size=12; d.arma.Center=true; d.arma.Outline=true; d.arma.Visible=false
    d.vidaF=Drawing.new("Line"); d.vidaF.Thickness=4; d.vidaF.Color=Color3.fromRGB(50,50,50); d.vidaF.Visible=false
    d.vida=Drawing.new("Line"); d.vida.Thickness=4; d.vida.Visible=false
    d.escudoF=Drawing.new("Line"); d.escudoF.Thickness=3; d.escudoF.Color=Color3.fromRGB(50,50,150); d.escudoF.Visible=false
    d.escudo=Drawing.new("Line"); d.escudo.Thickness=3; d.escudo.Visible=false
    d.cabeca7=Drawing.new("Circle"); d.cabeca7.Thickness=1; d.cabeca7.NumSides=20; d.cabeca7.Filled=false; d.cabeca7.Visible=false
    d.cabeca8=Drawing.new("Circle"); d.cabeca8.Thickness=1; d.cabeca8.NumSides=20; d.cabeca8.Filled=false; d.cabeca8.Visible=false
    d.esq5={}; d.esq31={}; d.esq37={}
    for i=1,7 do
        d.esq5[i]=Drawing.new("Line"); d.esq5[i].Thickness=1; d.esq5[i].Visible=false
        d.esq31[i]=Drawing.new("Line"); d.esq31[i].Thickness=1; d.esq31[i].Visible=false
        d.esq37[i]=Drawing.new("Line"); d.esq37[i].Thickness=1; d.esq37[i].Visible=false
    end
    d.juntas38={}; d.juntas39={}
    for i=1,7 do
        d.juntas38[i]=Drawing.new("Circle"); d.juntas38[i].Thickness=1; d.juntas38[i].NumSides=12; d.juntas38[i].Filled=true; d.juntas38[i].Visible=false
        d.juntas39[i]=Drawing.new("Circle"); d.juntas39[i].Thickness=2; d.juntas39[i].NumSides=12; d.juntas39[i].Filled=false; d.juntas39[i].Visible=false
    end
    d.chams=nil
    D[p]=d
end

local function RemoverD(p)
    if not D[p] then return end
    for _, o in pairs(D[p]) do
        if type(o)=="table" then for _, l in pairs(o) do if l and l.Remove then l:Remove() end end
        elseif o and o.Remove then o:Remove() end
    end
    if D[p].chams then D[p].chams:Destroy() end
    D[p]=nil
end

local function Esconder(d)
    for _, o in pairs(d) do
        if type(o)=="table" then for _, l in pairs(o) do if l then l.Visible=false end end
        elseif o then o.Visible=false end
    end
end

local function AtualizarJogador(p)
    local d=D[p]; if not d then return end
    local ch=p.Character
    if not ch or not ch:FindFirstChild("HumanoidRootPart") or not ch:FindFirstChild("Humanoid") then Esconder(d); return end
    if C.FiltroTime and MesmoTime(p) then Esconder(d); return end
    local hrp=ch.HumanoidRootPart
    local head=ch:FindFirstChild("Head")
    local hum=ch.Humanoid
    if hum.Health<=0 then Esconder(d); return end
    local rp,on=Camera:WorldToViewportPoint(hrp.Position)
    if not on then Esconder(d); return end
    local minhaPos=LP.Character and LP.Character:FindFirstChild("HumanoidRootPart") and LP.Character.HumanoidRootPart.Position or Camera.CFrame.Position
    local dist=math.floor((minhaPos-hrp.Position).Magnitude)
    if C.FiltroDist and dist>C.DistMax then Esconder(d); return end
    local hs=Camera:WorldToViewportPoint(head.Position+Vector3.new(0,0.5,0))
    local ls=Camera:WorldToViewportPoint(hrp.Position-Vector3.new(0,3,0))
    local alt=math.abs(hs.Y-ls.Y)*C.Tamanho
    local lar=alt*0.5
    local cx=rp.X
    local cy=rp.Y-alt*0.2
    local tr=C.Transparencia

    if C.ESP1 then d.linha1.Visible=true; d.linha1.Thickness=C.Espessura; d.linha1.From=Vector2.new(Camera.ViewportSize.X/2,Camera.ViewportSize.Y); d.linha1.To=Vector2.new(cx,cy+alt/2); d.linha1.Color=C.CorLinha else d.linha1.Visible=false end
    if C.ESP2 then d.box2.Visible=true; d.box2.Thickness=C.Espessura; d.box2.Size=Vector2.new(lar,alt); d.box2.Position=Vector2.new(cx-lar/2,cy-alt/2); d.box2.Color=C.CorBox else d.box2.Visible=false end
    if C.ESP3 then d.box3.Visible=true; d.box3.Thickness=C.Espessura; d.box3.Size=Vector2.new(lar,alt); d.box3.Position=Vector2.new(cx-lar/2,cy-alt/2); d.box3.Color=C.CorBox; d.box3.Transparency=tr else d.box3.Visible=false end
    if C.ESP4 then d.box4.Visible=true; d.box4.Thickness=C.Espessura+1; d.box4.Size=Vector2.new(lar*1.1,alt*1.1); d.box4.Position=Vector2.new(cx-lar*0.55,cy-alt*0.55); d.box4.Color=C.CorBox else d.box4.Visible=false end
    if C.ESP5 and head then
        local ps={head,ch:FindFirstChild("UpperTorso") or ch:FindFirstChild("Torso"),ch:FindFirstChild("LowerTorso") or ch:FindFirstChild("HumanoidRootPart"),ch:FindFirstChild("LeftUpperArm") or ch:FindFirstChild("Left Arm"),ch:FindFirstChild("RightUpperArm") or ch:FindFirstChild("Right Arm"),ch:FindFirstChild("LeftUpperLeg") or ch:FindFirstChild("Left Leg"),ch:FindFirstChild("RightUpperLeg") or ch:FindFirstChild("Right Leg")}
        local cs={{1,2},{2,3},{2,4},{2,5},{3,6},{3,7}}
        for i=1,7 do d.esq5[i].Visible=false end
        for i,co in ipairs(cs) do
            local p1,p2=ps[co[1]],ps[co[2]]
            if p1 and p2 then
                local s1,o1=Camera:WorldToViewportPoint(p1.Position)
                local s2,o2=Camera:WorldToViewportPoint(p2.Position)
                if o1 and o2 then local l=d.esq5[i]; l.From=Vector2.new(s1.X,s1.Y); l.To=Vector2.new(s2.X,s2.Y); l.Visible=true; l.Color=C.CorEsq; l.Thickness=C.Espessura end
            end
        end
    else for i=1,7 do d.esq5[i].Visible=false end end
    if C.ESP31 and head then
        local ps={head,ch:FindFirstChild("UpperTorso") or ch:FindFirstChild("Torso"),ch:FindFirstChild("LowerTorso") or ch:FindFirstChild("HumanoidRootPart"),ch:FindFirstChild("LeftUpperArm") or ch:FindFirstChild("Left Arm"),ch:FindFirstChild("RightUpperArm") or ch:FindFirstChild("Right Arm"),ch:FindFirstChild("LeftUpperLeg") or ch:FindFirstChild("Left Leg"),ch:FindFirstChild("RightUpperLeg") or ch:FindFirstChild("Right Leg")}
        local cs={{1,2},{2,3},{2,4},{2,5},{3,6},{3,7}}
        for i=1,7 do d.esq31[i].Visible=false end
        for i,co in ipairs(cs) do
            local p1,p2=ps[co[1]],ps[co[2]]
            if p1 and p2 then
                local s1,o1=Camera:WorldToViewportPoint(p1.Position)
                local s2,o2=Camera:WorldToViewportPoint(p2.Position)
                if o1 and o2 then local l=d.esq31[i]; l.From=Vector2.new(s1.X,s1.Y); l.To=Vector2.new(s2.X,s2.Y); l.Visible=true; l.Color=Color3.fromHSV((tick()*0.5+i*0.1)%1,1,1); l.Thickness=C.Espessura end
            end
        end
    else for i=1,7 do d.esq31[i].Visible=false end end
    if C.ESP37 and head then
        local ps={head,ch:FindFirstChild("UpperTorso") or ch:FindFirstChild("Torso"),ch:FindFirstChild("LowerTorso") or ch:FindFirstChild("HumanoidRootPart"),ch:FindFirstChild("LeftUpperArm") or ch:FindFirstChild("Left Arm"),ch:FindFirstChild("RightUpperArm") or ch:FindFirstChild("Right Arm"),ch:FindFirstChild("LeftUpperLeg") or ch:FindFirstChild("Left Leg"),ch:FindFirstChild("RightUpperLeg") or ch:FindFirstChild("Right Leg")}
        local cs={{1,2},{2,3},{2,4},{2,5},{3,6},{3,7}}
        for i=1,7 do d.esq37[i].Visible=false end
        for i,co in ipairs(cs) do
            local p1,p2=ps[co[1]],ps[co[2]]
            if p1 and p2 then
                local s1,o1=Camera:WorldToViewportPoint(p1.Position)
                local s2,o2=Camera:WorldToViewportPoint(p2.Position)
                if o1 and o2 then local l=d.esq37[i]; l.From=Vector2.new(s1.X,s1.Y); l.To=Vector2.new(s2.X,s2.Y); l.Visible=true; l.Color=C.CorEsq; l.Thickness=C.Espessura+1 end
            end
        end
    else for i=1,7 do d.esq37[i].Visible=false end end
    if C.ESP7 and head then d.cabeca7.Visible=true; d.cabeca7.Position=Vector2.new(cx,cy-alt/2-10); d.cabeca7.Radius=6; d.cabeca7.Color=C.CorBox else d.cabeca7.Visible=false end
    if C.ESP8 and head then d.cabeca8.Visible=true; d.cabeca8.Position=Vector2.new(cx,cy-alt/2-5); d.cabeca8.Radius=10; d.cabeca8.Color=C.CorBox else d.cabeca8.Visible=false end
    if C.ESP9 or C.ESP19 or C.ESP20 or C.ESP35 then d.nome.Visible=true; d.nome.Text=p.Name; d.nome.Position=Vector2.new(cx,cy-alt/2-16); d.nome.Color=C.CorNome else d.nome.Visible=false end
    if C.ESP10 then d.nomeDist.Visible=true; d.nomeDist.Text=p.Name.." ["..dist.."m]"; d.nomeDist.Position=Vector2.new(cx,cy-alt/2-16); d.nomeDist.Color=C.CorNome else d.nomeDist.Visible=false end
    if C.ESP19 then d.nomeVida.Visible=true; d.nomeVida.Text=p.Name.." ["..math.floor(hum.Health).."]"; d.nomeVida.Position=Vector2.new(cx,cy-alt/2-16); d.nomeVida.Color=C.CorNome else d.nomeVida.Visible=false end
    if C.ESP20 then d.nomeVidaDist.Visible=true; d.nomeVidaDist.Text=p.Name.." ["..math.floor(hum.Health).."] ["..dist.."m]"; d.nomeVidaDist.Position=Vector2.new(cx,cy-alt/2-16); d.nomeVidaDist.Color=C.CorNome else d.nomeVidaDist.Visible=false end
    if C.ESP11 or C.ESP13 or C.ESP16 or C.ESP19 or C.ESP20 or C.ESP36 then
        local pct=hum.Health/hum.MaxHealth
        local bx=cx-lar/2-6; local by=cy-alt/2
        d.vidaF.Visible=true; d.vidaF.From=Vector2.new(bx,by); d.vidaF.To=Vector2.new(bx,by+alt)
        d.vida.Visible=true; d.vida.Color=C.CorVida; d.vida.From=Vector2.new(bx,by+alt*(1-pct)); d.vida.To=Vector2.new(bx,by+alt)
    else d.vidaF.Visible=false; d.vida.Visible=false end
    if C.ESP12 or C.ESP16 or C.ESP19 or C.ESP20 or C.ESP36 then d.vidaN.Visible=true; d.vidaN.Text=tostring(math.floor(hum.Health)).."/"..tostring(math.floor(hum.MaxHealth)); d.vidaN.Position=Vector2.new(cx,cy-alt/2-30); d.vidaN.Color=C.CorVida else d.vidaN.Visible=false end
    if C.ESP14 then local pct=math.floor((hum.Health/hum.MaxHealth)*100); d.vidaPct.Visible=true; d.vidaPct.Text=pct.."%"; d.vidaPct.Position=Vector2.new(cx,cy-alt/2-44); d.vidaPct.Color=C.CorVida else d.vidaPct.Visible=false end
    if C.ESP15 or C.ESP16 then
        d.escudoF.Visible=true; d.escudoF.From=Vector2.new(cx+lar/2+6,cy-alt/2); d.escudoF.To=Vector2.new(cx+lar/2+6,cy+alt/2)
        d.escudo.Visible=true; d.escudo.Color=Color3.fromRGB(0,150,255); d.escudo.From=Vector2.new(cx+lar/2+6,cy-alt/2); d.escudo.To=Vector2.new(cx+lar/2+6,cy+alt/2)
    else d.escudoF.Visible=false; d.escudo.Visible=false end
    if C.ESP17 or C.ESP20 or C.ESP34 then d.dist.Visible=true; d.dist.Text="["..dist.."m]"; d.dist.Position=Vector2.new(cx,cy+alt/2+4); d.dist.Color=C.CorDist else d.dist.Visible=false end
    if C.ESP18 then d.distM.Visible=true; d.distM.Text=dist.."m"; d.distM.Position=Vector2.new(cx,cy+alt/2+18); d.distM.Color=C.CorDist else d.distM.Visible=false end
    if C.ESP21 then d.linha21.Visible=true; d.linha21.Thickness=C.Espessura; d.linha21.From=Vector2.new(Camera.ViewportSize.X/2,Camera.ViewportSize.Y/2); d.linha21.To=Vector2.new(cx,cy); d.linha21.Color=C.CorLinha else d.linha21.Visible=false end
    if C.ESP22 then d.linha22.Visible=true; d.linha22.Thickness=C.Espessura; d.linha22.From=Vector2.new(cx,0); d.linha22.To=Vector2.new(cx,cy-alt/2); d.linha22.Color=C.CorLinha else d.linha22.Visible=false end
    if C.ESP23 then d.linha23.Visible=true; d.linha23.Thickness=C.Espessura; d.linha23.From=Vector2.new(cx,cy+alt/2); d.linha23.To=Vector2.new(cx,Camera.ViewportSize.Y); d.linha23.Color=C.CorLinha else d.linha23.Visible=false end
    if C.ESP24 then d.linha24.Visible=true; d.linha24.Thickness=C.Espessura; d.linha24.From=Vector2.new(Camera.ViewportSize.X/2,Camera.ViewportSize.Y); d.linha24.To=Vector2.new(cx,cy+alt/2); d.linha24.Color=C.CorLinha else d.linha24.Visible=false end
    if C.ESP25 then d.box25.Visible=true; d.box25.Thickness=C.Espessura+1; d.box25.Size=Vector2.new(lar,alt); d.box25.Position=Vector2.new(cx-lar/2,cy-alt/2); d.box25.Color=C.CorBox else d.box25.Visible=false end
    if C.ESP28 then d.box28.Visible=true; d.box28.Thickness=C.Espessura; d.box28.Size=Vector2.new(lar*0.95,alt*0.95); d.box28.Position=Vector2.new(cx-lar*0.475,cy-alt*0.475); d.box28.Color=C.CorBox else d.box28.Visible=false end
    if C.ESP29 then d.box29.Visible=true; d.box29.Thickness=C.Espessura+2; d.box29.Size=Vector2.new(lar+4,alt+4); d.box29.Position=Vector2.new(cx-lar/2-2,cy-alt/2-2); d.box29.Color=Color3.fromRGB(0,0,0) else d.box29.Visible=false end
    if C.ESP30 then d.box30.Visible=true; d.box30.Thickness=C.Espessura+1; d.box30.Size=Vector2.new(lar,alt); d.box30.Position=Vector2.new(cx-lar/2,cy-alt/2); d.box30.Color=C.CorBox else d.box30.Visible=false end
    if C.ESP26 then d.boxP.Visible=true; d.boxP.Size=Vector2.new(lar,alt); d.boxP.Position=Vector2.new(cx-lar/2,cy-alt/2); d.boxP.Color=C.CorBox; d.boxP.Transparency=tr else d.boxP.Visible=false end
    if C.ESP27 then d.boxG.Visible=true; d.boxG.Size=Vector2.new(lar,alt); d.boxG.Position=Vector2.new(cx-lar/2,cy-alt/2); d.boxG.Color=C.CorBox; d.boxG.Transparency=0.3 else d.boxG.Visible=false end
    if (C.ESP38 or C.ESP39) and head then
        local ps={head,ch:FindFirstChild("UpperTorso") or ch:FindFirstChild("Torso"),ch:FindFirstChild("LowerTorso") or ch:FindFirstChild("HumanoidRootPart"),ch:FindFirstChild("LeftUpperArm") or ch:FindFirstChild("Left Arm"),ch:FindFirstChild("RightUpperArm") or ch:FindFirstChild("Right Arm"),ch:FindFirstChild("LeftUpperLeg") or ch:FindFirstChild("Left Leg"),ch:FindFirstChild("RightUpperLeg") or ch:FindFirstChild("Right Leg")}
        local alvo=C.ESP38 and d.juntas38 or d.juntas39
        local outra=C.ESP38 and d.juntas39 or d.juntas38
        for i=1,7 do
            if outra[i] then outra[i].Visible=false end
            local pt=ps[i]
            if pt then
                local sp,on2=Camera:WorldToViewportPoint(pt.Position)
                if on2 then alvo[i].Visible=true; alvo[i].Position=Vector2.new(sp.X,sp.Y); alvo[i].Radius=C.ESP39 and 6 or 4; alvo[i].Color=C.CorEsq else alvo[i].Visible=false end
            else alvo[i].Visible=false end
        end
    else for i=1,7 do d.juntas38[i].Visible=false; d.juntas39[i].Visible=false end end
    if C.ESPChams or C.ESP51 or C.ESP52 then
        if not d.chams or d.chams.Parent~=ch then
            if d.chams then d.chams:Destroy() end
            d.chams=Instance.new("Highlight"); d.chams.Name="ESP_Chams"; d.chams.Adornee=ch; d.chams.Parent=ch
        end
        d.chams.FillColor=C.CorChams; d.chams.OutlineColor=C.CorChams; d.chams.FillTransparency=0.6; d.chams.OutlineTransparency=0; d.chams.DepthMode=Enum.HighlightDepthMode.AlwaysOnTop
    else if d.chams then d.chams:Destroy(); d.chams=nil end end
    if C.ESPArma then
        local tool=ch:FindFirstChildOfClass("Tool")
        if tool then d.arma.Visible=true; d.arma.Text=tool.Name; d.arma.Position=Vector2.new(cx,cy+alt/2+32); d.arma.Color=C.CorArma else d.arma.Visible=false end
    else d.arma.Visible=false end
end

for _,p in ipairs(Players:GetPlayers()) do if p~=LP then CriarD(p) end end
Players.PlayerAdded:Connect(function(p)
    if p~=LP then CriarD(p) end
    p.CharacterAdded:Connect(function() task.wait(1); if p~=LP and not D[p] then CriarD(p) end end)
end)
Players.PlayerRemoving:Connect(RemoverD)

local function GetMelhorAlvo()
    local melhor, ms = nil, math.huge
    local ct = Vector2.new(Camera.ViewportSize.X/2, Camera.ViewportSize.Y/2)
    local mp = LP.Character and LP.Character:FindFirstChild("HumanoidRootPart") and LP.Character.HumanoidRootPart.Position or Camera.CFrame.Position
    for _, p in ipairs(Players:GetPlayers()) do
        if p ~= LP and not MesmoTime(p) and p.Character then
            local ch = p.Character
            local hum = ch:FindFirstChildOfClass("Humanoid")
            local hrp = ch:FindFirstChild("HumanoidRootPart")
            if hum and hum.Health > 0 and hrp then
                local pt = ParteAlvo(ch)
                if pt then
                    local dr = (hrp.Position - mp).Magnitude
                    if dr <= C.AimDist then
                        local sp, on = Camera:WorldToViewportPoint(pt.Position)
                        if on then
                            local dt = (Vector2.new(sp.X, sp.Y) - ct).Magnitude
                            if dt <= C.FOV then
                                local vis = true
                                if C.VisObrig then
                                    local rp = RaycastParams.new()
                                    rp.FilterType = Enum.RaycastFilterType.Exclude
                                    rp.FilterDescendantsInstances = {LP.Character, pt.Parent}
                                    vis = workspace:Raycast(Camera.CFrame.Position, pt.Position - Camera.CFrame.Position, rp) == nil
                                end
                                if vis then
                                    local sc = dt + dr * 0.05
                                    if sc < ms then ms = sc; melhor = pt end
                                end
                            end
                        end
                    end
                end
            end
        end
    end
    return melhor
end

local function AplicarAimbot()
    if not C.Aimbot then return end
    local alvo = GetMelhorAlvo()
    if not alvo then return end
    local pp = alvo.Position + (alvo.AssemblyLinearVelocity or Vector3.zero) * C.Pred
    if C.AimbotTipo == "Camera" then
        local cf = CFrame.new(Camera.CFrame.Position, pp)
        Camera.CFrame = Camera.CFrame:Lerp(cf, math.clamp(C.Suav/100, 0.01, 1))
    elseif C.AimbotTipo == "Mouse" then
        local screenPos, on = Camera:WorldToViewportPoint(pp)
        if on and mousemoverel then
            local dx = screenPos.X - Camera.ViewportSize.X/2
            local dy = screenPos.Y - Camera.ViewportSize.Y/2
            local sens = (100 - C.Suav) / 1000
            mousemoverel(dx * sens, dy * sens)
        end
    elseif C.AimbotTipo == "Silent" then
        local cf = CFrame.new(Camera.CFrame.Position, pp)
        Camera.CFrame = Camera.CFrame:Lerp(cf, 0.5)
    end
end

local function TPJogadorMaisProximo()
    local char = LP.Character
    if not char then return end
    local hrp = char:FindFirstChild("HumanoidRootPart")
    if not hrp then return end
    local maisProximo = nil
    local menorDist = math.huge
    for _, p in ipairs(Players:GetPlayers()) do
        if p ~= LP and p.Character then
            local alvoHrp = p.Character:FindFirstChild("HumanoidRootPart")
            local hum = p.Character:FindFirstChildOfClass("Humanoid")
            if alvoHrp and hum and hum.Health > 0 then
                local dist = (hrp.Position - alvoHrp.Position).Magnitude
                if dist < menorDist then
                    menorDist = dist
                    maisProximo = alvoHrp
                end
            end
        end
    end
    if maisProximo then
        hrp.CFrame = maisProximo.CFrame * CFrame.new(0, 0, -3)
    end
end

local function IniciarVoo()
    local ch=LP.Character; if not ch then return end
    local hrp=ch:FindFirstChild("HumanoidRootPart")
    local hum=ch:FindFirstChildOfClass("Humanoid")
    if not hrp or not hum then return end
    hum.PlatformStand=true
    bPos=Instance.new("BodyPosition"); bPos.MaxForce=Vector3.new(1e5,1e5,1e5); bPos.P=10000; bPos.D=500; bPos.Position=hrp.Position; bPos.Parent=hrp
    bGyr=Instance.new("BodyGyro"); bGyr.MaxTorque=Vector3.new(1e5,1e5,1e5); bGyr.P=10000; bGyr.D=500; bGyr.CFrame=hrp.CFrame; bGyr.Parent=hrp
    vooC=RunService.RenderStepped:Connect(function()
        if not C.Voo then return end
        local cam=workspace.CurrentCamera
        if not cam or not hrp or not hrp.Parent then return end
        local dir=Vector3.zero
        if UIS:IsKeyDown(Enum.KeyCode.W) then dir+=cam.CFrame.LookVector end
        if UIS:IsKeyDown(Enum.KeyCode.S) then dir-=cam.CFrame.LookVector end
        if UIS:IsKeyDown(Enum.KeyCode.A) then dir-=cam.CFrame.RightVector end
        if UIS:IsKeyDown(Enum.KeyCode.D) then dir+=cam.CFrame.RightVector end
        if UIS:IsKeyDown(Enum.KeyCode.Space) then dir+=Vector3.new(0,1,0) end
        if UIS:IsKeyDown(Enum.KeyCode.LeftControl) then dir-=Vector3.new(0,1,0) end
        if dir.Magnitude>0 then dir=dir.Unit end
        bPos.Position=bPos.Position+dir*C.VooVel
        bGyr.CFrame=CFrame.new(bPos.Position,bPos.Position+cam.CFrame.LookVector)
    end)
end

local function PararVoo()
    if vooC then vooC:Disconnect(); vooC=nil end
    if bPos then bPos:Destroy(); bPos=nil end
    if bGyr then bGyr:Destroy(); bGyr=nil end
    local ch=LP.Character
    if ch then
        local hum=ch:FindFirstChildOfClass("Humanoid"); if hum then hum.PlatformStand=false end
        local hrp=ch:FindFirstChild("HumanoidRootPart"); if hrp then hrp.Velocity=Vector3.zero; hrp.RotVelocity=Vector3.zero end
    end
end

local function RestNoclip()
    local ch=LP.Character
    if ch then for _,pt in ipairs(ch:GetDescendants()) do if pt:IsA("BasePart") then pt.CanCollide=true end end end
end

local function AplicarSpeed()
    local ch=LP.Character
    if ch then local hum=ch:FindFirstChildOfClass("Humanoid"); if hum then hum.WalkSpeed=C.Speed and C.SpeedVal or 16 end end
end

local function DesativarTudo()
    for k,v in pairs(C) do
        if type(v)=="boolean" and k:match("^ESP") then C[k]=false end
    end
    C.RGBAtivo=false; C.Aimbot=false
    C.Voo=false; PararVoo()
    C.Noclip=false; RestNoclip()
    C.Speed=false; AplicarSpeed()
    C.SJump=false; C.HUD=false
    for p,_ in pairs(D) do RemoverD(p) end
    for _,p in ipairs(Players:GetPlayers()) do if p~=LP then CriarD(p) end end
end

-- ==========================================
-- 15 FUNÇÕES NOVAS (PROTEGIDAS)
-- ==========================================
local function GetAlvoSilent()
    local melhor, menorDist = nil, C.SilentFOV
    local centro = Vector2.new(Camera.ViewportSize.X/2, Camera.ViewportSize.Y/2)
    for _, p in ipairs(Players:GetPlayers()) do
        if p ~= LP and p.Character then
            local head = p.Character:FindFirstChild("Head")
            local hum = p.Character:FindFirstChildOfClass("Humanoid")
            if head and hum and hum.Health > 0 then
                local sp, on = Camera:WorldToViewportPoint(head.Position)
                if on then
                    local dist = (Vector2.new(sp.X, sp.Y) - centro).Magnitude
                    if dist < menorDist then
                        menorDist = dist
                        melhor = head
                    end
                end
            end
        end
    end
    return melhor
end

pcall(function()
    local oldRaycast = workspace.Raycast
    workspace.Raycast = function(self, origem, direcao, params)
        if C.SilentAim then
            local alvo = GetAlvoSilent()
            if alvo then
                local novaDir = (alvo.Position - origem).Unit * direcao.Magnitude
                return oldRaycast(self, origem, novaDir, params)
            end
        end
        return oldRaycast(self, origem, direcao, params)
    end
end)

task.spawn(function()
    while true do
        task.wait(0.5)
        pcall(function()
            if C.HitboxExpander then
                for _, p in ipairs(Players:GetPlayers()) do
                    if p ~= LP and p.Character then
                        for _, parte in ipairs(p.Character:GetDescendants()) do
                            if parte:IsA("BasePart") and parte.Name ~= "HumanoidRootPart" then
                                parte.Size = parte.Size * C.HitboxSize
                                parte.Transparency = 0.5
                            end
                        end
                    end
                end
            end
        end)
    end
end)

task.spawn(function()
    while true do
        task.wait(0.1)
        pcall(function()
            if C.AntiStun then
                local char = LP.Character
                if char then
                    local hum = char:FindFirstChildOfClass("Humanoid")
                    if hum then
                        if hum.PlatformStand then hum.PlatformStand = false end
                        hum.WalkSpeed = C.SpeedVal or 50
                    end
                end
            end
        end)
    end
end)

local freecamConnection = nil
local freecamCFrame = nil
local function IniciarFreecam()
    local char = LP.Character
    if not char then return end
    freecamCFrame = Camera.CFrame
    if freecamConnection then freecamConnection:Disconnect() end
    freecamConnection = RunService.RenderStepped:Connect(function()
        if not C.Freecam then return end
        local dir = Vector3.zero
        if UIS:IsKeyDown(Enum.KeyCode.W) then dir += freecamCFrame.LookVector end
        if UIS:IsKeyDown(Enum.KeyCode.S) then dir -= freecamCFrame.LookVector end
        if UIS:IsKeyDown(Enum.KeyCode.A) then dir -= freecamCFrame.RightVector end
        if UIS:IsKeyDown(Enum.KeyCode.D) then dir += freecamCFrame.RightVector end
        freecamCFrame = freecamCFrame + dir * C.FreecamSpeed
        Camera.CFrame = freecamCFrame
    end)
end
local function PararFreecam()
    if freecamConnection then freecamConnection:Disconnect(); freecamConnection = nil end
end

local function InstantKill()
    local alvo = GetAlvoSilent()
    if alvo then
        local hum = alvo.Parent:FindFirstChildOfClass("Humanoid")
        if hum then hum.Health = 0 end
    end
end

local function TeleportKill()
    local alvo = GetAlvoSilent()
    if alvo then
        local char = LP.Character
        if char then
            local hrp = char:FindFirstChild("HumanoidRootPart")
            if hrp then hrp.CFrame = alvo.CFrame * CFrame.new(0, 0, -3) end
        end
    end
end

local function TeleportAll()
    local char = LP.Character
    if not char then return end
    local hrp = char:FindFirstChild("HumanoidRootPart")
    if not hrp then return end
    for _, p in ipairs(Players:GetPlayers()) do
        if p ~= LP and p.Character then
            local alvoHrp = p.Character:FindFirstChild("HumanoidRootPart")
            if alvoHrp then
                alvoHrp.CFrame = hrp.CFrame * CFrame.new(math.random(-10, 10), 5, math.random(-10, 10))
            end
        end
    end
end

local function FlingAll()
    local char = LP.Character
    if not char then return end
    local hrp = char:FindFirstChild("HumanoidRootPart")
    if not hrp then return end
    for _, p in ipairs(Players:GetPlayers()) do
        if p ~= LP and p.Character then
            local alvoHrp = p.Character:FindFirstChild("HumanoidRootPart")
            if alvoHrp then
                alvoHrp.Velocity = Vector3.new(math.random(-100, 100), 200, math.random(-100, 100))
            end
        end
    end
end

local function SoundSpam()
    if C.SoundId == 0 then return end
    local char = LP.Character
    if not char then return end
    local hrp = char:FindFirstChild("HumanoidRootPart")
    if not hrp then return end
    local sound = Instance.new("Sound")
    sound.SoundId = "rbxassetid://" .. C.SoundId
    sound.Volume = 10
    sound.Parent = hrp
    sound:Play()
    task.wait(1)
    sound:Destroy()
end

RunService.RenderStepped:Connect(function()
    pcall(function()
        if C.RainbowESP then
            local hue = (tick() * 0.3) % 1
            C.CorBox = Color3.fromHSV(hue, 1, 1)
            C.CorLinha = Color3.fromHSV((hue + 0.1) % 1, 1, 1)
            C.CorNome = Color3.fromHSV((hue + 0.2) % 1, 1, 1)
            C.CorEsq = Color3.fromHSV((hue + 0.3) % 1, 1, 1)
        end
        if C.SpinBot then
            local char = LP.Character
            if char then
                local hrp = char:FindFirstChild("HumanoidRootPart")
                if hrp then hrp.CFrame = hrp.CFrame * CFrame.Angles(0, math.rad(C.SpinSpeed), 0) end
            end
        end
    end)
end)

task.spawn(function()
    while true do
        task.wait(0.5)
        pcall(function()
            if C.NoCooldown then
                local char = LP.Character
                if char then
                    for _, obj in ipairs(char:GetDescendants()) do
                        if obj:IsA("Script") then pcall(function() obj.Disabled = false end) end
                    end
                end
            end
        end)
    end
end)

task.spawn(function()
    while true do
        task.wait(0.2)
        pcall(function()
            if C.AutoFarm then
                local char = LP.Character
                if char then
                    local hum = char:FindFirstChildOfClass("Humanoid")
                    if hum then hum:Move(Vector3.new(0, 0, 1), false) end
                end
            end
        end)
    end
end)

LP.CharacterAdded:Connect(function()
    task.wait(1); AplicarSpeed()
    if C.Voo then C.Voo=false; PararVoo() end
end)

RunService.RenderStepped:Connect(function()
    pcall(function()
        if C.RGBAtivo then
            C.Hue=(C.Hue+0.005*C.RGBVel)%1
            local cor=Color3.fromHSV(C.Hue,1,C.RGBBri)
            C.CorBox=cor; C.CorLinha=cor; C.CorNome=cor; C.CorEsq=cor; C.CorChams=cor
        end
        for p,_ in pairs(D) do if p.Parent then AtualizarJogador(p) else RemoverD(p) end end
        if C.MostrarFOV and C.Aimbot then
            if not FOVC then FOVC=Drawing.new("Circle"); FOVC.Thickness=1; FOVC.Filled=false; FOVC.NumSides=64 end
            FOVC.Visible=true; FOVC.Radius=C.FOV; FOVC.Position=Vector2.new(Camera.ViewportSize.X/2,Camera.ViewportSize.Y/2); FOVC.Color=C.CorChams
        elseif FOVC then FOVC.Visible=false end
        if C.Cross then
            if not CrossD then CrossD=Drawing.new("Circle"); CrossD.Thickness=1; CrossD.Filled=false; CrossD.NumSides=4; CrossD.Radius=8 end
            CrossD.Visible=true; CrossD.Position=Vector2.new(Camera.ViewportSize.X/2,Camera.ViewportSize.Y/2); CrossD.Color=C.CorChams
        elseif CrossD then CrossD.Visible=false end
        if C.Aimbot and (C.AimToggle or UIS:IsKeyDown(C.AimKey)) then AplicarAimbot() end
        if C.Noclip then
            local ch=LP.Character
            if ch then for _,pt in ipairs(ch:GetDescendants()) do if pt:IsA("BasePart") then pt.CanCollide=false end end end
        end
        if C.Speed then
            local ch=LP.Character
            if ch then local hum=ch:FindFirstChildOfClass("Humanoid"); if hum and hum.WalkSpeed~=C.SpeedVal then hum.WalkSpeed=C.SpeedVal end end
        end
        if C.SJump then
            local ch=LP.Character
            if ch then local hum=ch:FindFirstChildOfClass("Humanoid"); if hum then hum.JumpPower=150 end end
        end
        if C.HUD then
            if not fpsL then fpsL=Drawing.new("Text"); fpsL.Size=14; fpsL.Outline=true; tempoL=Drawing.new("Text"); tempoL.Size=14; tempoL.Outline=true; alvoL=Drawing.new("Text"); alvoL.Size=14; alvoL.Outline=true end
            local fps=math.floor(1/math.max(0.016,0.001))
            table.insert(fpsH,fps); if #fpsH>30 then table.remove(fpsH,1) end
            local fm=0; for _,v in ipairs(fpsH) do fm=fm+v end; fm=math.floor(fm/#fpsH)
            local al=0; for _ in pairs(D) do al=al+1 end
            fpsL.Visible=true; fpsL.Text="FPS: "..fm; fpsL.Position=Vector2.new(15,15); fpsL.Color=C.CorChams
            tempoL.Visible=true; tempoL.Text="Sessao: "..math.floor(tick()-t0).."s"; tempoL.Position=Vector2.new(15,35); tempoL.Color=C.CorChams
            alvoL.Visible=true; alvoL.Text="Alvos: "..al; alvoL.Position=Vector2.new(15,55); alvoL.Color=C.CorChams
        else
            if fpsL then fpsL.Visible=false end
            if tempoL then tempoL.Visible=false end
            if alvoL then alvoL.Visible=false end
        end
    end)
end)

UIS.InputBegan:Connect(function(i,gp)
    if gp then return end
    pcall(function()
        if i.KeyCode==C.KeyMenu then
            if MenuGui then local m=MenuGui:FindFirstChildWhichIsA("Frame"); if m then m.Visible=not m.Visible end end
            return
        end
        if i.KeyCode==C.KeyHUD then C.HUD=not C.HUD return end
        if i.KeyCode==C.KeyUpd then
            for p,_ in pairs(D) do RemoverD(p) end
            for _,p in ipairs(Players:GetPlayers()) do if p~=LP then CriarD(p) end end
            return
        end
        if i.KeyCode==C.KeyVoo then C.Voo=not C.Voo; if C.Voo then IniciarVoo() else PararVoo() end return end
        if i.KeyCode==C.KeyGhost then C.Noclip=not C.Noclip; if not C.Noclip then RestNoclip() end return end
        if i.KeyCode==C.KeySpeed then C.Speed=not C.Speed; AplicarSpeed(); return end
        if i.KeyCode==C.KeyTP then TPJogadorMaisProximo(); return end
        if i.KeyCode==Enum.KeyCode.Z then C.SilentAim=not C.SilentAim return end
        if i.KeyCode==Enum.KeyCode.X then C.Freecam=not C.Freecam; if C.Freecam then IniciarFreecam() else PararFreecam() end return end
        if i.KeyCode==Enum.KeyCode.C then InstantKill() return end
        if i.KeyCode==Enum.KeyCode.Q then TeleportKill() return end
        if i.KeyCode==Enum.KeyCode.R then TeleportAll() return end
        if i.KeyCode==Enum.KeyCode.T then FlingAll() return end
        if i.KeyCode==Enum.KeyCode.G then SoundSpam() return end
    end)
end)

-- ==========================================
-- MENU (protegido com pcall)
-- ==========================================
pcall(function()
    if MenuGui then MenuGui:Destroy() end
    local P = {
        bg=C.MenuFundo, bgHeader=C.MenuHeader, bgSidebar=Color3.fromRGB(15,15,20),
        card=C.MenuCard, cardHover=Color3.fromRGB(30,30,40), cardActive=Color3.fromRGB(45,12,20),
        accent=C.MenuAccent, accentLight=Color3.fromRGB(255,80,95), accentGlow=Color3.fromRGB(255,120,130),
        text=Color3.fromRGB(235,235,245), textDim=Color3.fromRGB(130,130,145), border=Color3.fromRGB(45,25,35),
        success=Color3.fromRGB(80,220,120),
    }
    local gui = Instance.new("ScreenGui")
    gui.Name = "RD_Ultimate_Premium"; gui.ResetOnSpawn = false; gui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
    local parent = game.CoreGui
    if gethui then local ok,res=pcall(gethui); if ok and res then parent=res end end
    gui.Parent = parent; MenuGui = gui
    local main = Instance.new("Frame")
    main.Size = UDim2.new(0, 620, 0, 460)
    main.Position = UDim2.new(0.5, -310, 0.5, -230)
    main.BackgroundColor3 = P.bg; main.BorderSizePixel = 0; main.Active = true; main.Draggable = true; main.Parent = gui
    local mc = Instance.new("UICorner"); mc.CornerRadius = UDim.new(0,12); mc.Parent = main
    local ms = Instance.new("UIStroke"); ms.Color = P.accent; ms.Thickness = 1.5; ms.Transparency = 0.4; ms.Parent = main
    local topLine = Instance.new("Frame")
    topLine.Size = UDim2.new(1,0,0,2); topLine.BackgroundColor3 = P.accent; topLine.BorderSizePixel = 0; topLine.Parent = main
    local tlC = Instance.new("UICorner"); tlC.CornerRadius = UDim.new(0,12); tlC.Parent = topLine
    local header = Instance.new("Frame")
    header.Size = UDim2.new(1,0,0,56); header.BackgroundColor3 = P.bgHeader; header.BorderSizePixel = 0; header.Parent = main
    local hc = Instance.new("UICorner"); hc.CornerRadius = UDim.new(0,12); hc.Parent = header
    local logoBox = Instance.new("Frame")
    logoBox.Size = UDim2.new(0,36,0,36); logoBox.Position = UDim2.new(0,16,0,10)
    logoBox.BackgroundColor3 = P.accent; logoBox.BorderSizePixel = 0; logoBox.Parent = header
    local lc = Instance.new("UICorner"); lc.CornerRadius = UDim.new(0,9); lc.Parent = logoBox
    local logoText = Instance.new("TextLabel")
    logoText.Size = UDim2.new(1,0,1,0); logoText.BackgroundTransparency = 1; logoText.Text = "RD"
    logoText.TextColor3 = P.text; logoText.Font = Enum.Font.GothamBlack; logoText.TextSize = 16; logoText.Parent = logoBox
    local titulo = Instance.new("TextLabel")
    titulo.Size = UDim2.new(0,300,0,20); titulo.Position = UDim2.new(0,62,0,12); titulo.BackgroundTransparency = 1
    titulo.Text = "RD CHEATS ULTIMATE v7.1"; titulo.TextColor3 = P.text; titulo.Font = Enum.Font.GothamBlack
    titulo.TextSize = 15; titulo.TextXAlignment = Enum.TextXAlignment.Left; titulo.Parent = header
    local statusLabel = Instance.new("TextLabel")
    statusLabel.Size = UDim2.new(0,400,0,16); statusLabel.Position = UDim2.new(0,62,0,32); statusLabel.BackgroundTransparency = 1
    statusLabel.Text = "ONLINE | 60 ESPs | 3 AIMBOTS | 15 EXTRAS"; statusLabel.TextColor3 = P.success
    statusLabel.Font = Enum.Font.GothamMedium; statusLabel.TextSize = 10
    statusLabel.TextXAlignment = Enum.TextXAlignment.Left; statusLabel.Parent = header
    local btnOcultar = Instance.new("TextButton")
    btnOcultar.Size = UDim2.new(0,70,0,28); btnOcultar.Position = UDim2.new(1,-190,0,14)
    btnOcultar.BackgroundColor3 = P.card; btnOcultar.Text = "OCULTAR"; btnOcultar.TextColor3 = P.textDim
    btnOcultar.Font = Enum.Font.GothamBold; btnOcultar.TextSize = 10; btnOcultar.BorderSizePixel = 0; btnOcultar.Parent = header
    local boc = Instance.new("UICorner"); boc.CornerRadius = UDim.new(0,7); boc.Parent = btnOcultar
    btnOcultar.MouseButton1Click:Connect(function() main.Visible = false end)
    local btnSalvar = Instance.new("TextButton")
    btnSalvar.Size = UDim2.new(0,60,0,28); btnSalvar.Position = UDim2.new(1,-116,0,14)
    btnSalvar.BackgroundColor3 = P.card; btnSalvar.Text = "SALVAR"; btnSalvar.TextColor3 = P.textDim
    btnSalvar.Font = Enum.Font.GothamBold; btnSalvar.TextSize = 10; btnSalvar.BorderSizePixel = 0; btnSalvar.Parent = header
    local bsc = Instance.new("UICorner"); bsc.CornerRadius = UDim.new(0,7); bsc.Parent = btnSalvar
    btnSalvar.MouseButton1Click:Connect(function()
        pcall(function()
            if writefile then
                local dados={}
                for k,v in pairs(C) do if type(v)=="boolean" or type(v)=="number" or type(v)=="string" then dados[k]=v end end
                writefile("rdcheats_config.json", HttpService:JSONEncode(dados))
            end
        end)
        btnSalvar.Text = "OK!"; task.wait(1); btnSalvar.Text = "SALVAR"
    end)
    local btnFechar = Instance.new("TextButton")
    btnFechar.Size = UDim2.new(0,28,0,28); btnFechar.Position = UDim2.new(1,-44,0,14)
    btnFechar.BackgroundColor3 = P.accent; btnFechar.Text = "X"; btnFechar.TextColor3 = P.text
    btnFechar.Font = Enum.Font.GothamBold; btnFechar.TextSize = 14; btnFechar.BorderSizePixel = 0; btnFechar.Parent = header
    local bfc = Instance.new("UICorner"); bfc.CornerRadius = UDim.new(0,7); bfc.Parent = btnFechar
    btnFechar.MouseButton1Click:Connect(function()
        DesativarTudo(); if MenuGui then MenuGui:Destroy(); MenuGui = nil end
    end)
    local sidebar = Instance.new("Frame")
    sidebar.Size = UDim2.new(0,160,1,-76); sidebar.Position = UDim2.new(0,12,0,66)
    sidebar.BackgroundColor3 = P.bgSidebar; sidebar.BorderSizePixel = 0; sidebar.Parent = main
    local sbc = Instance.new("UICorner"); sbc.CornerRadius = UDim.new(0,10); sbc.Parent = sidebar
    local sbs = Instance.new("UIStroke"); sbs.Color = P.border; sbs.Thickness = 1; sbs.Parent = sidebar
    local sbl = Instance.new("UIListLayout"); sbl.Padding = UDim.new(0,5); sbl.Parent = sidebar
    local sbp = Instance.new("UIPadding"); sbp.PaddingTop = UDim.new(0,10); sbp.PaddingLeft = UDim.new(0,8); sbp.PaddingRight = UDim.new(0,8); sbp.Parent = sidebar
    local content = Instance.new("Frame")
    content.Size = UDim2.new(1,-190,1,-76); content.Position = UDim2.new(0,178,0,66)
    content.BackgroundColor3 = P.bgSidebar; content.BorderSizePixel = 0; content.Parent = main
    local ctc = Instance.new("UICorner"); ctc.CornerRadius = UDim.new(0,10); ctc.Parent = content
    local cts = Instance.new("UIStroke"); cts.Color = P.border; cts.Thickness = 1; cts.Parent = content
    local abas = {}
    local botoes = {}
    local function novaAba()
        local s = Instance.new("ScrollingFrame")
        s.Size = UDim2.new(1,-12,1,-12); s.Position = UDim2.new(0,6,0,6)
        s.BackgroundTransparency = 1; s.ScrollBarThickness = 3; s.ScrollBarImageColor3 = P.accent
        s.CanvasSize = UDim2.new(0,0,0,0); s.AutomaticCanvasSize = Enum.AutomaticSize.Y
        s.Visible = false; s.Parent = content
        local l = Instance.new("UIListLayout"); l.SortOrder = Enum.SortOrder.LayoutOrder; l.Padding = UDim.new(0,4); l.Parent = s
        return s
    end
    local function seccao(parent, txt)
        local l = Instance.new("TextLabel")
        l.Size = UDim2.new(1,-8,0,22); l.BackgroundTransparency = 1
        l.Text = txt:upper(); l.TextColor3 = P.accentLight; l.Font = Enum.Font.GothamBold
        l.TextSize = 10; l.TextXAlignment = Enum.TextXAlignment.Left; l.Parent = parent
    end
    local function toggle(parent, nome, key, cb)
        local b = Instance.new("TextButton")
        b.Size = UDim2.new(1,-8,0,30); b.BackgroundColor3 = P.card; b.Text = ""
        b.BorderSizePixel = 0; b.AutoButtonColor = false; b.Parent = parent
        local c = Instance.new("UICorner"); c.CornerRadius = UDim.new(0,6); c.Parent = b
        local stroke = Instance.new("UIStroke"); stroke.Color = P.border; stroke.Thickness = 1; stroke.Parent = b
        local dot = Instance.new("Frame")
        dot.Size = UDim2.new(0,8,0,8); dot.Position = UDim2.new(0,10,0.5,-4)
        dot.BackgroundColor3 = P.textDim; dot.BorderSizePixel = 0; dot.Parent = b
        local dc = Instance.new("UICorner"); dc.CornerRadius = UDim.new(1,0); dc.Parent = dot
        local txt = Instance.new("TextLabel")
        txt.Size = UDim2.new(1,-40,1,0); txt.Position = UDim2.new(0,26,0,0)
        txt.BackgroundTransparency = 1; txt.Text = nome; txt.TextColor3 = P.textDim
        txt.Font = Enum.Font.GothamMedium; txt.TextSize = 12; txt.TextXAlignment = Enum.TextXAlignment.Left; txt.Parent = b
        local estado = false
        local function aplicar()
            if estado then
                b.BackgroundColor3 = P.cardActive; stroke.Color = P.accent
                dot.BackgroundColor3 = P.accentLight; txt.TextColor3 = P.text
            else
                b.BackgroundColor3 = P.card; stroke.Color = P.border
                dot.BackgroundColor3 = P.textDim; txt.TextColor3 = P.textDim
            end
        end
        b.MouseEnter:Connect(function() if not estado then b.BackgroundColor3 = P.cardHover end end)
        b.MouseLeave:Connect(function() if not estado then b.BackgroundColor3 = P.card end end)
        b.MouseButton1Click:Connect(function()
            estado = not estado; C[key] = estado; aplicar()
            if cb then cb(estado) end
        end)
    end
    local function slider(parent, nome, key, min, max, cb)
        local f = Instance.new("Frame")
        f.Size = UDim2.new(1,-8,0,46); f.BackgroundColor3 = P.card; f.BorderSizePixel = 0; f.Parent = parent
        local c = Instance.new("UICorner"); c.CornerRadius = UDim.new(0,6); c.Parent = f
        local lbl = Instance.new("TextLabel")
        lbl.Size = UDim2.new(1,-20,0,20); lbl.Position = UDim2.new(0,10,0,4); lbl.BackgroundTransparency = 1
        lbl.Text = nome.."  .  "..tostring(C[key]); lbl.TextColor3 = P.text
        lbl.Font = Enum.Font.GothamMedium; lbl.TextSize = 11; lbl.TextXAlignment = Enum.TextXAlignment.Left; lbl.Parent = f
        local bar = Instance.new("Frame")
        bar.Size = UDim2.new(1,-20,0,5); bar.Position = UDim2.new(0,10,0,30)
        bar.BackgroundColor3 = Color3.fromRGB(35,35,45); bar.BorderSizePixel = 0; bar.Parent = f
        local bc = Instance.new("UICorner"); bc.CornerRadius = UDim.new(1,0); bc.Parent = bar
        local fill = Instance.new("Frame")
        fill.Size = UDim2.new((C[key]-min)/(max-min),0,1,0); fill.BackgroundColor3 = P.accent
        fill.BorderSizePixel = 0; fill.Parent = bar
        local fc = Instance.new("UICorner"); fc.CornerRadius = UDim.new(1,0); fc.Parent = fill
        local knob = Instance.new("Frame")
        knob.Size = UDim2.new(0,10,0,10); knob.Position = UDim2.new(fill.Size.X.Scale,-5,0.5,-5)
        knob.BackgroundColor3 = P.accentGlow; knob.BorderSizePixel = 0; knob.Parent = bar
        local kc = Instance.new("UICorner"); kc.CornerRadius = UDim.new(1,0); kc.Parent = knob
        local dragging = false
        local function upd(x)
            local rel = math.clamp((x-bar.AbsolutePosition.X)/bar.AbsoluteSize.X, 0, 1)
            local val = math.floor(min+(max-min)*rel); C[key] = val
            fill.Size = UDim2.new(rel,0,1,0); knob.Position = UDim2.new(rel,-5,0.5,-5)
            lbl.Text = nome.."  .  "..tostring(val)
            if cb then cb(val) end
        end
        bar.InputBegan:Connect(function(i) if i.UserInputType==Enum.UserInputType.MouseButton1 then dragging=true; upd(i.Position.X) end end)
        UIS.InputChanged:Connect(function(i) if dragging and i.UserInputType==Enum.UserInputType.MouseMovement then upd(i.Position.X) end end)
        UIS.InputEnded:Connect(function(i) if i.UserInputType==Enum.UserInputType.MouseButton1 then dragging=false end end)
    end
    local sESP=novaAba(); local sVIDA=novaAba(); local sMARCADORES=novaAba()
    local sSKELETON=novaAba(); local sINDICADORES=novaAba(); local sPERSONALIZACAO=novaAba()
    local sRGB=novaAba(); local sAIM=novaAba(); local sMOVE=novaAba(); local sMENU=novaAba()
    abas["ESP"]=sESP; abas["VIDA"]=sVIDA; abas["MARCADORES"]=sMARCADORES
    abas["SKELETON"]=sSKELETON; abas["INDICADORES"]=sINDICADORES; abas["PERSONALIZACAO"]=sPERSONALIZACAO
    abas["RGB"]=sRGB; abas["AIM"]=sAIM; abas["MOVIMENTO"]=sMOVE; abas["MENU"]=sMENU
    seccao(sESP,"Visual ESP")
    toggle(sESP,"1. ESP Linha","ESP1"); toggle(sESP,"2. ESP Box","ESP2"); toggle(sESP,"3. ESP Box 2D","ESP3")
    toggle(sESP,"4. ESP Box 3D","ESP4"); toggle(sESP,"5. ESP Skeleton","ESP5"); toggle(sESP,"6. ESP Esqueleto Completo","ESP6")
    toggle(sESP,"7. ESP Cabeca","ESP7"); toggle(sESP,"8. ESP Circulo na Cabeca","ESP8")
    toggle(sESP,"9. ESP Nome","ESP9"); toggle(sESP,"10. ESP Nome com Distancia","ESP10")
    seccao(sVIDA,"Vida e Informacoes")
    toggle(sVIDA,"11. ESP Vida","ESP11"); toggle(sVIDA,"12. ESP Vida com Numeracao","ESP12")
    toggle(sVIDA,"13. ESP Barra de Vida","ESP13"); toggle(sVIDA,"14. ESP Vida em Porcentagem","ESP14")
    toggle(sVIDA,"15. ESP Escudo","ESP15"); toggle(sVIDA,"16. ESP Vida e Escudo","ESP16")
    toggle(sVIDA,"17. ESP Distancia","ESP17"); toggle(sVIDA,"18. ESP Distancia em Metros","ESP18")
    toggle(sVIDA,"19. ESP Nome e Vida","ESP19"); toggle(sVIDA,"20. ESP Nome, Vida e Distancia","ESP20")
    seccao(sMARCADORES,"Marcadores")
    toggle(sMARCADORES,"21. ESP Linha do Centro","ESP21"); toggle(sMARCADORES,"22. ESP Linha do Topo","ESP22")
    toggle(sMARCADORES,"23. ESP Linha dos Pes","ESP23"); toggle(sMARCADORES,"24. ESP Linha Dinamica","ESP24")
    toggle(sMARCADORES,"25. ESP Box com Contorno","ESP25"); toggle(sMARCADORES,"26. ESP Box Preenchida","ESP26")
    toggle(sMARCADORES,"27. ESP Box com Gradiente","ESP27"); toggle(sMARCADORES,"28. ESP Box Arredondada","ESP28")
    toggle(sMARCADORES,"29. ESP Box com Sombra","ESP29"); toggle(sMARCADORES,"30. ESP Box Neon","ESP30")
    seccao(sSKELETON,"Skeleton e Modelos")
    toggle(sSKELETON,"31. ESP Skeleton Colorido","ESP31"); toggle(sSKELETON,"32. ESP Skeleton Neon","ESP32")
    toggle(sSKELETON,"33. ESP Skeleton com Distancia","ESP33"); toggle(sSKELETON,"34. ESP Skeleton com Nome","ESP34")
    toggle(sSKELETON,"35. ESP Skeleton com Vida","ESP35"); toggle(sSKELETON,"36. ESP Skeleton Completo","ESP36")
    toggle(sSKELETON,"37. ESP Skeleton Completo 2","ESP37"); toggle(sSKELETON,"38. ESP Juntas","ESP38")
    toggle(sSKELETON,"39. ESP Articulacoes","ESP39"); toggle(sSKELETON,"40. ESP Estrutura Corporal","ESP40")
    seccao(sINDICADORES,"Indicadores Avancados")
    toggle(sINDICADORES,"41. ESP Indicador de Alvo","ESP41"); toggle(sINDICADORES,"42. ESP Circulo de Distancia","ESP42")
    toggle(sINDICADORES,"43. ESP Indicador de Direcao","ESP43"); toggle(sINDICADORES,"44. ESP Indicador de Posicao","ESP44")
    toggle(sINDICADORES,"45. ESP Marcador Superior","ESP45"); toggle(sINDICADORES,"46. ESP Marcador Inferior","ESP46")
    toggle(sINDICADORES,"47. ESP Caixa de Informacoes","ESP47"); toggle(sINDICADORES,"48. ESP Painel de Status","ESP48")
    toggle(sINDICADORES,"49. ESP Etiqueta de Identificacao","ESP49"); toggle(sINDICADORES,"50. ESP Marcador Personalizado","ESP50")
    seccao(sPERSONALIZACAO,"Personalizacao")
    toggle(sPERSONALIZACAO,"51. ESP RGB","ESP51"); toggle(sPERSONALIZACAO,"52. ESP Arco-Iris","ESP52")
    toggle(sPERSONALIZACAO,"53. ESP Cor Personalizada","ESP53"); toggle(sPERSONALIZACAO,"54. ESP Gradiente RGB","ESP54")
    toggle(sPERSONALIZACAO,"55. ESP Contorno Dinamico","ESP55"); toggle(sPERSONALIZACAO,"56. ESP Transparencia Ajustavel","ESP56")
    toggle(sPERSONALIZACAO,"57. ESP Espessura Personalizada","ESP57"); toggle(sPERSONALIZACAO,"58. ESP Tamanho Ajustavel","ESP58")
    toggle(sPERSONALIZACAO,"59. ESP Tema Minimalista","ESP59"); toggle(sPERSONALIZACAO,"60. ESP Personalizado","ESP60")
    seccao(sRGB,"Controlador RGB")
    toggle(sRGB,"RGB Ativo","RGBAtivo"); slider(sRGB,"Velocidade RGB","RGBVel",1,10); slider(sRGB,"Brilho","RGBBri",1,10)
    seccao(sAIM,"Tipo de Aimbot")
    local tipos = {"Camera", "Mouse", "Silent"}
    local tipoBtns = {}
    local tipoFrame = Instance.new("Frame")
    tipoFrame.Size = UDim2.new(1,-8,0,32); tipoFrame.BackgroundColor3 = P.card; tipoFrame.BorderSizePixel = 0; tipoFrame.Parent = sAIM
    local tfc = Instance.new("UICorner"); tfc.CornerRadius = UDim.new(0,6); tfc.Parent = tipoFrame
    local tfl = Instance.new("UIListLayout"); tfl.FillDirection = Enum.FillDirection.Horizontal; tfl.Padding = UDim.new(0,4); tfl.Parent = tipoFrame
    local tfp = Instance.new("UIPadding"); tfp.PaddingLeft = UDim.new(0,4); tfp.PaddingTop = UDim.new(0,4); tfp.Parent = tipoFrame
    local function atualizarTipos()
        for t,b in pairs(tipoBtns) do
            if C.AimbotTipo==t then b.BackgroundColor3=P.accent; b.TextColor3=P.text
            else b.BackgroundColor3=P.cardHover; b.TextColor3=P.textDim end
        end
    end
    for _,t in ipairs(tipos) do
        local b = Instance.new("TextButton")
        b.Size = UDim2.new(0,88,0,24); b.BackgroundColor3=P.cardHover; b.Text=t
        b.TextColor3=P.textDim; b.Font=Enum.Font.GothamBold; b.TextSize=10; b.BorderSizePixel=0; b.Parent=tipoFrame
        local bc = Instance.new("UICorner"); bc.CornerRadius=UDim.new(0,4); bc.Parent=b
        tipoBtns[t]=b
        b.MouseButton1Click:Connect(function() C.AimbotTipo=t; atualizarTipos() end)
    end
    atualizarTipos()
    seccao(sAIM,"Configuracoes")
    toggle(sAIM,"Aimbot Ativar","Aimbot"); toggle(sAIM,"Aimbot Toggle (sem segurar)","AimToggle")
    toggle(sAIM,"Mostrar FOV","MostrarFOV"); toggle(sAIM,"So se Visivel","VisObrig"); toggle(sAIM,"Crosshair","Cross")
    slider(sAIM,"FOV","FOV",20,1000); slider(sAIM,"Suavidade","Suav",1,100)
    slider(sAIM,"Distancia Maxima","AimDist",50,1000); slider(sAIM,"Predicao","Pred",0,50)
    seccao(sMOVE,"Voo")
    toggle(sMOVE,"Voar (V)","Voo",function(v) if v then IniciarVoo() else PararVoo() end end)
    slider(sMOVE,"Velocidade do Voo","VooVel",1,20)
    seccao(sMOVE,"Outros")
    toggle(sMOVE,"Noclip (G)","Noclip",function(v) if not v then RestNoclip() end end)
    toggle(sMOVE,"Speed (M)","Speed",function() AplicarSpeed() end)
    slider(sMOVE,"Valor do Speed","SpeedVal",16,300,function() AplicarSpeed() end)
    toggle(sMOVE,"Super Jump","SJump")
    toggle(sMOVE,"TP JOGADOR PROXIMO (B)","_tpBotao",function() TPJogadorMaisProximo() end)
    seccao(sMOVE,"APELAO")
    toggle(sMOVE,"SILENT AIM (Z)","SilentAim")
    toggle(sMOVE,"HITBOX EXPANDER","HitboxExpander")
    toggle(sMOVE,"AUTO-PARRY","AutoParry")
    toggle(sMOVE,"INFINITE YIELD","InfiniteYield")
    toggle(sMOVE,"ANTI-STUN","AntiStun")
    toggle(sMOVE,"FREECAM (X)","Freecam",function(v) if v then IniciarFreecam() else PararFreecam() end end)
    toggle(sMOVE,"RAINBOW ESP","RainbowESP")
    toggle(sMOVE,"SPINBOT","SpinBot")
    toggle(sMOVE,"NO COOLDOWN","NoCooldown")
    toggle(sMOVE,"AUTO FARM","AutoFarm")
    seccao(sMENU,"Cor do Menu")
    local function colorSlider(parent, nome, get, set)
        local f = Instance.new("Frame")
        f.Size = UDim2.new(1,-8,0,46); f.BackgroundColor3 = P.card; f.BorderSizePixel = 0; f.Parent = parent
        local c = Instance.new("UICorner"); c.CornerRadius = UDim.new(0,6); c.Parent = f
        local lbl = Instance.new("TextLabel")
        lbl.Size = UDim2.new(1,-20,0,20); lbl.Position = UDim2.new(0,10,0,4); lbl.BackgroundTransparency = 1
        lbl.Text = nome.."  .  "..tostring(math.floor(get()*255)); lbl.TextColor3 = P.text
        lbl.Font = Enum.Font.GothamMedium; lbl.TextSize = 11; lbl.TextXAlignment = Enum.TextXAlignment.Left; lbl.Parent = f
        local bar = Instance.new("Frame")
        bar.Size = UDim2.new(1,-20,0,5); bar.Position = UDim2.new(0,10,0,30)
        bar.BackgroundColor3 = Color3.fromRGB(35,35,45); bar.BorderSizePixel = 0; bar.Parent = f
        local bc = Instance.new("UICorner"); bc.CornerRadius = UDim.new(1,0); bc.Parent = bar
        local fill = Instance.new("Frame")
        fill.Size = UDim2.new(get(),0,1,0); fill.BackgroundColor3 = P.accent; fill.BorderSizePixel = 0; fill.Parent = bar
        local fc = Instance.new("UICorner"); fc.CornerRadius = UDim.new(1,0); fc.Parent = fill
        local knob = Instance.new("Frame")
        knob.Size = UDim2.new(0,10,0,10); knob.Position = UDim2.new(get(),-5,0.5,-5)
        knob.BackgroundColor3 = P.accentGlow; knob.BorderSizePixel = 0; knob.Parent = bar
        local kc = Instance.new("UICorner"); kc.CornerRadius = UDim.new(1,0); kc.Parent = knob
        local dragging = false
        local function upd(x)
            local rel = math.clamp((x-bar.AbsolutePosition.X)/bar.AbsoluteSize.X, 0, 1)
            fill.Size = UDim2.new(rel,0,1,0); knob.Position = UDim2.new(rel,-5,0.5,-5)
            lbl.Text = nome.."  .  "..tostring(math.floor(rel*255))
            set(rel)
        end
        bar.InputBegan:Connect(function(i) if i.UserInputType==Enum.UserInputType.MouseButton1 then dragging=true; upd(i.Position.X) end end)
        UIS.InputChanged:Connect(function(i) if dragging and i.UserInputType==Enum.UserInputType.MouseMovement then upd(i.Position.X) end end)
        UIS.InputEnded:Connect(function(i) if i.UserInputType==Enum.UserInputType.MouseButton1 then dragging=false end end)
    end
    colorSlider(sMENU, "Fundo R", function() return C.MenuFundo.R end, function(v) C.MenuFundo=Color3.new(v,C.MenuFundo.G,C.MenuFundo.B); main.BackgroundColor3=C.MenuFundo end)
    colorSlider(sMENU, "Fundo G", function() return C.MenuFundo.G end, function(v) C.MenuFundo=Color3.new(C.MenuFundo.R,v,C.MenuFundo.B); main.BackgroundColor3=C.MenuFundo end)
    colorSlider(sMENU, "Fundo B", function() return C.MenuFundo.B end, function(v) C.MenuFundo=Color3.new(C.MenuFundo.R,C.MenuFundo.G,v); main.BackgroundColor3=C.MenuFundo end)
    colorSlider(sMENU, "Accent R", function() return C.MenuAccent.R end, function(v) C.MenuAccent=Color3.new(v,C.MenuAccent.G,C.MenuAccent.B); ms.Color=C.MenuAccent end)
    colorSlider(sMENU, "Accent G", function() return C.MenuAccent.G end, function(v) C.MenuAccent=Color3.new(C.MenuAccent.R,v,C.MenuAccent.B); ms.Color=C.MenuAccent end)
    colorSlider(sMENU, "Accent B", function() return C.MenuAccent.B end, function(v) C.MenuAccent=Color3.new(C.MenuAccent.R,C.MenuAccent.G,v); ms.Color=C.MenuAccent end)
    local function botaoAba(nome)
        local b = Instance.new("TextButton")
        b.Size = UDim2.new(1,0,0,32); b.BackgroundColor3 = P.card; b.Text = ""
        b.BorderSizePixel = 0; b.AutoButtonColor = false; b.Parent = sidebar
        local c = Instance.new("UICorner"); c.CornerRadius = UDim.new(0,6); c.Parent = b
        local stroke = Instance.new("UIStroke"); stroke.Color = P.border; stroke.Thickness = 1; stroke.Parent = b
        local ind = Instance.new("Frame")
        ind.Size = UDim2.new(0,3,0.6,0); ind.Position = UDim2.new(0,0,0.2,0)
        ind.BackgroundColor3 = P.accent; ind.BorderSizePixel = 0; ind.Visible = false; ind.Parent = b
        local ic = Instance.new("UICorner"); ic.CornerRadius = UDim.new(0,2); ic.Parent = ind
        local txt = Instance.new("TextLabel")
        txt.Size = UDim2.new(1,-16,1,0); txt.Position = UDim2.new(0,12,0,0)
        txt.BackgroundTransparency = 1; txt.Text = nome; txt.TextColor3 = P.textDim
        txt.Font = Enum.Font.GothamMedium; txt.TextSize = 11; txt.TextXAlignment = Enum.TextXAlignment.Left; txt.Parent = b
        botoes[nome] = {btn=b, ind=ind, txt=txt, stroke=stroke}
        b.MouseEnter:Connect(function() if b.BackgroundColor3~=P.cardActive then b.BackgroundColor3=P.cardHover end end)
        b.MouseLeave:Connect(function() if b.BackgroundColor3~=P.cardActive then b.BackgroundColor3=P.card end end)
        b.MouseButton1Click:Connect(function()
            for n,s in pairs(abas) do s.Visible = (n==nome) end
            for n,d in pairs(botoes) do
                if n==nome then
                    d.btn.BackgroundColor3=P.cardActive; d.ind.Visible=true
                    d.txt.TextColor3=P.text; d.stroke.Color=P.accent
                else
                    d.btn.BackgroundColor3=P.card; d.ind.Visible=false
                    d.txt.TextColor3=P.textDim; d.stroke.Color=P.border
                end
            end
        end)
    end
    botaoAba("ESP"); botaoAba("VIDA"); botaoAba("MARCADORES"); botaoAba("SKELETON")
    botaoAba("INDICADORES"); botaoAba("PERSONALIZACAO"); botaoAba("RGB")
    botaoAba("AIM"); botaoAba("MOVIMENTO"); botaoAba("MENU")
    abas["ESP"].Visible = true
    botoes["ESP"].btn.BackgroundColor3 = P.cardActive
    botoes["ESP"].ind.Visible = true
    botoes["ESP"].txt.TextColor3 = P.text
    botoes["ESP"].stroke.Color = P.accent
end)
