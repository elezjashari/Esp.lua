# Esp.lua
local p=game:GetService("Players")
local lp=p.LocalPlayer
local function e(c,pl)
    if c:FindFirstChild("ESP_Highlight")then return end
    local h=Instance.new("Highlight")
    h.Name="ESP_Highlight"
    h.Adornee=c
    h.Parent=c
    if pl.Team then h.FillColor=pl.TeamColor.Color else h.FillColor=Color3.new(1,1,0)end
    h.FillTransparency=0.5
    h.OutlineTransparency=0
    local head=c:FindFirstChild("Head")
    if head then
        local b=Instance.new("BillboardGui")
        b.Name="ESP_Dot"
        b.Size=UDim2.new(0,6,0,6)
        b.Adornee=head
        b.AlwaysOnTop=true
        b.Parent=head
        local d=Instance.new("Frame")
        d.Size=UDim2.new(1,0,1,0)
        d.BackgroundColor3=h.FillColor
        d.BorderSizePixel=0
        d.Parent=b
    end
end
for _,pl in pairs(p:GetPlayers())do
    if pl~=lp then
        pl.CharacterAdded:Connect(function(c)c:WaitForChild("HumanoidRootPart")e(c,pl)end)
        if pl.Character then e(pl.Character,pl)end
    end
end
p.PlayerAdded:Connect(function(pl)
    if pl~=lp then
        pl.CharacterAdded:Connect(function(c)c:WaitForChild("HumanoidRootPart")e(c,pl)end)
    end
end)
