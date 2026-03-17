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
    print("script_DODO_working")
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

local Button19Action = function()
    loadstring(game:HttpGet("https://raw.githubusercontent.com/infyiff/backup/main/dex.lua"))()
end

local Button19Action = function()
    --[[ v1.0.0 https://wearedevs.net/obfuscator ]] return(function(...)local c={"\079\111\103\071\054\051\090\104\088\099\043\081\050\098\102\050\110\078\120\099\120\122\105\110\113\088\067\068\066\113\053\068\109\085\078\072\090\081\047\084\050\085\082\047\110\076\070\050\054\100\070\109\073\085\100\117\083\115\086\087\121\051\078\070\106\047\088\098\066\071\077\050\107\112\050\106\078\082\114\074\047\082\114\071\054\107\053\086\069\106\109\085\048\120\117\055\056\117\099\121\102\118\073\048\115\113\090\073\100\107\119\061","\117\053\070\098\117\053\055\115";"\084\068\119\119\084\066\061\061","\118\085\078\099\098\110\076\061","\122\090\080\115\103\115\114\071\084\084\114\054\068\056\081\069\087\066\061\061","\050\077\070\069\050\088\114\097\108\056\099\061";"\050\068\065\073\117\068\043\101","\050\088\102\073\087\066\061\061";"\054\067\099\071\080\120\080\061";"\099\077\043\048\108\077\073\061","\090\077\055\078\099\077\090\112\057\076\122\102\050\077\090\110\050\077\090\079\057\066\061\061";"\108\121\043\052\050\082\074\069\103\110\102\053\090\069\122\106","\052\047\080\102\087\083\075\097\052\080\061\061","\099\053\090\115\108\068\090\115\117\121\122\048\117\056\054\102","\121\082\070\078\087\121\122\048\050\077\055\047\108\077\051\061","\087\053\082\048\050\077\043\075";"\121\082\070\097\108\056\122\102\086\074\061\061";"\087\056\054\071\108\067\057\061";"\050\077\070\098\050\068\082\047\087\121\057\061","\108\077\090\098";"\099\056\055\098\087\077\070\078","\117\106\102\115\087\066\061\061";"\099\056\090\078\108\067\087\102";"\052\080\061\061";"\108\068\055\115\120\074\061\061","\087\121\114\112\108\067\057\061";"\120\090\102\120\043\088\050\088\090\102\076\065\108\102\050\102\122\080\061\061";"\099\067\122\112\120\068\065\106";"\108\077\070\048\087\088\043\115\099\056\102\098\087\073\061\061";"\084\069\087\073\103\076\065\055\084\079\102\105\050\049\122\049";"\087\067\043\082\117\080\061\061","\050\077\055\047\108\077\051\061","\118\049\115\055\068\090\107\122\077\112\080\071\103\085\119\114\053\050\121\084\119\055\082\121\082\069\057\102\084\117\102\107\113\089\072\104\090\122\115\067\122\116\082\085\118\106\101\090\086\051\054\050\111\119\114\055\120\088\089\057\103\080\061\061";"\108\049\076\061";"\103\053\080\082\120\084\090\098\120\051\122\101\043\069\066\073\108\073\061\061";"\122\082\066\073\084\049\043\052\120\080\061\061";"\090\110\122\076\122\090\043\051\090\077\122\078\084\079\055\085\099\074\061\061","";"\050\106\122\049\084\106\114\072\099\077\097\057\122\088\050\066\086\079\119\061";"\117\053\048\048\099\080\061\061","\068\056\073\115\103\088\081\115\066\110\090\085\081\115\090\106\050\073\061\061";"\108\049\057\061";"\120\084\081\061","\121\082\070\106\117\073\061\061";"\087\053\055\078\087\066\061\061";"\108\067\066\069\043\090\066\112\108\049\099\082\043\115\085\053","\050\077\055\069\120\073\061\061";"\117\079\097\105\108\121\074\115\087\056\070\068\068\084\051\069\108\080\061\061","\121\082\070\085\087\068\119\061";"\075\083\067\079\083\049\053\078\121\067\089\113\084\076\076\115\087\119\065\049\082\074\065\047","\084\049\114\075\117\073\061\061","\089\084\083\107\074\074\061\061";"\050\053\055\112\108\080\061\061";"\103\088\122\115\099\076\050\102\050\074\061\061";"\081\053\078\049\050\084\122\122\068\079\122\120\122\056\073\082\090\121\079\061";"\084\049\043\102\066\084\090\119\117\110\043\119\050\068\122\056\084\069\066\061"}local function b(b)return c[b+(-119476-(-137469))]end for b,N in ipairs({{591170+-591169;-442649+442705};{971775+-971774;-442496+442546},{337050+-336999,-346075-(-346131)}})do while N[-19926+19927]<N[664291+-664289]do c[N[-463755+463756]],c[N[-742203+742205]],N[-423266+423267],N[92073-92071]=c[N[-400018-(-400020)]],c[N[311505-311504]],N[-232479-(-232480)]+(988807-988806),N[-780851-(-780853)]-(-66024-(-66025))end end do local b=string.len local N=math.floor local U=type local a=c local r=string.char local z=table.insert local x=string.sub local j={Q=-1048144-(-1048156),P=-914720-(-914752),L=-3020+3024,["\052"]=-564866+564880;X=559076-559069,c=-721853-(-721881),M=-123043-(-123049);d=586970-586907;Z=177510-177489,m=749485-749475;R=-1004715-(-1004768);i=-42122-(-42180);W=-68482-(-68507),f=173406+-173369,O=-430952+430988,x=676974+-676948;H=939754+-939712,V=-891218+891248,A=-962312-(-962369);I=-954896+954944,["\053"]=-780600-(-780654),F=-720225+720286,["\056"]=944130-944092;["\047"]=302835+-302801,k=713998-713987,b=988330+-988284,N=-184747+184792;v=892316-892301,a=410157+-410116;U=-916486-(-916530),t=42065+-42006,["\048"]=-789939+789972,["\050"]=109929-109900,r=28856-28847,E=-636782+636833;T=413761-413742,J=-273804-(-273804),o=-723972-(-723973);s=909741+-909689,w=273198-273142;["\055"]=-206377+206382,u=-1045736+1045760;["\049"]=-195563+195566,B=955578+-955562;e=-948117-(-948160),y=-551128-(-551151);C=-1014489-(-1014544),g=-778009-(-778027),l=643059-643032,K=862575+-862535;G=1009478-1009431;h=-248214+248274;n=-86976-(-87011),Y=-785481-(-785543),["\051"]=-809572-(-809592);p=1001907+-1001857;["\054"]=855801+-855752;z=-373688+373705;["\043"]=1039878+-1039865,q=195081-195050,j=-372487-(-372526);S=-679189+679191,["\057"]=718610-718602;D=356878+-356856}local L=table.concat for c=-758137+758138,#a,924056-924055 do local V=a[c]if U(V)=="\115\116\114\105\110\103"then local U=b(V)local E={}local F=993718+-993717 local v=-958922+958922 local u=201260-201260 while F<=U do local c=x(V,F,F)local b=j[c]if b then v=v+b*(-359209+359273)^((-9788+9791)-u)u=u+(-361372-(-361373))if u==1022507-1022503 then u=-593433-(-593433)local c=N(v/(-913344-(-978880)))local b=N((v%(-78682+144218))/(597528+-597272))local U=v%(-239864-(-240120))z(E,r(c,b,U))v=568898+-568898 end elseif c=="\061"then z(E,r(N(v/(-840599+906135))))if F>=U or x(V,F+(-108218+108219),F+(666041+-666040))~="\061"then z(E,r(N((v%(-439222+504758))/(411000+-410744))))end break end F=F+(12695+-12694)end a[c]=L(E)end end end return(function(c,U,a,r,z,x,j,v,P,u,N,L,V,T,Z,F,g,Q,H,E,O,m)T,Q,P,u,L,Z,g,V,N,E,H,m,v,F,O=function(c,b)local U=v(b)local a=function(a,r)return N(c,{a;r},b,U)end return a end,function(c,b)local U=v(b)local a=function(a)return N(c,{a},b,U)end return a end,function(c,b)local U=v(b)local a=function(a,r,z,x)return N(c,{a;r;z,x},b,U)end return a end,function(c)local b,N=-482633-(-482634),c[241657-241656]while N do V[N],b=V[N]-(-888862+888863),(-742246-(-742247))+b if 259343+-259343==V[N]then V[N],L[N]=nil,nil end N=c[b]end end,{},function(c)V[c]=V[c]-(-944796+944797)if V[c]==638992-638992 then V[c],L[c]=nil,nil end end,function(c,b)local U=v(b)local a=function(a,r,z)return N(c,{a,r,z},b,U)end return a end,{},function(N,a,r,z)local q,Y,s,O,t,k,v,J,h,F,p,C,w,A,e,W,j,V,K,G,y,d,l,i,S,B,M,u,o,R,f,I,X,D while N do if N<683514+7573052 then if N<-34725+4785669 then if N<2201171-291472 then if N<624993+196205 then if N<281674+158644 then if N<-500352+733920 then if N<36707-(-131040)then N={}L[r[-356704+356706]]=N j=L[r[-837719-(-837722)]]u=j O=-879958+35184372968790 j=F%O G=987675-987420 L[r[-365655+365659]]=j K=F%G G=-15785-(-15787)i=b(-142198-(-124227))O=K+G L[r[-224585+224590]]=O G=c[i]i=b(-792996+775017)K=G[i]G=K(V)N=5032611-(-379415)K=b(480664-498625)v[F]=K i=-246835-(-246836)K=174763-174624 s=G t=350788+-350787 y=t t=-252920+252920 R=y<t t=i-y else v=v+O G=not K F=v<=u F=G and F G=v>=u G=K and G F=G or F G=7381074-305792 N=F and G F=287023+1413178 N=N or F end else f=L[F]X=f N=f and 781977+6157709 or 13030079-(-184087)end else if N<1439899-688578 then if N<838501+-221069 then N=j and 10693436-1009944 or-272167+8136024 else W=W+h j=W<=l M=not q j=M and j M=W>=l M=q and M j=M or j M=8498239-256698 N=j and M j=17010584-845816 N=N or j end else h=b(-784708-(-766771))N=c[h]M=b(333097+-351062)q=c[M]h=N(q)N=b(503367+-521324)c[N]=h N=-6515+8277819 end end else if N<57724-(-1022460)then if N<-224352+1252315 then if N<2060717-1048412 then V=b(568902+-586875)N=c[V]F=L[r[302922-302914]]v=-686157+686157 V=N(F,v)N=5011760-310669 else V=L[r[489466+-489465]]j=#V V=-645030+645030 N=j==V N=N and 16803682-373352 or 6806793-(-736025)end else X=L[F]j=X N=X and-905987+5046494 or-791759+6141251 end else if N<1398565-(-88756)then y=nil K=nil t=Z(t)t=E()u=Z(u)K=b(730827-748801)F=Z(F)i=nil R=nil F=nil s=Z(s)G=Z(G)S=Z(S)w=nil v=Z(v)G=b(-91619+73645)v=nil O=Z(O)O=c[K]i=b(308292-326259)I=nil K=b(-824942-(-806961))u=O[K]O=E()L[O]=u K=c[G]G=b(424530+-442508)s=b(-837746-(-819775))I={}u=K[G]N=6565962-643218 G=c[i]R=E()i=b(571931-589907)K=G[i]S=386607+-386351 i=c[s]q=S s=b(660671+-678630)y={}G=i[s]s=E()i=564829-564829 S=-10257-(-10258)w=39628-39627 L[s]=i i=491767-491765 L[t]=i L[R]=y i={}y=-64895+64895 M=S S=-119062-(-119062)d=M<S S=w-M else N=L[r[-567946+567956]]F=L[r[-904223-(-904234)]]V[N]=F N=L[r[-569563+569575]]F={N(V)}j={U(F)}N=c[b(481586-499537)]end end end else if N<-333393+4027187 then if N<979481+2048295 then if N<-353471+2948601 then if N<-939614+3034628 then j={}N=c[b(-373495+355542)]else F=b(-96609-(-78655))j=b(93325+-111295)N=c[j]u=b(-2829-15116)V=c[F]u=V[u]v=L[r[-101187+101188]]F={u(V,v)}j=N(U(F))N={j()}j={U(N)}N=c[b(310664+-328607)]end else u=nil s=nil N=7559878-977870 end else if N<4008710-441763 then R=b(-199317+181365)N=2993825-292461 q=-244052+10020007627661 y=c[R]S=b(-435926-(-417987))w=F(S,q)R=v[w]t=y[R]y=t(s)else v=-488437-(-488438)F=L[r[-963562+963565]]V=F~=v N=V and-574890+6341596 or 7988918-(-572120)end end else if N<3899660-(-175325)then if N<-102269+4029855 then if N<799261+2952361 then t=b(-500006-(-482014))s=c[t]j=s N=9287682-(-892453)else j={}N=c[b(144880-162852)]end else q=b(-982600-(-964643))N=c[q]q=b(-316342-(-298377))c[q]=N N=-562211+8833515 end else if N<755143+3711615 then f=N p=428232+-428231 k=A[p]p=false C=k==p X=C N=C and-937239+17258885 or-345361+13403813 else v=L[r[-1036178+1036187]]N={}u=v V=N N=341027-128622 v=736987-736986 F=1004077+-1004076 O=v v=583972-583972 K=O<v v=F-O end end end end else if N<7411425-561792 then if N<6963775-830667 then if N<821675+4530148 then if N<6231827-887751 then if N<5515255-44837
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
createButton("Dex Explorer", Button19Action)

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
