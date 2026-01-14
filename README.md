local HUB_NAME = "Pedro Scripts"

local Players = game:GetService("Players")
local UIS = game:GetService("UserInputService")
local TweenService = game:GetService("TweenService")

local LP = Players.LocalPlayer

local gui = Instance.new("ScreenGui")
gui.Name = "PedroScriptsHub"
gui.ResetOnSpawn = false
gui.Parent = LP:WaitForChild("PlayerGui")

local main = Instance.new("Frame")
main.Size = UDim2.fromScale(0.55, 0.6)
main.Position = UDim2.fromScale(0.225, 0.2)
main.BackgroundColor3 = Color3.fromRGB(15, 15, 18)
main.BorderSizePixel = 0
main.Parent = gui
main.Size = UDim2.fromScale(0, 0)
main.Position = UDim2.fromScale(0.5, 0.5)
TweenService:Create(main, TweenInfo.new(0.4, Enum.EasingStyle.Quart, Enum.EasingDirection.Out), {
	Size = UDim2.fromScale(0.55, 0.6),
	Position = UDim2.fromScale(0.225, 0.2)
}):Play()

local corner = Instance.new("UICorner")
corner.CornerRadius = UDim.new(0, 18)
corner.Parent = main

local bg = Instance.new("ImageLabel")
bg.Image = ""
bg.Size = UDim2.fromScale(1, 1)
bg.BackgroundTransparency = 1
bg.ImageTransparency = 0.65
bg.ScaleType = Enum.ScaleType.Crop
bg.Parent = main

local overlay = Instance.new("Frame")
overlay.Size = UDim2.fromScale(1, 1)
overlay.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
overlay.BackgroundTransparency = 0.35
overlay.BorderSizePixel = 0
overlay.Parent = main

local oc = Instance.new("UICorner")
oc.CornerRadius = UDim.new(0, 18)
oc.Parent = overlay

local header = Instance.new("Frame")
header.Size = UDim2.fromScale(1, 0.12)
header.BackgroundTransparency = 1
header.Parent = overlay

local title = Instance.new("TextLabel")
title.Text = HUB_NAME
title.Font = Enum.Font.GothamBlack
title.TextScaled = true
title.TextColor3 = Color3.fromRGB(255, 255, 255)
title.BackgroundTransparency = 1
title.Size = UDim2.fromScale(0.7, 1)
title.Position = UDim2.fromScale(0.03, 0)
title.Parent = header

local close = Instance.new("TextButton")
close.Text = "✕"
close.Font = Enum.Font.GothamBold
close.TextScaled = true
close.TextColor3 = Color3.fromRGB(255, 120, 120)
close.BackgroundTransparency = 1
close.Size = UDim2.fromScale(0.07, 0.7)
close.Position = UDim2.fromScale(0.9, 0.15)
close.Parent = header

local sidebar = Instance.new("Frame")
sidebar.Size = UDim2.fromScale(0.22, 0.88)
sidebar.Position = UDim2.fromScale(0, 0.12)
sidebar.BackgroundColor3 = Color3.fromRGB(18, 18, 22)
sidebar.BorderSizePixel = 0
sidebar.Parent = overlay

local sc = Instance.new("UICorner")
sc.CornerRadius = UDim.new(0, 14)
sc.Parent = sidebar

local tabsLayout = Instance.new("UIListLayout")
tabsLayout.Padding = UDim.new(0, 10)
tabsLayout.HorizontalAlignment = Enum.HorizontalAlignment.Center
tabsLayout.VerticalAlignment = Enum.VerticalAlignment.Top
tabsLayout.Parent = sidebar

local content = Instance.new("Frame")
content.Size = UDim2.fromScale(0.78, 0.88)
content.Position = UDim2.fromScale(0.22, 0.12)
content.BackgroundTransparency = 1
content.Parent = overlay

local pages = {}

local function createPage(name)
	local page = Instance.new("Frame")
	page.Name = name
	page.Size = UDim2.fromScale(1, 1)
	page.BackgroundTransparency = 1
	page.Visible = false
	page.Parent = content
	pages[name] = page

	local pad = Instance.new("UIPadding")
	pad.PaddingTop = UDim.new(0, 14)
	pad.PaddingLeft = UDim.new(0, 14)
	pad.PaddingRight = UDim.new(0, 14)
	pad.PaddingBottom = UDim.new(0, 14)
	pad.Parent = page

	local list = Instance.new("UIListLayout")
	list.Padding = UDim.new(0, 12)
	list.Parent = page

	return page
end

local function createTab(text, pageName)
	local btn = Instance.new("TextButton")
	btn.Text = text
	btn.Font = Enum.Font.GothamBold
	btn.TextScaled = true
	btn.TextColor3 = Color3.fromRGB(230, 230, 235)
	btn.BackgroundColor3 = Color3.fromRGB(28, 28, 34)
	btn.Size = UDim2.fromScale(0.9, 0.1)
	btn.Parent = sidebar

	local c = Instance.new("UICorner")
	c.CornerRadius = UDim.new(0, 10)
	c.Parent = btn

	TweenService:Create(btn, TweenInfo.new(0.15), {BackgroundTransparency = 0.05}):Play()

	btn.MouseButton1Click:Connect(function()
		TweenService:Create(btn, TweenInfo.new(0.15), {Size = UDim2.fromScale(0.88, 0.1)}):Play()
		task.delay(0.15, function()
			TweenService:Create(btn, TweenInfo.new(0.15), {Size = UDim2.fromScale(0.9, 0.1)}):Play()
		end)
		for _, p in pairs(pages) do p.Visible = false end
		pages[pageName].Visible = true
	end)
end

local function toggleItem(parent, label, default, callback)
	local wrap = Instance.new("Frame")
	wrap.Size = UDim2.fromScale(1, 0.12)
	wrap.BackgroundColor3 = Color3.fromRGB(25, 25, 30)
	wrap.Parent = parent

	local c = Instance.new("UICorner")
	c.CornerRadius = UDim.new(0, 10)
	c.Parent = wrap

	local txt = Instance.new("TextLabel")
	txt.Text = label
	txt.Font = Enum.Font.Gotham
	txt.TextScaled = true
	txt.TextColor3 = Color3.fromRGB(240, 240, 245)
	txt.BackgroundTransparency = 1
	txt.Size = UDim2.fromScale(0.7, 1)
	txt.Parent = wrap

	local btn = Instance.new("TextButton")
	btn.Text = default and "ON" or "OFF"
	btn.Font = Enum.Font.GothamBold
	btn.TextScaled = true
	btn.TextColor3 = Color3.fromRGB(0,0,0)
	btn.BackgroundColor3 = default and Color3.fromRGB(90, 220, 140) or Color3.fromRGB(220, 90, 90)
	btn.Size = UDim2.fromScale(0.25, 0.7)
	btn.Position = UDim2.fromScale(0.72, 0.15)
	btn.Parent = wrap

	local bc = Instance.new("UICorner")
	bc.CornerRadius = UDim.new(0, 8)
	bc.Parent = btn

	local state = default
	btn.MouseButton1Click:Connect(function()
		state = not state
		btn.Text = state and "ON" or "OFF"
		btn.BackgroundColor3 = state and Color3.fromRGB(90, 220, 140) or Color3.fromRGB(220, 90, 90)
		callback(state)
	end)
end

local pageAimbot = createPage("Aimbot")
local pageESP = createPage("ESP")
local pageSettings = createPage("Settings")

createTab("Aimbot", "Aimbot")
createTab("ESP", "ESP")
createTab("Config", "Settings")

pages.Aimbot.Visible = true

toggleItem(pageAimbot, "Aimbot Ativado", false, function(v) _G.AimbotEnabled = v end)

toggleItem(pageAimbot, "AimLock", false, function(v) _G.AimLockEnabled = v end)

toggleItem(pageESP, "ESP Ativado", true, function(v) _G.ESPEnabled = v end)

toggleItem(pageESP, "Team Check", true, function(v) _G.TeamCheck = v end)

toggleItem(pageSettings, "Mostrar Hub", true, function(v) gui.Enabled = v end)

local dragging, dragStart, startPos

main.InputBegan:Connect(function(input)
	if input.UserInputType == Enum.UserInputType.MouseButton1 then
		dragging = true
		dragStart = input.Position
		startPos = main.Position
	end
end)

main.InputEnded:Connect(function(input)
	if input.UserInputType == Enum.UserInputType.MouseButton1 then
		dragging = false
	end
end)

UIS.InputChanged:Connect(function(input)
	if dragging and input.UserInputType == Enum.UserInputType.MouseMovement then
		local delta = input.Position - dragStart
		main.Position = UDim2.new(startPos.X.Scale, startPos.X.Offset + delta.X, startPos.Y.Scale, startPos.Y.Offset + delta.Y)
	end
end)

close.MouseButton1Click:Connect(function()
	gui.Enabled = false
end)
