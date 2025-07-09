-- Auto Farm Blox Fruits (NPC Attack) - Exemplo Educacional
local player = game.Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local humanoid = character:WaitForChild("Humanoid")

local function getNearestEnemy()
    local shortestDistance = math.huge
    local nearestEnemy = nil
    for _, v in pairs(workspace.Enemies:GetChildren()) do
        if v:FindFirstChild("HumanoidRootPart") and v:FindFirstChild("Humanoid") and v.Humanoid.Health > 0 then
            local dist = (character.HumanoidRootPart.Position - v.HumanoidRootPart.Position).magnitude
            if dist < shortestDistance then
                shortestDistance = dist
                nearestEnemy = v
            end
        end
    end
    return nearestEnemy
end

while wait(0.5) do
    local enemy = getNearestEnemy()
    if enemy then
        character.HumanoidRootPart.CFrame = enemy.HumanoidRootPart.CFrame * CFrame.new(0,0,2)
        game:GetService("VirtualUser"):Button1Down(Vector2.new())
        wait(0.2)
        game:GetService("VirtualUser"):Button1Up(Vector2.new())
    end
end
