local ScreenGui = Instance.new("ScreenGui")
local ui = Instance.new("ImageButton")
local UICorner = Instance.new("UICorner")

--Properties:

ScreenGui.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui")
ScreenGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling

ui.Name = "ui"
ui.Parent = ScreenGui
ui.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
ui.BorderColor3 = Color3.fromRGB(0, 0, 0)
ui.BorderSizePixel = 0
ui.Position = UDim2.new(0.120833337, 0, 0.0952890813, 0)
ui.Size = UDim2.new(0, 55, 0, 57)
ui.Image = "rbxassetid://14491200389"
ui.MouseButton1Click:Connect(function()
    game.CoreGui:FindFirstChild("ScreenGui").Enabled = not game.CoreGui:FindFirstChild("ScreenGui").Enabled
end)


UICorner.CornerRadius = UDim.new(0.300000012, 0)
UICorner.Parent = ui





local Fluent = loadstring(game:HttpGet("https://github.com/dawid-scripts/Fluent/releases/latest/download/main.lua"))()
local SaveManager = loadstring(game:HttpGet("https://raw.githubusercontent.com/title33/SaveManager/main/README.md"))()
local InterfaceManager = loadstring(game:HttpGet("https://raw.githubusercontent.com/dawid-scripts/Fluent/master/Addons/InterfaceManager.lua"))()

local Window = Fluent:CreateWindow({
    Title = "Xylo Hub",
    SubTitle = "by Sky",
    TabWidth = 160,
    Size = UDim2.fromOffset(530, 340),
    Acrylic = true, -- The blur may be detectable, setting this to false disables blur entirely
    Theme = "Dark",
    MinimizeKey = Enum.KeyCode.LeftControl -- Used when theres no MinimizeKeybind
})

--Fluent provides Lucide Icons https://lucide.dev/icons/ for the tabs, icons are optional
local Tabs = {
    General = Window:AddTab({ Title = "General", Icon = "home" }),
    Skil = Window:AddTab({ Title = "Skil", Icon = "battery-charging" }),
    TP = Window:AddTab({ Title = "TP", Icon = "chevrons-right" }),
    Fruit = Window:AddTab({ Title = "Fruit", Icon = "apple" }),
    Inventory = Window:AddTab({ Title = "Inventory", Icon = "scroll" }),
    Settings = Window:AddTab({ Title = "Settings", Icon = "settings" })
}

local Options = Fluent.Options

function No()
    for i, v in ipairs(workspace.Lives:GetChildren()) do
        if not game:GetService("Players"):GetPlayerFromCharacter(v) then -- if not player then
            local cleanedName = string.gsub(v.Name, "%d+$", "")
            v.Name = tostring(cleanedName)
        end
    end

    workspace.Lives.ChildAdded:Connect(function(model)
        wait()
        if not game:GetService("Players"):GetPlayerFromCharacter(model) then -- if not player then
            local cleanedName = string.gsub(model.Name, "%d+$", "")
            model.Name = cleanedName
        end
    end)
end

function TP(targetCFrame)
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = targetCFrame
end


Boss = {
 "None",
 "Natsu",
 "Choso",
 "Ichigo",
 "Killua",
 "Gojo [Unleashed]",
 "Sukuna [Half Power]",
 "Gojo",
 "Sukuna",
 "Shank",
 "Kashimo",
 "Artoria",
 "Bomb Man",
 "Sand Man",
 "Monkey King",
 "Bandit Leader"
}


local Dropdown = Tabs.General:AddDropdown("Boss", {
    Title = "Boss",
 Values = {"None", "Bandit", "Bandit Leader", "Clown Pirate", "Marine", "Monkey", "Monkey King", "Bomb Man", "Sand Man", "Snow Bandit", "Snow Bandit Leader"},
    Multi = false,
    Default = 1,
})

Dropdown:SetValue("None")

Dropdown:OnChanged(function(v)
    free = v
end)

local Toggle = Tabs.General:AddToggle("MyToggle", {Title = "Auto Farm Boss", Default = false })

Toggle:OnChanged(function(t)
 No()
_G.p = t

function A()
  game:GetService'VirtualUser':CaptureController()
game:GetService'VirtualUser':Button1Down(Vector2.new(1280, 672))
end

end)

Options.MyToggle:SetValue(false)

spawn(function()
    while wait() do
        pcall(function()
            if _G.p then
                for _, v in pairs(game:GetService("Workspace").Lives:GetDescendants()) do
                    if v.Name == free and v:FindFirstChild("HumanoidRootPart") and v.Humanoid.Health >= 1 then
                        repeat
                            wait()
                            A()
                            v.HumanoidRootPart.Size = Vector3.new(10, 10, 10)
                            v.HumanoidRootPart.Transparency = 0.9
                            v.Humanoid.WalkSpeed = 0
                            v.Humanoid.JumpPower = 0
                            TP(v.HumanoidRootPart.CFrame * CFrame.new(0, 0, 5))
                        until not _G.p
                    end
                end
            end
        end)
    end
end)


function MonsSpawned(Mons)
   for _, v in pairs(game:GetService('Workspace').Lives:GetDescendants()) do
        if v.Name == Mons and v:FindFirstChild("HumanoidRootPart") and v.Humanoid.Health >= 1 then
            return true
        end
    end
    return false
end

function FarmBoss(v)
    if v:FindFirstChild("HumanoidRootPart") and v.Humanoid.Health >= 1 then
        repeat
            No()
            wait()
            v.HumanoidRootPart.Size = Vector3.new(10, 10, 10)
            v.HumanoidRootPart.Transparency = 0.9
            game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = v.HumanoidRootPart.CFrame * CFrame.new(0, 0, 7)
        until _G.eami == false or v.Humanoid.Health <= 0
    end
end

spawn(function()
    while wait() do
        pcall(function()
            if _G.eami then
                local MonNames = {
                    "Shadow",
                    "Gojo",
                    "Kashimo",
                    "Sukuna",
                    "Artoria",
                    "Uraume",
                    "Gojo [Unleashed]",
                    "Sukuna [Half Power]",
                    "Rimuru",
                    "Killua",
                    "Ichigo",
                    "Choso"
                }

                for _, v in pairs(game:GetService('Workspace').Lives:GetDescendants()) do
                    if table.find(MonNames, v.Name) then
                        FarmBoss(v)
                    end
                end
            end
        end)
    end
end)

local Toggle = Tabs.General:AddToggle("Auto Farm Boss [ALL]", { Title = "Auto Farm Boss [ALL]", Default = false })

Toggle:OnChanged(function(a)
    _G.eami = a
end)



local Weaponlist = {}
local Weapon = nil
for i,v in pairs(game:GetService("Players").LocalPlayer.Backpack:GetChildren()) do
    table.insert(Weaponlist,v.Name)
    end

Tabs.General:AddDropdown("Weapon", {
        Title = "Weapon",
        Values = Weaponlist,
        Multi = false,
        Default = nil,
        Callback = function(v)
        _G.Weapon = v
       end
   })



     local Toggle = Tabs.General:AddToggle("Auto Equip", {Title = "Auto Equip", Default = false })
    Toggle:OnChanged(function(a)
    _G.AutoEquiped = a
    end)
    
spawn(function()
while wait() do
if _G.AutoEquiped then
pcall(function()
game.Players.LocalPlayer.Character.Humanoid:EquipTool(game:GetService("Players").LocalPlayer.Backpack:FindFirstChild(_G.Weapon))
end)
end
end
end)    

    local Toggle = Tabs.General:AddToggle("Auto Attack", {Title = "Auto Attack", Default = false })
    Toggle:OnChanged(function(ah)
_G.Ato = ah
while _G.Ato do wait()
game:GetService'VirtualUser':CaptureController()
game:GetService'VirtualUser':Button1Down(Vector2.new(1280, 672))
end
    end)


    local Toggle = Tabs.General:AddToggle("Auto Chests", {Title = "Auto Chests", Default = false })
    Toggle:OnChanged(function(wow)
        _G.aa = wow
        while _G.aa do wait()
for i,v in pairs(game:GetService("Workspace").Chests:GetDescendants()) do
if v.ClassName == "ProximityPrompt" then
fireproximityprompt(v,30)
                end
            end
        end
    end)








    local Toggle = Tabs.Skil:AddToggle("Auto Skil Z", {Title = "Auto Skil Z", Default = false })

    Toggle:OnChanged(function(G)
       _G.AutoZ = G

spawn(function()
while wait(.1) do
    pcall(function()
if _G.AutoZ then
game:GetService("VirtualInputManager"):SendKeyEvent(true,"Z",false,game)
                end
        end)
   end
end)

    end)

    Options.MyToggle:SetValue(false)
    


    local Toggle = Tabs.Skil:AddToggle("Auto Skil X", {Title = "Auto Skil X", Default = false })

    Toggle:OnChanged(function(G)
       _G.AutoX = G

spawn(function()
while wait(.1) do
    pcall(function()
if _G.AutoX then
game:GetService("VirtualInputManager"):SendKeyEvent(true,"X",false,game)
                end
        end)
   end
end)

    end)

    Options.MyToggle:SetValue(false)


    local Toggle = Tabs.Skil:AddToggle("Auto Skil C", {Title = "Auto Skil C", Default = false })

    Toggle:OnChanged(function(G)
       _G.AutoC = G

spawn(function()
while wait(.1) do
    pcall(function()
if _G.AutoC then
game:GetService("VirtualInputManager"):SendKeyEvent(true,"C",false,game)
                end
        end)
   end
end)

    end)

    Options.MyToggle:SetValue(false)
 


    local Toggle = Tabs.Skil:AddToggle("Auto Skil V", {Title = "Auto Skil V", Default = false })

    Toggle:OnChanged(function(G)
       _G.AutoV = G

spawn(function()
while wait(.1) do
    pcall(function()
if _G.AutoV then
game:GetService("VirtualInputManager"):SendKeyEvent(true,"V",false,game)
                end
        end)
   end
end)

    end)

    Options.MyToggle:SetValue(false)


    local Toggle = Tabs.Fruit:AddToggle("Auto Random Fruit [Beli]", {Title = "Auto Random Fruit [Beli]", Default = false })
    Toggle:OnChanged(function(Random)
        _G.Fruit1 = Random 
        while _G. Fruit1 do wait()
for i,v in pairs(game:GetService("Workspace").Shop:GetDescendants()) do
if v.ClassName == "ProximityPrompt" then
fireproximityprompt(v,30)
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(790.203735, 35.5073013, 1201.40369, 0.026754817, -8.37544611e-09, 0.999642015, 1.24128064e-07, 1, 5.05623188e-09, -0.999642015, 1.23948354e-07, 0.026754817)
                    end
                end
            end
        end)

    local Toggle = Tabs.Fruit:AddToggle("Auto Random fruit Gem", {Title = "Auto Random fruit Gem", Default = false })
    Toggle:OnChanged(function(Random)
        _G.Fruit2 = Random
        while _G.Fruit2 do wait()
for i,v in pairs(game:GetService("Workspace").Shop:GetDescendants()) do
if v.ClassName == "ProximityPrompt" then
fireproximityprompt(v,30)
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-741.048889, 43.4787788, -1933.82019, -0.0251465552, 7.8026531e-08, 0.999683797, -1.09866749e-09, 1, -7.80788483e-08, -0.999683797, -3.06173398e-09, -0.0251465552)
end
end
end
    end)



players = {}

for i, v in pairs(game:GetService("Players"):GetChildren()) do
    table.insert(players, v.Name)
end

local DropdownPlayer = Tabs.TP:AddDropdown("Player", {
    Title = "Player",
    Values = players,
    Multi = false,
    Default = 1,
})

DropdownPlayer:SetValue("None")

DropdownPlayer:OnChanged(function(V)
    Select = V
end)

Tabs.TP:AddButton({
    Title = "Refresh",
    Description = "Refresh",
    Callback = function()
        Window:Dialog({
            Title = "Refresh",
            Content = "Refresh",
            Buttons = {
                {
                    Title = "Confirm",
                    Callback = function()
                        table.clear(players)
                        for i, v in pairs(game:GetService("Players"):GetChildren()) do
                            table.insert(players, v.Name)
                        end
                    end
                },
                {
                    Title = "Cancel",
                    Callback = function()
                        print("no")
                    end
                }
            }
        })
    end
})

Tabs.TP:AddButton({
    Title = "Teleport to Player",
    Description = "Teleport to the selected player",
    Callback = function()
        Window:Dialog({
            Title = "Teleport to Player",
            Content = "Teleport to the selected player",
            Buttons = {
                {
                    Title = "Confirm",
                    Callback = function()
                        game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
                    end
                },
                {
                    Title = "Cancel",
                    Callback = function()
                        print("no")
                    end
                }
            }
        })
    end
})


    shop = {}
for i ,v in pairs(game:GetService("Workspace").Shop:GetChildren()) do
table.insert(shop,v.Name)
end

Tabs.TP:AddDropdown("shop", {
        Title = "shop",
        Values = shop,
        Multi = false,
        Default = nil,
        Callback = function(ma)
        shop = ma
       end
   })



        Tabs.TP:AddButton({
        Title = "TP To Shop",
        Description = "",
        Callback = function()
      		for i,v in pairs(game:GetService("Workspace").Shop[shop]:GetDescendants()) do
if v.ClassName == "ProximityPrompt" then
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = v.Parent.CFrame * CFrame.new(0,5,0)
end
      end
        end
    })
    


map = {}
for i ,v in pairs(game:GetService("Workspace").Locations:GetChildren()) do
table.insert(map,v.Name)
end

Tabs.TP:AddDropdown("island", {
        Title = "island",
        Values = map,
        Multi = false,
        Default = nil,
        Callback = function(mt)
        map = mt
       end
   })
   
        Tabs.TP:AddButton({
        Title = "TP To island",
        Description = "TP To island",
        Callback = function()
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.workspace.Locations[map].CFrame * CFrame.new(0,-100,0)
        end
    })


        Tabs.TP:AddButton({
        Title = "Go to Traveling merchant",
        Description = "Go to Traveling merchant",
        Callback = function()
            for i,v in pairs(game:GetService("Workspace").NPC["Traveling merchant"]:GetDescendants()) do

if v.ClassName == "ProximityPrompt" then

game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = v.Parent.CFrame * CFrame.new(0,3,0)

wait(.1)

fireproximityprompt(v,30)

end

      end
        end
    })


local StatusRimuru = Tabs.Inventory:AddParagraph({
    Title = "Katana"
})

spawn(function()
    while wait() do
        pcall(function()
            if game.Players.LocalPlayer.PlayerGui.MainUI.Interface.Inventory.WeaponFrame:FindFirstChild("Katana") then
                StatusRimuru:SetTitle("Katana : ✅")
            else
                StatusRimuru:SetTitle("Katana : ❌")
            end
        end)
    end
end)

local Cutlass = Tabs.Inventory:AddParagraph({
    Title = "Cutlass"
})

spawn(function()
    while wait() do
        pcall(function()
            if game.Players.LocalPlayer.PlayerGui.MainUI.Interface.Inventory.WeaponFrame:FindFirstChild("Cutlass") then
                Cutlass:SetTitle("Cutlass : ✅")
            else
                Cutlass:SetTitle("Cutlass : ❌")
            end
        end)
    end
end)

local KashimoPoleCurse = Tabs.Inventory:AddParagraph({
    Title = "Kashimo's Pole V1 [Curse]"
})

spawn(function()
    while wait() do
        pcall(function()
            if game.Players.LocalPlayer.PlayerGui.MainUI.Interface.Inventory.WeaponFrame:FindFirstChild("Kashimo's Pole [Curse]") then
                KashimoPoleCurse:SetTitle("Kashimo's Pole V1 [Curse] : ✅")
            else
                KashimoPoleCurse:SetTitle("Kashimo's Pole V1 [Curse] : ❌")
            end
        end)
    end
end)

local KashimoPolePowerless = Tabs.Inventory:AddParagraph({
    Title = "Kashimo's Pole V2 [Powerless]"
})

spawn(function()
    while wait() do
        pcall(function()
            if game.Players.LocalPlayer.PlayerGui.MainUI.Interface.Inventory.WeaponFrame:FindFirstChild("Kashimo's Pole [Powerless]") then
                KashimoPolePowerless:SetTitle("Kashimo's Pole V2 [Powerless] : ✅")
            else
                KashimoPolePowerless:SetTitle("Kashimo's Pole V2 [Powerless] : ❌")
            end
        end)
    end
end)

local Saber = Tabs.Inventory:AddParagraph({
    Title = "Saber"
})

spawn(function()
    while wait() do
        pcall(function()
            if game.Players.LocalPlayer.PlayerGui.MainUI.Interface.Inventory.WeaponFrame:FindFirstChild("Saber") then
                Saber:SetTitle("Saber : ✅")
            else
                Saber:SetTitle("Saber : ❌")
            end
        end)
    end
end)

local Yoru = Tabs.Inventory:AddParagraph({
    Title = "Yoru"
})

spawn(function()
    while wait() do
        pcall(function()
            if game.Players.LocalPlayer.PlayerGui.MainUI.Interface.Inventory.WeaponFrame:FindFirstChild("Yoru") then
                Yoru:SetTitle("Yoru : ✅")
            else
                Yoru:SetTitle("Yoru : ❌")
            end
        end)
    end
end)

local Excalibur = Tabs.Inventory:AddParagraph({
    Title = "Excalibur"
})

spawn(function()
    while wait() do
        pcall(function()
            if game.Players.LocalPlayer.PlayerGui.MainUI.Interface.Inventory.WeaponFrame:FindFirstChild("Excalibur") then
                Excalibur:SetTitle("Excalibur : ✅")
            else
                Excalibur:SetTitle("Excalibur : ❌")
            end
        end)
    end
end)

local CidSword = Tabs.Inventory:AddParagraph({
    Title = "Cid's Sword"
})

spawn(function()
    while wait() do
        pcall(function()
            if game.Players.LocalPlayer.PlayerGui.MainUI.Interface.Inventory.WeaponFrame:FindFirstChild("Cid's Sword") then
                CidSword:SetTitle("Cid's Sword : ✅")
            else
                CidSword:SetTitle("Cid's Sword : ❌")
            end
        end)
    end
end)

local RimuruSword = Tabs.Inventory:AddParagraph({
    Title = "Rimuru's Sword"
})

spawn(function()
    while wait() do
        pcall(function()
            if game.Players.LocalPlayer.PlayerGui.MainUI.Interface.Inventory.WeaponFrame:FindFirstChild("Rimuru's Sword") then
                RimuruSword:SetTitle("Rimuru's Sword : ✅")
            else
                RimuruSword:SetTitle("Rimuru's Sword : ❌")
            end
        end)
    end
end)

local GodCheck = Tabs.Inventory:AddParagraph({
        Title = "God Light Fruit",
        Content = "Status : "
    })
    
    spawn(function()
                    while wait() do
                        pcall(function()
local LightFruit = 0
for _,v in pairs(game.Players[Players.LocalPlayer.Name].Backpack:GetChildren()) do
if v.Name == "God Light Fruit" then
    LightFruit = LightFruit + 1
GodCheck:SetDesc("God Light Fruit : "..(LightFruit))
else
  GodCheck:SetDesc("God Light Fruit : "..(LightFruit))
end
end
end)
end
end)

local DarkFlameCheck = Tabs.Inventory:AddParagraph({
        Title = "Dark Flame Fruit",
        Content = "Status : "
    })
    
    spawn(function()
                    while wait() do
                        pcall(function()
local FlameFruit = 0
for _,v in pairs(game.Players[Players.LocalPlayer.Name].Backpack:GetChildren()) do
if v.Name == "Dark Flame Fruit" then
    FlameFruit = FlameFruit + 1
DarkFlameCheck:SetDesc("Dark Flame Fruit: "..(FlameFruit))
else
  DarkFlameCheck:SetDesc("Dark Flame Fruit : "..(FlameFruit))
end
end
end)
end
end)

local FourLeaf = Tabs.Inventory:AddParagraph({
        Title = "Four Leaf Clover",
        Content = "Status : "
    })
    
       spawn(function()
                    while wait() do
                        pcall(function()
FourLeaf:SetDesc("Four Leaf Clover "..(game:GetService("Players").LocalPlayer.PlayerGui.MainUI.Interface.Inventory.ItemsFrame["1Four Leaf Clover"].Frame.Number.Text))
end)
end
end)

local Tensa = Tabs.Inventory:AddParagraph({
        Title = "Tensa Zangetsu",
        Content = "Status : "
    })
    
    spawn(function()
                    while wait() do
                        pcall(function()
Tensa:SetDesc("Tensa Zangetsu "..(
game:GetService("Players").LocalPlayer.PlayerGui.MainUI.Interface.Inventory.ItemsFrame["1Tensa Zangetsu"].Frame.Number.Text))
end)
end
end)

local Six = Tabs.Inventory:AddParagraph({
        Title = "Six Eyes",
        Content = "Status : "
    })
    
    spawn(function()
                    while wait() do
                        pcall(function()
Six:SetDesc("Six Eyes "..(game:GetService("Players").LocalPlayer.PlayerGui.MainUI.Interface.Inventory.ItemsFrame["1Six Eyes"].Frame.Number.Text))
end)
end
end)

local Haki = Tabs.Inventory:AddParagraph({
        Title = "Busoshoku Haki Book",
        Content = "Status : "
    })
    
    spawn(function()
                    while wait() do
                        pcall(function()
Haki:SetDesc("Busoshoku Haki Book "..(game:GetService("Players").LocalPlayer.PlayerGui.MainUI.Interface.Inventory.ItemsFrame["2Busoshoku Haki Book"].Frame.Number.Text))
end)
end
end)

local Club = Tabs.Inventory:AddParagraph({
        Title = "Club Card",
        Content = "Status : "
    })
    
    spawn(function()
                    while wait() do
                        pcall(function()
Club:SetDesc("Club Card "..(game:GetService("Players").LocalPlayer.PlayerGui.MainUI.Interface.Inventory.ItemsFrame["2Club Card"].Frame.Number.Text))
end)
end
end)

local Heart = Tabs.Inventory:AddParagraph({
        Title = "Heart Card",
        Content = "Status : "
    })
    
        spawn(function()
                    while wait() do
                        pcall(function()
Heart:SetDesc("Heart Card "..(game:GetService("Players").LocalPlayer.PlayerGui.MainUI.Interface.Inventory.ItemsFrame["2Heart Card"].Frame.Number.Text))
end)
end
end)

local Diamond = Tabs.Inventory:AddParagraph({
        Title = "Diamond Card",
        Content = "Status : "
    })
    
    spawn(function()
                    while wait() do
                        pcall(function()
Diamond:SetDesc("Diamond Card "..(game:GetService("Players").LocalPlayer.PlayerGui.MainUI.Interface.Inventory.ItemsFrame["2Diamond Card"].Frame.Number.Text))
end)
end
end)

local Infinity = Tabs.Inventory:AddParagraph({
        Title = "Infinity Orb",
        Content = "Status : "
    })
    
    spawn(function()
                    while wait() do
                        pcall(function()
Infinity:SetDesc("Infinity Orb "..(game:GetService("Players").LocalPlayer.PlayerGui.MainUI.Interface.Inventory.ItemsFrame["2Infinity Orb"].Frame.Number.Text))
end)
end
end)

local Kenbunshoku = Tabs.Inventory:AddParagraph({
        Title = "Kenbunshoku Haki Book",
        Content = "Status : "
    })
    
    spawn(function()
                    while wait() do
                        pcall(function()
Kenbunshoku:SetDesc("Kenbunshoku Haki Book "..(game:GetService("Players").LocalPlayer.PlayerGui.MainUI.Interface.Inventory.ItemsFrame["2Kenbunshoku Haki Book"].Frame.Number.Text))
end)
end
end)

local Lightning = Tabs.Inventory:AddParagraph({
        Title = "Lightning Orb",
        Content = "Status : "
    })
    
    spawn(function()
                    while wait() do
                        pcall(function()
Lightning:SetDesc("Lightning Orb "..(game:GetService("Players").LocalPlayer.PlayerGui.MainUI.Interface.Inventory.ItemsFrame["2Lightning Orb"].Frame.Number.Text))
end)
end
end)

local Race = Tabs.Inventory:AddParagraph({
        Title = "Race Reroll",
        Content = "Status : "
    })
    
    spawn(function()
                    while wait() do
                        pcall(function()
Race:SetDesc("Race Reroll "..(
game:GetService("Players").LocalPlayer.PlayerGui.MainUI.Interface.Inventory.ItemsFrame["2Race Reroll"].Frame.Number.Text))
end)
end
end)

local Choso = Tabs.Inventory:AddParagraph({
        Title = "[Choso] Cursed Womb",
        Content = "Status : "
    })
    
    spawn(function()
                    while wait() do
                        pcall(function()
Choso:SetDesc("[Choso] Cursed Womb "..(game:GetService("Players").LocalPlayer.PlayerGui.MainUI.Interface.Inventory.ItemsFrame["2[Choso] Cursed Womb"].Frame.Number.Text))
end)
end
end)

local Fishing = Tabs.Inventory:AddParagraph({
        Title = "Fishing Rod",
        Content = "Status : "
    })
    
    spawn(function()
                    while wait() do
                        pcall(function()
Fishing:SetDesc("Fishing Rod "..(game:GetService("Players").LocalPlayer.PlayerGui.MainUI.Interface.Inventory.ItemsFrame["3Fishing Rod"].Frame.Number.Text))
end)
end
end)

local HakiColor  = Tabs.Inventory:AddParagraph({
        Title = "Haki Color Reroll",
        Content = "Status : "
    })
    
    spawn(function()
                    while wait() do
                        pcall(function()
HakiColor:SetDesc("Haki Color Reroll "..(game:GetService("Players").LocalPlayer.PlayerGui.MainUI.Interface.Inventory.ItemsFrame["3Haki Color Reroll"].Frame.Number.Text))
end)
end
end)

local Holy  = Tabs.Inventory:AddParagraph({
        Title = "Holy Grail",
        Content = "Status : "
    })
    
    spawn(function()
                    while wait() do
                        pcall(function()
Holy:SetDesc("Haki Color Reroll "..(game:GetService("Players").LocalPlayer.PlayerGui.MainUI.Interface.Inventory.ItemsFrame["3Holy Grail"].Frame.Number.Text))
end)
end
end)

local Sukuna  = Tabs.Inventory:AddParagraph({
        Title = "Sukuna Finger",
        Content = "Status : "
    })
    
    spawn(function()
                    while wait() do
                        pcall(function()
Sukuna:SetDesc("Sukuna Finger "..(game:GetService("Players").LocalPlayer.PlayerGui.MainUI.Interface.Inventory.ItemsFrame["3SukunaFinger"].Frame.Number.Text))
end)
end
end)


-- Addons:
-- SaveManager (Allows you to have a configuration system)
-- InterfaceManager (Allows you to have a interface managment system)

-- Hand the library over to our managers
SaveManager:SetLibrary(Fluent)
InterfaceManager:SetLibrary(Fluent)

-- Ignore keys that are used by ThemeManager.
-- (we dont want configs to save themes, do we?)
SaveManager:IgnoreThemeSettings()

-- You can add indexes of elements the save manager should ignore
SaveManager:SetIgnoreIndexes({})

-- use case for doing it this way:
-- a script hub could have themes in a global folder
-- and game configs in a separate folder per game
InterfaceManager:SetFolder("FluentScriptHub")
SaveManager:SetFolder("FluentScriptHub/specific-game")

InterfaceManager:BuildInterfaceSection(Tabs.Settings)
SaveManager:BuildConfigSection(Tabs.Settings)


Window:SelectTab(1)


-- You can use the SaveManager:LoadAutoloadConfig() to load a config
-- which has been marked to be one that auto loads!
SaveManager:LoadAutoloadConfig()
