# Rebuilding the final version of the TrollAdminGUI script as a standalone Lua file for loadstring use
final_gui_script = """
-- Troll Admin GUI Script (Loadstring Version)
if game:GetService("RunService"):IsServer() then return end

local Players = game:GetService("Players")
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local localPlayer = Players.LocalPlayer

-- GUI Setup
local screenGui = Instance.new("ScreenGui")
screenGui.Name = "TrollPanel"
screenGui.ResetOnSpawn = false
screenGui.Parent = localPlayer:WaitForChild("PlayerGui")

local frame = Instance.new("Frame")
frame.Size = UDim2.new(0, 300, 0, 500)
frame.Position = UDim2.new(0, 100, 0, 100)
frame.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
frame.Active = true
frame.Draggable = true
frame.Parent = screenGui

local uilist = Instance.new("UIListLayout")
uilist.Padding = UDim.new(0, 6)
uilist.Parent = frame

local targetBox = Instance.new("TextBox")
targetBox.PlaceholderText = "Enter player name..."
targetBox.Size = UDim2.new(1, -10, 0, 30)
targetBox.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
targetBox.TextColor3 = Color3.fromRGB(255, 255, 255)
targetBox.Parent = frame

local function createButton(text, remoteName)
    local button = Instance.new("TextButton")
    button.Text = text
    button.Size = UDim2.new(1, -10, 0, 30)
    button.BackgroundColor3 = Color3.fromRGB(70, 70, 70)
    button.TextColor3 = Color3.new(1,1,1)
    button.MouseButton1Click:Connect(function()
        local input = targetBox.Text:lower()
        for _, p in ipairs(Players:GetPlayers()) do
            if p.Name:lower():sub(1, #input) == input then
                local remote = ReplicatedStorage:FindFirstChild(remoteName)
                if remote then
                    remote:FireServer(p)
                end
                break
            end
        end
    end)
    button.Parent = frame
end

-- Button List
createButton("Fly", "FlyPlayer")
createButton("Fling", "FlingPlayer")
createButton("Kick", "KickPlayer")
createButton("Ban", "BanPlayer")
createButton("Bring", "BringPlayer")
createButton("Go To", "GoToPlayer")
createButton("Explode", "ExplodePlayer")
createButton("Spin", "SpinPlayer")
createButton("Float", "FloatPlayer")
createButton("Jumpscare", "JumpscarePlayer")
"""

# Save the Lua file
lua_file_path = Path("/mnt/data/TrollAdminGUI.lua")
lua_file_path.write_text(final_gui_script)

lua_file_path.name
