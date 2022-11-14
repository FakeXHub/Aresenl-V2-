local Library = loadstring(Game:HttpGet("https://raw.githubusercontent.com/bloodball/-back-ups-for-libs/main/wizard"))()

local PhantomForcesWindow = Library:NewWindow("POWER X HUB V1")
local KillingCheats = PhantomForcesWindow:NewSection("Combat")

KillingCheats:CreateButton("Silent Aim", function()
game:GetService("StarterGui"):SetCore("SendNotification",{
Title = "Silent Aim Open!!",
Text = "", 
Duration = 5
})
local CurrentCamera = workspace.CurrentCamera
local Players = game.Players
local LocalPlayer = Players.LocalPlayer
local Mouse = LocalPlayer:GetMouse()
function ClosestPlayer()
    local MaxDist, Closest = math.huge
    for I,V in pairs(Players.GetPlayers(Players)) do
        if V == LocalPlayer then continue end
        if V.Team == LocalPlayer then continue end
        if not V.Character then continue end
        local Head = V.Character.FindFirstChild(V.Character, "Head")
        if not Head then continue end
        local Pos, Vis = CurrentCamera.WorldToScreenPoint(CurrentCamera, Head.Position)
        if not Vis then continue end
        local MousePos, TheirPos = Vector2.new(workspace.CurrentCamera.ViewportSize.X / 2, workspace.CurrentCamera.ViewportSize.Y / 2), Vector2.new(Pos.X, Pos.Y)
        local Dist = (TheirPos - MousePos).Magnitude
        if Dist < MaxDist then
            MaxDist = Dist
            Closest = V
        end
    end
    return Closest
end
local MT = getrawmetatable(game)
local OldNC = MT.__namecall
local OldIDX = MT.__index
setreadonly(MT, false)
MT.__namecall = newcclosure(function(self, ...)
    local Args, Method = {...}, getnamecallmethod()
    if Method == "FindPartOnRayWithIgnoreList" and not checkcaller() then
        local CP = ClosestPlayer()
        if CP and CP.Character and CP.Character.FindFirstChild(CP.Character, "Head") then
            Args[1] = Ray.new(CurrentCamera.CFrame.Position, (CP.Character.Head.Position - CurrentCamera.CFrame.Position).Unit * 1000)
            return OldNC(self, unpack(Args))
        end
    end
    return OldNC(self, ...)
end)
MT.__index = newcclosure(function(self, K)
    if K == "Clips" then
        return workspace.Map
    end
    return OldIDX(self, K)
end)
setreadonly(MT, true)
end)
KillingCheats:CreateToggle("Semi wallbang", function(wallbang)
_G.Enable = wallbang
local MT = getrawmetatable(game)
local OldIndex = MT.__index
setreadonly(MT, false)
MT.__index = newcclosure(function(A, B)
    if B == "Clips" then
        if _G.Enable then
            return workspace.Map
        end
    end
    return OldIndex(A, B)
end)
game:GetService("UserInputService").InputBegan:Connect(function(Key, _)
    if not _ and Key.KeyCode == Enum.KeyCode.T then
        _G.Enable = not _G.Enable
    end
end)
end)
KillingCheats:CreateToggle("Aimbot", function(aimbot)
local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local UserInputService = game:GetService("UserInputService")
local GuiService = game:GetService("GuiService")
local LocalPlayer = Players.LocalPlayer
local Mouse = LocalPlayer:GetMouse()
local Camera = workspace.CurrentCamera
local sc = Vector2.new(Camera.ViewportSize.X / 2, Camera.ViewportSize.Y / 2)
local Down = true
local Inset = GuiService:GetGuiInset()
--// Options \\--
getgenv().Options = {
    Enabled = aimbot,
    TeamCheck = true,
    Triggerbot = true,
    Smoothness = true,
    AimPart = "Head",
    FOV = 150
}
--// Functions \\--
local gc = function()
	local nearest = math.huge
	local nearplr
	for i, v in pairs(game:GetService("Players"):GetPlayers()) do
		if v ~= game:GetService("Players").LocalPlayer and v.Character and v.Character:FindFirstChild(Options.AimPart) then
			if Options.TeamCheck then
				if game:GetService("Players").LocalPlayer.Team ~= v.Team then
                    local pos = Camera:WorldToScreenPoint(v.Character[Options.AimPart].Position)
                    local diff = math.sqrt((pos.X - sc.X) ^ 2 + (pos.Y + Inset.Y - sc.Y) ^ 2)
                    if diff < nearest and diff < Options.FOV then
                        nearest = diff
                        nearplr = v
                    end
                end
			else
				local pos = Camera:WorldToScreenPoint(v.Character[Options.AimPart].Position)
				local diff = math.sqrt((pos.X - sc.X) ^ 2 + (pos.Y + Inset.Y - sc.Y) ^ 2)
				if diff < nearest and diff < Options.FOV then
					nearest = diff
					nearplr = v
                end
			end
		end
	end
	return nearplr
end -- google chrome made this but i modified it for it to use teamcheck
function Circle()
    local circ = Drawing.new('Circle')
    circ.Transparency = 1
    circ.Thickness = 1.5
    circ.Visible = true
    circ.Color = Color3.fromRGB(255,255,255)
	circ.Filled = false
	circ.NumSides = 150
    circ.Radius = Options.FOV
    return circ
end
curc = Circle()
--// Main \\--
UserInputService.InputBegan:Connect(function( input )
    if input.UserInputType == Enum.UserInputType.MouseButton2 then
        Down = true
	end
end)
UserInputService.InputEnded:Connect(function( input )
    if input.UserInputType == Enum.UserInputType.MouseButton2 then
        Down = false
    end
end)
RunService.RenderStepped:Connect(function( ... )
    if Options.Enabled then
        if Down then
            if gc() ~= nil and gc().Character:FindFirstChild(Options.AimPart) then
                if Options.Smoothness then
                    pcall(function( ... )
                        local Info = TweenInfo.new(0.05,Enum.EasingStyle.Linear,Enum.EasingDirection.Out)
                        game:GetService("TweenService"):Create(Camera,Info,{
                            CFrame = CFrame.new(Camera.CFrame.p,gc().Character[Options.AimPart].CFrame.p)
                        }):Play()
                    end)
                else
                    pcall(function()
                        Camera.CFrame = CFrame.new(Camera.CFrame.p,gc().Character[Options.AimPart].CFrame.p)
                    end)
                end
            end
        end
        curc.Visible = false
        curc.Position = Vector2.new(Mouse.X, Mouse.Y+Inset.Y)
    else
        -- do nothing except remove the fov
        curc.Visible = false
    end
end)
end)

KillingCheats:CreateButton("Fov Circle", function()
game:GetService("StarterGui"):SetCore("SendNotification",{
Title = "Fov Circle",
Text = "Fov Circle Open!!", 
Duration = 5
})
local dwCamera = workspace.CurrentCamera
local dwRunService = game:GetService("RunService")
local dwUIS = game:GetService("UserInputService")
local dwEntities = game:GetService("Players")
local dwLocalPlayer = dwEntities.LocalPlayer
local dwMouse = dwLocalPlayer:GetMouse()
local settings = {
    Aimbot_Draw_FOV = true,
    Aimbot_FOV_Radius = 150,
    Aimbot_FOV_Color = Color3.fromRGB(255,255,255)
}
local fovcircle = Drawing.new("Circle")
fovcircle.Visible = settings.Aimbot_Draw_FOV
fovcircle.Radius = settings.Aimbot_FOV_Radius
fovcircle.Color = settings.Aimbot_FOV_Color
fovcircle.Thickness = 5
fovcircle.Filled = false
fovcircle.Transparency = 1
fovcircle.Position = Vector2.new(dwCamera.ViewportSize.X / 2, dwCamera.ViewportSize.Y / 2)
dwUIS.InputBegan:Connect(function(i)
    if i.UserInputType == Enum.UserInputType.MouseButton2 then
        settings.Aiming = false
    end
end)
end)

local KillingCheats = PhantomForcesWindow:NewSection("Visuals")
KillingCheats:CreateButton("Esp box", function()
game:GetService("StarterGui"):SetCore("SendNotification",{
Title = "Esp box ,
Text = "Esp box Open!!", 
Duration = 5
})
-- settings
local settings = {
   defaultcolor = Color3.fromRGB(255,0,0),
   teamcheck = false,
   teamcolor = true
};
-- services
local runService = game:GetService("RunService");
local players = game:GetService("Players");
-- variables
local localPlayer = players.LocalPlayer;
local camera = workspace.CurrentCamera;
-- functions
local newVector2, newColor3, newDrawing = Vector2.new, Color3.new, Drawing.new;
local tan, rad = math.tan, math.rad;
local round = function(...) local a = {}; for i,v in next, table.pack(...) do a[i] = math.round(v); end return unpack(a); end;
local wtvp = function(...) local a, b = camera.WorldToViewportPoint(camera, ...) return newVector2(a.X, a.Y), b, a.Z end;
local espCache = {};
local function createEsp(player)
   local drawings = {};
   
   drawings.box = newDrawing("Square");
   drawings.box.Thickness = 5;
   drawings.box.Filled = false;
   drawings.box.Color = settings.defaultcolor;
   drawings.box.Visible = false;
   drawings.box.ZIndex = 2;
   drawings.boxoutline = newDrawing("Square");
   drawings.boxoutline.Thickness = 3;
   drawings.boxoutline.Filled = false;
   drawings.boxoutline.Color = newColor3();
   drawings.boxoutline.Visible = false;
   drawings.boxoutline.ZIndex = 1;
   espCache[player] = drawings;
end
local function removeEsp(player)
   if rawget(espCache, player) then
       for _, drawing in next, espCache[player] do
           drawing:Remove();
       end
       espCache[player] = nil;
   end
end
local function updateEsp(player, esp)
   local character = player and player.Character;
   if character then
       local cframe = character:GetModelCFrame();
       local position, visible, depth = wtvp(cframe.Position);
       esp.box.Visible = visible;
       esp.boxoutline.Visible = visible;
       if cframe and visible then
           local scaleFactor = 1 / (depth * tan(rad(camera.FieldOfView / 2)) * 2) * 1000;
           local width, height = round(4 * scaleFactor, 5 * scaleFactor);
           local x, y = round(position.X, position.Y);
           esp.box.Size = newVector2(width, height);
           esp.box.Position = newVector2(round(x - width / 2, y - height / 2));
           esp.box.Color = settings.teamcolor and player.TeamColor.Color or settings.defaultcolor;
           esp.boxoutline.Size = esp.box.Size;
           esp.boxoutline.Position = esp.box.Position;
       end
   else
       esp.box.Visible = false;
       esp.boxoutline.Visible = false;
   end
end
-- main
for _, player in next, players:GetPlayers() do
   if player ~= localPlayer then
       createEsp(player);
   end
end
players.PlayerAdded:Connect(function(player)
   createEsp(player);
end);
players.PlayerRemoving:Connect(function(player)
   removeEsp(player);
end)
runService:BindToRenderStep("esp", Enum.RenderPriority.Camera.Value, function()
   for player, drawings in next, espCache do
       if settings.teamcheck and player.Team == localPlayer.Team then
           continue;
       end
       if drawings and player ~= localPlayer then
           updateEsp(player, drawings);
       end
   end
end)
end)

KillingCheats:CreateButton("Esp Name", function()
while wait() do
     pcall(function()
       for i,v in pairs(game.Players:GetChildren()) do
            if not v.Character.Head:FindFirstChild("ESP") then
                local BillboardGui = Instance.new("BillboardGui")
                local TextLabel = Instance.new("TextLabel")
                BillboardGui.Parent = v.Character.Head
                BillboardGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
                BillboardGui.Active = true
                BillboardGui.Name = "ESP"
                BillboardGui.AlwaysOnTop = true
                BillboardGui.LightInfluence = 1.000
                BillboardGui.Size = UDim2.new(0, 40, 0, 50)
                BillboardGui.StudsOffset = Vector3.new(0, 2.5, 0)
                TextLabel.Parent = BillboardGui
                TextLabel.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
                TextLabel.BackgroundTransparency = 1.000
                TextLabel.Size = UDim2.new(0, 40, 0, 50)
                TextLabel.Font = Enum.Font.GothamBold
                TextLabel.Text = v.Name
                TextLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
                TextLabel.TextScaled = true
                TextLabel.TextSize = 6.000
                TextLabel.TextStrokeTransparency = 0.000
                TextLabel.TextWrapped = true
            end
        end
    end) 
end
end)

KillingCheats:CreateButton("Tracers", function()
game:GetService("StarterGui"):SetCore("SendNotification",{
Title = "Tracers",
Text = "Tracers Open!!", 
Duration = 5
})
local lplr = game.Players.LocalPlayer
local camera = game:GetService("Workspace").CurrentCamera
local CurrentCamera = workspace.CurrentCamera
local worldToViewportPoint = CurrentCamera.worldToViewportPoint
_G.TeamCheck = true-- Use True or False to toggle TeamCheck
for i,v in pairs(game.Players:GetChildren()) do
    local Tracer = Drawing.new("Line")
    Tracer.Visible = false
    Tracer.Color = Color3.new(1,1,1)
    Tracer.Thickness = 5
    Tracer.Transparency = 1
    function lineesp()
        game:GetService("RunService").RenderStepped:Connect(function()
            if v.Character ~= nil and v.Character:FindFirstChild("Humanoid") ~= nil and v.Character:FindFirstChild("HumanoidRootPart") ~= nil and v ~= lplr and v.Character.Humanoid.Health > 0 then
                local Vector, OnScreen = camera:worldToViewportPoint(v.Character.HumanoidRootPart.Position)
                if OnScreen then
                    Tracer.From = Vector2.new(camera.ViewportSize.X / 2, camera.ViewportSize.Y / 1)
                    Tracer.To = Vector2.new(Vector.X, Vector.Y)
                    if _G.TeamCheck and v.TeamColor == lplr.TeamColor then
                        --//Teammates
                        Tracer.Visible = true
                    else
                        --//Enemies
                        Tracer.Visible = true
                    end
                else
                    Tracer.Visible = false
                end
            else
                Tracer.Visible = false
            end
        end)
    end
    coroutine.wrap(lineesp)()
end
game.Players.PlayerAdded:Connect(function(v)
    local Tracer = Drawing.new("Line")
    Tracer.Visible = false
    Tracer.Color = Color3.new(1,1,1)
    Tracer.Thickness = 1
    Tracer.Transparency = 1
    function lineesp()
        game:GetService("RunService").RenderStepped:Connect(function()
            if v.Character ~= nil and v.Character:FindFirstChild("Humanoid") ~= nil and v.Character:FindFirstChild("HumanoidRootPart") ~= nil and v ~= lplr and v.Character.Humanoid.Health > 0 then
                local Vector, OnScreen = camera:worldToViewportPoint(v.Character.HumanoidRootPart.Position)
                if OnScreen then
                    Tracer.From = Vector2.new(camera.ViewportSize.X / 2, camera.ViewportSize.Y / 1)
                    Tracer.To = Vector2.new(Vector.X, Vector.Y)
                    if _G.TeamCheck and v.TeamColor == lplr.TeamColor then
                        --//Teammates
                        Tracer.Visible = false
                    else
                        --//Enemies
                        Tracer.Visible = true
                    end
                else
                    Tracer.Visible = false
                end
            else
                Tracer.Visible = false
            end
        end)
    end
    coroutine.wrap(lineesp)()
end)
end)

local KillingCheats = PhantomForcesWindow:NewSection("Gun Mods")
KillingCheats:CreateButton("Fast Click", function()
game:GetService("StarterGui"):SetCore("SendNotification",{
Title = "Fast Click",
Text = "Fast Click Open!!", 
Duration = 5
})
local replicationstorage = game.ReplicatedStorage
for i, v in pairs(replicationstorage.Weapons:GetDescendants()) do
   if v.Name == "Auto" then
       v.Value = true
   end
   if v.Name == "RecoilControl" then
       v.Value = 0
   end
   if v.Name == "MaxSpread" then
       v.Value = 0
   end
   if v.Name == "ReloadTime" then
      v.Value = 0
   end
   if v.Name == "FireRate" then
       v.Value = 0.05
   end
   if v.Name == "Crit" then
       v.Value = 20
   end
end
end)
KillingCheats:CreateButton("RGB gun", function()
game:GetService("StarterGui"):SetCore("SendNotification",{
Title = "RGB Gun ",
Text = "RBG Gun Open!!", 
Duration = 5
})
local c = 1 function zigzag(X)  return math.acos(math.cos(X * math.pi)) / math.pi end game:GetService("RunService").RenderStepped:Connect(function()  if game.Workspace.Camera:FindFirstChild('Arms') then   for i,v in pairs(game.Workspace.Camera.Arms:GetDescendants()) do    if v.ClassName == 'MeshPart' then      v.Color = Color3.fromHSV(zigzag(c),1,1)     c = c + .0001    end   end  end end)
end)
KillingCheats:CreateButton("Infinite ammo", function()
    while wait() do
        game:GetService("Players").LocalPlayer.PlayerGui.GUI.Client.Variables.ammocount.Value = 999
        game:GetService("Players").LocalPlayer.PlayerGui.GUI.Client.Variables.ammocount2.Value = 999
    end
end)
local KillingCheats = PhantomForcesWindow:NewSection("Player")
KillingCheats:CreateDropdown("Speed", {"15", "30", "50", "70", "100"}, 2, function(speed)
while true do
wait()
game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = speed
end
end)
