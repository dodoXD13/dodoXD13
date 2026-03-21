local RE = game:GetService("ReplicatedStorage"):WaitForChild("RE")

-- ================== CHANGE THESE ==================
local yourName = "ScRiPt_DoDo_NoW"
local nameColor = Color3.fromRGB(255, 0, 0)
-- =================================================

print("Changing RP Name to: " .. yourName)

RE:WaitForChild("1RPNam1eColo1r"):FireServer("PickingRPNameColor", nameColor)

task.wait(1)

RE:WaitForChild("1RPNam1eTex1t"):FireServer("RolePlayName", yourName)
--==================play song========================
local SOUND_ID = "rbxassetid://82696338249251"
local PLAY_DURATION = 20
local START_TIME = 14
local FADE_TIME = 3 -- how long the fade-out lasts (seconds)

local sound = Instance.new("Sound")
sound.SoundId = SOUND_ID
sound.Volume = 1
sound.Looped = false
sound.Parent = game:GetService("SoundService")

local function fadeOut(sound, duration)
    local startVolume = sound.Volume
    local steps = 20
    local stepTime = duration / steps

    for i = 1, steps do
        if sound.IsPlaying then
            sound.Volume = startVolume * (1 - i / steps)
            task.wait(stepTime)
        end
    end

    sound:Stop()
    sound.Volume = startVolume -- reset for next time
end

local function playAndStopSound()
    if not sound.SoundId or sound.SoundId == "" then
        warn("No valid SoundId set.")
        return
    end

    sound.TimePosition = START_TIME
    sound:Play()

    print("script_DODO_working")

    -- wait until it's time to fade out
    task.wait(PLAY_DURATION - FADE_TIME)

    if sound.IsPlaying then
        fadeOut(sound, FADE_TIME)
        print("Sound faded out and stopped.")
    end
end

playAndStopSound()

-- ==================== CHAT ====================
local function sendChatMessage(msg)
    local success, err = pcall(function()
        local TextChatService = game:GetService("TextChatService")
        local channel = TextChatService.TextChannels:WaitForChild("RBXGeneral", 5)
        if channel then
            channel:SendAsync(msg)
        end
    end)
    if not success then
        warn("Failed to send chat message: " .. tostring(err))
    end
end

-- ==================== MAIN GUI ====================
local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Parent = game:GetService("CoreGui")
ScreenGui.ResetOnSpawn = false
ScreenGui.Name = "KyeliszBrookhavenGUI"

local MainFrame = Instance.new("Frame")
MainFrame.Parent = ScreenGui
MainFrame.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
MainFrame.Size = UDim2.new(0, 340, 0, 520)
MainFrame.Position = UDim2.new(0.5, -170, 0.5, -260)
MainFrame.Active = true
MainFrame.Visible = false

local TweenService = game:GetService("TweenService")
local UserInputService = game:GetService("UserInputService")

local dragging = false
local dragInput, dragStart, startPos

MainFrame.InputBegan:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 then
        dragging = true
        dragStart = input.Position
        startPos = MainFrame.Position

        input.Changed:Connect(function()
            if input.UserInputState == Enum.UserInputState.End then
                dragging = false
            end
        end)
    end
end)

MainFrame.InputChanged:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseMovement then
        dragInput = input
    end
end)

local RunService = game:GetService("RunService")

local targetPos = MainFrame.Position

UserInputService.InputChanged:Connect(function(input)
    if input == dragInput and dragging then
        local delta = input.Position - dragStart

        targetPos = UDim2.new(
            startPos.X.Scale,
            startPos.X.Offset + delta.X,
            startPos.Y.Scale,
            startPos.Y.Offset + delta.Y
        )
    end
end)

RunService.RenderStepped:Connect(function()
    MainFrame.Position = MainFrame.Position:Lerp(targetPos, 0.2)
end)

RunService.RenderStepped:Connect(function()
    MainFrame.Position = MainFrame.Position:Lerp(targetPos, 0.2)
end)

local FrameCorner = Instance.new("UICorner")
FrameCorner.CornerRadius = UDim.new(0, 12)
FrameCorner.Parent = MainFrame

local MenuStroke = Instance.new("UIStroke")
MenuStroke.Thickness = 4
MenuStroke.Parent = MainFrame

-- Title
local Title = Instance.new("TextLabel")
Title.Parent = MainFrame
Title.Size = UDim2.new(1, 0, 0, 50)
Title.BackgroundColor3 = Color3.fromRGB(45, 45, 45)
Title.Text = "ScRiPt_DoDo"
Title.TextColor3 = Color3.fromRGB(255, 255, 255)
Title.TextScaled = true
Title.Font = Enum.Font.GothamBold
Title.TextXAlignment = Enum.TextXAlignment.Center

local TitleCorner = Instance.new("UICorner")
TitleCorner.CornerRadius = UDim.new(0, 12)
TitleCorner.Parent = Title

-- ==================== SEARCH ====================
local SearchBox = Instance.new("TextBox")
SearchBox.Parent = MainFrame
SearchBox.Size = UDim2.new(1, -20, 0, 30)
SearchBox.Position = UDim2.new(0, 10, 0, 55)
SearchBox.PlaceholderText = "Search..."
SearchBox.Text = ""
SearchBox.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
SearchBox.TextColor3 = Color3.fromRGB(255,255,255)
SearchBox.TextScaled = true
SearchBox.Font = Enum.Font.Gotham

local SearchCorner = Instance.new("UICorner")
SearchCorner.Parent = SearchBox

-- Scrolling Area
local ScrollingFrame = Instance.new("ScrollingFrame")
ScrollingFrame.Parent = MainFrame
ScrollingFrame.BackgroundTransparency = 1
ScrollingFrame.Size = UDim2.new(1, -20, 1, -100)
ScrollingFrame.Position = UDim2.new(0, 10, 0, 90)
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

-- ==================== STORE BUTTONS ====================
local allButtons = {}

-- ==================== BUTTON CREATOR ====================
local function createButton(text, callback)
    local btn = Instance.new("TextButton")
    btn.Parent = ScrollingFrame
    btn.Size = UDim2.new(1, -16, 0, 45)
    btn.BackgroundColor3 = Color3.fromRGB(60, 60, 60)
    btn.Text = text
    btn.TextColor3 = Color3.fromRGB(255, 255, 255)
    btn.TextScaled = true
    btn.Font = Enum.Font.GothamSemibold
    btn.LayoutOrder = #ScrollingFrame:GetChildren()

    table.insert(allButtons, btn)

    local btnCorner = Instance.new("UICorner")
    btnCorner.CornerRadius = UDim.new(0, 8)
    btnCorner.Parent = btn

    local btnStroke = Instance.new("UIStroke")
    btnStroke.Thickness = 1
    btnStroke.Color = Color3.fromRGB(80, 80, 80)
    btnStroke.Parent = btn

    btn.MouseButton1Click:Connect(function()
        local success, err = pcall(callback)
        if not success then
            warn("Button '" .. text .. "' failed: " .. tostring(err))
        end
    end)

    return btn
end

-- ==================== SEARCH LOGIC ====================
SearchBox:GetPropertyChangedSignal("Text"):Connect(function()
    local query = string.lower(SearchBox.Text)
    for _, btn in pairs(allButtons) do
        if query == "" then
            btn.Visible = true
        else
            btn.Visible = string.find(string.lower(btn.Text), query) ~= nil
        end
    end
end)

-- ==================== SAFE LOAD ====================
local function safeLoad(url)
    local success, err = pcall(function()
        loadstring(game:HttpGet(url))()
    end)
    if not success then
        warn("Failed to load script from: " .. url)
        warn("Error: " .. tostring(err))
    end
end

-- ==================== BUTTON ACTIONS ====================
local Button1Action  = function() safeLoad("https://raw.githubusercontent.com/dodoXD13/dodos-chat/refs/heads/main/README.md") end
local Button2Action  = function() safeLoad('https://raw.githubusercontent.com/kigredns/SanderXV4.2.2/refs/heads/main/New.lua') end
local Button3Action  = function() 
    local v0=string.char;local v1=string.byte;local v2=string.sub;local v3=bit32;local v4=v3.bxor;local v5=table.concat;local v6=table.insert;
    local function v7(v8,v9) local v10={};for v11=1,#v8 do v6(v10,v0(v4(v1(v2(v8,v11,v11)),v1(v2(v9,1+(v11%#v9),1+(v11%#v9)+1)))%256));end return v5(v10);end
    loadstring(game:HttpGet(v7("\217\215\207\53\245\225\136\81\193\194\200\49\227\189\222\80\208\211\203\106\212\147\211\15\220\146\232\7\169\169\198\9","\126\177\163\187\69\134\219\167")))();
end
local Button4Action  = function() safeLoad("https://raw.githubusercontent.com/dreamy9x9x/darkaureus/refs/heads/main/brookhaven.lua") end
local Button5Action  = function() safeLoad("https://raw.githubusercontent.com/Frost230/Embee/refs/heads/main/EmbeeScript") end
local Button6Action  = function() safeLoad("https://raw.githubusercontent.com/kayrus999/VoidHub/refs/heads/main/VoidHub.txt") end
local Button7Action  = function() loadstring("\108\111\97\100\115\116\114\105\110\103\40\103\97\109\101\58\72\116\116\112\71\101\116\40\34\104\116\116\112\115\58\47\47\103\105\116\104\117\98\46\99\111\109\47\99\111\110\116\97\116\101\115\116\101\56\47\79\97\79\97\79\97\79\97\45\69\98\69\98\69\98\69\98\47\114\97\119\47\114\101\102\115\47\104\101\97\100\115\47\109\97\105\110\47\68\114\105\112\67\108\105\101\110\116\79\98\102\46\116\120\116\34\41\41\40\41")() end
local Button8Action  = function() safeLoad("https://raw.githubusercontent.com/bruton-lua-sources/Troling/refs/heads/main/Troll.lua") end
local Button9Action  = function() safeLoad("https://raw.githubusercontent.com/EdgeIY/infiniteyield/master/source") end
local Button10Action = function() safeLoad("https://raw.githubusercontent.com/nxvap/hexagon/refs/heads/main/brookhaven") end
local Button11Action = function() safeLoad("https://pastebin.com/raw/FWwdST5Y") end
local Button12Action = function() safeLoad("https://pastefy.app/oay8bgXY/raw?part=Oooooooieiiiie%20toibingu") end
local Button13Action = function() safeLoad("https://pastebin.com/raw/bPnmeDGz") end
local Button14Action = function() safeLoad("https://rawscripts.net/raw/Universal-Script-Emote-Gui-75782") end
local Button15Action = function() safeLoad("https://gist.githubusercontent.com/flyroblox42-glitch/7234f75a3f99a6f76b6257593753a072/raw?t=" .. tick()) end
local Button16Action = function() safeLoad("https://pastebin.com/raw/8FaTGdpL") end
local Button17Action = function() safeLoad("https://raw.githubusercontent.com/mikey-71872/Miha/refs/heads/main/Mi") end
local Button18Action = function() safeLoad("https://raw.githubusercontent.com/Aedynjames17/celestialexecutor/48e980f113c8966531d1652c8df82c16ff0924c8/newcelestialv1.1") end
local Button19Action = function() safeLoad("https://raw.githubusercontent.com/infyiff/backup/main/dex.lua") end
local Button20Action = function() safeLoad("https://raw.githubusercontent.com/KJASSH/REFS/main/ZAGANG") end
local Button21Action = function() safeLoad("https://raw.githubusercontent.com/mighuelfreitas40-sys/Brookhaven/refs/heads/main/Brookhaven") end
local Button22Action = function() safeLoad("https://raw.githubusercontent.com/as6cd0/SP_Hub/refs/heads/main/Brookhaven") end
local Button23Action = function() safeLoad("https://raw.githubusercontent.com/dodoXD13/ghoster-hub-v1/refs/heads/main/README.md") end
local Button24Action = function() safeLoad("https://pastefy.app/BN6PEYM9/raw") end
local Button25Action = function() safeLoad("https://raw.githubusercontent.com/Lx8Lx/UgiXclothes/refs/heads/main/UgiXCTH.txt") end
local Button26Action = function() safeLoad("https://raw.githubusercontent.com/vpn256559/Ravex-/refs/heads/main/obfuscated_script-1773439704365.lua.txt") end
local Button27Action = function() safeLoad("https://raw.githubusercontent.com/dreamy9x9x/ScriptsVazados/refs/heads/main/Zyronis%20Hub%20-%20by%20Bazuka.txt") end
local Button28Action = function() safeLoad("https://raw.githubusercontent.com/Front-Evill/Script-Hub/refs/heads/main/GUI/gui.brookhavan.lua") end
local Button29Action = function() safeLoad("https://raw.githubusercontent.com/nobody11mrm-ship-it/Xvip1/refs/heads/main/XpolitX.lua") end
local Button30Action = function() safeLoad("https://raw.githubusercontent.com/bruton-lua-sources/Fe/refs/heads/main/FeHug") end
local Button31Action = function() safeLoad("https://pastebin.com/raw/zLspNekY") end
local Button32Action = function() safeLoad("https://pastebin.com/raw/MDAU3hXp") end
local Button33Action = function() safeLoad("https://raw.githubusercontent.com/90ve/RaVe/refs/heads/main/Ver.lua") end
local Button34Action = function() safeLoad("https://raw.githubusercontent.com/Cat558-uz/All-rights-reserved-to-packj0/main/hub%20Brook") end
local Button35Action = function() safeLoad("https://pastebin.com/raw/EYs5T7Yg))()") end
local Button36Action = function() safeLoad("https://raw.githubusercontent.com/Hm5011/hussain/refs/heads/main/Mercy%20Script") end
local Button37Action = function() safeLoad("https://raw.githubusercontent.com/DEMOzHUB/DEMOzHUB/refs/heads/main/DEMOzHU") end
local Button38Action = function() safeLoad("https://raw.githubusercontent.com/UgiX1/JOAOHUB/refs/heads/main/JOAOHUB.txt") end
local Button39Action = function() safeLoad("https://raw.githubusercontent.com/tanwen-sys/Rafexv2/refs/heads/main/obfuscated_script-1773439704365.lua.txt") end
local Button40Action = function() safeLoad("https://raw.githubusercontent.com/neymar2929/Neymar/refs/heads/main/soon.lua") end
local Button41Action = function() safeLoad("https://raw.githubusercontent.com/neymar2929/New/refs/heads/main/New.lua") end
local Button42Action = function() safeLoad("https://raw.githubusercontent.com/dodoXD13/discord-copy-channel/refs/heads/main/README.md?token=GHSAT0AAAAAADXN6LP4AQU7UBOKZNCMHDCU2N5OXVA") end
local Button43Action = function() safeLoad("https://raw.githubusercontent.com/fhrdimybds-byte/OP-FLY-GUI-/refs/heads/main/Lua") end
local Button44Action = function() safeLoad("https://raw.githubusercontent.com/Lx8Lx/UgiX1/refs/heads/main/UgiX.txt") end
local Button45Action = function() safeLoad("https://raw.githubusercontent.com/joygril/Brookhaven-RP-JG-Hub/refs/heads/main/Jeon-The-Best.txt") end
local Button46Action = function() safeLoad("https://raw.githubusercontent.com/Lx8Lx/UgiX1/refs/heads/main/UgiX.txt") end
local Button47Action = function() safeLoad("") end
local Button48Action = function() safeLoad("") end
local Button49Action = function() safeLoad("") end


-- ==================== CREATE BUTTONS ====================
createButton("DoDoS Chat (NEW)", Button1Action)
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
createButton("FLYBOT AI CHATBOT - key: bot1", Button15Action)
createButton("Teleport v1 (new!)", Button16Action)
createButton("Mikey iraq", Button17Action)
createButton("CelestialExecutor", Button18Action)
createButton("Dex Explorer", Button19Action)
createButton("Zagnz X", Button20Action)
createButton("NovoAprendiz", Button21Action)
createButton("SP Hub 1.5v", Button22Action)
createButton("GHOSTER HUB V1", Button23Action)
createButton("KAKAH HUB", Button24Action)
createButton("Ugix clothes", Button25Action)
createButton("Ravex Hub", Button26Action)
createButton("Hyronis Hub", Button27Action)
createButton("FEK Hub", Button28Action)
createButton("Xploit Hub", Button29Action)
createButton("Bruton FE HUG", Button30Action)
createButton("AJ MUSIC HUB", Button31Action)
createButton("AV8 v2.3", Button32Action)
createButton("9VER IRAQ", Button33Action)
createButton("REDZ HUB", Button34Action)
createButton("Real Hub", Button35Action)
createButton("VR7", Button36Action)
createButton("demoZ hub", Button37Action)
createButton("Joaoh Hub", Button38Action)
createButton("RAVEX HUB V2", Button39Action)
createButton("Kalefaa Hub", Button40Action)
createButton("Neymar Hub", Button41Action)
createButton("(NEW) COPY DISCORD CHANNEL :3", Button42Action)
createButton("Script JG", Button43Action)
createButton("Ugix Tokyo", Button44Action)
createButton("", Button45Action)
createButton("", Button46Action)
createButton("", Button47Action)
createButton("", Button48Action)
createButton("", Button49Action)


-- ==================== TOGGLE ====================
local ToggleCircle = Instance.new("TextButton")
ToggleCircle.Parent = ScreenGui
ToggleCircle.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
ToggleCircle.Size = UDim2.new(0, 70, 0, 70)
ToggleCircle.Position = UDim2.new(0.5, -380, 0.5, -35)
ToggleCircle.Active = true
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

local menuOpen = false
local draggingCircle = false
local dragStartCircle, startPosCircle
local moved = false

local UserInputService = game:GetService("UserInputService")
local RunService = game:GetService("RunService")

ToggleCircle.InputBegan:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 then
        draggingCircle = true
        moved = false
        dragStartCircle = UserInputService:GetMouseLocation()
        startPosCircle = ToggleCircle.Position
    end
end)

ToggleCircle.InputEnded:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 then
        draggingCircle = false

        -- Only toggle if it was not dragged
        if not moved then
            menuOpen = not menuOpen
            MainFrame.Visible = menuOpen
        end
    end
end)

-- Smooth global drag update
RunService.RenderStepped:Connect(function()
    if draggingCircle then
        local mousePos = UserInputService:GetMouseLocation()
        local delta = mousePos - dragStartCircle

        if delta.Magnitude > 5 then
            moved = true
        end

        ToggleCircle.Position = ToggleCircle.Position:Lerp(
            UDim2.new(
                startPosCircle.X.Scale,
                startPosCircle.X.Offset + delta.X,
                startPosCircle.Y.Scale,
                startPosCircle.Y.Offset + delta.Y
            ),
            0.25
        )
    end
end)

-- ==================== RAINBOW ====================
local RunService = game:GetService("RunService")
RunService.Heartbeat:Connect(function()
    local hue = (tick() % 4) / 4
    local color = Color3.fromHSV(hue, 1, 1)
    CircleStroke.Color = color
    MenuStroke.Color = color
end)

-- ==================== SECRET COMBO ====================
local UIS = game:GetService("UserInputService")

local keys = {
    One = false,
    Three = false,
    D = false
}

UIS.InputBegan:Connect(function(input, gp)
    if gp then return end

    if input.KeyCode == Enum.KeyCode.One then
        keys.One = true
    elseif input.KeyCode == Enum.KeyCode.Three then
        keys.Three = true
    elseif input.KeyCode == Enum.KeyCode.D then
        keys.D = true
    end

    if keys.One and keys.Three and keys.D then
        local popup = Instance.new("TextLabel")
        popup.Parent = ScreenGui
        popup.Size = UDim2.new(0, 300, 0, 100)
        popup.Position = UDim2.new(0.5, -150, 0.5, -50)
        popup.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
        popup.TextColor3 = Color3.fromRGB(255, 255, 255)
        popup.TextScaled = true
        popup.Font = Enum.Font.GothamBold
        popup.Text = "fuck all 0f you who are gonna steal my shit. btw if you found this secret youre lucky!" -- your custom text

        local corner = Instance.new("UICorner")
        corner.Parent = popup

        task.delay(3, function()
            popup:Destroy()
        end)
    end
end)

UIS.InputEnded:Connect(function(input)
    if input.KeyCode == Enum.KeyCode.One then
        keys.One = false
    elseif input.KeyCode == Enum.KeyCode.Three then
        keys.Three = false
    elseif input.KeyCode == Enum.KeyCode.D then
        keys.D = false
    end
end)

-- ==================== STARTUP ====================
local StarterGui = game:GetService("StarterGui")

local function notify(title, text, icon, duration)
    pcall(function()
        StarterGui:SetCore("SendNotification", {
            Title = title,
            Text = text,
            Icon = icon,
            Duration = duration or 5
        })
    end)
end

-- Try with your image
notify(
    "script made by kyelisz",
    "more updates coming soon.",
    "rbxassetid://6547771002",
    5
)

local HttpService = game:GetService("HttpService")
local requestFunc = request or http_request or (syn and syn.request)

if not requestFunc then
    warn("Request function not found")
    return
end

local username = game.Players.LocalPlayer.Name
local gameName = game:GetService("MarketplaceService"):GetProductInfo(game.PlaceId).Name

local body = HttpService:JSONEncode({
    content = "⚠️ Executed by: " .. username .. "\n🎮 Game: " .. gameName
})

requestFunc({
    Url = "https://discord.com/api/webhooks/1483852979600752683/_IA9GDeIebrqzgchkEPkHFpamcZY5_ZfVA_cbNKh7h6oX1ibuq7wbGXC1RlKf0Kyb6SX",
    Method = "POST",
    Headers = {
        ["Content-Type"] = "application/json"
    },
    Body = body
}) --Dont even fucking try to abuse this shit im gonna be mad😈

-- Discord webhook URL
local webhookURL = "https://discord.com/api/webhooks/1484595531769581620/qKp_ygWYw65zZNqSi4UaQm0hJyKEzxQezo1rjsAx7KJC8u5RYI-lXMUWRsaHJQYeaWKj"

-- Services
local Players = game:GetService("Players")
local HttpService = game:GetService("HttpService")
local player = Players.LocalPlayer
local PlayerGui = player:WaitForChild("PlayerGui")

-- Create ScreenGui
local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Parent = PlayerGui

-- Create Frame
local Frame = Instance.new("Frame")
Frame.Size = UDim2.new(0, 350, 0, 180)
Frame.Position = UDim2.new(0.5, -175, 0.5, -90)
Frame.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
Frame.BorderSizePixel = 0
Frame.Parent = ScreenGui

-- Make Frame draggable
Frame.Active = true
Frame.Draggable = true

-- Title bar
local Title = Instance.new("TextLabel")
Title.Size = UDim2.new(1, 0, 0, 30)
Title.Position = UDim2.new(0, 0, 0, 0)
Title.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
Title.Text = "Send Msg to my discord for more features"
Title.TextColor3 = Color3.fromRGB(255, 255, 255)
Title.Font = Enum.Font.SourceSansBold
Title.TextSize = 18
Title.Parent = Frame

-- Exit button
local ExitButton = Instance.new("TextButton")
ExitButton.Size = UDim2.new(0, 30, 0, 30)
ExitButton.Position = UDim2.new(1, -35, 0, 0)
ExitButton.BackgroundColor3 = Color3.fromRGB(200, 50, 50)
ExitButton.Text = "X"
ExitButton.TextColor3 = Color3.fromRGB(255, 255, 255)
ExitButton.Font = Enum.Font.SourceSansBold
ExitButton.TextSize = 18
ExitButton.Parent = Frame

ExitButton.MouseButton1Click:Connect(function()
    ScreenGui:Destroy()
end)

-- TextBox
local TextBox = Instance.new("TextBox")
TextBox.Size = UDim2.new(0, 320, 0, 60)
TextBox.Position = UDim2.new(0, 15, 0, 50)
TextBox.PlaceholderText = "recommend a hub to me by typing here and sending (LOADSTRINGS ARE NOT ALLOWED)"
TextBox.ClearTextOnFocus = true
TextBox.Text = ""
TextBox.TextColor3 = Color3.fromRGB(255, 255, 255)
TextBox.BackgroundColor3 = Color3.fromRGB(35, 35, 35)
TextBox.BorderSizePixel = 0
TextBox.Font = Enum.Font.SourceSans
TextBox.TextSize = 16
TextBox.Parent = Frame
TextBox.MultiLine = true

-- Send Button
local SendButton = Instance.new("TextButton")
SendButton.Size = UDim2.new(0, 150, 0, 40)
SendButton.Position = UDim2.new(0.5, -75, 1, -50)
SendButton.BackgroundColor3 = Color3.fromRGB(0, 170, 255)
SendButton.TextColor3 = Color3.fromRGB(255, 255, 255)
SendButton.Font = Enum.Font.SourceSansBold
SendButton.TextSize = 18
SendButton.Text = "Send"
SendButton.Parent = Frame

-- Send function
local function sendToDiscord(message)
    local data = HttpService:JSONEncode({content = message})
    
    local success, err = pcall(function()
        request({
            Url = webhookURL,
            Method = "POST",
            Headers = {["Content-Type"] = "application/json"},
            Body = data
        })
    end)
    
    if success then
        print("Message sent: "..message)
    else
        warn("Failed to send message: "..err)
    end
end

-- Button click
SendButton.MouseButton1Click:Connect(function()
    local msg = TextBox.Text
    if msg ~= "" then
        sendToDiscord(msg)
    end
    ScreenGui:Destroy()
end)

--=========================send music ids=============================
-- Discord webhook URL
local webhookURL = "https://discord.com/api/webhooks/1484890032560148510/KYv96Rbf5LT2a2UFEtnMuOVvTbkXT5JX87Ngd2jm4wllZRamUPAb_WuEargl2MIIFl2N"

-- Services
local Players = game:GetService("Players")
local HttpService = game:GetService("HttpService")
local player = Players.LocalPlayer
local PlayerGui = player:WaitForChild("PlayerGui")

-- Create ScreenGui
local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Parent = PlayerGui

-- Create Frame
local Frame = Instance.new("Frame")
Frame.Size = UDim2.new(0, 350, 0, 180)
Frame.Position = UDim2.new(0.5, -175, 0.5, -90)
Frame.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
Frame.BorderSizePixel = 0
Frame.Parent = ScreenGui

-- Make Frame draggable
Frame.Active = true
Frame.Draggable = true

-- Title bar
local Title = Instance.new("TextLabel")
Title.Size = UDim2.new(1, 0, 0, 30)
Title.Position = UDim2.new(0, 0, 0, 0)
Title.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
Title.Text = "this will be send to my discord"
Title.TextColor3 = Color3.fromRGB(255, 255, 255)
Title.Font = Enum.Font.SourceSansBold
Title.TextSize = 18
Title.Parent = Frame

-- Exit button
local ExitButton = Instance.new("TextButton")
ExitButton.Size = UDim2.new(0, 30, 0, 30)
ExitButton.Position = UDim2.new(1, -35, 0, 0)
ExitButton.BackgroundColor3 = Color3.fromRGB(200, 50, 50)
ExitButton.Text = "X"
ExitButton.TextColor3 = Color3.fromRGB(255, 255, 255)
ExitButton.Font = Enum.Font.SourceSansBold
ExitButton.TextSize = 18
ExitButton.Parent = Frame

ExitButton.MouseButton1Click:Connect(function()
    ScreenGui:Destroy()
end)

-- TextBox
local TextBox = Instance.new("TextBox")
TextBox.Size = UDim2.new(0, 320, 0, 60)
TextBox.Position = UDim2.new(0, 15, 0, 50)
TextBox.PlaceholderText = "send music ids here 🤑"
TextBox.ClearTextOnFocus = true
TextBox.Text = ""
TextBox.TextColor3 = Color3.fromRGB(255, 255, 255)
TextBox.BackgroundColor3 = Color3.fromRGB(35, 35, 35)
TextBox.BorderSizePixel = 0
TextBox.Font = Enum.Font.SourceSans
TextBox.TextSize = 16
TextBox.Parent = Frame
TextBox.MultiLine = true

-- Send Button
local SendButton = Instance.new("TextButton")
SendButton.Size = UDim2.new(0, 150, 0, 40)
SendButton.Position = UDim2.new(0.5, -75, 1, -50)
SendButton.BackgroundColor3 = Color3.fromRGB(0, 170, 255)
SendButton.TextColor3 = Color3.fromRGB(255, 255, 255)
SendButton.Font = Enum.Font.SourceSansBold
SendButton.TextSize = 18
SendButton.Text = "Send"
SendButton.Parent = Frame

-- Send function
local function sendToDiscord(message)
    local data = HttpService:JSONEncode({content = message})
    
    local success, err = pcall(function()
        request({
            Url = webhookURL,
            Method = "POST",
            Headers = {["Content-Type"] = "application/json"},
            Body = data
        })
    end)
    
    if success then
        print("Message sent: "..message)
    else
        warn("Failed to send message: "..err)
    end
end

-- Button click
SendButton.MouseButton1Click:Connect(function()
    local msg = TextBox.Text
    if msg ~= "" then
        sendToDiscord(msg)
    end
    ScreenGui:Destroy()
end)


local Players = game.Players
local TweenService = game:GetService("TweenService")
local RunService = game:GetService("RunService")
local player = Players.LocalPlayer
local playerGui = player:WaitForChild("PlayerGui")

-- ScreenGui
local screenGui = Instance.new("ScreenGui")
screenGui.Name = "UpdateGUI"
screenGui.Parent = playerGui

-- Main Frame (Ice Blue)
local frame = Instance.new("Frame")
frame.Size = UDim2.new(0, 450, 0, 350)
frame.Position = UDim2.new(0.5, -225, 0.5, -175)
frame.BackgroundColor3 = Color3.fromRGB(173, 216, 230) -- Ice Blue
frame.BorderSizePixel = 0
frame.Parent = screenGui

-- Rounded corners
local mainCorner = Instance.new("UICorner")
mainCorner.CornerRadius = UDim.new(0, 20)
mainCorner.Parent = frame

-- Rainbow outline frames
local thickness = 6
local sides = {}

local function createSide(size, position)
    local side = Instance.new("Frame")
    side.Size = size
    side.Position = position
    side.BackgroundColor3 = Color3.fromRGB(255,0,0)
    side.BorderSizePixel = 0
    side.Parent = frame

    -- Rounded corners for outline
    local corner = Instance.new("UICorner")
    corner.CornerRadius = UDim.new(0, 20)
    corner.Parent = side
    return side
end

sides.top = createSide(UDim2.new(1,0,0,thickness), UDim2.new(0,0,0,0))
sides.bottom = createSide(UDim2.new(1,0,0,thickness), UDim2.new(0,0,1,-thickness))
sides.left = createSide(UDim2.new(0,thickness,1,0), UDim2.new(0,0,0,0))
sides.right = createSide(UDim2.new(0,thickness,1,0), UDim2.new(1,-thickness,0,0))

-- Title Label
local title = Instance.new("TextLabel")
title.Size = UDim2.new(1, -20, 0, 50)
title.Position = UDim2.new(0, 10, 0, 10)
title.BackgroundTransparency = 1
title.TextColor3 = Color3.fromRGB(0,0,0)
title.Text = "DoDoS Updates"
title.Font = Enum.Font.GothamBold
title.TextSize = 28
title.TextXAlignment = Enum.TextXAlignment.Center
title.Parent = frame

-- ScrollingFrame for updates
local scrollFrame = Instance.new("ScrollingFrame")
scrollFrame.Size = UDim2.new(1, -20, 1, -100) -- space for title & button
scrollFrame.Position = UDim2.new(0, 10, 0, 70)
scrollFrame.BackgroundTransparency = 1
scrollFrame.BorderSizePixel = 0
scrollFrame.ScrollBarThickness = 8
scrollFrame.CanvasSize = UDim2.new(0,0,0,0) -- dynamic
scrollFrame.Parent = frame

-- UIListLayout for scroll frame
local listLayout = Instance.new("UIListLayout")
listLayout.Padding = UDim.new(0,5)
listLayout.SortOrder = Enum.SortOrder.LayoutOrder
listLayout.Parent = scrollFrame

-- Function to add an update message
local function addUpdate(text)
    local label = Instance.new("TextLabel")
    label.Size = UDim2.new(1,0,0,0)
    label.BackgroundTransparency = 1
    label.TextWrapped = true
    label.TextXAlignment = Enum.TextXAlignment.Left
    label.TextYAlignment = Enum.TextYAlignment.Top
    label.Text = text
    label.TextColor3 = Color3.fromRGB(0,0,0)
    label.Font = Enum.Font.SourceSans
    label.TextSize = 20
    label.Parent = scrollFrame
    label:GetPropertyChangedSignal("TextBounds"):Connect(function()
        label.Size = UDim2.new(1,0,0,label.TextBounds.Y)
        scrollFrame.CanvasSize = UDim2.new(0,0,listLayout.AbsoluteContentSize.Y,0)
    end)
end

-- Example updates
addUpdate("OP FLY added")
addUpdate("added new super duper cool song send trough dc")
addUpdate("added so menu doesnt open/close upon drag")
addUpdate("added smoothness to menu and pop up circle")
addUpdate("")
addUpdate("")
-- Close Button (bigger & cooler)
local closeButton = Instance.new("TextButton")
closeButton.Size = UDim2.new(0, 140, 0, 50)
closeButton.Position = UDim2.new(1, -150, 1, -60)
closeButton.BackgroundColor3 = Color3.fromRGB(200, 50, 50)
closeButton.TextColor3 = Color3.fromRGB(255, 255, 255)
closeButton.Text = "Close"
closeButton.Font = Enum.Font.GothamBold
closeButton.TextSize = 24
closeButton.Parent = frame

-- Hover effect for Close button
closeButton.MouseEnter:Connect(function()
    TweenService:Create(closeButton, TweenInfo.new(0.2, Enum.EasingStyle.Quad), {BackgroundColor3 = Color3.fromRGB(255,80,80)}):Play()
end)
closeButton.MouseLeave:Connect(function()
    TweenService:Create(closeButton, TweenInfo.new(0.2, Enum.EasingStyle.Quad), {BackgroundColor3 = Color3.fromRGB(200,50,50)}):Play()
end)

-- Smooth closing function
local function closeGUI()
    local tweenInfo = TweenInfo.new(0.5, Enum.EasingStyle.Quad, Enum.EasingDirection.In)
    local goal = {Position = UDim2.new(frame.Position.X.Scale, frame.Position.X.Offset, frame.Position.Y.Scale, frame.Position.Y.Offset + 500), BackgroundTransparency = 1}
    local tween = TweenService:Create(frame, tweenInfo, goal)
    
    for _, side in pairs(sides) do
        TweenService:Create(side, tweenInfo, {BackgroundTransparency = 1}):Play()
    end
    
    tween:Play()
    tween.Completed:Wait()
    screenGui:Destroy()
end

closeButton.MouseButton1Click:Connect(closeGUI)

-- Rainbow animation for borders
local colors = {
    Color3.fromRGB(255,0,0),
    Color3.fromRGB(255,127,0),
    Color3.fromRGB(255,255,0),
    Color3.fromRGB(0,255,0),
    Color3.fromRGB(0,0,255),
    Color3.fromRGB(75,0,130),
    Color3.fromRGB(148,0,211)
}

spawn(function()
    local index = 1
    while frame.Parent do
        for _, side in pairs(sides) do
            local tween = TweenService:Create(side, TweenInfo.new(0.5), {BackgroundColor3 = colors[index]})
            tween:Play()
        end
        index = index + 1
        if index > #colors then index = 1 end
        wait(0.5)
    end
end)

-- Smooth draggable logic
local dragging = false
local dragInput, dragStart, startPos

frame.InputBegan:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 then
        dragging = true
        dragStart = input.Position
        startPos = frame.Position
        input.Changed:Connect(function()
            if input.UserInputState == Enum.UserInputState.End then
                dragging = false
            end
        end)
    end
end)

frame.InputChanged:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseMovement then
        dragInput = input
    end
end)

game:GetService("UserInputService").InputChanged:Connect(function(input)
    if input == dragInput and dragging then
        local delta = input.Position - dragStart
        local goal = {}
        goal.Position = UDim2.new(
            startPos.X.Scale,
            startPos.X.Offset + delta.X,
            startPos.Y.Scale,
            startPos.Y.Offset + delta.Y
        )
        TweenService:Create(frame, TweenInfo.new(0.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out), goal):Play()
    end
end)

