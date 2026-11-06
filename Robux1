--[[
  Delfi Gifter Gui
ITS NOT REAL!! - https://www.rblxscripts.net/
]]

local Players = game:GetService("Players")
local TweenService = game:GetService("TweenService")
local UIS = game:GetService("UserInputService")
local lp = Players.LocalPlayer

if getgenv().__DelfiPropCleanup then pcall(getgenv().__DelfiPropCleanup) end

---------------------------------------------------------------- style
local C = {
	panel      = Color3.fromRGB(16, 22, 34),
	panelEdge  = Color3.fromRGB(58, 140, 255),
	row        = Color3.fromRGB(13, 17, 27),
	rowEdge    = Color3.fromRGB(38, 52, 78),
	section    = Color3.fromRGB(62, 110, 205),
	title      = Color3.fromRGB(64, 132, 255),
	rowText    = Color3.fromRGB(104, 146, 228),
	admin      = Color3.fromRGB(255, 136, 36),
	white      = Color3.fromRGB(236, 240, 248),
	toggleOn   = Color3.fromRGB(40, 122, 232),
	toggleOff  = Color3.fromRGB(22, 28, 42),
	knobOff    = Color3.fromRGB(150, 172, 206),
}
local function font(w) return Font.new("rbxasset://fonts/families/GothamSSm.json", w or Enum.FontWeight.Bold) end
local function corner(p, r) local c = Instance.new("UICorner"); c.CornerRadius = UDim.new(0, r); c.Parent = p; return c end
local function stroke(p, col, th, tr)
	local s = Instance.new("UIStroke"); s.Color = col; s.Thickness = th or 1; s.Transparency = tr or 0
	s.ApplyStrokeMode = Enum.ApplyStrokeMode.Border; s.Parent = p; return s
end
local function label(parent, text, x, y, w, h, size, color, weight, xAlign)
	local l = Instance.new("TextLabel")
	l.BackgroundTransparency = 1; l.Position = UDim2.fromOffset(x, y); l.Size = UDim2.fromOffset(w, h)
	l.FontFace = font(weight); l.TextSize = size; l.TextColor3 = color; l.Text = text
	l.TextXAlignment = xAlign or Enum.TextXAlignment.Left; l.Parent = parent
	return l
end

---------------------------------------------------------------- window
local gui = Instance.new("ScreenGui")
gui.Name = "DelfiGifterProp"; gui.ResetOnSpawn = false; gui.DisplayOrder = 900
gui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling; gui.IgnoreGuiInset = true
gui.Parent = lp:WaitForChild("PlayerGui")

local W, H = 308, 372
local win = Instance.new("Frame")
win.Name = "Window"; win.Size = UDim2.fromOffset(W, H); win.Position = UDim2.new(0.5, -W / 2, 0.5, -H / 2)
win.BackgroundColor3 = C.panel; win.BackgroundTransparency = 0.12; win.BorderSizePixel = 0
win.ClipsDescendants = true; win.Parent = gui
corner(win, 14)
stroke(win, C.panelEdge, 2.5)

-- soft blue glow around the edge (two faint outer rings)
local halos = {}
for i, spec in ipairs({{4, 5, 0.55}, {9, 6, 0.82}}) do
	local pad, th, tr = spec[1], spec[2], spec[3]
	local h = Instance.new("Frame")
	h.Name = "Halo" .. i; h.BackgroundTransparency = 1; h.ZIndex = 0; h.Parent = gui
	corner(h, 14 + pad)
	stroke(h, C.panelEdge, th, tr)
	halos[#halos + 1] = {frame = h, pad = pad}
end
local function syncGlow()
	local ap, as = win.AbsolutePosition, win.AbsoluteSize
	for _, h in ipairs(halos) do
		h.frame.Position = UDim2.fromOffset(ap.X - h.pad, ap.Y - h.pad)
		h.frame.Size = UDim2.fromOffset(as.X + h.pad * 2, as.Y + h.pad * 2)
	end
end

-- header
local header = Instance.new("Frame")
header.BackgroundTransparency = 1; header.Size = UDim2.new(1, 0, 0, 52); header.Parent = win
label(header, "DELFI", 18, 10, 120, 14, 12, C.title, Enum.FontWeight.Bold)
local t2 = label(header, "GIFTER", 18, 24, 160, 18, 15, C.title, Enum.FontWeight.Heavy)
local grad = Instance.new("UIGradient")
grad.Color = ColorSequence.new(Color3.fromRGB(70, 150, 255), Color3.fromRGB(40, 100, 230)); grad.Parent = t2

local mini = Instance.new("TextButton")
mini.Size = UDim2.fromOffset(26, 26); mini.Position = UDim2.new(1, -40, 0, 12)
mini.BackgroundColor3 = Color3.fromRGB(10, 18, 34); mini.AutoButtonColor = false
mini.Text = "-"; mini.FontFace = font(Enum.FontWeight.Heavy); mini.TextSize = 16; mini.TextColor3 = C.white
mini.Parent = header; corner(mini, 6); stroke(mini, Color3.fromRGB(40, 70, 130), 1)

-- body
local body = Instance.new("Frame")
body.BackgroundTransparency = 1; body.Position = UDim2.fromOffset(0, 52); body.Size = UDim2.new(1, 0, 1, -52)
body.Parent = win

local function section(text, y) label(body, text, 18, y, 260, 14, 10, C.section, Enum.FontWeight.Heavy) end
local function rowBox(y, h)
	local f = Instance.new("Frame")
	f.Position = UDim2.fromOffset(16, y); f.Size = UDim2.new(1, -32, 0, h or 40)
	f.BackgroundColor3 = C.row; f.BackgroundTransparency = 0.05; f.BorderSizePixel = 0; f.Parent = body
	corner(f, 8); stroke(f, C.rowEdge, 1, 0.2)
	return f
end

section("ROBUX AMOUNT", 8)
local amountRow = rowBox(30, 40)
local box = Instance.new("TextBox")
box.BackgroundTransparency = 1; box.Position = UDim2.fromOffset(12, 0); box.Size = UDim2.new(1, -24, 1, 0)
box.FontFace = font(Enum.FontWeight.Medium); box.TextSize = 14; box.TextColor3 = C.white
box.PlaceholderText = "Amount"; box.PlaceholderColor3 = Color3.fromRGB(90, 105, 135)
box.Text = "241421421"; box.ClearTextOnFocus = false; box.TextXAlignment = Enum.TextXAlignment.Left
box.Parent = amountRow
box:GetPropertyChangedSignal("Text"):Connect(function() -- numbers only, like the original
	local digits = box.Text:gsub("%D", "")
	if digits ~= box.Text then box.Text = digits end
end)

local apply = Instance.new("TextButton")
apply.Position = UDim2.fromOffset(16, 80); apply.Size = UDim2.new(1, -32, 0, 40)
apply.BackgroundColor3 = Color3.fromRGB(12, 18, 32); apply.AutoButtonColor = false
apply.Text = "APPLY"; apply.FontFace = font(Enum.FontWeight.Heavy); apply.TextSize = 14; apply.TextColor3 = C.white
apply.Parent = body; corner(apply, 8)
local applyStroke = stroke(apply, Color3.fromRGB(52, 78, 128), 1)

local function toggleRow(y, text, textColor, on)
	local r = rowBox(y, 40)
	label(r, text, 14, 0, 180, 40, 13, textColor, Enum.FontWeight.Bold)
	local pill = Instance.new("TextButton")
	pill.AnchorPoint = Vector2.new(1, 0.5); pill.Position = UDim2.new(1, -12, 0.5, 0); pill.Size = UDim2.fromOffset(48, 24)
	pill.AutoButtonColor = false; pill.Text = ""; pill.Parent = r; corner(pill, 12)
	local knob = Instance.new("Frame")
	knob.AnchorPoint = Vector2.new(0.5, 0.5); knob.Size = UDim2.fromOffset(18, 18); knob.BorderSizePixel = 0
	knob.Parent = pill; corner(knob, 9)
	local state = on
	local function render(anim)
		local goalPill = {BackgroundColor3 = state and C.toggleOn or C.toggleOff, BackgroundTransparency = state and 0 or 1}
		local goalKnob = {Position = state and UDim2.new(1, -14, 0.5, 0) or UDim2.new(0, 14, 0.5, 0),
			BackgroundColor3 = state and Color3.new(1, 1, 1) or C.knobOff}
		if anim then
			TweenService:Create(pill, TweenInfo.new(0.15), goalPill):Play()
			TweenService:Create(knob, TweenInfo.new(0.15, Enum.EasingStyle.Quad), goalKnob):Play()
		else
			for k, v in pairs(goalPill) do pill[k] = v end
			for k, v in pairs(goalKnob) do knob[k] = v end
		end
	end
	render(false)
	pill.Activated:Connect(function() state = not state; render(true) end)
	return r
end

toggleRow(130, "Roblox Plus", C.rowText, true)
toggleRow(180, "Plus Promo", C.rowText, false)
section("OVERHEAD TAG", 230)
toggleRow(252, "Admin", C.admin, false)

---------------------------------------------------------------- behaviour (cosmetic only)
-- Apply: just a press flash. It changes nothing.
apply.Activated:Connect(function()
	TweenService:Create(apply, TweenInfo.new(0.08), {BackgroundColor3 = Color3.fromRGB(28, 44, 78)}):Play()
	applyStroke.Color = C.panelEdge
	task.wait(0.12)
	TweenService:Create(apply, TweenInfo.new(0.25), {BackgroundColor3 = Color3.fromRGB(12, 18, 32)}):Play()
	applyStroke.Color = Color3.fromRGB(52, 78, 128)
end)

-- minimise
local minimised = false
mini.Activated:Connect(function()
	minimised = not minimised
	mini.Text = minimised and "+" or "-"
	TweenService:Create(win, TweenInfo.new(0.2, Enum.EasingStyle.Quad), {Size = UDim2.fromOffset(W, minimised and 52 or H)}):Play()
end)

-- drag by header
local dragging, dragStart, startPos
header.InputBegan:Connect(function(i)
	if i.UserInputType == Enum.UserInputType.MouseButton1 or i.UserInputType == Enum.UserInputType.Touch then
		dragging, dragStart, startPos = true, i.Position, win.Position
	end
end)
local conns = {}
table.insert(conns, UIS.InputChanged:Connect(function(i)
	if dragging and (i.UserInputType == Enum.UserInputType.MouseMovement or i.UserInputType == Enum.UserInputType.Touch) then
		local d = i.Position - dragStart
		win.Position = UDim2.new(startPos.X.Scale, startPos.X.Offset + d.X, startPos.Y.Scale, startPos.Y.Offset + d.Y)
	end
end))
table.insert(conns, UIS.InputEnded:Connect(function(i)
	if i.UserInputType == Enum.UserInputType.MouseButton1 or i.UserInputType == Enum.UserInputType.Touch then dragging = false end
end))
table.insert(conns, game:GetService("RunService").RenderStepped:Connect(syncGlow))

getgenv().__DelfiPropCleanup = function()
	for _, c in ipairs(conns) do c:Disconnect() end
	gui:Destroy()
end
