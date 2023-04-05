--[[local Hwid = {
    --["GayKong"] = ""
    ["Jinglen"] = "F7C22509-6CEF-4701-B6CF-8A0AC4BA45E2"
    ["033D5083"] = "033D5083-9501-4CDF-8906-F303BEC6C4CE"
}
local ClientId = game:GetService("RbxAnalyticsService"):GetClientId()
local Hwide = string.split((ClientId),"-")
local Key = Hwide[1]

if _G.Key == Key then
    if Hwid[_G.Key] == game:GetService("RbxAnalyticsService"):GetClientId() then]]--
if not game:IsLoaded() then 
    repeat game.Loaded:Wait()
    until game:IsLoaded() 
end
repeat wait(1)
    pcall(function()
        if game:GetService("Players").LocalPlayer.PlayerGui.Main:FindFirstChild("ChooseTeam") then
            if game:GetService("Players").LocalPlayer.PlayerGui.Main.ChooseTeam.Visible == true then
                if _G.Team == "Marines" then
                    for i,v in pairs(getconnections(game:GetService("Players").LocalPlayer.PlayerGui.Main.ChooseTeam.Container.Marines.Frame.ViewportFrame.TextButton.MouseButton1Click)) do
                        v.Function()
                    end
                else
                    for i,v in pairs(getconnections(game:GetService("Players").LocalPlayer.PlayerGui.Main.ChooseTeam.Container.Pirates.Frame.ViewportFrame.TextButton.MouseButton1Click)) do
                        v.Function()
                    end
                end
            end
        end
    end)
until game.Players.localPlayer.Neutral == false
if _G.Fast_Delay == nil then
	_G.Fast_Delay = 0.3
end
spawn(function()
    while true do wait()
        getgenv().rejoin = game:GetService("CoreGui").RobloxPromptGui.promptOverlay.ChildAdded:Connect(function(Kick)
            if not _G.TP_Ser and _G.Rejoin then
                if Kick.Name == 'ErrorPrompt' and Kick:FindFirstChild('MessageArea') and Kick.MessageArea:FindFirstChild("ErrorFrame") then
                    game:GetService("TeleportService"):Teleport(game.PlaceId)
                    wait(50)
                end
            end
        end)
    end
end)

local VirtualUser=game:service'VirtualUser'
game:service'Players'.LocalPlayer.Idled:connect(function()
	VirtualUser:CaptureController()
	VirtualUser:ClickButton2(Vector2.new())
end)

spawn(function()
	while wait(3) do
		game:GetService'VirtualUser':CaptureController()
	end
end)

Old_World = false
New_World = false
Three_World = false
local placeId = game.PlaceId
if placeId == 2753915549 then
    Old_World = true
elseif placeId == 4442272183 then
    New_World = true
elseif placeId == 7449423635 then
    Three_World = true
end
_G.Color = Color3.fromRGB(68, 202, 186)

_G.Setting_table = {
    Auto_Farm = false,
    FastAttack = true,
	Auto_Buso = true,
	Auto_Ken = true,
	Show_Damage = true,
	NoClip = true,
	Save_Member = true,
	Melee_A = true,
	Defense_A = true,
	SkillZ = true,
	Rejoin = true,
	Anti_AFK = true,
	K_MAX = 50,
	Chest_Lock = 50,
	Delay_C = 15
}

_G.Check_Save_Setting = "CheckSaveSetting"

getgenv()['JsonEncode'] = function(msg)
    return game:GetService("HttpService"):JSONEncode(msg)
end
getgenv()['JsonDecode'] = function(msg)
    return game:GetService("HttpService"):JSONDecode(msg)
end
getgenv()['Check_Setting'] = function(Name)
    if not _G.Dis and not isfolder('Switch Hub BF Premium') then
        makefolder('Switch Hub BF Premium')
    end
    if not _G.Dis and not isfile('Switch Hub BF Premium/'..Name..'.json') then
        writefile('Switch Hub BF Premium/'..Name..'.json',JsonEncode(_G.Setting_table))
    end
end
getgenv()['Get_Setting'] = function(Name)
    if not _G.Dis and isfolder('Switch Hub BF Premium') and isfile('Switch Hub BF Premium/'..Name..'.json') then
        _G.Setting_table = JsonDecode(readfile('Switch Hub BF Premium/'..Name..'.json'))
        return _G.Setting_table
	elseif not _G.Dis then
        Check_Setting(Name)
    end
end
getgenv()['Update_Setting'] = function(Name)
    if not _G.Dis and isfolder('Switch Hub BF Premium') and isfile('Switch Hub BF Premium/'..Name..'.json') then
        writefile('Switch Hub BF Premium/'..Name..'.json',JsonEncode(_G.Setting_table))
	elseif not _G.Dis then
        Check_Setting(Name)
    end
end

Check_Setting(_G.Check_Save_Setting)
Get_Setting(_G.Check_Save_Setting)

if _G.Setting_table.Save_Member then
	getgenv()['MyName'] = game.Players.LocalPlayer.Name
	print("Save Member")
elseif _G.Setting_table.Save_All_Member then
	getgenv()['MyName'] = "AllMember"
	print("Save All Member")
else
	getgenv()['MyName'] = "None"
	_G.Dis = true
end

Check_Setting(getgenv()['MyName'])
Get_Setting(getgenv()['MyName'])

_G.Setting_table.Key = _G.wl_key
Update_Setting(getgenv()['MyName'])

if type(_G.Setting_table.Weapon) ~= 'string' then
	for i2,v2 in pairs(game.Players.LocalPlayer.Backpack:GetChildren()) do  
		if tostring(v2.ToolTip) == "Melee" then
			_G.Setting_table.Weapon = v2.Name
		end
	end
end


function Text(value)
    game.StarterGui:SetCore("SendNotification", {
        Title = "King of god hub", 
        Text = tostring(value),
        Duration = 10
    })
end
function Com()
    game.StarterGui:SetCore("SendNotification", {
        Title = "King of god hub", 
        Text = "✅  Complete",
        Duration = 5
    })
end

function TC(p)
	if (p.Position-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude >= 2000 then
	    TP3(CFrame.new(-2151.62353515625, 69.98303985595703, -12403.9228515625))
	end
end

function TelePBoss(p)
	if (p.Position-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude >= 2000 and not Auto_Raid and game.Players.LocalPlayer.Character.Humanoid.Health > 0 then
		if NameQuest == "FishmanQuest" then
			_G.Stop_Tween = true
			TP(game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame)
			wait(.5)
			game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(61163.8515625, 11.6796875, 1819.7841796875))
			_G.Stop_Tween = nil
		elseif Ms == "God's Guard [Lv. 450]"  then
			_G.Stop_Tween = true
			TP(game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame)
			wait(.5)
			game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(-4607.82275, 872.54248, -1667.55688))
			_G.Stop_Tween = nil
		elseif NameQuest == "SkyExp1Quest" then
			_G.Stop_Tween = true
			TP(game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame)
			wait(.5)
			game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(-7894.6176757813, 5547.1416015625, -380.29119873047))
			_G.Stop_Tween = nil
		elseif NameQuest == "ShipQuest1" then
			_G.Stop_Tween = true
			TP(game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame)
			wait(.5)
			game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(923.21252441406, 126.9760055542, 32852.83203125))
			_G.Stop_Tween = nil
		elseif NameQuest == "ShipQuest2" then
			_G.Stop_Tween = true
			TP(game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame)
			wait(.5)
			game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(923.21252441406, 126.9760055542, 32852.83203125))
			_G.Stop_Tween = nil
		elseif NameQuest == "FrostQuest" then
			_G.Stop_Tween = true
			TP(game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame)
			wait(.5)
			game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(-6508.5581054688, 89.034996032715, -132.83953857422))
			_G.Stop_Tween = nil
		else
			Mix_Farm = true
			_G.Stop_Tween = true
			game.Players.LocalPlayer.Character.Humanoid:ChangeState(15)
			repeat wait(.5)
				game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = p
				wait()
				game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("SetSpawnPoint")
			until (p.Position-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude < 1500 and game.Players.LocalPlayer.Character.Humanoid.Health > 0
			wait(.5)
			_G.Stop_Tween = nil
			Mix_Farm = nil
		end
	end
end

function CheckQuestBoss()
	-- Old World
		if _G.SelectBoss == "Saber Expert [Lv. 200] [Boss]" then
			MsBoss = "Saber Expert [Lv. 200] [Boss]"
			NameBoss = "Saber Expert"
			CFrameBoss = CFrame.new(-1458.89502, 29.8870335, -50.633564, 0.858821094, 1.13848939e-08, 0.512275636, -4.85649254e-09, 1, -1.40823326e-08, -0.512275636, 9.6063415e-09, 0.858821094)
		elseif _G.SelectBoss == "The Saw [Lv. 100] [Boss]" then
			MsBoss = "The Saw [Lv. 100] [Boss]"
			NameBoss = "The Saw"
			CFrameBoss = CFrame.new(-683.519897, 13.8534927, 1610.87854, -0.290192783, 6.88365773e-08, 0.956968188, 6.98413629e-08, 1, -5.07531119e-08, -0.956968188, 5.21077759e-08, -0.290192783)
		elseif _G.SelectBoss == "Greybeard [Lv. 750] [Raid Boss]" then
			MsBoss = "Greybeard [Lv. 750] [Raid Boss]"
			NameBoss = "Greybeard"
			CFrameBoss = CFrame.new(-4955.72949, 80.8163834, 4305.82666, -0.433646321, -1.03394289e-08, 0.901083171, -3.0443168e-08, 1, -3.17633075e-09, -0.901083171, -2.88092288e-08, -0.433646321)
		elseif _G.SelectBoss == "The Gorilla King [Lv. 25] [Boss]" then
			MsBoss = "The Gorilla King [Lv. 25] [Boss]" 
			NameBoss = "The Gorilla King"
			NameQuestBoss = "JungleQuest"
			QuestLvBoss = 3
			CFrameQBoss = CFrame.new(-1604.12012, 36.8521118, 154.23732, 0.0648873374, -4.70858913e-06, -0.997892559, 1.41431883e-07, 1, -4.70933674e-06, 0.997892559, 1.64442184e-07, 0.0648873374)
			CFrameBoss = CFrame.new(-1223.52808, 6.27936459, -502.292664, 0.310949147, -5.66602516e-08, 0.950426519, -3.37275488e-08, 1, 7.06501808e-08, -0.950426519, -5.40241736e-08, 0.310949147)
			TelePBoss(CFrameBoss)
		elseif _G.SelectBoss == "Bobby [Lv. 55] [Boss]" then
			MsBoss = "Bobby [Lv. 55] [Boss]"
			NameBoss = "Bobby"
			NameQuestBoss = "BuggyQuest1"
			QuestLvBoss = 3
			CFrameQBoss = CFrame.new(-1139.59717, 4.75205183, 3825.16211, -0.959730506, -7.5857054e-09, 0.280922383, -4.06310328e-08, 1, -1.11807175e-07, -0.280922383, -1.18718916e-07, -0.959730506)
			CFrameBoss = CFrame.new(-1147.65173, 32.5966301, 4156.02588, 0.956680477, -1.77109952e-10, -0.29113996, 5.16530874e-10, 1, 1.08897802e-09, 0.29113996, -1.19218679e-09, 0.956680477)
			TelePBoss(CFrameBoss)
		elseif _G.SelectBoss == "Yeti [Lv. 110] [Boss]" then
			MsBoss = "Yeti [Lv. 110] [Boss]"
			NameBoss = "Yeti"
			NameQuestBoss = "SnowQuest"
			QuestLvBoss = 3
			CFrameQBoss = CFrame.new(1384.90247, 87.3078308, -1296.6825, 0.280209213, 2.72035177e-08, -0.959938943, -6.75690828e-08, 1, 8.6151708e-09, 0.959938943, 6.24481444e-08, 0.280209213)
			CFrameBoss = CFrame.new(1221.7356, 138.046906, -1488.84082, 0.349343032, -9.49245944e-08, 0.936994851, 6.29478194e-08, 1, 7.7838429e-08, -0.936994851, 3.17894653e-08, 0.349343032)
			TelePBoss(CFrameBoss)
		elseif _G.SelectBoss == "Mob Leader [Lv. 120] [Boss]" then
			MsBoss = "Mob Leader [Lv. 120] [Boss]"
			NameBoss = "Mob Leader"
			CFrameBoss = CFrame.new(-2848.59399, 7.4272871, 5342.44043, -0.928248107, -8.7248246e-08, 0.371961564, -7.61816636e-08, 1, 4.44474857e-08, -0.371961564, 1.29216433e-08, -0.92824)
		elseif _G.SelectBoss == "Vice Admiral [Lv. 130] [Boss]" then
			MsBoss = "Vice Admiral [Lv. 130] [Boss]"
			NameBoss = "Vice Admiral"
			NameQuestBoss = "MarineQuest2"
			QuestLvBoss = 2
			CFrameQBoss = CFrame.new(-5035.42285, 28.6520386, 4324.50293, -0.0611100644, -8.08395768e-08, 0.998130739, -1.57416586e-08, 1, 8.00271849e-08, -0.998130739, -1.08217701e-08, -0.0611100644)
			CFrameBoss = CFrame.new(-5078.45898, 99.6520691, 4402.1665, -0.555574954, -9.88630566e-11, 0.831466436, -6.35508286e-08, 1, -4.23449258e-08, -0.831466436, -7.63661632e-08, -0.555574954)
			TelePBoss(CFrameBoss)
		elseif _G.SelectBoss == "Warden [Lv. 220] [Boss]" then
			MsBoss = "Warden [Lv. 220] [Boss]"
			NameBoss = "Warden"
			NameQuestBoss = "ImpelQuest"
			QuestLvBoss = 1
			CFrameQBoss = CFrame.new(4851.35059, 5.68744135, 743.251282, -0.538484037, -6.68303741e-08, -0.842635691, 1.38001752e-08, 1, -8.81300792e-08, 0.842635691, -5.90851599e-08, -0.538484037)
			CFrameBoss = CFrame.new(5232.5625, 5.26856995, 747.506897, 0.943829298, -4.5439414e-08, 0.330433697, 3.47818627e-08, 1, 3.81658154e-08, -0.330433697, -2.45289105e-08, 0.943829298)
			TelePBoss(CFrameBoss)
		elseif _G.SelectBoss == "Chief Warden [Lv. 230] [Boss]" then
			MsBoss = "Chief Warden [Lv. 230] [Boss]"
			NameBoss = "Chief Warden"
			NameQuestBoss = "ImpelQuest"
			QuestLvBoss = 2
			CFrameQBoss = CFrame.new(4851.35059, 5.68744135, 743.251282, -0.538484037, -6.68303741e-08, -0.842635691, 1.38001752e-08, 1, -8.81300792e-08, 0.842635691, -5.90851599e-08, -0.538484037)
			CFrameBoss = CFrame.new(5232.5625, 5.26856995, 747.506897, 0.943829298, -4.5439414e-08, 0.330433697, 3.47818627e-08, 1, 3.81658154e-08, -0.330433697, -2.45289105e-08, 0.943829298)
			TelePBoss(CFrameBoss)
		elseif _G.SelectBoss == "Swan [Lv. 240] [Boss]" then
			MsBoss = "Swan [Lv. 240] [Boss]"
			NameBoss = "Swan"
			NameQuestBoss = "ImpelQuest"
			QuestLvBoss = 3
			CFrameQBoss = CFrame.new(4851.35059, 5.68744135, 743.251282, -0.538484037, -6.68303741e-08, -0.842635691, 1.38001752e-08, 1, -8.81300792e-08, 0.842635691, -5.90851599e-08, -0.538484037)
			CFrameBoss = CFrame.new(5232.5625, 5.26856995, 747.506897, 0.943829298, -4.5439414e-08, 0.330433697, 3.47818627e-08, 1, 3.81658154e-08, -0.330433697, -2.45289105e-08, 0.943829298)
			TelePBoss(CFrameBoss)
		elseif _G.SelectBoss == "Magma Admiral [Lv. 350] [Boss]" then
			MsBoss = "Magma Admiral [Lv. 350] [Boss]"
			NameBoss = "Magma Admiral"
			NameQuestBoss = "MagmaQuest"
			QuestLvBoss = 3
			CFrameQBoss = CFrame.new(-5317.07666, 12.2721891, 8517.41699, 0.51175487, -2.65508806e-08, -0.859131515, -3.91131572e-08, 1, -5.42026761e-08, 0.859131515, 6.13418294e-08, 0.51175487)
			CFrameBoss = CFrame.new(-5530.12646, 22.8769703, 8859.91309, 0.857838571, 2.23414389e-08, 0.513919294, 1.53689133e-08, 1, -6.91265853e-08, -0.513919294, 6.71978384e-08, 0.857838571)
			TelePBoss(CFrameBoss)
		elseif _G.SelectBoss == "Fishman Lord [Lv. 425] [Boss]" then
			MsBoss = "Fishman Lord [Lv. 425] [Boss]"
			NameBoss = "Fishman Lord"
			NameQuestBoss = "FishmanQuest"
			QuestLvBoss = 3
			CFrameQBoss = CFrame.new(61123.0859, 18.5066795, 1570.18018, 0.927145958, 1.0624845e-07, 0.374700129, -6.98219367e-08, 1, -1.10790765e-07, -0.374700129, 7.65569368e-08, 0.927145958)
			CFrameBoss = CFrame.new(61351.7773, 31.0306778, 1113.31409, 0.999974668, 0, -0.00714713801, 0, 1.00000012, 0, 0.00714714266, 0, 0.999974549)
			if (CFrameQBoss.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 3000 then
				game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(61163.8515625, 11.6796875, 1819.7841796875))
			end
		elseif _G.SelectBoss == "Wysper [Lv. 500] [Boss]" then
			MsBoss = "Wysper [Lv. 500] [Boss]"
			NameBoss = "Wysper"
			NameQuestBoss = "SkyExp1Quest"
			QuestLvBoss = 3
			CFrameQBoss = CFrame.new(-7862.94629, 5545.52832, -379.833954, 0.462944925, 1.45838088e-08, -0.886386991, 1.0534996e-08, 1, 2.19553424e-08, 0.886386991, -1.95022007e-08, 0.462944925)
			CFrameBoss = CFrame.new(-7925.48389, 5550.76074, -636.178345, 0.716468513, -1.22915289e-09, 0.697619379, 3.37381434e-09, 1, -1.70304748e-09, -0.697619379, 3.57381835e-09, 0.716468513)
			if (CFrameQBoss.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 3000 then
				game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(-4607.82275, 872.54248, -1667.55688))
			end
		elseif _G.SelectBoss == "Thunder God [Lv. 575] [Boss]" then
			MsBoss = "Thunder God [Lv. 575] [Boss]"
			NameBoss = "Thunder God"
			NameQuestBoss = "SkyExp2Quest"
			QuestLvBoss = 3
			CFrameQBoss = CFrame.new(-7902.78613, 5635.99902, -1411.98706, -0.0361216255, -1.16895912e-07, 0.999347389, 1.44533963e-09, 1, 1.17024491e-07, -0.999347389, 5.6715117e-09, -0.0361216255)
			CFrameBoss = CFrame.new(-7917.53613, 5616.61377, -2277.78564, 0.965189934, 4.80563429e-08, -0.261550069, -6.73089886e-08, 1, -6.46515304e-08, 0.261550069, 8.00056768e-08, 0.965189934)
			if (CFrameQBoss.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 3000 then
				game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(61163.8515625, 11.6796875, 1819.7841796875))
			end
			TelePBoss(CFrameBoss)
		elseif _G.SelectBoss == "Cyborg [Lv. 675] [Boss]" then
			MsBoss = "Cyborg [Lv. 675] [Boss]"
			NameBoss = "Cyborg"
			NameQuestBoss = "FountainQuest"
			QuestLvBoss = 3
			CFrameQBoss = CFrame.new(5253.54834, 38.5361786, 4050.45166, -0.0112687312, -9.93677887e-08, -0.999936521, 2.55291371e-10, 1, -9.93769547e-08, 0.999936521, -1.37512213e-09, -0.0112687312)
			CFrameBoss = CFrame.new(6041.82813, 52.7112198, 3907.45142, -0.563162148, 1.73805248e-09, -0.826346457, -5.94632716e-08, 1, 4.26280238e-08, 0.826346457, 7.31437524e-08, -0.563162148)
			TelePBoss(CFrameBoss)
		-- New World
		elseif _G.SelectBoss == "Diamond [Lv. 750] [Boss]" then
			MsBoss = "Diamond [Lv. 750] [Boss]"
			NameBoss = "Diamond"
			NameQuestBoss = "Area1Quest"
			QuestLvBoss = 3
			CFrameQBoss = CFrame.new(-424.080078, 73.0055847, 1836.91589, 0.253544956, -1.42165932e-08, 0.967323601, -6.00147771e-08, 1, 3.04272909e-08, -0.967323601, -6.5768397e-08, 0.253544956)
			CFrameBoss = CFrame.new(-1736.26587, 198.627731, -236.412857, -0.997808516, 0, -0.0661673471, 0, 1, 0, 0.0661673471, 0, -0.997808516)
			TelePBoss(CFrameBoss)
		elseif _G.SelectBoss == "Jeremy [Lv. 850] [Boss]" then
			MsBoss = "Jeremy [Lv. 850] [Boss]"
			NameBoss = "Jeremy"
			NameQuestBoss = "Area2Quest"
			QuestLvBoss = 3
			CFrameQBoss = CFrame.new(632.698608, 73.1055908, 918.666321, -0.0319722369, 8.96074881e-10, -0.999488771, 1.36326533e-10, 1, 8.92172336e-10, 0.999488771, -1.07732087e-10, -0.0319722369)
			CFrameBoss = CFrame.new(2203.76953, 448.966034, 752.731079, -0.0217453763, 0, -0.999763548, 0, 1, 0, 0.999763548, 0, -0.0217453763)
			TelePBoss(CFrameBoss)
		elseif _G.SelectBoss == "Fajita [Lv. 925] [Boss]" then
			MsBoss = "Fajita [Lv. 925] [Boss]"
			NameBoss = "Fajita"
			NameQuestBoss = "MarineQuest3"
			QuestLvBoss = 3
			CFrameQBoss = CFrame.new(-2442.65015, 73.0511475, -3219.11523, -0.873540044, 4.2329841e-08, -0.486752301, 5.64383384e-08, 1, -1.43220786e-08, 0.486752301, -3.99823996e-08, -0.873540044)
			CFrameBoss = CFrame.new(-2297.40332, 115.449463, -3946.53833, 0.961227536, -1.46645796e-09, -0.275756449, -2.3212845e-09, 1, -1.34094433e-08, 0.275756449, 1.35296352e-08, 0.961227536)
			TelePBoss(CFrameBoss)
		elseif _G.SelectBoss == "Don Swan [Lv. 1000] [Boss]" then
			MsBoss = "Don Swan [Lv. 1000] [Boss]"
			NameBoss = "Don Swan"
			CFrameBoss = CFrame.new(2288.802, 15.1870775, 863.034607, 0.99974072, -8.41247214e-08, -0.0227668174, 8.4774733e-08, 1, 2.75850098e-08, 0.0227668174, -2.95079072e-08, 0.99974072)
			TelePBoss(CFrameBoss)
		elseif _G.SelectBoss == "Smoke Admiral [Lv. 1150] [Boss]" then
			MsBoss = "Smoke Admiral [Lv. 1150] [Boss]"
			NameBoss = "Smoke Admiral"
			NameQuestBoss = "IceSideQuest"
			QuestLvBoss = 3
			CFrameQBoss = CFrame.new(-6059.96191, 15.9868021, -4904.7373, -0.444992423, -3.0874483e-09, 0.895534337, -3.64098796e-08, 1, -1.4644522e-08, -0.895534337, -3.91229982e-08, -0.444992423)
			CFrameBoss = CFrame.new(-5115.72754, 23.7664986, -5338.2207, 0.251453817, 1.48345061e-08, -0.967869282, 4.02796978e-08, 1, 2.57916977e-08, 0.967869282, -4.54708946e-08, 0.251453817)
			TelePBoss(CFrameBoss)
		elseif _G.SelectBoss == "Cursed Captain [Lv. 1325] [Raid Boss]" then
			MsBoss = "Cursed Captain [Lv. 1325] [Raid Boss]"
			NameBoss = "Cursed Captain"
			CFrameBoss = CFrame.new(916.928589, 181.092773, 33422, -0.999505103, 9.26310495e-09, 0.0314563364, 8.42916226e-09, 1, -2.6643713e-08, -0.0314563364, -2.63653774e-08, -0.999505103)
		elseif _G.SelectBoss == "Darkbeard [Lv. 1000] [Raid Boss]" then
			MsBoss = "Darkbeard [Lv. 1000] [Raid Boss]"
			NameBoss = "Darkbeard"
			CFrameBoss = CFrame.new(3876.00366, 24.6882591, -3820.21777, -0.976951957, 4.97356325e-08, 0.213458836, 4.57335361e-08, 1, -2.36868622e-08, -0.213458836, -1.33787044e-08, -0.976951957)
		elseif _G.SelectBoss == "Order [Lv. 1250] [Raid Boss]" then
			MsBoss = "Order [Lv. 1250] [Raid Boss]"
			NameBoss = "Order"
			CFrameBoss = CFrame.new(-6221.15039, 16.2351036, -5045.23584, -0.380726993, 7.41463495e-08, 0.924687505, 5.85604774e-08, 1, -5.60738549e-08, -0.924687505, 3.28013137e-08, -0.380726993)
		elseif _G.SelectBoss == "Awakened Ice Admiral [Lv. 1400] [Boss]" then
			MsBoss = "Awakened Ice Admiral [Lv. 1400] [Boss]"
			NameBoss = "Awakened Ice Admiral"
			NameQuestBoss = "FrostQuest"
			QuestLvBoss = 3
			CFrameQBoss = CFrame.new(5669.33203, 28.2118053, -6481.55908, 0.921275556, -1.25320829e-08, 0.388910472, 4.72230788e-08, 1, -7.96414241e-08, -0.388910472, 9.17372489e-08, 0.921275556)
			CFrameBoss = CFrame.new(6407.33936, 340.223785, -6892.521, 0.49051559, -5.25310213e-08, -0.871432424, -2.76146022e-08, 1, -7.58250565e-08, 0.871432424, 6.12576301e-08, 0.49051559)
			TelePBoss(CFrameBoss)
		elseif _G.SelectBoss == "Tide Keeper [Lv. 1475] [Boss]" then
			MsBoss = "Tide Keeper [Lv. 1475] [Boss]"
			NameBoss = "Tide Keeper"
			NameQuestBoss = "ForgottenQuest"             
			QuestLvBoss = 3
			CFrameQBoss = CFrame.new(-3053.89648, 236.881363, -10148.2324, -0.985987961, -3.58504737e-09, 0.16681771, -3.07832915e-09, 1, 3.29612559e-09, -0.16681771, 2.73641976e-09, -0.985987961)
			CFrameBoss = CFrame.new(-3570.18652, 123.328949, -11555.9072, 0.465199202, -1.3857326e-08, 0.885206044, 4.0332897e-09, 1, 1.35347511e-08, -0.885206044, -2.72606271e-09, 0.465199202)
			TelePBoss(CFrameBoss)
		-- Thire World
		elseif _G.SelectBoss == "Stone [Lv. 1550] [Boss]" then
			MsBoss = "Stone [Lv. 1550] [Boss]"
			NameBoss = "Stone"
			NameQuestBoss = "PiratePortQuest"             
			QuestLvBoss = 3
			CFrameQBoss = CFrame.new(-290, 44, 5577)
			CFrameBoss = CFrame.new(-1085, 40, 6779)
			TelePBoss(CFrameBoss)
		elseif _G.SelectBoss == "Island Empress [Lv. 1675] [Boss]" then
			MsBoss = "Island Empress [Lv. 1675] [Boss]"
			NameBoss = "Island Empress"
			NameQuestBoss = "AmazonQuest2"             
			QuestLvBoss = 3
			CFrameQBoss = CFrame.new(5443, 602, 752)
			CFrameBoss = CFrame.new(5659, 602, 244)
			if (MsBoss.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 3000 then
				game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(5741.791015625, 610.4240112304688, -269.8805847167969))
			end
			TelePBoss(CFrameBoss)
		elseif _G.SelectBoss == "Kilo Admiral [Lv. 1750] [Boss]" then
			MsBoss = "Kilo Admiral [Lv. 1750] [Boss]"
			NameBoss = "Kilo Admiral"
			NameQuestBoss = "MarineTreeIsland"             
			QuestLvBoss = 3
			CFrameQBoss = CFrame.new(2178, 29, -6737)
			CFrameBoss =CFrame.new(2846, 433, -7100)
			TelePBoss(CFrameBoss)
		elseif _G.SelectBoss == "Captain Elephant [Lv. 1875] [Boss]" then
			MsBoss = "Captain Elephant [Lv. 1875] [Boss]"
			NameBoss = "Captain Elephant"
			NameQuestBoss = "DeepForestIsland"             
			QuestLvBoss = 3
			CFrameQBoss = CFrame.new(-13232, 333, -7631)
			CFrameBoss = CFrame.new(-13221, 325, -8405)
			if (MsBoss.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 3000 then
				game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(-12476.8515625, 374.9144592285156, -7567.9111328125))
			end
			TelePBoss(CFrameBoss)
		elseif _G.SelectBoss == "Beautiful Pirate [Lv. 1950] [Boss]" then
			MsBoss = "Beautiful Pirate [Lv. 1950] [Boss]"
			NameBoss = "Beautiful Pirate"
			NameQuestBoss = "DeepForestIsland2"             
			QuestLvBoss = 3
			CFrameQBoss = CFrame.new(-12686, 391, -9902)
			CFrameBoss = CFrame.new(5182, 23, -20)
			if (MsBoss.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 3000 then
				game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(5314.58203125, 22.53643226623535, -125.94227600097656))
			end
			TelePBoss(CFrameBoss)
		elseif _G.SelectBoss == "rip_indra True Form [Lv. 5000] [Raid Boss]" then
			MsBoss = "rip_indra True Form [Lv. 5000] [Raid Boss]"
			NameBoss = "rip_indra True Form"
			CFrameBoss = CFrame.new(-5359, 424, -2735)
			TelePBoss(CFrameBoss)
		elseif _G.SelectBoss == "Longma [Lv. 2000] [Boss]" then
			MsBoss = "Longma [Lv. 2000] [Boss]"
			NameBoss = "Longma"
			CFrameBoss = CFrame.new(-10248.3936, 353.79129, -9306.34473)
			TelePBoss(CFrameBoss)
		elseif _G.SelectBoss == "Soul Reaper [Lv. 2100] [Raid Boss]" then
			MsBoss = "Soul Reaper [Lv. 2100] [Raid Boss]"
			NameBoss = "Soul Reaper"
			CFrameBoss = CFrame.new(-9515.62109, 315.925537, 6691.12012)
			TelePBoss(CFrameBoss)
		elseif _G.SelectBoss == "Cake Queen [Lv. 2175] [Boss]" then
			MsBoss = "Cake Queen [Lv. 2175] [Boss]"
			NameBoss = "Cake Queen"
			NameQuestBoss = "IceCreamIslandQuest"             
			QuestLvBoss = 3
			CFrameQBoss = CFrame.new(-821.267456, 65.9448776, -10964.3994, 0.814093888, -3.67296735e-08, -0.58073324, 3.30765637e-08, 1, -1.6879099e-08, 0.58073324, -5.46748513e-09, 0.814093888)
			CFrameBoss = CFrame.new(-715.467102, 381.69104, -11019.8896, 0.955998719, -1.07319993e-08, -0.293370903, 5.00311881e-09, 1, -2.02781667e-08, 0.293370903, 1.7918131e-08, 0.955998719)
			TelePBoss(CFrameBoss)
		end
	end

		function CheckLevel()
			local Lv = game:GetService("Players").LocalPlayer.Data.Level.Value
			if Old_World then
				if Lv == 1 or Lv <= 9 or SelectMonster == "Bandit [Lv. 5]" then -- Bandit
					Ms = "Bandit [Lv. 5]"
					NameQuest = "BanditQuest1"
					QuestLv = 1
					NameMon = "Bandit"
					CFrameQ = CFrame.new(1060.9383544922, 16.455066680908, 1547.7841796875)
					CFrameMon = CFrame.new(932.8062133789062, 50.273521423339844, 1515.4857177734375)
					CFrameMon2 = CFrame.new(1020.5850830078125, 50.273521423339844, 1566.209228515625)
					CFrameMon3 = CFrame.new(951.9865112304688, 50.273590087890625, 1624.841064453125)
					CFrameMon4 = CFrame.new(1100.512939453125, 50.273609161376953, 1593.30859375)
					CFrameMon5 = CFrame.new(1123.3743896484375, 50.273609161376953, 1663.6324462890625)
					CFrameMon6 = CFrame.new(1219.28308, 50.4678574, 1676.11877)
					CFrameMon7 = CFrame.new(1284.30542, 50.7171984, 1627.62842)
					CFrameMon8 = CFrame.new(1231.89722, 50.4568367, 1541.047)
				elseif Lv == 10 or Lv <= 14 or SelectMonster == "Monkey [Lv. 14]" then -- Monkey
					Ms = "Monkey [Lv. 14]"
					NameQuest = "JungleQuest"
					QuestLv = 1
					NameMon = "Monkey"
					CFrameQ = CFrame.new(-1601.6553955078, 36.85213470459, 153.38809204102)
					CFrameMon = CFrame.new(-1578.40002, 40.0510254, 376.473907)
					CFrameMon2 = CFrame.new(-1202.49963, 40.5991755, 278.730499)
					CFrameMon3 = CFrame.new(-1291.31116, 40.1025791, -4.68253756)
					CFrameMon4 = CFrame.new(-1489.24976, 40.550066, 88.4902802)
					CFrameMon5 = CFrame.new(-1610.48572, 40.3196087, -48.0345688)
					CFrameMon6 = CFrame.new(-1743.51038, 40.3173809, -91.2508316)
					CFrameMon7 = CFrame.new(-1800.5564, 40.7170601, 109.951523)
					CFrameMon8 = CFrame.new(-1800.5564, 40.7170601, 109.951523)
				elseif Lv == 15 or Lv <= 29 or SelectMonster == "Gorilla [Lv. 20]" then -- Gorilla
					Ms = "Gorilla [Lv. 20]"
					NameQuest = "JungleQuest"
					QuestLv = 2
					NameMon = "Gorilla"
					CFrameQ = CFrame.new(-1601.6553955078, 36.85213470459, 153.38809204102)
					CFrameMon = CFrame.new(-1362.0625, 30.8125114, -487.021637)
					CFrameMon2 = CFrame.new(-1249.05078, 30.01767778, -456.178711)
					CFrameMon3 = CFrame.new(-1248.04932, 30.0324049, -548.841492)
					CFrameMon4 = CFrame.new(-1188.06848, 30.0483704, -650.220398)
					CFrameMon5 = CFrame.new(-1362.0625, 30.8125114, -487.021637)
					CFrameMon6 = CFrame.new(-1249.05078, 30.01767778, -456.178711)
					CFrameMon7 = CFrame.new(-1248.04932, 30.0324049, -548.841492)
					CFrameMon8 = CFrame.new(-1188.06848, 30.0483704, -650.220398)
				elseif Lv == 30 or Lv <= 119 or SelectMonster == "Royal Squad [Lv. 525]" then -- Shanda
					_G.FM = false
					Ms = "Royal Squad [Lv. 525]"
					NameQuest = "JungleQuest"
					QuestLv = 2
					NameMon = "Gorila"
					CFrameQ = CFrame.new(-7863.1596679688, 5545.5190429688, -378.42266845703)
					CFrameMon = CFrame.new(-7787.81494140625, 5600.49169921875, -502.2948303222656)
					CFrameMon2 = CFrame.new(-7725.74072, 5600.29004, -585.480713)
					CFrameMon3 = CFrame.new(-7595.16895, 5600.93994, -653.530457)
					CFrameMon4 = CFrame.new(-7540.33887, 5600.27539, -517.048096)
					CFrameMon5 = CFrame.new(-7564.64746, 5600.68262, -418.750336)
					CFrameMon6 = CFrame.new(-7564.64746, 5600.68262, -418.750336)
					CFrameMon7 = CFrame.new(-7709.42822, 5600.29492, -337.002502)
					CFrameMon8 = CFrame.new(-7709.42822, 5600.29492, -337.002502)
					if Auto_Farm and (CFrameMon.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 3000 then
						game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(-7894.6176757813, 5547.1416015625, -380.29119873047))
					end
					
				elseif Lv == 120 or Lv <= 149 or SelectMonster == "Chief Petty Officer [Lv. 120]" then -- Chief Petty Officer
					Ms = "Chief Petty Officer [Lv. 120]"
					NameQuest = "MarineQuest2"
					QuestLv = 1
					NameMon = "Chief Petty Officer"
					CFrameQ = CFrame.new(-5035.49609375, 28.677835464478, 4324.1840820313)
					CFrameMon = CFrame.new(-4923.10791, 40.3499947, 4076.94336)
					CFrameMon2 = CFrame.new(-4805.28809, 40.090353, 3993.9248)
					CFrameMon3 = CFrame.new(-4989.27148, 40.0766487, 3947.69263)
					CFrameMon4 = CFrame.new(-5121.31006, 40.1290245, 4059.63696)
					CFrameMon5 = CFrame.new(-4615.01855, 40.3923702, 4415.97705)
					CFrameMon6 = CFrame.new(-4634.14697, 40.3546143, 4551.83789)
					CFrameMon7 = CFrame.new(-4808.26562, 40.5440979, 4540.03223)
					CFrameMon8 = CFrame.new(-4873.88184, 40.0598965, 4655.65576)
				elseif Lv == 150 or Lv <= 174 or SelectMonster == "Sky Bandit [Lv. 150]" then -- Sky Bandit
					Ms = "Sky Bandit [Lv. 150]"
					NameQuest = "SkyQuest"
					QuestLv = 1
					NameMon = "Sky Bandit"
					CFrameQ = CFrame.new(-4842.1372070313, 717.69543457031, -2623.0483398438)
					CFrameMon = CFrame.new(-5081.87354, 300.785797, -2938.69385)
					CFrameMon2 = CFrame.new(-5119.59375, 300.550598, -2809.85327)
					CFrameMon3 = CFrame.new(-4944.93799, 300.755371, -2785.14746)
					CFrameMon4 = CFrame.new(-4861.03271, 300.834167, -2904.71436)
					CFrameMon5 = CFrame.new(-5081.87354, 300.785797, -2938.69385)
					CFrameMon6 = CFrame.new(-5119.59375, 300.550598, -2809.85327)
					CFrameMon7 = CFrame.new(-4944.93799, 300.755371, -2785.14746)
					CFrameMon8 = CFrame.new(-4861.03271, 300.834167, -2904.71436)
				elseif Lv == 175 or Lv <= 249 or SelectMonster == "Dark Master [Lv. 175]" then -- Dark Master
					Ms = "Dark Master [Lv. 175]"
					NameQuest = "SkyQuest"
					QuestLv = 2
					NameMon = "Dark Master"
					CFrameQ = CFrame.new(-4842.1372070313, 717.69543457031, -2623.0483398438)
					CFrameMon = CFrame.new(-5235.76172, 400.407043, -2366.71899)
					CFrameMon2 = CFrame.new(-5171.20557, 400.632629, -2243.04346)
					CFrameMon3 = CFrame.new(-5244.14307, 400.553833, -2154.95386)
					CFrameMon4 = CFrame.new(-5338.07666, 400.419495, -2256.87036)
					CFrameMon5 = CFrame.new(-5235.76172, 400.407043, -2366.71899)
					CFrameMon6 = CFrame.new(-5171.20557, 400.632629, -2243.04346)
					CFrameMon7 = CFrame.new(-5244.14307, 400.553833, -2154.95386)
					CFrameMon8 = CFrame.new(-5338.07666, 400.419495, -2256.87036)
				elseif Lv == 190 or Lv <= 209 and SelectMonster == "Prisoner [Lv. 190]" then
					Ms = "Prisoner [Lv. 190]"
					QuestLv = 1
					NameQuest = "PrisonerQuest"
					NameMon = "Prisoner"
					CFrameQ = CFrame.new(5308.93115, 1.65517521, 475.120514, -0.0894274712, -5.00292918e-09, -0.995993316, 1.60817859e-09, 1, -5.16744869e-09, 0.995993316, -2.06384709e-09, -0.0894274712)
					CFrameMon = CFrame.new(4937.33154, 30.1021862, 649.563477)
					CFrameMon2 = CFrame.new(5065.7749, 30.43290985, 546.996643)
					CFrameMon3 = CFrame.new(5088.85205, 30.63439715, 424.919891)
					CFrameMon4 = CFrame.new(5223.32422, 30.45370162, 449.392792)
					CFrameMon5 = CFrame.new(5350.27783, 30.8864578, 391.263519)
					CFrameMon6 = CFrame.new(4937.33154, 30.1021862, 649.563477)
					CFrameMon7 = CFrame.new(5065.7749, 30.43290985, 546.996643)
					CFrameMon8 = CFrame.new(5088.85205, 30.63439715, 424.919891)
				elseif Lv == 210 or Lv <= 249 or SelectMonster == "Dangerous Prisoner [Lv. 210]" then
					Ms = "Dangerous Prisoner [Lv. 210]"
					QuestLv = 2
					NameQuest = "PrisonerQuest"
					NameMon = "Dangerous Prisoner"
					CFrameQ = CFrame.new(5308.93115, 1.65517521, 475.120514, -0.0894274712, -5.00292918e-09, -0.995993316, 1.60817859e-09, 1, -5.16744869e-09, 0.995993316, -2.06384709e-09, -0.0894274712)
					CFrameMon = CFrame.new(5485.27686, 30.48984313, 468.049164)
					CFrameMon2 = CFrame.new(5553.6123, 30.37830436, 583.482605)
					CFrameMon3 = CFrame.new(5645.55957, 30.49353886, 764.599121)
					CFrameMon4 = CFrame.new(5561.3667, 30.4825983, 964.727722)
					CFrameMon5 = CFrame.new(5442.04785, 30.43965244, 1078.86829)
					CFrameMon6 = CFrame.new(5101.04688, 30.43209672, 1056.52319)
					CFrameMon7 = CFrame.new(4955.92383, 30.43116331, 925.554199)
					CFrameMon8 = CFrame.new(4955.92383, 30.43116331, 925.554199)
				elseif Lv == 250 or Lv <= 274 or SelectMonster == "Toga Warrior [Lv. 250]" then -- Toga Warrior
					Ms = "Toga Warrior [Lv. 250]"
					NameQuest = "ColosseumQuest"
					QuestLv = 1
					NameMon = "Toga Warrior"
					CFrameQ = CFrame.new(-1577.7890625, 7.4151420593262, -2984.4838867188)
					CFrameMon = CFrame.new(-1671.87439, 30.46971226, -2684.46704)
					CFrameMon2 = CFrame.new(-1798.56873, 30.69850779, -2852.0918)
					CFrameMon3 = CFrame.new(-1839.27844, 30.54717255, -2670.43506)
					CFrameMon4 = CFrame.new(-2056.15601, 30.7379818, -2713.5896)
					CFrameMon5 = CFrame.new(-2128.38818, 30.74061298, -2853.23096)
					CFrameMon6 = CFrame.new(-1671.87439, 30.46971226, -2684.46704)
					CFrameMon7 = CFrame.new(-1798.56873, 30.69850779, -2852.0918)
					CFrameMon8 = CFrame.new(-1839.27844, 30.54717255, -2670.43506)
				elseif Lv == 275 or Lv <= 299 or SelectMonster == "Gladiator [Lv. 275]" then -- Gladiator
					Ms = "Gladiator [Lv. 275]"
					NameQuest = "ColosseumQuest"
					QuestLv = 2
					NameMon = "Gladiator"
					CFrameQ = CFrame.new(-1577.7890625, 7.4151420593262, -2984.4838867188)
					CFrameMon = CFrame.new(-1483.69543, 30.23153687, -3195.19263)
					CFrameMon2 = CFrame.new(-1370.75085, 30.02963066, -3375.76953)
					CFrameMon3 = CFrame.new(-1356.93213, 30.05916834, -3590.58716)
					CFrameMon4 = CFrame.new(-1125.12451, 30.91520119, -3270.04932)
					CFrameMon5 = CFrame.new(-1228.21082, 30.91372013, -3051.61963)
					CFrameMon6 = CFrame.new(-1483.69543, 30.23153687, -3195.19263)
					CFrameMon7 = CFrame.new(-1370.75085, 30.02963066, -3375.76953)
					CFrameMon8 = CFrame.new(-1356.93213, 30.05916834, -3590.58716)
				elseif Lv == 300 or Lv <= 324 or SelectMonster == "Military Soldier [Lv. 300]" then -- Military Soldier
					Ms = "Military Soldier [Lv. 300]"
					NameQuest = "MagmaQuest"
					QuestLv = 1
					NameMon = "Military Soldier"
					CFrameQ = CFrame.new(-5316.1157226563, 12.262831687927, 8517.00390625)
					CFrameMon = CFrame.new(-5287.19775, 30.68863678, 8659.86328)
					CFrameMon2 = CFrame.new(-5412.09326, 30.3730135, 8591.76855)
					CFrameMon3 = CFrame.new(-5439.79492, 30.07931805, 8349.15137)
					CFrameMon4 = CFrame.new(-5565.604, 30.28863716, 8327.56641)
					CFrameMon5 = CFrame.new(-5667.80664, 30.28863716, 8428.66992)
					CFrameMon6 = CFrame.new(-5287.19775, 30.68863678, 8659.86328)
					CFrameMon7 = CFrame.new(-5412.09326, 30.3730135, 8591.76855)
					CFrameMon8 = CFrame.new(-5439.79492, 30.07931805, 8349.15137)
				elseif Lv == 325 or Lv <= 374 or SelectMonster == "Military Spy [Lv. 325]" then -- Military Spy
					Ms = "Military Spy [Lv. 325]"
					NameQuest = "MagmaQuest"
					QuestLv = 2
					NameMon = "Military Spy"
					CFrameQ = CFrame.new(-5316.1157226563, 12.262831687927, 8517.00390625)
					CFrameMon = CFrame.new(-5786.98828, 100.5823822, 8651.63672)
					CFrameMon2 = CFrame.new(-5857.32812, 100.6921616, 8775.98242)
					CFrameMon3 = CFrame.new(-5916.4082, 100.9983063, 8845.14355)
					CFrameMon4 = CFrame.new(-5806.90088, 100.4439621, 8903.08789)
					CFrameMon5 = CFrame.new(-5786.98828, 100.5823822, 8651.63672)
					CFrameMon6 = CFrame.new(-5857.32812, 100.6921616, 8775.98242)
					CFrameMon7 = CFrame.new(-5916.4082, 100.9983063, 8845.14355)
					CFrameMon8 = CFrame.new(-5806.90088, 100.4439621, 8903.08789)
				elseif Lv == 375 or Lv <= 399 or SelectMonster == "Fishman Warrior [Lv. 375]" then -- Fishman Warrior 
					_G.FM = true
					Ms = "Fishman Warrior [Lv. 375]"
					NameQuest = "FishmanQuest"
					QuestLv = 1
					NameMon = "Fishman Warrior"
					CFrameQ = CFrame.new(61122.65234375, 18.497442245483, 1569.3997802734)
					CFrameMon = CFrame.new(60943.918, 40.9676781, 1744.12366)
					CFrameMon2 = CFrame.new(60841.9023, 40.9637394, 1651.12573)
					CFrameMon3 = CFrame.new(60788.9023, 40.1695957, 1526.11133)
					CFrameMon4 = CFrame.new(60905.6641, 40.2607841, 1470.10828)
					CFrameMon5 = CFrame.new(60947.5195, 40.2365685, 1377.84827)
					CFrameMon6 = CFrame.new(60840.9023, 40.1695957, 1301.12561)
					CFrameMon7 = CFrame.new(60926.3203, 40.2709007, 1179.21045)
					CFrameMon8 = CFrame.new(60840.9023, 40.1695957, 1301.12561)
					if Auto_Farm and (CFrameMon.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 3000 then
						game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(61163.8515625, 11.6796875, 1819.7841796875))
					end
				elseif Lv == 400 or Lv <= 449 or SelectMonster == "Fishman Commando [Lv. 400]" then -- Fishman Commando
					_G.FM = true
					Ms = "Fishman Commando [Lv. 400]"
					NameQuest = "FishmanQuest"
					QuestLv = 2
					NameMon = "Fishman Commando"
					CFrameQ = CFrame.new(61122.65234375, 18.497442245483, 1569.3997802734)
					CFrameMon = CFrame.new(61699.625, 40.2699566, 1520.59375)
					CFrameMon2 = CFrame.new(61760.9062, 40.2607517, 1460.12573)
					CFrameMon3 = CFrame.new(61785.5391, 40.3575878, 1286.50964)
					CFrameMon4 = CFrame.new(62051.4727, 40.418438, 1419.75146)
					CFrameMon5 = CFrame.new(61977.8516, 40.4545078, 1615.34143)
					CFrameMon6 = CFrame.new(61856.6602, 40.2217426, 1695.47583)
					CFrameMon7 = CFrame.new(61699.625, 40.2699566, 1520.59375)
					CFrameMon8 = CFrame.new(61760.9062, 40.2607517, 1460.12573)
					if Auto_Farm and (CFrameMon.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 3000 then
						game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(61163.8515625, 11.6796875, 1819.7841796875))
					end
				elseif Lv == 450 or Lv <= 474 or SelectMonster == "God's Guard [Lv. 450]" then -- God's Guard
					_G.FM = false
					Ms = "God's Guard [Lv. 450]"
					NameQuest = "SkyExp1Quest"
					QuestLv = 1
					NameMon = "God's Guard"
					CFrameQ = CFrame.new(-4721.8603515625, 845.30297851563, -1953.8489990234)
					CFrameMon = CFrame.new(-4700.29004, 880.319214, -1793.46985)
					CFrameMon2 = CFrame.new(-4830.60791, 880.985046, -1779.0907)
					CFrameMon3 = CFrame.new(-4864.05322, 880.410156, -1909.01013)
					CFrameMon4 = CFrame.new(-4820.02979, 880.343811, -2048.61499)
					CFrameMon5 = CFrame.new(-4618.6333, 880.07782, -2043.47839)
					CFrameMon6 = CFrame.new(-4583.79443, 880.31604, -1939.10498)
					CFrameMon7 = CFrame.new(-4700.29004, 880.319214, -1793.46985)
					CFrameMon8 = CFrame.new(-4830.60791, 880.985046, -1779.0907)
					if Auto_Farm and (CFrameMon.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 3000 then
						game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(-4607.82275, 872.54248, -1667.55688))
					end
				elseif Lv == 475 or Lv <= 524 or SelectMonster == "Shanda [Lv. 475]" then -- Shanda
					_G.FM = false
					Ms = "Shanda [Lv. 475]"
					NameQuest = "SkyExp1Quest"
					QuestLv = 2
					NameMon = "Shanda"
					CFrameQ = CFrame.new(-7863.1596679688, 5545.5190429688, -378.42266845703)
					CFrameMon = CFrame.new(-7787.81494140625, 5600.49169921875, -502.2948303222656)
					CFrameMon2 = CFrame.new(-7725.74072, 5600.29004, -585.480713)
					CFrameMon3 = CFrame.new(-7595.16895, 5600.93994, -653.530457)
					CFrameMon4 = CFrame.new(-7540.33887, 5600.27539, -517.048096)
					CFrameMon5 = CFrame.new(-7564.64746, 5600.68262, -418.750336)
					CFrameMon6 = CFrame.new(-7564.64746, 5600.68262, -418.750336)
					CFrameMon7 = CFrame.new(-7709.42822, 5600.29492, -337.002502)
					CFrameMon8 = CFrame.new(-7709.42822, 5600.29492, -337.002502)
					if Auto_Farm and (CFrameMon.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 3000 then
						game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(-7894.6176757813, 5547.1416015625, -380.29119873047))
					end
				elseif Lv == 525 or Lv <= 549 or SelectMonster == "Royal Squad [Lv. 525]" then -- Royal Squad
					Ms = "Royal Squad [Lv. 525]"
					NameQuest = "SkyExp2Quest"
					QuestLv = 1
					NameMon = "Royal Squad"
					CFrameQ = CFrame.new(-7903.3828125, 5635.9897460938, -1410.923828125)
					CFrameMon = CFrame.new(-7841.7041, 5630.08496, -1403.62402)
					CFrameMon2 = CFrame.new(-7724.96143, 5630.62109, -1510.87366)
					CFrameMon3 = CFrame.new(-7669.97656, 5630.33398, -1379.02832)
					CFrameMon4 = CFrame.new(-7513.9126, 5630.75098, -1420.87598)
					CFrameMon5 = CFrame.new(-7528.86475, 5630.06201, -1537.9574)
					CFrameMon6 = CFrame.new(-7841.7041, 5630.08496, -1403.62402)
					CFrameMon7 = CFrame.new(-7724.96143, 5630.62109, -1510.87366)
					CFrameMon8 = CFrame.new(-7669.97656, 5630.33398, -1379.02832)
				elseif Lv == 550 or Lv <= 624 or SelectMonster == "Royal Soldier [Lv. 550]" then -- Royal Soldier
					Ms = "Royal Soldier [Lv. 550]"
					NameQuest = "SkyExp2Quest"
					QuestLv = 2
					NameMon = "Royal Soldier"
					CFrameQ = CFrame.new(-7903.3828125, 5635.9897460938, -1410.923828125)
					CFrameMon = CFrame.new(-7935.60889, 5630.03613, -1624.62866)
					CFrameMon2 = CFrame.new(-7916.33789, 5630.62305, -1719.72119)
					CFrameMon3 = CFrame.new(-7946.00195, 5630.05859, -1822.9917)
					CFrameMon4 = CFrame.new(-7759.49854, 5630.90527, -1862.73206)
					CFrameMon5 = CFrame.new(-7761.07422, 5630.06641, -1720.46008)
					CFrameMon6 = CFrame.new(-7935.60889, 5630.03613, -1624.62866)
					CFrameMon7 = CFrame.new(-7916.33789, 5630.62305, -1719.72119)
					CFrameMon8 = CFrame.new(-7946.00195, 5630.05859, -1822.9917)
				elseif Lv == 625 or Lv <= 649 or SelectMonster == "Galley Pirate [Lv. 625]" then -- Galley Pirate
					Ms = "Galley Pirate [Lv. 625]"
					NameQuest = "FountainQuest"
					QuestLv = 1
					NameMon = "Galley Pirate"
					CFrameQ = CFrame.new(5258.2788085938, 38.526931762695, 4050.044921875)
					CFrameMon = CFrame.new(5348.28906, 70.2900734, 3953.27271)
					CFrameMon2 = CFrame.new(5522.05127, 70.2985611, 3934.32764)
					CFrameMon3 = CFrame.new(5483.07275, 80.2408676, 4059.32227)
					CFrameMon4 = CFrame.new(5654.06592, 70.2936058, 3914.33545)
					CFrameMon5 = CFrame.new(5717.08154, 80.5104256, 4042.30713)
					CFrameMon6 = CFrame.new(5838.05615, 75.3037033, 3914.26831)
					CFrameMon7 = CFrame.new(5348.28906, 70.2900734, 3953.27271)
					CFrameMon8 = CFrame.new(5522.05127, 70.2985611, 3934.32764)
				elseif Lv >= 650 or SelectMonster == "Galley Captain [Lv. 650]" then -- Galley Captain
					Ms = "Galley Captain [Lv. 650]"
					NameQuest = "FountainQuest"
					QuestLv = 2
					NameMon = "Galley Captain"
					CFrameQ = CFrame.new(5258.2788085938, 38.526931762695, 4050.044921875)
					CFrameMon = CFrame.new(5416.99805, 80.5530357, 4780.41553)
					CFrameMon2 = CFrame.new(5352.02979, 60.6015701, 4929.40381)
					CFrameMon3 = CFrame.new(5580.05811, 70.2926521, 4887.41357)
					CFrameMon4 = CFrame.new(5557.02441, 60.6046066, 4996.39062)
					CFrameMon5 = CFrame.new(5792.35107, 80.9391937, 4823.94287)
					CFrameMon6 = CFrame.new(5892.34326, 60.6050987, 4951.91113)
					CFrameMon7 = CFrame.new(5954.96387, 60.5344315, 4882.104)
					CFrameMon8 = CFrame.new(5922.35742, 80.6824799, 4765.85303)
				end
			end
			if New_World then
				if Lv == 700 or Lv <= 724 or SelectMonster == "Raider [Lv. 700]" then -- Raider
					Ms = "Raider [Lv. 700]"
					NameQuest = "Area1Quest"
					QuestLv = 1
					NameMon = "Raider"
					CFrameQ = CFrame.new(-427.72567749023, 72.99634552002, 1835.9426269531)
					CFrameMon = CFrame.new(265.562622, 50.051445, 2497.43481)
					CFrameMon2 = CFrame.new(475.539307, 50.7705688, 2433.41528)
					CFrameMon3 = CFrame.new(549.550598, 50.7821999, 2190.44897)
					CFrameMon4 = CFrame.new(241.562622, 50.9522018, 2195.46753)
					CFrameMon5 = CFrame.new(-612.431946, 50.7861061, 2557.42017)
					CFrameMon6 = CFrame.new(-607.841309, 50.2306099, 2204.09521)
					CFrameMon7 = CFrame.new(-917.401367, 50.7533951, 2250.45459)
					CFrameMon8 = CFrame.new(-904.317383, 50.7743683, 2501.42383)
				elseif Lv == 725 or Lv <= 774 or SelectMonster == "Mercenary [Lv. 725]" then -- Mercenary
					Ms = "Mercenary [Lv. 725]"
					NameQuest = "Area1Quest"
					QuestLv = 2
					NameMon = "Mercenary"
					CFrameQ = CFrame.new(-427.72567749023, 72.99634552002, 1835.9426269531)
					CFrameMon = CFrame.new(-924.691284, 90.7750931, 1788.09863)
					CFrameMon2 = CFrame.new(-1085.13818, 90.7490768, 1696.39294)
					CFrameMon3 = CFrame.new(-915.357422, 90.0287857, 1574.66357)
					CFrameMon4 = CFrame.new(-1135.89746, 90.1187363, 1246.63953)
					CFrameMon5 = CFrame.new(-1209.23328, 90.7195435, 1073.02075)
					CFrameMon6 = CFrame.new(-988.285217, 90.1274414, 1087.69702)
					CFrameMon7 = CFrame.new(-924.691284, 90.7750931, 1788.09863)
					CFrameMon8 = CFrame.new(-1085.13818, 90.7490768, 1696.39294)
				elseif Lv == 775 or Lv <= 799 or SelectMonster == "Swan Pirate [Lv. 775]" then -- Swan Pirate
					Ms = "Swan Pirate [Lv. 775]"
					NameQuest = "Area2Quest"
					QuestLv = 1
					NameMon = "Swan Pirate"
					CFrameQ = CFrame.new(635.61151123047, 73.096351623535, 917.81298828125)
					CFrameMon = CFrame.new(823.615295, 90.7710724, 1162.20508)
					CFrameMon2 = CFrame.new(967.173828, 90.8330917, 1180.75647)
					CFrameMon3 = CFrame.new(1066.99438, 90.8330917, 1080.91797)
					CFrameMon4 = CFrame.new(1063.20959, 90.7636032, 1399.74609)
					CFrameMon5 = CFrame.new(984.6474, 90.7639771, 1401.67834)
					CFrameMon6 = CFrame.new(827.783386, 90.7645111, 1326.89404)
					CFrameMon7 = CFrame.new(823.615295, 90.7710724, 1162.20508)
					CFrameMon8 = CFrame.new(967.173828, 90.8330917, 1180.75647)
				elseif Lv == 800 or Lv <= 874 or SelectMonster == "Factory Staff [Lv. 800]" then -- Factory Staff
					Ms = "Factory Staff [Lv. 800]"
					NameQuest = "Area2Quest"
					QuestLv = 2
					NameMon = "Factory Staff"
					CFrameQ = CFrame.new(635.61151123047, 73.096351623535, 917.81298828125)
					CFrameMon = CFrame.new(936.100891, 90.7891922, -71.2398453)
					CFrameMon2 = CFrame.new(692.110413, 90.8410339, 227.752106)
					CFrameMon3 = CFrame.new(386.107452, 90.8410339, 91.7514038)
					CFrameMon4 = CFrame.new(-92.731041, 90.1639786, -32.960495)
					CFrameMon5 = CFrame.new(-426.878845, 90.8410339, -367.267761)
					CFrameMon6 = CFrame.new(-105.888847, 90.7819061, -670.231934)
					CFrameMon7 = CFrame.new(936.100891, 90.7891922, -71.2398453)
					CFrameMon8 = CFrame.new(692.110413, 90.8410339, 227.752106)
				elseif Lv == 875 or Lv <= 899 or SelectMonster == "Marine Lieutenant [Lv. 875]" then -- Marine Lieutenant
					Ms = "Marine Lieutenant [Lv. 875]"
					NameQuest = "MarineQuest3"
					QuestLv = 1
					NameMon = "Marine Lieutenant"
					CFrameQ = CFrame.new(-2440.9934082031, 73.04190826416, -3217.7082519531)
					CFrameMon = CFrame.new(-2583.93091, 90.8043213, -3039.63013)
					CFrameMon2 = CFrame.new(-2766.0686, 90.8153305, -3144.73267)
					CFrameMon3 = CFrame.new(-3012.86523, 90.8052673, -2921.84399)
					CFrameMon4 = CFrame.new(-3258.53369, 90.8076172, -2990.86768)
					CFrameMon5 = CFrame.new(-2932.48462, 90.8056259, -2604.10669)
					CFrameMon6 = CFrame.new(-2583.93091, 90.8043213, -3039.63013)
					CFrameMon7 = CFrame.new(-2766.0686, 90.8153305, -3144.73267)
					CFrameMon8 = CFrame.new(-3012.86523, 90.8052673, -2921.84399)
				elseif Lv == 900 or Lv <= 949 or SelectMonster == "Marine Captain [Lv. 900]" then -- Marine Captain
					Ms = "Marine Captain [Lv. 900]"
					NameQuest = "MarineQuest3"
					QuestLv = 2
					NameMon = "Marine Captain"
					CFrameQ = CFrame.new(-2440.9934082031, 73.04190826416, -3217.7082519531)
					CFrameMon = CFrame.new(-2105.40601, 90.6410751, -3260.68042)
					CFrameMon2 = CFrame.new(-2030.24768, 90.9695282, -3477.63477)
					CFrameMon3 = CFrame.new(-1928.38892, 90.9695282, -3119.57959)
					CFrameMon4 = CFrame.new(-1808.03503, 90.2457352, -3313.89746)
					CFrameMon5 = CFrame.new(-1603.00159, 90.1955719, -3314.84521)
					CFrameMon6 = CFrame.new(-2105.40601, 90.6410751, -3260.68042)
					CFrameMon7 = CFrame.new(-2030.24768, 90.9695282, -3477.63477)
					CFrameMon8 = CFrame.new(-1928.38892, 90.9695282, -3119.57959)
					if Lv >= 925 then
						_G.SelectBoss = "Fajita [Lv. 925] [Boss]"
					end
				elseif Lv == 950 or Lv <= 974 or SelectMonster == "Zombie [Lv. 950]" then -- Zombie
					Ms = "Zombie [Lv. 950]"
					NameQuest = "ZombieQuest"
					QuestLv = 1
					NameMon = "Zombie"
					CFrameQ = CFrame.new(-5494.3413085938, 48.505931854248, -794.59094238281)
					CFrameMon = CFrame.new(-5510.59229, 60.6537132, -847.672302)
					CFrameMon2 = CFrame.new(-5613.43359, 60.1997719, -937.974243)
					CFrameMon3 = CFrame.new(-5765.74951, 60.6884003, -826.096375)
					CFrameMon4 = CFrame.new(-5855.54834, 90.018486, -740.286621)
					CFrameMon5 = CFrame.new(-5761.98535, 60.35355, -654.943359)
					CFrameMon6 = CFrame.new(-5595.59229, 60.256424, -524.287292)
					CFrameMon7 = CFrame.new(-5510.59229, 60.6537132, -847.672302)
					CFrameMon8 = CFrame.new(-5613.43359, 60.1997719, -937.974243)
				elseif Lv == 975 or Lv <= 999 or SelectMonster == "Vampire [Lv. 975]" then -- Vampire
					Ms = "Vampire [Lv. 975]"
					NameQuest = "ZombieQuest"
					QuestLv = 2
					NameMon = "Vampire"
					CFrameQ = CFrame.new(-5494.3413085938, 48.505931854248, -794.59094238281)
					CFrameMon = CFrame.new(-6038.21533, 30.60701132, -1100.01733)
					CFrameMon2 = CFrame.new(-5776.56689, 30.19985104, -1373.43335)
					CFrameMon3 = CFrame.new(-5952.97754, 30.70087671, -1568.36951)
					CFrameMon4 = CFrame.new(-6130.99219, 30.06086016, -1465.32556)
					CFrameMon5 = CFrame.new(-6276.0293, 30.6362915, -1270.61499)
					CFrameMon6 = CFrame.new(-6038.21533, 30.60701132, -1100.01733)
					CFrameMon7 = CFrame.new(-5776.56689, 30.19985104, -1373.43335)
					CFrameMon8 = CFrame.new(-5952.97754, 30.70087671, -1568.36951)
				elseif Lv == 1000 or Lv <= 1049 or SelectMonster == "Snow Trooper [Lv. 1000]" then -- Snow Trooper
					Ms = "Snow Trooper [Lv. 1000]"
					NameQuest = "SnowMountainQuest"
					QuestLv = 1
					NameMon = "Snow Trooper"
					CFrameQ = CFrame.new(607.05963134766, 401.44781494141, -5370.5546875)
					CFrameMon = CFrame.new(430.4216, 430.745422, -5069.31396)
					CFrameMon2 = CFrame.new(392.417816, 430.660065, -5207.88477)
					CFrameMon3 = CFrame.new(436.43045, 450.987854, -5467.16504)
					CFrameMon4 = CFrame.new(484.540863, 430.748322, -5472.30225)
					CFrameMon5 = CFrame.new(641.43457, 430.701202, -5453.10303)
					CFrameMon6 = CFrame.new(572.734924, 430.165436, -5605.1333)
					CFrameMon7 = CFrame.new(716.612183, 430.156342, -5706.35547)
					CFrameMon8 = CFrame.new(392.417816, 430.660065, -5207.88477)
				elseif Lv == 1050 or Lv <= 1099 or SelectMonster == "Winter Warrior [Lv. 1050]" then -- Winter Warrior
					Ms = "Winter Warrior [Lv. 1050]"
					NameQuest = "SnowMountainQuest"
					QuestLv = 2
					NameMon = "Winter Warrior"
					CFrameQ = CFrame.new(607.05963134766, 401.44781494141, -5370.5546875)
					CFrameMon = CFrame.new(1044.96838, 450.593323, -5049.94287)
					CFrameMon2 = CFrame.new(1142.43262, 450.232819, -5043.06494)
					CFrameMon3 = CFrame.new(1226.46851, 450.477966, -5216.06689)
					CFrameMon4 = CFrame.new(1205.46912, 450.21579, -5397.3418)
					CFrameMon5 = CFrame.new(1446.13562, 450.495361, -5369.10449)
					CFrameMon6 = CFrame.new(1371.82556, 450.545044, -5196.37695)
					CFrameMon7 = CFrame.new(1044.96838, 450.593323, -5049.94287)
					CFrameMon8 = CFrame.new(1142.43262, 450.232819, -5043.06494)
				elseif Lv == 1100 or Lv <= 1124 or SelectMonster == "Lab Subordinate [Lv. 1100]" then -- Lab Subordinate
					Ms = "Lab Subordinate [Lv. 1100]"
					NameQuest = "IceSideQuest"
					QuestLv = 1
					NameMon = "Lab Subordinate"
					CFrameQ = CFrame.new(-6061.841796875, 15.926671981812, -4902.0385742188)
					CFrameMon = CFrame.new(-5640.40674, 30.7589941, -4680.94629)
					CFrameMon2 = CFrame.new(-5897.82178, 30.2995815, -4554.60498)
					CFrameMon3 = CFrame.new(-5963.45996, 30.7573175, -4340.27393)
					CFrameMon4 = CFrame.new(-5766.34863, 30.7593508, -4249.68555)
					CFrameMon5 = CFrame.new(-5590.31738, 30.7585506, -4436.54688)
					CFrameMon6 = CFrame.new(-5640.40674, 30.7589941, -4680.94629)
					CFrameMon7 = CFrame.new(-5897.82178, 30.2995815, -4554.60498)
					CFrameMon8 = CFrame.new(-5963.45996, 30.7573175, -4340.27393)
				elseif Lv == 1125 or Lv <= 1174 or SelectMonster == "Horned Warrior [Lv. 1125]" then -- Horned Warrior
					Ms = "Horned Warrior [Lv. 1125]"
					NameQuest = "IceSideQuest"
					QuestLv = 2
					NameMon = "Horned Warrior"
					CFrameQ = CFrame.new(-6061.841796875, 15.926671981812, -4902.0385742188)
					CFrameMon = CFrame.new(-6499.00146, 30.6707783, -5514.1167)
					CFrameMon2 = CFrame.new(-6588.12061, 30.6189499, -5719.7002)
					CFrameMon3 = CFrame.new(-6516.33154, 30.7509747, -5868.68945)
					CFrameMon4 = CFrame.new(-6331.74854, 30.7566242, -5778.93115)
					CFrameMon5 = CFrame.new(-6221.72314, 30.7332659, -5951.27881)
					CFrameMon6 = CFrame.new(-6093.67139, 30.5871658, -6061.11035)
					CFrameMon7 = CFrame.new(-6499.00146, 30.6707783, -5514.1167)
					CFrameMon8 = CFrame.new(-6588.12061, 30.6189499, -5719.7002)
				elseif Lv == 1175 or Lv <= 1199 or SelectMonster == "Magma Ninja [Lv. 1175]" then -- Magma Ninja
					Ms = "Magma Ninja [Lv. 1175]"
					NameQuest = "FireSideQuest"
					QuestLv = 1
					NameMon = "Magma Ninja"
					CFrameQ = CFrame.new(-5429.0473632813, 15.977565765381, -5297.9614257813)
					CFrameMon = CFrame.new(-5803.59277, 40.6432133, -5710.04443)
					CFrameMon2 = CFrame.new(-5768.63623, 40.7313824, -5945.5708)
					CFrameMon3 = CFrame.new(-5560.96436, 40.92278, -5804.56348)
					CFrameMon4 = CFrame.new(-5206.89893, 40.0855122, -5977.41162)
					CFrameMon5 = CFrame.new(-5099.0918, 40.9871378, -6115.96631)
					CFrameMon6 = CFrame.new(-5259.62549, 40.1081581, -6288.00146)
					CFrameMon7 = CFrame.new(-5803.59277, 40.6432133, -5710.04443)
					CFrameMon8 = CFrame.new(-5768.63623, 40.7313824, -5945.5708)
				elseif Lv == 1200 or Lv <= 1249 or SelectMonster == "Lava Pirate [Lv. 1200]" then -- Lava Pirate
					Ms = "Lava Pirate [Lv. 1200]"
					NameQuest = "FireSideQuest"
					QuestLv = 2
					NameMon = "Lava Pirate"
					CFrameQ = CFrame.new(-5429.0473632813, 15.977565765381, -5297.9614257813)
					CFrameMon = CFrame.new(-5340.02832, 40.195673, -4935.52588)
					CFrameMon2 = CFrame.new(-5431.78369, 40.1615105, -4642.13184)
					CFrameMon3 = CFrame.new(-5264.50244, 40.1666908, -4343.44482)
					CFrameMon4 = CFrame.new(-5159.77588, 40.1742325, -4652.88818)
					CFrameMon5 = CFrame.new(-4942.99365, 50.9293747, -4791.62109)
					CFrameMon6 = CFrame.new(-5340.02832, 40.195673, -4935.52588)
					CFrameMon7 = CFrame.new(-5431.78369, 40.1615105, -4642.13184)
					CFrameMon8 = CFrame.new(-5264.50244, 40.1666908, -4343.44482)
				elseif Lv == 1250 or Lv <= 1274 or SelectMonster == "Ship Deckhand [Lv. 1250]" then -- Ship Deckhand
					Ms = "Ship Deckhand [Lv. 1250]"
					NameQuest = "ShipQuest1"
					QuestLv = 1
					NameMon = "Ship Deckhand"
					CFrameQ = CFrame.new(1040.2927246094, 125.08293151855, 32911.0390625)
					CFrameMon = CFrame.new(1157.3252, 145.506523, 32930.1289)
					CFrameMon2 = CFrame.new(1257.60742, 145.92379, 33031.8867)
					CFrameMon3 = CFrame.new(1176.3291, 145.51265, 33119.0977)
					CFrameMon4 = CFrame.new(1247.4281, 145.89933, 33216.4453)
					CFrameMon5 = CFrame.new(719.283325, 145.464821, 33032)
					CFrameMon6 = CFrame.new(580.323303, 145.535988, 32930.1172)
					CFrameMon7 = CFrame.new(580.340881, 145.8246, 33124.2383)
					CFrameMon8 = CFrame.new(1257.60742, 145.92379, 33031.8867)
					if Auto_Farm and (CFrameMon.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 20000 then
						game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(923.21252441406, 126.9760055542, 32852.83203125))
					end
				elseif Lv == 1275 or Lv <= 1299 or SelectMonster == "Ship Engineer [Lv. 1275]" then -- Ship Engineer
					Ms = "Ship Engineer [Lv. 1275]"
					NameQuest = "ShipQuest1"
					QuestLv = 2
					NameMon = "Ship Engineer"
					CFrameQ = CFrame.new(1040.2927246094, 125.08293151855, 32911.0390625)
					CFrameMon = CFrame.new(1024.89197, 60.7224884, 32739.4121)
					CFrameMon2 = CFrame.new(1088.22607, 60.8481369, 32890.0977)
					CFrameMon3 = CFrame.new(1016.47278, 60.5837517, 33072.4844)
					CFrameMon4 = CFrame.new(834.826904, 60.8366547, 32720.9355)
					CFrameMon5 = CFrame.new(729.271057, 60.228653, 32950.3047)
					CFrameMon6 = CFrame.new(816.991028, 60.5993958, 33110.3555)
					CFrameMon7 = CFrame.new(1024.89197, 60.7224884, 32739.4121)
					CFrameMon8 = CFrame.new(1088.22607, 60.8481369, 32890.0977)
					if Auto_Farm and (CFrameMon.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 20000 then
						game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(923.21252441406, 126.9760055542, 32852.83203125))
					end
				elseif Lv == 1300 or Lv <= 1324 or SelectMonster == "Ship Steward [Lv. 1300]" then -- Ship Steward
					Ms = "Ship Steward [Lv. 1300]"
					NameQuest = "ShipQuest2"
					QuestLv = 1
					NameMon = "Ship Steward"
					CFrameQ = CFrame.new(971.42065429688, 125.08293151855, 33245.54296875)
					CFrameMon = CFrame.new(986.858826, 150.990578, 33366.9492)
					CFrameMon2 = CFrame.new(1032.4696, 150.000481, 33512.3984)
					CFrameMon3 = CFrame.new(920.477234, 150.321541, 33506.7812)
					CFrameMon4 = CFrame.new(801.389832, 150.996452, 33505.1836)
					CFrameMon5 = CFrame.new(815.020813, 150.999084, 33376.2148)
					CFrameMon6 = CFrame.new(986.858826, 150.990578, 33366.9492)
					CFrameMon7 = CFrame.new(1032.4696, 150.000481, 33512.3984)
					CFrameMon8 = CFrame.new(920.477234, 150.321541, 33506.7812)
					if Auto_Farm and (CFrameMon.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 20000 then
						game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(923.21252441406, 126.9760055542, 32852.83203125))
					end
				elseif Lv == 1325 or Lv <= 1349 or SelectMonster == "Ship Officer [Lv. 1325]" then -- Ship Officer
					Ms = "Ship Officer [Lv. 1325]"
					NameQuest = "ShipQuest2"
					QuestLv = 2
					NameMon = "Ship Officer"
					CFrameQ = CFrame.new(971.42065429688, 125.08293151855, 33245.54296875)
					CFrameMon = CFrame.new(1162.54968, 200.86264, 33445.6016)
					CFrameMon2 = CFrame.new(1320.52185, 200.869965, 33294.5977)
					CFrameMon3 = CFrame.new(1144.53174, 200.930923, 33112.6094)
					CFrameMon4 = CFrame.new(657.546753, 200.869415, 33460.6367)
					CFrameMon5 = CFrame.new(505.5177, 200.86937, 33263.5586)
					CFrameMon6 = CFrame.new(694.507202, 200.600266, 33112.6406)
					CFrameMon7 = CFrame.new(1162.54968, 200.86264, 33445.6016)
					CFrameMon8 = CFrame.new(1320.52185, 200.869965, 33294.5977)
					if Auto_Farm and (CFrameMon.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 20000 then
						game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(923.21252441406, 126.9760055542, 32852.83203125))
					end
				elseif Lv == 1350 or Lv <= 1374 or SelectMonster == "Arctic Warrior [Lv. 1350]" then -- Arctic Warrior
					Ms = "Arctic Warrior [Lv. 1350]"
					NameQuest = "FrostQuest"
					QuestLv = 1
					NameMon = "Arctic Warrior"
					CFrameQ = CFrame.new(5668.1372070313, 28.202531814575, -6484.6005859375)
					CFrameMon = CFrame.new()
					CFrameMon2 = CFrame.new()
					CFrameMon3 = CFrame.new()
					CFrameMon4 = CFrame.new()
					CFrameMon5 = CFrame.new()
					CFrameMon6 = CFrame.new()
					CFrameMon7 = CFrame.new()
					CFrameMon8 = CFrame.new()
					if Auto_Farm and (CFrameMon.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 20000 then
						game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(-6508.5581054688, 89.034996032715, -132.83953857422))
					end
				elseif Lv == 1375 or Lv <= 1424 or SelectMonster == "Snow Lurker [Lv. 1375]" then -- Snow Lurker
					Ms = "Snow Lurker [Lv. 1375]"
					NameQuest = "FrostQuest"
					QuestLv = 2
					NameMon = "Snow Lurker"
					CFrameQ = CFrame.new(5668.1372070313, 28.202531814575, -6484.6005859375)
					CFrameMon = CFrame.new()
					CFrameMon2 = CFrame.new()
					CFrameMon3 = CFrame.new()
					CFrameMon4 = CFrame.new()
					CFrameMon5 = CFrame.new()
					CFrameMon6 = CFrame.new()
					CFrameMon7 = CFrame.new()
					CFrameMon8 = CFrame.new()
				elseif Lv == 1425 or Lv <= 1449 or SelectMonster == "Sea Soldier [Lv. 1425]" then -- Sea Soldier
					Ms = "Sea Soldier [Lv. 1425]"
					NameQuest = "ForgottenQuest"
					QuestLv = 1
					NameMon = "Sea Soldier"
					CFrameQ = CFrame.new(-3054.5827636719, 236.87213134766, -10147.790039063)
					CFrameMon = CFrame.new(-3499.34546, 50.1113892, -9712.00488)
					CFrameMon2 = CFrame.new(-3292.8894, 50.41152239, -9640.78223)
					CFrameMon3 = CFrame.new(-3240.32959, 50.8411598, -9813.96582)
					CFrameMon4 = CFrame.new(-3457.94263, 50.0302029, -9933.0752)
					CFrameMon5 = CFrame.new(-2838.66821, 50.2311764, -9813.09473)
					CFrameMon6 = CFrame.new(-2550.9231, 50.8412743, -9839.99707)
					CFrameMon7 = CFrame.new(-2550.9231, 50.8412743, -9839.99707)
					CFrameMon8 = CFrame.new(-2550.9231, 50.8412743, -9839.99707)
				elseif Lv >= 1450 or SelectMonster == "Water Fighter [Lv. 1450]" then -- Water Fighter
					Ms = "Water Fighter [Lv. 1450]"
					NameQuest = "ForgottenQuest"
					QuestLv = 2
					NameMon = "Water Fighter"
					CFrameQ = CFrame.new(-3054.5827636719, 236.87213134766, -10147.790039063)
					CFrameMon = CFrame.new(-3316.75146, 260.719513, -10323.1689)
					CFrameMon2 = CFrame.new(-3511.88721, 260.592819, -10347.0479)
					CFrameMon3 = CFrame.new(-3655.82471, 260.921265, -10589.9717)
					CFrameMon4 = CFrame.new(-3396.36108, 260.280075, -10745.1064)
					CFrameMon5 = CFrame.new(-3396.36108, 260.280075, -10745.1064)
					CFrameMon6 = CFrame.new(-3267.715576171875, 299.0077209472656)
					CFrameMon7 = CFrame.new(-3446.317626953125, 299.18936157226562)
					CFrameMon8 = CFrame.new(-3640.9677734375, 299.18931579589844)
				end
			end
			if Three_World then
				if Lv == 1500 or Lv <= 1524 or SelectMonster == "Pirate Millionaire [Lv. 1500]" then -- Pirate Millionaire
					Ms = "Pirate Millionaire [Lv. 1500]"
					NameQuest = "PiratePortQuest"
					QuestLv = 1
					NameMon = "Pirate Millionaire"
					CFrameQ = CFrame.new(-289.61752319336, 43.819011688232, 5580.0903320313)
					CFrameMon = CFrame.new(21.1219501, 80.537796, 5738.73389, 0.150900155, -0.0115619572, 0.988481343, -0.00985086896, 0.99986434, 0.0131989252, -0.988499939, -0.0117291249, 0.150765806)
					CFrameMon2 = CFrame.new(53.4405632, 80.5410385, 5631.99658, 0.90992862, 0.00738224061, 0.414699197, -0.0129538644, 0.999859631, 0.0106243053, -0.414562553, -0.0150393145, 0.909896553)
					CFrameMon3 = CFrame.new(-132.432053, 80.5391731, 5596.90381, 0.999880433, 0.0100116208, -0.0117853917, -0.00985103659, 0.999858916, 0.01360498, 0.0119199343, -0.0134872487, 0.999838054)
					CFrameMon4 = CFrame.new(-445.261993, 80.5448647, 5511.87207, 0.985708892, 0.0123982541, -0.168000594, -0.00985119678, 0.999823689, 0.0159859452, 0.168169141, -0.0141024766, 0.985657275)
					CFrameMon5 = CFrame.new(-615.322571, 80.5444374, 5429.97266, 0.0234457999, 0.0145146754, -0.999619722, -0.0102334945, 0.999845684, 0.0142779406, 0.999672771, 0.00989485811, 0.0235907175)
					CFrameMon6 = CFrame.new(-679.278015, 80.1347046, 5552.1543, 0.713729382, -0.032395497, -0.699672043, -4.97093424e-08, 0.998929799, -0.0462514721, 0.700421572, 0.0330110788, 0.712965608)
					CFrameMon7 = CFrame.new(-543.567078, 80.5370674, 5639.16748, 0.99179846, 0.00787727721, 0.127568662, -0.0098586008, 0.99984026, 0.0149074495, -0.127430856, -0.016042836, 0.991717756)
					CFrameMon8 = CFrame.new(-543.567078, 80.5370674, 5639.16748, 0.99179846, 0.00787727721, 0.127568662, -0.0098586008, 0.99984026, 0.0149074495, -0.127430856, -0.016042836, 0.991717756)
				elseif Lv == 1525 or Lv <= 1574 or SelectMonster == "Pistol Billionaire [Lv. 1525]" then -- Pistol Billoonaire
					Ms = "Pistol Billionaire [Lv. 1525]"
					NameQuest = "PiratePortQuest"
					QuestLv = 2
					NameMon = "Pistol Billionaire"
					CFrameQ = CFrame.new(-289.61752319336, 43.819011688232, 5580.0903320313)
					CFrameMon = CFrame.new(-991.425842, 90.1421127, 5755.03711, -0.104543321, 0.157078624, -0.982037127, 0, 0.987448096, 0.157944113, 0.994520307, 0.0165120028, -0.103231095)
					CFrameMon2 = CFrame.new(-776.206726, 90.0469437, 5965.37549, 0.933587492, 0.0387514494, -0.356248051, 0, 0.994135737, 0.108138695, 0.358349502, -0.100956932, 0.928112745)
					CFrameMon3 = CFrame.new(-571.425598, 90.9609909, 5899.98633, 0.779831827, -0.158408895, -0.605614603, -0.24328196, 0.814708829, -0.526368141, 0.576780915, 0.557813704, 0.596797884)
					CFrameMon4 = CFrame.new(-355.41687, 90.9771652, 5960.31738, 0.668431818, -0.278464973, -0.689678311, -0.250106722, 0.789117992, -0.56101656, 0.70046097, 0.547494471, 0.457825601)
					CFrameMon5 = CFrame.new(-140.905304, 90.0344162, 6018.31738, 0.99939096, 0.0053995247, -0.0344747305, 2.5400821e-08, 0.987955689, 0.154737011, 0.034895014, -0.154642776, 0.98735404)
					CFrameMon6 = CFrame.new(56.383728, 90.4476318, 6012.4585, 0.357457966, 0.657616854, -0.663147032, 0.250523329, -0.751555502, -0.610247791, -0.89970094, 0.0520040989, -0.433397889)
					CFrameMon7 = CFrame.new(5.88352394, 90.0776443, 6134.64648, -0.499959469, -0.102667883, 0.85994184, 0, 0.992948413, 0.118547454, -0.866048813, 0.0592689216, -0.496433944)
					CFrameMon8 = CFrame.new(95.2235184, 90.9311905, 6248.39111, 0.737284839, 0.558373809, -0.38030231, 0.234562039, -0.739480138, -0.630990982, -0.633554816, 0.376015663, -0.67618084)
				elseif Lv == 1575 or Lv <= 1599 or SelectMonster == "Dragon Crew Warrior [Lv. 1575]" then -- Dragon Crew Warrior
					Ms = "Dragon Crew Warrior [Lv. 1575]"
					NameQuest = "AmazonQuest"
					QuestLv = 1
					NameMon = "Dragon Crew Warrior"
					CFrameQ = CFrame.new(5833.1147460938, 51.60498046875, -1103.0693359375)
					CFrameMon = CFrame.new(6356.71143, 80.3945885, -923.532227, 0.342042685, 0, -0.939684391, 0, 1, 0, 0.939684391, 0, 0.342042685)
					CFrameMon2 = CFrame.new(6644.70215, 80.6418915, -929.486389, 0.275688082, -0.118190505, 0.953953385, 0, 0.99241221, 0.122955382, -0.961247146, -0.0338973328, 0.273596197)
					CFrameMon3 = CFrame.new(6527.77246, 80.6504402, -1121.5498, -0.898790359, -0.0314917117, 0.437246144, 0, 0.997416377, 0.0718367621, -0.438378751, 0.0645661876, -0.896468222)
					CFrameMon4 = CFrame.new(6384.40381, 80.6508369, -1552.87195, -0.829036474, -0.0779409558, 0.55373615, 0, 0.990238845, 0.139380738, -0.559194565, 0.115551718, -0.82094413)
					CFrameMon5 = CFrame.new(5868.32178, 80.2569427, -1895.47876, -0.436190963, 0.463348091, -0.771392167, -0.552127242, -0.814718962, -0.177167535, -0.710558176, 0.348627746, 0.611200213)
					CFrameMon6 = CFrame.new(4305.94385, 80.6192131, -1242.94202, 0.996191859, 0.0111581562, -0.0864714831, 0, 0.991777062, 0.127977476, 0.0871884301, -0.127490118, 0.988000214)
					CFrameMon7 = CFrame.new(3930.8335, 80.6119232, -1237.40588, -0.788016915, 0.0455877185, -0.613963425, 0, 0.997254729, 0.0740476772, 0.615653574, 0.0583508238, -0.785853624)
					CFrameMon8 = CFrame.new(4279.08447, 80.6257324, -1490.43127, -0.981621504, 0, -0.190838262, 0, 1, 0, 0.190838262, 0, -0.981621504)
				elseif Lv == 1600 or Lv <= 1624 or SelectMonster == "Dragon Crew Archer [Lv. 1600]" then -- Dragon Crew Archer
					Ms = "Dragon Crew Archer [Lv. 1600]"
					NameQuest = "AmazonQuest"
					QuestLv = 2
					NameMon = "Dragon Crew Archer"
					CFrameQ = CFrame.new(5833.1147460938, 51.60498046875, -1103.0693359375)
					CFrameMon = CFrame.new(6607.06787, 400.831024, 417.48703, 0.915030658, 0.388575226, -0.108297482, 0.237315461, -0.735655069, -0.634423316, -0.32619071, 0.554816127, -0.765361786)
					CFrameMon2 = CFrame.new(6798.05371, 400.486267, 397.218475, 0.438346624, -0.0263376161, 0.898420036, 0, 0.999570549, 0.0293028913, -0.898806036, -0.0128448233, 0.438158363)
					CFrameMon3 = CFrame.new(6765.01709, 400.014771, 211.27829, -0.642763495, -0.0828390196, 0.761572599, 0, 0.994136155, 0.108135812, -0.766064644, 0.0695057511, -0.638994455)
					CFrameMon4 = CFrame.new(6587.7666, 400.55014, 74.2128525, -0.0776618049, -0.141331047, 0.986911476, -0.000269241398, 0.989904106, 0.141738415, -0.996979713, 0.0107419435, -0.0769157857)
					CFrameMon5 = CFrame.new(6582.40137, 380.160553, -58.0201187, 0.898790359, 0.0141606182, -0.438149989, 0, 0.999478161, 0.0323022455, 0.438378751, -0.0290329475, 0.898321331)
					CFrameMon6 = CFrame.new(6453.38965, 380.582184, -171.99617, 0.819155693, 0, -0.573571265, 0, 1, 0, 0.573571265, 0, 0.819155693)
					CFrameMon7 = CFrame.new(6453.38965, 380.582184, -171.99617, 0.819155693, 0, -0.573571265, 0, 1, 0, 0.573571265, 0, 0.819155693)
					CFrameMon8 = CFrame.new(6453.38965, 380.582184, -171.99617, 0.819155693, 0, -0.573571265, 0, 1, 0, 0.573571265, 0, 0.819155693)
				elseif Lv == 1625 or Lv <= 1649 or SelectMonster == "Female Islander [Lv. 1625]" then -- Female Islander
					Ms = "Female Islander [Lv. 1625]"
					NameQuest = "AmazonQuest2"
					QuestLv = 1
					NameMon = "Female Islander"
					CFrameQ = CFrame.new(5446.8793945313, 601.62945556641, 749.45672607422)
					CFrameMon = CFrame.new()
					CFrameMon2 = CFrame.new()
					CFrameMon3 = CFrame.new()
					CFrameMon4 = CFrame.new()
					CFrameMon5 = CFrame.new()
					CFrameMon6 = CFrame.new()
					CFrameMon7 = CFrame.new()
					CFrameMon8 = CFrame.new()
				elseif Lv == 1650 or Lv <= 1699 or SelectMonster == "Giant Islander [Lv. 1650]" then -- Giant Islander
					Ms = "Giant Islander [Lv. 1650]"
					NameQuest = "AmazonQuest2"
					QuestLv = 2
					NameMon = "Giant Islander"
					CFrameQ = CFrame.new(5446.8793945313, 601.62945556641, 749.45672607422)
					CFrameMon = CFrame.new()
					CFrameMon2 = CFrame.new()
					CFrameMon3 = CFrame.new()
					CFrameMon4 = CFrame.new()
					CFrameMon5 = CFrame.new()
					CFrameMon6 = CFrame.new()
					CFrameMon7 = CFrame.new()
					CFrameMon8 = CFrame.new()
				elseif Lv == 1700 or Lv <= 1724 or SelectMonster == "Marine Commodore [Lv. 1700]" then -- Marine Commodore
					Ms = "Marine Commodore [Lv. 1700]"
					NameQuest = "MarineTreeIsland"
					QuestLv = 1
					NameMon = "Marine Commodore"
					CFrameQ = CFrame.new(2179.98828125, 28.731239318848, -6740.0551757813)
					CFrameMon = CFrame.new()
					CFrameMon2 = CFrame.new()
					CFrameMon3 = CFrame.new()
					CFrameMon4 = CFrame.new()
					CFrameMon5 = CFrame.new()
					CFrameMon6 = CFrame.new()
					CFrameMon7 = CFrame.new()
					CFrameMon8 = CFrame.new()
				elseif Lv == 1725 or Lv <= 1774 or SelectMonster == "Marine Rear Admiral [Lv. 1725]" then -- Marine Rear Admiral
					Ms = "Marine Rear Admiral [Lv. 1725]"
					NameQuest = "MarineTreeIsland"
					QuestLv = 2
					NameMon = "Marine Rear Admiral"
					CFrameQ = CFrame.new(2179.98828125, 28.731239318848, -6740.0551757813)
					CFrameMon = CFrame.new()
					CFrameMon2 = CFrame.new()
					CFrameMon3 = CFrame.new()
					CFrameMon4 = CFrame.new()
					CFrameMon5 = CFrame.new()
					CFrameMon6 = CFrame.new()
					CFrameMon7 = CFrame.new()
					CFrameMon8 = CFrame.new()
				elseif Lv == 1775 or Lv <= 1799 or SelectMonster == "Fishman Raider [Lv. 1775]" then -- Fishman Raide
					Ms = "Fishman Raider [Lv. 1775]"
					NameQuest = "DeepForestIsland3"
					QuestLv = 1
					NameMon = "Fishman Raider"
					CFrameQ = CFrame.new(-10582.759765625, 331.78845214844, -8757.666015625)
					CFrameMon = CFrame.new()
					CFrameMon2 = CFrame.new()
					CFrameMon3 = CFrame.new()
					CFrameMon4 = CFrame.new()
					CFrameMon5 = CFrame.new()
					CFrameMon6 = CFrame.new()
					CFrameMon7 = CFrame.new()
					CFrameMon8 = CFrame.new()
				elseif Lv == 1800 or Lv <= 1824 or SelectMonster == "Fishman Captain [Lv. 1800]" then -- Fishman Captain
					Ms = "Fishman Captain [Lv. 1800]"
					NameQuest = "DeepForestIsland3"
					QuestLv = 2
					NameMon = "Fishman Captain"
					CFrameQ = CFrame.new(-10583.099609375, 331.78845214844, -8759.4638671875)
					CFrameMon = CFrame.new()
					CFrameMon2 = CFrame.new()
					CFrameMon3 = CFrame.new()
					CFrameMon4 = CFrame.new()
					CFrameMon5 = CFrame.new()
					CFrameMon6 = CFrame.new()
					CFrameMon7 = CFrame.new()
					CFrameMon8 = CFrame.new()
				elseif Lv == 1825 or Lv <= 1849 or SelectMonster == "Forest Pirate [Lv. 1825]" then -- Forest Pirate
					Ms = "Forest Pirate [Lv. 1825]"
					NameQuest = "DeepForestIsland"
					QuestLv = 1
					NameMon = "Forest Pirate"
					CFrameQ = CFrame.new(-13232.662109375, 332.40396118164, -7626.4819335938)
					CFrameMon = CFrame.new()
					CFrameMon2 = CFrame.new()
					CFrameMon3 = CFrame.new()
					CFrameMon4 = CFrame.new()
					CFrameMon5 = CFrame.new()
					CFrameMon6 = CFrame.new()
					CFrameMon7 = CFrame.new()
					CFrameMon8 = CFrame.new()
				elseif Lv == 1850 or Lv <= 1899 or SelectMonster == "Mythological Pirate [Lv. 1850]" then -- Mythological Pirate
					Ms = "Mythological Pirate [Lv. 1850]"
					NameQuest = "DeepForestIsland"
					QuestLv = 2
					NameMon = "Mythological Pirate"
					CFrameQ = CFrame.new(-13232.662109375, 332.40396118164, -7626.4819335938)
					CFrameMon = CFrame.new()
					CFrameMon2 = CFrame.new()
					CFrameMon3 = CFrame.new()
					CFrameMon4 = CFrame.new()
					CFrameMon5 = CFrame.new()
					CFrameMon6 = CFrame.new()
					CFrameMon7 = CFrame.new()
					CFrameMon8 = CFrame.new()
				elseif Lv >= 1900 and Lv <= 1924 or SelectMonster == "Jungle Pirate [Lv. 1900]" then -- Jungle Pirate
					Ms = "Jungle Pirate [Lv. 1900]"
					NameQuest = "DeepForestIsland2"
					QuestLv = 1
					NameMon = "Jungle Pirate"
					CFrameQ = CFrame.new(-12682.096679688, 390.88653564453, -9902.1240234375)
					CFrameMon = CFrame.new()
					CFrameMon2 = CFrame.new()
					CFrameMon3 = CFrame.new()
					CFrameMon4 = CFrame.new()
					CFrameMon5 = CFrame.new()
					CFrameMon6 = CFrame.new()
					CFrameMon7 = CFrame.new()
					CFrameMon8 = CFrame.new()
				elseif Lv >= 1925 and Lv <= 1974 or SelectMonster == "Musketeer Pirate [Lv. 1925]" then -- Musketeer Pirate
					Ms = "Musketeer Pirate [Lv. 1925]"
					NameQuest = "DeepForestIsland2"
					QuestLv = 2
					NameMon = "Musketeer Pirate"
					CFrameQ = CFrame.new(-12682.096679688, 390.88653564453, -9902.1240234375)
					CFrameMon = CFrame.new()
					CFrameMon2 = CFrame.new()
					CFrameMon3 = CFrame.new()
					CFrameMon4 = CFrame.new()
					CFrameMon5 = CFrame.new()
					CFrameMon6 = CFrame.new()
					CFrameMon7 = CFrame.new()
					CFrameMon8 = CFrame.new()
				elseif Lv >= 1975 and Lv <= 1999 or SelectMonster == "Reborn Skeleton [Lv. 1975]" then -- Reborn Skeleton
					Ms = "Musketeer Pirate [Lv. 1925]"
					NameQuest = "DeepForestIsland2"
					QuestLv = 2
					NameMon = "Musketeer Pirate"
					CFrameQ = CFrame.new(-12682.096679688, 390.88653564453, -9902.1240234375)
					CFrameMon = CFrame.new()
					CFrameMon2 = CFrame.new()
					CFrameMon3 = CFrame.new()
					CFrameMon4 = CFrame.new()
					CFrameMon5 = CFrame.new()
					CFrameMon6 = CFrame.new()
					CFrameMon7 = CFrame.new()
					CFrameMon8 = CFrame.new()
				elseif Lv >= 2000 and Lv <= 2024 or SelectMonster == "Living Zombie [Lv. 2000]" then -- Living Zombie
					Ms = "Living Zombie [Lv. 2000]"
					NameQuest = "HauntedQuest1"
					QuestLv = 2
					NameMon = "Living Zombie"
					CFrameQ = CFrame.new(-9480.80762, 142.130661, 5566.37305)
					CFrameMon = CFrame.new()
					CFrameMon2 = CFrame.new()
					CFrameMon3 = CFrame.new()
					CFrameMon4 = CFrame.new()
					CFrameMon5 = CFrame.new()
					CFrameMon6 = CFrame.new()
					CFrameMon7 = CFrame.new()
					CFrameMon8 = CFrame.new()
				elseif Lv >= 2025 and Lv <= 2049 or SelectMonster == "Demonic Soul [Lv. 2025]" then -- Demonic Soul
					Ms = "Demonic Soul [Lv. 2025]"
					NameQuest = "HauntedQuest1"
					QuestLv = 1
					NameMon = "Demonic Souls"
					CFrameQ = CFrame.new(-9515.39551, 172.266037, 6078.89746)
					CFrameMon = CFrame.new()
					CFrameMon2 = CFrame.new()
					CFrameMon3 = CFrame.new()
					CFrameMon4 = CFrame.new()
					CFrameMon5 = CFrame.new()
					CFrameMon6 = CFrame.new()
					CFrameMon7 = CFrame.new()
					CFrameMon8 = CFrame.new()
				elseif Lv >= 2050 and Lv <= 2074 or SelectMonster == "Posessed Mummy [Lv. 2050]" then -- Posessed Mummy
					Ms = "Posessed Mummy [Lv. 2050]"
					NameQuest = "HauntedQuest2"
					QuestLv = 2
					NameMon = "Posessed Mummys"
					CFrameQ = CFrame.new(-9515.39551, 172.266037, 6078.89746)
					CFrameMon = CFrame.new()
					CFrameMon2 = CFrame.new()
					CFrameMon3 = CFrame.new()
					CFrameMon4 = CFrame.new()
					CFrameMon5 = CFrame.new()
					CFrameMon6 = CFrame.new()
					CFrameMon7 = CFrame.new()
					CFrameMon8 = CFrame.new()
				elseif Lv >= 2075 and Lv <= 2099 or SelectMonster == "Peanut Scout [Lv. 2075]" then -- Peanut Scout
					Ms = "Peanut Scout [Lv. 2075]"
					NameQuest = "PeanutQuest1"
					QuestLv = 1
					NameMon = "Peanut Scout"
					CFrameQ = CFrame.new(-2104.453125, 38.129974365234, -10194.0078125)
					CFrameMon = CFrame.new()
					CFrameMon2 = CFrame.new()
					CFrameMon3 = CFrame.new()
					CFrameMon4 = CFrame.new()
					CFrameMon5 = CFrame.new()
					CFrameMon6 = CFrame.new()
					CFrameMon7 = CFrame.new()
					CFrameMon8 = CFrame.new()
				elseif Lv >= 2100 and Lv <= 2124 or SelectMonster == "Peanut President [Lv. 2100]" then -- Peanut President
					Ms = "Peanut President [Lv. 2100]"
					NameQuest = "PeanutQuest2"
					QuestLv = 2
					NameMon = "Peanut Presidents"
					CFrameQ = CFrame.new(-2104.453125, 38.129974365234, -10194.0078125)
					CFrameMon = CFrame.new()
					CFrameMon2 = CFrame.new()
					CFrameMon3 = CFrame.new()
					CFrameMon4 = CFrame.new()
					CFrameMon5 = CFrame.new()
					CFrameMon6 = CFrame.new()
					CFrameMon7 = CFrame.new()
					CFrameMon8 = CFrame.new()
				elseif Lv >= 2125 and Lv <= 2149 or SelectMonster == "Ice Cream Chef [Lv. 2125]" then --Ice Cream Chef
					Ms = "Ice Cream Chef [Lv. 2125]"
					NameQuest = "IceCreamQuest1"
					QuestLv = 1
					NameMon = "	Ice Cream Chefs"
					CFrameQ = CFrame.new(-821.35913085938, 65.845329284668, -10965.2578125)
					CFrameMon = CFrame.new()
					CFrameMon2 = CFrame.new()
					CFrameMon3 = CFrame.new()
					CFrameMon4 = CFrame.new()
					CFrameMon5 = CFrame.new()
					CFrameMon6 = CFrame.new()
					CFrameMon7 = CFrame.new()
					CFrameMon8 = CFrame.new()
				elseif Lv >= 2150 and Lv <= 2200 or SelectMonster == "Ice Cream Commander [Lv. 2150]" then -- Ice Cream Commander
					Ms = "Ice Cream Commander [Lv. 2150]"
					NameQuest = "IceCreamIslandQuest"
					QuestLv = 2
					NameMon = "Ice Cream Commanders"
					CFrameQ = CFrame.new(-821.35913085938, 65.845329284668, -10965.2578125)
					CFrameMon = CFrame.new()
					CFrameMon2 = CFrame.new()
					CFrameMon3 = CFrame.new()
					CFrameMon4 = CFrame.new()
					CFrameMon5 = CFrame.new()
					CFrameMon6 = CFrame.new()
					CFrameMon7 = CFrame.new()
					CFrameMon8 = CFrame.new()
				elseif Lv >= 2200 and Lv <= 2250 or SelectMonster == "Ice Cream Commander [Lv. 2150]" then -- Ice Cream Commander
					Ms = "Cookie Crafter [Lv. 2200]"
					NameQuest = "CakeQuest1"
					QuestLv = 1
					NameMon = "Cookie Crafters"
					CFrameQ = CFrame.new(-2017.4874267578125, 36.85276412963867, -12027.53515625)
					CFrameMon = CFrame.new()
					CFrameMon2 = CFrame.new()
					CFrameMon3 = CFrame.new()
					CFrameMon4 = CFrame.new()
					CFrameMon5 = CFrame.new()
					CFrameMon6 = CFrame.new()
					CFrameMon7 = CFrame.new()
					CFrameMon8 = CFrame.new()
				elseif Lv >= 2225 and Lv <= 2299 or SelectMonster == "Cake Guard [Lv. 2225]" then
					Ms = "Cake Guard [Lv. 2225]"
					NameQuest = "CakeQuest1"
					QuestLv = 2
					NameMon = "Cake Guards"
					CFrameMon = CFrame.new()
					CFrameMon2 = CFrame.new()
					CFrameMon3 = CFrame.new()
					CFrameMon4 = CFrame.new()
					CFrameMon5 = CFrame.new()
					CFrameMon6 = CFrame.new()
					CFrameMon7 = CFrame.new()
					CFrameMon8 = CFrame.new()
					CFrameQ = CFrame.new(-2017.4874267578125, 36.85276412963867, -12027.53515625)
				elseif Lv >= 2300 and Lv <= 2324 or SelectMonster == "Cocoa Warrior [Lv. 2300]" then
					Ms = "Cocoa Warrior [Lv. 2300]"
					NameQuest = "ChocQuest1"
					QuestLv = 1
					NameMon = "Cocoa Warrior"
					CFrameMon = CFrame.new()
					CFrameMon2 = CFrame.new()
					CFrameMon3 = CFrame.new()
					CFrameMon4 = CFrame.new()
					CFrameMon5 = CFrame.new()
					CFrameMon6 = CFrame.new()
					CFrameMon7 = CFrame.new()
					CFrameMon8 = CFrame.new()
					CFrameQ = CFrame.new(231.68377685546875, 25.077497482299805, -12196.4892578125)
				elseif Lv >= 2325 and Lv <= 2349 or SelectMonster == "Chocolate Bar Battler [Lv. 2325]" then
					Ms = "Chocolate Bar Battler [Lv. 2325]"
					NameQuest = "ChocQuest1"
					QuestLv = 2
					NameMon = "Chocolate Bar Battler"
					CFrameMon = CFrame.new()
					CFrameMon2 = CFrame.new()
					CFrameMon3 = CFrame.new()
					CFrameMon4 = CFrame.new()
					CFrameMon5 = CFrame.new()
					CFrameMon6 = CFrame.new()
					CFrameMon7 = CFrame.new()
					CFrameMon8 = CFrame.new()
					CFrameQ = CFrame.new(231.68377685546875, 25.077497482299805, -12196.4892578125)
				elseif Lv >= 2350 and Lv <= 2374 or SelectMonster == "Sweet Thief [Lv. 2350]" then
					Ms = "Sweet Thief [Lv. 2350]"
					NameQuest = "ChocQuest2"
					QuestLv = 1
					NameMon = "Sweet Thief"
					CFrameMon = CFrame.new()
					CFrameMon2 = CFrame.new()
					CFrameMon3 = CFrame.new()
					CFrameMon4 = CFrame.new()
					CFrameMon5 = CFrame.new()
					CFrameMon6 = CFrame.new()
					CFrameMon7 = CFrame.new()
					CFrameMon8 = CFrame.new()
					CFrameQ = CFrame.new(148.7130584716797, 25.137081146240234, -12774.9052734375)
				elseif Lv >= 2375 and Lv <= 2399 or SelectMonster == "Candy Rebel [Lv. 2375]" then
					Ms = "Candy Rebel [Lv. 2375]"
					NameQuest = "ChocQuest2"
					QuestLv = 2
					NameMon = "Candy Rebel"
					CFrameMon = CFrame.new()
					CFrameMon2 = CFrame.new()
					CFrameMon3 = CFrame.new()
					CFrameMon4 = CFrame.new()
					CFrameMon5 = CFrame.new()
					CFrameMon6 = CFrame.new()
					CFrameMon7 = CFrame.new()
					CFrameMon8 = CFrame.new()
					CFrameQ = CFrame.new(148.7130584716797, 25.137081146240234, -12774.9052734375)
				elseif Lv >= 2400 and Lv <= 2424 or SelectMonster == "Candy Pirate [Lv. 2400]" then
					Ms = "Candy Pirate [Lv. 2400]"
					NameQuest = "CandyQuest1"
					QuestLv = 1
					NameMon = "Candy Pirate"
					CFrameMon = CFrame.new(-1225.8407, 40.70440292, -14702.5811)
					CFrameMon2 = CFrame.new(-1299.79883, 40.0102119, -14801.2295)
					CFrameMon3 = CFrame.new(-1411.04895, 40.2383375, -14703.4199)
					CFrameMon4 = CFrame.new(-1370.88086, 40.9806051, -14477.8525)
					CFrameMon5 = CFrame.new(-1291.07166, 40.8216858, -14385.0557)
					CFrameMon6 = CFrame.new(-1436.48059, 40.6319561, -14386.876)
					CFrameMon7 = CFrame.new(-1436.48059, 40.6319561, -14386.876)
					CFrameMon8 = CFrame.new(-1436.48059, 40.6319561, -14386.876)
					CFrameQ = CFrame.new(-1147.0028076171875, 14.450505256652832, -14445.3818359375)
				elseif Lv >= 2425 or SelectMonster == "Snow Demon [Lv. 2425]" then
					Ms = "Snow Demon [Lv. 2425]"
					NameQuest = "CandyQuest1"
					QuestLv = 2
					NameMon = "Snow Demon"
					CFrameMon = CFrame.new(-849.702454, 40.2957001, -14407.29)
					CFrameMon2 = CFrame.new(-902.147339, 40.2959757, -14309.4268)
					CFrameMon3 = CFrame.new(-800.331482, 40.7142744, -14291.1357)
					CFrameMon4 = CFrame.new(-896.080078, 40.70440292, -14624.3779)
					CFrameMon5 = CFrame.new(-809.856934, 40.6076746, -14687.751)
					CFrameMon6 = CFrame.new(-928.158264, 40.0589685, -14762.2178)
					CFrameMon7 = CFrame.new(-928.158264, 40.0589685, -14762.2178)
					CFrameMon8 = CFrame.new(-928.158264, 40.0589685, -14762.2178)
					CFrameQ = CFrame.new(-1147.0028076171875, 14.450505256652832, -14445.3818359375)
				end
			end
		end --Fix not Complete

		function CheckLevel2()
			local Lv = game:GetService("Players").LocalPlayer.Data.Level.Value
			if _G.Upto then
				Lv = Lv + 100
			end
			if Old_World and not Auto_Raid then
				if Lv == 1 or Lv <= 9 or SelectMonster == "" then -- Bandit
					Ms = "Bandit [Lv. 5]"
					NameQuest = "BanditQuest1"
					QuestLv = 1
					NameMon = "Bandit"
					CFrameQ = CFrame.new(1059.37195, 15.4495068, 1550.4231, 0.939700544, -0, -0.341998369, 0, 1, -0, 0.341998369, 0, 0.939700544)
					CFrameMon = CFrame.new(932.8062133789062, 50.273521423339844, 1515.4857177734375)
					CFrameMon2 = CFrame.new(1020.5850830078125, 50.273521423339844, 1566.209228515625)
					CFrameMon3 = CFrame.new(951.9865112304688, 50.273590087890625, 1624.841064453125)
					CFrameMon4 = CFrame.new(1100.512939453125, 50.273609161376953, 1593.30859375)
					CFrameMon5 = CFrame.new(1123.3743896484375, 50.273609161376953, 1663.6324462890625)
					CFrameMon6 = CFrame.new(1219.28308, 50.4678574, 1676.11877, 0.491706252, 0.653990805, -0.574909568, 0.239682883, -0.736385643, -0.632683575, -0.837124228, 0.173298508, -0.518835723)
					CFrameMon7 = CFrame.new(1284.30542, 50.7171984, 1627.62842, 0.499959469, -0.0363993086, 0.865283549, 0, 0.999116361, 0.0420291647, -0.866048813, -0.021012878, 0.499517679)
					CFrameMon8 = CFrame.new(1231.89722, 50.4568367, 1541.047, -0.691286325, -0.584750295, 0.424488306, 0.234685749, -0.737307549, -0.633482456, 0.683407485, -0.338296384, 0.646923304)
					CFrameMon9 = CFrame.new(1341.77808, 50.7331057, 1568.89648, 0.499959469, -0.029190246, 0.865556777, 0, 0.999431849, 0.0337050818, -0.866048813, -0.0168511756, 0.499675423)
					CFrameMon10 = CFrame.new(1331.83191, 50.7480268, 1498.00366, -0.74314785, -0.0143532939, 0.668973267, 0, 0.999769926, 0.0214507692, -0.669127226, 0.0159410927, -0.742976844)
					TelePBoss(CFrameQ)
				elseif Lv == 10 or Lv <= 14 or SelectMonster == "Monkey [Lv. 14]" then -- Monkey
					 
					Ms = "Monkey [Lv. 14]"
					NameQuest = "JungleQuest"
					QuestLv = 1
					NameMon = "Monkey"
					CFrameQ = CFrame.new(-1598.08911, 35.5501175, 153.377838, 0, 0, 1, 0, 1, -0, -1, 0, 0)
					CFrameMon = CFrame.new(-1578.40002, 40.0510254, 376.473907, 0.799455941, 0.519646227, -0.30139327, 0.24136968, -0.737300873, -0.630973697, -0.550100684, 0.431688488, -0.714866579)
					CFrameMon2 = CFrame.new(-1202.49963, 40.5991755, 278.730499, 1, 0, 0, 0, 0.988172114, 0.153348491, 0, -0.153348491, 0.988172114)
					CFrameMon3 = CFrame.new(-1291.31116, 40.1025791, -4.68253756, -0.952686191, 0.0732820556, 0.294989794, -0.246494859, -0.754113972, -0.608730257, 0.177846909, -0.65264231, 0.736497521)
					CFrameMon4 = CFrame.new(-1489.24976, 40.550066, 88.4902802, -1, 0, 0, 0, 1, 0, 0, 0, -1)
					CFrameMon5 = CFrame.new(-1610.48572, 40.3196087, -48.0345688, -0.707134247, -0.019071456, 0.706822038, 0, 0.999636173, 0.0269721597, -0.707079291, 0.0190729387, -0.706876993)
					CFrameMon6 = CFrame.new(-1743.51038, 40.3173809, -91.2508316, -0.707134247, 0.023433838, -0.706690907, 0, 0.999450684, 0.0331417397, 0.707079291, 0.0234356597, -0.706745803)
					CFrameMon7 = CFrame.new(-1800.5564, 40.7170601, 109.951523, -0.545955539, -0.590623736, -0.594219029, -0.250604779, 0.791900158, -0.556858599, 0.799456, -0.155105934, -0.580355406)
					CFrameMon8 = CFrame.new(-1800.5564, 40.7170601, 109.951523, -0.545955539, -0.590623736, -0.594219029, -0.250604779, 0.791900158, -0.556858599, 0.799456, -0.155105934, -0.580355406)
					TelePBoss(CFrameQ)
					
				elseif Lv == 15 or Lv <= 29 or SelectMonster == "Gorilla [Lv. 20]" then -- Gorilla
					Ms = "Gorilla [Lv. 20]"
					NameQuest = "JungleQuest"
					QuestLv = 2
					NameMon = "Gorilla"
					CFrameQ = CFrame.new(-1598.08911, 35.5501175, 153.377838, 0, 0, 1, 0, 1, -0, -1, 0, 0)
					CFrameMon = CFrame.new(-1362.0625, 30.8125114, -487.021637, -0.553064823, -0.433036685, 0.711757243, -0.234503761, -0.738856256, -0.631743073, 0.799454272, -0.516304612, 0.307086766)
					CFrameMon2 = CFrame.new(-1249.05078, 30.01767778, -456.178711, -0.00332166697, 0.142852128, -0.989738405, -1.32135893e-08, 0.989743948, 0.142852902, 0.999994457, 0.00047452288, -0.00328759779)
					CFrameMon3 = CFrame.new(-1248.04932, 30.0324049, -548.841492, -0.799633741, 0.519399822, -0.301346183, -0.244738176, -0.7401582, -0.626313686, -0.548351169, -0.427070618, 0.718972504)
					CFrameMon4 = CFrame.new(-1188.06848, 30.0483704, -650.220398, -0.939987123, 0.0570550412, -0.336405993, 0.237240091, 0.81789434, -0.524181187, 0.24523735, -0.572532594, -0.782345891)
					CFrameMon5 = CFrame.new(-1362.0625, 30.8125114, -487.021637, -0.553064823, -0.433036685, 0.711757243, -0.234503761, -0.738856256, -0.631743073, 0.799454272, -0.516304612, 0.307086766)
					CFrameMon6 = CFrame.new(-1249.05078, 30.01767778, -456.178711, -0.00332166697, 0.142852128, -0.989738405, -1.32135893e-08, 0.989743948, 0.142852902, 0.999994457, 0.00047452288, -0.00328759779)
					CFrameMon7 = CFrame.new(-1248.04932, 30.0324049, -548.841492, -0.799633741, 0.519399822, -0.301346183, -0.244738176, -0.7401582, -0.626313686, -0.548351169, -0.427070618, 0.718972504)
					CFrameMon8 = CFrame.new(-1188.06848, 30.0483704, -650.220398, -0.939987123, 0.0570550412, -0.336405993, 0.237240091, 0.81789434, -0.524181187, 0.24523735, -0.572532594, -0.782345891)
					TelePBoss(CFrameQ)
					if Lv >= 25 then
						_G.SelectBoss = "The Gorilla King [Lv. 25] [Boss]" 
					end
					SelectMonster = "Monkey [Lv. 14]"
				elseif Lv == 30 or Lv <= 119 or SelectMonster == "Shanda [Lv. 475]" then -- Shanda
					_G.FM = false
					Ms = "Shanda [Lv. 475]"
					NameQuest = "JungleQuest"
					QuestLv = 2
					NameMon = "Gorila"
					CFrameQ = CFrame.new(-7863.1596679688, 5545.5190429688, -378.42266845703)
					CFrameMon = CFrame.new(-7787.81494140625, 5600.49169921875, -502.2948303222656)
					CFrameMon2 = CFrame.new(-7725.74072, 5600.29004, -585.480713)
					CFrameMon3 = CFrame.new(-7595.16895, 5600.93994, -653.530457)
					CFrameMon4 = CFrame.new(-7540.33887, 5600.27539, -517.048096)
					CFrameMon5 = CFrame.new(-7564.64746, 5600.68262, -418.750336)
					CFrameMon6 = CFrame.new(-7564.64746, 5600.68262, -418.750336)
					CFrameMon7 = CFrame.new(-7709.42822, 5600.29492, -337.002502)
					CFrameMon8 = CFrame.new(-7709.42822, 5600.29492, -337.002502)
					if Auto_Farm and (CFrameMon.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 3000 then
						game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(-7894.6176757813, 5547.1416015625, -380.29119873047))
					end
					_G.Farm_Mon = true
				elseif Lv == 120 or Lv <= 149 or SelectMonster == "Chief Petty Officer [Lv. 120]" then -- Chief Petty Officer
					Ms = "Chief Petty Officer [Lv. 120]"
					NameQuest = "MarineQuest2"
					QuestLv = 1
					NameMon = "Chief Petty Officer"
					CFrameQ = CFrame.new(-5039.58643, 27.3500385, 4324.68018, 0, 0, -1, 0, 1, 0, 1, 0, 0)
					CFrameMon = CFrame.new(-4923.10791, 40.3499947, 4076.94336)
					CFrameMon2 = CFrame.new(-4805.28809, 40.090353, 3993.9248)
					CFrameMon3 = CFrame.new(-4989.27148, 40.0766487, 3947.69263)
					CFrameMon4 = CFrame.new(-5121.31006, 40.1290245, 4059.63696)
					CFrameMon5 = CFrame.new(-4615.01855, 40.3923702, 4415.97705)
					CFrameMon6 = CFrame.new(-4634.14697, 40.3546143, 4551.83789)
					CFrameMon7 = CFrame.new(-4808.26562, 40.5440979, 4540.03223)
					CFrameMon8 = CFrame.new(-4873.88184, 40.0598965, 4655.65576)
					TelePBoss(CFrameQ)
					if Lv >= 130 then
						_G.SelectBoss = "Vice Admiral [Lv. 130] [Boss]"
					end
					
				elseif SelectMonster == "Sky Bandit [Lv. 150]" then -- Sky Bandit
					Ms = "Sky Bandit [Lv. 150]"
					NameQuest = "SkyQuest"
					QuestLv = 1
					NameMon = "Sky Bandit"
					CFrameQ = CFrame.new(-4839.53027, 716.368591, -2619.44165, 0.866007268, 0, 0.500031412, 0, 1, 0, -0.500031412, 0, 0.866007268)
					CFrameMon = CFrame.new(-5081.87354, 300.785797, -2938.69385)
					CFrameMon2 = CFrame.new(-5119.59375, 300.550598, -2809.85327)
					CFrameMon3 = CFrame.new(-4944.93799, 300.755371, -2785.14746)
					CFrameMon4 = CFrame.new(-4861.03271, 300.834167, -2904.71436)
					CFrameMon5 = CFrame.new(-5081.87354, 300.785797, -2938.69385)
					CFrameMon6 = CFrame.new(-5119.59375, 300.550598, -2809.85327)
					CFrameMon7 = CFrame.new(-4944.93799, 300.755371, -2785.14746)
					CFrameMon8 = CFrame.new(-4861.03271, 300.834167, -2904.71436)
					TelePBoss(CFrameQ)
					
				elseif Lv == 175 or Lv <= 190 or SelectMonster == "Dark Master [Lv. 175]" then -- Dark Master
					 
					Ms = "Dark Master [Lv. 175]"
					NameQuest = "SkyQuest"
					QuestLv = 2
					NameMon = "Dark Master"
					CFrameQ = CFrame.new(-4839.53027, 716.368591, -2619.44165, 0.866007268, 0, 0.500031412, 0, 1, 0, -0.500031412, 0, 0.866007268)
					CFrameMon = CFrame.new(-5235.76172, 400.407043, -2366.71899)
					CFrameMon2 = CFrame.new(-5171.20557, 400.632629, -2243.04346)
					CFrameMon3 = CFrame.new(-5244.14307, 400.553833, -2154.95386)
					CFrameMon4 = CFrame.new(-5338.07666, 400.419495, -2256.87036)
					CFrameMon5 = CFrame.new(-5235.76172, 400.407043, -2366.71899)
					CFrameMon6 = CFrame.new(-5171.20557, 400.632629, -2243.04346)
					CFrameMon7 = CFrame.new(-5244.14307, 400.553833, -2154.95386)
					CFrameMon8 = CFrame.new(-5338.07666, 400.419495, -2256.87036)
					TelePBoss(CFrameQ)
					SelectMonster = "Sky Bandit [Lv. 150]"
				elseif Lv == 190 or Lv <= 209 and SelectMonster == "Prisoner [Lv. 190]" then
					Ms = "Prisoner [Lv. 190]"
					QuestLv = 1
					NameQuest = "PrisonerQuest"
					NameMon = "Prisoner"
					CFrameQ = CFrame.new(5308.93115, 1.65517521, 475.120514, -0.0894274712, -5.00292918e-09, -0.995993316, 1.60817859e-09, 1, -5.16744869e-09, 0.995993316, -2.06384709e-09, -0.0894274712)
					CFrameMon = CFrame.new(4937.33154, 30.1021862, 649.563477)
					CFrameMon2 = CFrame.new(5065.7749, 30.43290985, 546.996643)
					CFrameMon3 = CFrame.new(5088.85205, 30.63439715, 424.919891)
					CFrameMon4 = CFrame.new(5223.32422, 30.45370162, 449.392792)
					CFrameMon5 = CFrame.new(5350.27783, 30.8864578, 391.263519)
					CFrameMon6 = CFrame.new(4937.33154, 30.1021862, 649.563477)
					CFrameMon7 = CFrame.new(5065.7749, 30.43290985, 546.996643)
					CFrameMon8 = CFrame.new(5088.85205, 30.63439715, 424.919891)
					TelePBoss(CFrameQ)
				elseif Lv == 210 or Lv <= 249 or SelectMonster == "Dangerous Prisoner [Lv. 210]" then
					 
					Ms = "Dangerous Prisoner [Lv. 210]"
					QuestLv = 2
					NameQuest = "PrisonerQuest"
					NameMon = "Dangerous Prisoner"
					CFrameQ = CFrame.new(5308.93115, 1.65517521, 475.120514, -0.0894274712, -5.00292918e-09, -0.995993316, 1.60817859e-09, 1, -5.16744869e-09, 0.995993316, -2.06384709e-09, -0.0894274712)
					CFrameMon = CFrame.new(5485.27686, 30.48984313, 468.049164)
					CFrameMon2 = CFrame.new(5553.6123, 30.37830436, 583.482605)
					CFrameMon3 = CFrame.new(5645.55957, 30.49353886, 764.599121)
					CFrameMon4 = CFrame.new(5561.3667, 30.4825983, 964.727722)
					CFrameMon5 = CFrame.new(5442.04785, 30.43965244, 1078.86829)
					CFrameMon6 = CFrame.new(5101.04688, 30.43209672, 1056.52319)
					CFrameMon7 = CFrame.new(4955.92383, 30.43116331, 925.554199)
					CFrameMon8 = CFrame.new(4955.92383, 30.43116331, 925.554199)
					TelePBoss(CFrameQ)
					if Lv >= 240 then
						_G.SelectBoss = "Swan [Lv. 240] [Boss]"
						
					elseif Lv >= 230 then
						_G.SelectBoss = "Chief Warden [Lv. 230] [Boss]"
						
					elseif Lv >= 220 then
						_G.SelectBoss = "Warden [Lv. 220] [Boss]"
					end
					SelectMonster = "Prisoner [Lv. 190]"
				elseif Lv == 250 or Lv <= 274 or SelectMonster == "Toga Warrior [Lv. 250]" then -- Toga Warrior
					 
					Ms = "Toga Warrior [Lv. 250]"
					NameQuest = "ColosseumQuest"
					QuestLv = 1
					NameMon = "Toga Warrior"
					CFrameQ = CFrame.new(-1576.11743, 7.38933945, -2983.30762, 0.576966345, 1.22114863e-09, 0.816767931, -3.58496594e-10, 1, -1.24185606e-09, -0.816767931, 4.2370063e-10, 0.576966345)
					CFrameMon = CFrame.new(-1671.87439, 30.46971226, -2684.46704)
					CFrameMon2 = CFrame.new(-1798.56873, 30.69850779, -2852.0918)
					CFrameMon3 = CFrame.new(-1839.27844, 30.54717255, -2670.43506)
					CFrameMon4 = CFrame.new(-2056.15601, 30.7379818, -2713.5896)
					CFrameMon5 = CFrame.new(-2128.38818, 30.74061298, -2853.23096)
					CFrameMon6 = CFrame.new(-1671.87439, 30.46971226, -2684.46704)
					CFrameMon7 = CFrame.new(-1798.56873, 30.69850779, -2852.0918)
					CFrameMon8 = CFrame.new(-1839.27844, 30.54717255, -2670.43506)
					TelePBoss(CFrameQ)
					
				elseif Lv == 275 or Lv <= 299 or SelectMonster == "Gladiator [Lv. 275]" then -- Gladiato
					 
					Ms = "Gladiator [Lv. 275]"
					NameQuest = "ColosseumQuest"
					QuestLv = 2
					NameMon = "Gladiato"
					CFrameQ = CFrame.new(-1576.11743, 7.38933945, -2983.30762, 0.576966345, 1.22114863e-09, 0.816767931, -3.58496594e-10, 1, -1.24185606e-09, -0.816767931, 4.2370063e-10, 0.576966345)
					CFrameMon = CFrame.new(-1483.69543, 30.23153687, -3195.19263)
					CFrameMon2 = CFrame.new(-1370.75085, 30.02963066, -3375.76953)
					CFrameMon3 = CFrame.new(-1356.93213, 30.05916834, -3590.58716)
					CFrameMon4 = CFrame.new(-1125.12451, 30.91520119, -3270.04932)
					CFrameMon5 = CFrame.new(-1228.21082, 30.91372013, -3051.61963)
					CFrameMon6 = CFrame.new(-1483.69543, 30.23153687, -3195.19263)
					CFrameMon7 = CFrame.new(-1370.75085, 30.02963066, -3375.76953)
					CFrameMon8 = CFrame.new(-1356.93213, 30.05916834, -3590.58716)
					TelePBoss(CFrameQ)
					SelectMonster = "Toga Warrior [Lv. 250]"
				elseif Lv == 300 or Lv <= 324 or SelectMonster == "Military Soldier [Lv. 300]" then -- Military Soldier
					Ms = "Military Soldier [Lv. 300]"
					NameQuest = "MagmaQuest"
					QuestLv = 1
					NameMon = "Military Soldier"
					CFrameQ = CFrame.new(-5316.55859, 12.2370615, 8517.2998, 0.588437557, -1.37880001e-08, -0.808542669, -2.10116209e-08, 1, -3.23446478e-08, 0.808542669, 3.60215964e-08, 0.588437557)
					CFrameMon = CFrame.new(-5287.19775, 30.68863678, 8659.86328)
					CFrameMon2 = CFrame.new(-5412.09326, 30.3730135, 8591.76855)
					CFrameMon3 = CFrame.new(-5439.79492, 30.07931805, 8349.15137)
					CFrameMon4 = CFrame.new(-5565.604, 30.28863716, 8327.56641)
					CFrameMon5 = CFrame.new(-5667.80664, 30.28863716, 8428.66992)
					CFrameMon6 = CFrame.new(-5287.19775, 30.68863678, 8659.86328)
					CFrameMon7 = CFrame.new(-5412.09326, 30.3730135, 8591.76855)
					CFrameMon8 = CFrame.new(-5439.79492, 30.07931805, 8349.15137)
					TelePBoss(CFrameQ)
					
				elseif Lv == 325 or Lv <= 374 or SelectMonster == "Military Spy [Lv. 325]" then -- Military Spy
					 
					Ms = "Military Spy [Lv. 325]"
					NameQuest = "MagmaQuest"
					QuestLv = 2
					NameMon = "Military Spy"
					CFrameQ = CFrame.new(-5316.55859, 12.2370615, 8517.2998, 0.588437557, -1.37880001e-08, -0.808542669, -2.10116209e-08, 1, -3.23446478e-08, 0.808542669, 3.60215964e-08, 0.588437557)
					CFrameMon = CFrame.new(-5786.98828, 100.5823822, 8651.63672)
					CFrameMon2 = CFrame.new(-5857.32812, 100.6921616, 8775.98242)
					CFrameMon3 = CFrame.new(-5916.4082, 100.9983063, 8845.14355)
					CFrameMon4 = CFrame.new(-5806.90088, 100.4439621, 8903.08789)
					CFrameMon5 = CFrame.new(-5786.98828, 100.5823822, 8651.63672)
					CFrameMon6 = CFrame.new(-5857.32812, 100.6921616, 8775.98242)
					CFrameMon7 = CFrame.new(-5916.4082, 100.9983063, 8845.14355)
					CFrameMon8 = CFrame.new(-5806.90088, 100.4439621, 8903.08789)
					TelePBoss(CFrameQ)
					if Lv >= 350 then
						_G.SelectBoss = "Magma Admiral [Lv. 350] [Boss]"
					end
					SelectMonster = "Military Soldier [Lv. 300]"
				elseif Lv == 375 or Lv <= 399 or SelectMonster == "Fishman Warrior [Lv. 375]" then -- Fishman Warrior
					 
					Ms = "Fishman Warrior [Lv. 375]"
					NameQuest = "FishmanQuest"
					QuestLv = 1
					NameMon = "Fishman Warrior"
					CFrameQ = CFrame.new(61122.5625, 18.4716396, 1568.16504, 0.893533468, 3.95251609e-09, 0.448996574, -2.34327455e-08, 1, 3.78297464e-08, -0.448996574, -4.43233645e-08, 0.893533468)
					CFrameMon = CFrame.new(60943.918, 40.9676781, 1744.12366)
					CFrameMon2 = CFrame.new(60841.9023, 40.9637394, 1651.12573)
					CFrameMon3 = CFrame.new(60788.9023, 40.1695957, 1526.11133)
					CFrameMon4 = CFrame.new(60905.6641, 40.2607841, 1470.10828)
					CFrameMon5 = CFrame.new(60947.5195, 40.2365685, 1377.84827)
					CFrameMon6 = CFrame.new(60840.9023, 40.1695957, 1301.12561)
					CFrameMon7 = CFrame.new(60926.3203, 40.2709007, 1179.21045)
					CFrameMon8 = CFrame.new(60840.9023, 40.1695957, 1301.12561)
					if Auto_Farm and (CFrameMon.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 3000 then
						_G.Stop_Tween = true
						TP(CFrameQ)
						wait(.5)
						game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(61163.8515625, 11.6796875, 1819.7841796875))
						wait(.5)
						_G.Stop_Tween = nil
					end
					
				elseif Lv == 400 or Lv <= 449 or SelectMonster == "Fishman Commando [Lv. 400]" then -- Fishman Commando
					 
					Ms = "Fishman Commando [Lv. 400]"
					NameQuest = "FishmanQuest"
					QuestLv = 2
					NameMon = "Fishman Commando"
					CFrameQ = CFrame.new(61122.5625, 18.4716396, 1568.16504)
					CFrameMon = CFrame.new(61699.625, 40.2699566, 1520.59375)
					CFrameMon2 = CFrame.new(61760.9062, 40.2607517, 1460.12573)
					CFrameMon3 = CFrame.new(61785.5391, 40.3575878, 1286.50964)
					CFrameMon4 = CFrame.new(62051.4727, 40.418438, 1419.75146)
					CFrameMon5 = CFrame.new(61977.8516, 40.4545078, 1615.34143)
					CFrameMon6 = CFrame.new(61856.6602, 40.2217426, 1695.47583)
					CFrameMon7 = CFrame.new(61699.625, 40.2699566, 1520.59375)
					CFrameMon8 = CFrame.new(61760.9062, 40.2607517, 1460.12573)
					if Auto_Farm and (CFrameMon.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 3000 then
						_G.Stop_Tween = true
						TP(CFrameQ)
						wait(.5)
						game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(61163.8515625, 11.6796875, 1819.7841796875))
						wait(.5)
						_G.Stop_Tween = nil
					end
					if Lv >= 425 then
						_G.SelectBoss = "Fishman Lord [Lv. 425] [Boss]"
					end
					SelectMonster = "Fishman Warrior [Lv. 375]"
				elseif Lv == 450 or Lv <= 474 or SelectMonster == "God's Guard [Lv. 450]" then 
					Ms = "God's Guard [Lv. 450]"
					NameQuest = "SkyExp1Quest"
					QuestLv = 1
					NameMon = "God's Guards"
					CFrameQ = CFrame.new(-4721.71436, 845.277161, -1954.20105)
					CFrameMon = CFrame.new(-4700.29004, 880.319214, -1793.46985)
					CFrameMon2 = CFrame.new(-4830.60791, 880.985046, -1779.0907)
					CFrameMon3 = CFrame.new(-4864.05322, 880.410156, -1909.01013)
					CFrameMon4 = CFrame.new(-4820.02979, 880.343811, -2048.61499)
					CFrameMon5 = CFrame.new(-4618.6333, 880.07782, -2043.47839)
					CFrameMon6 = CFrame.new(-4583.79443, 880.31604, -1939.10498)
					CFrameMon7 = CFrame.new(-4700.29004, 880.319214, -1793.46985)
					CFrameMon8 = CFrame.new(-4830.60791, 880.985046, -1779.0907)
					if Auto_Farm and (CFrameMon.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 3000 then
						_G.Stop_Tween = true
						TP(CFrameQ)
						wait(.5)
						game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(-4607.82275, 872.54248, -1667.55688))
						wait(.5)
						_G.Stop_Tween = nil
					end
					if Lv >= 425 then
						_G.SelectBoss = "Fishman Lord [Lv. 425] [Boss]"
					end
					SelectMonster = "Fishman Commando [Lv. 400]"
				elseif Lv == 475 or Lv <= 524 or SelectMonster == "Shanda [Lv. 475]" then
					Ms = "Shanda [Lv. 475]"
					NameQuest = "SkyExp1Quest"
					QuestLv = 2
					NameMon = "Gorilla"
					CFrameQ = CFrame.new(-7859.09814, 5544.19043, -381.476196, -0.422592998, 0, 0.906319618, 0, 1, 0, -0.906319618, 0, -0.422592998)
					CFrameMon = CFrame.new(-7787.81494140625, 5600.49169921875, -502.2948303222656)
					CFrameMon2 = CFrame.new(-7725.74072, 5600.29004, -585.480713)
					CFrameMon3 = CFrame.new(-7595.16895, 5600.93994, -653.530457)
					CFrameMon4 = CFrame.new(-7540.33887, 5600.27539, -517.048096)
					CFrameMon5 = CFrame.new(-7564.64746, 5600.68262, -418.750336)
					CFrameMon6 = CFrame.new(-7564.64746, 5600.68262, -418.750336)
					CFrameMon7 = CFrame.new(-7709.42822, 5600.29492, -337.002502)
					CFrameMon8 = CFrame.new(-7709.42822, 5600.29492, -337.002502)
					if Auto_Farm and (CFrameMon.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 3000 then
						_G.Stop_Tween = true
						TP(CFrameQ)
						wait(.5)
						game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(-7894.6176757813, 5547.1416015625, -380.29119873047))
						wait(.5)
						_G.Stop_Tween = nil
					end
					if Lv >= 500 then
						_G.SelectBoss = "Wysper [Lv. 500] [Boss]"
					end
					SelectMonster = "God's Guard [Lv. 450]"
				elseif Lv == 525 or Lv <= 549 or SelectMonster == "Royal Squad [Lv. 525]" then -- Royal Squad
					 
					Ms = "Royal Squad [Lv. 525]"
					NameQuest = "SkyExp2Quest"
					QuestLv = 1
					NameMon = "Royal Squad"
					CFrameQ = CFrame.new(-7906.81592, 5634.6626, -1411.99194, 0, 0, -1, 0, 1, 0, 1, 0, 0)
					CFrameMon = CFrame.new(-7841.7041, 5630.08496, -1403.62402)
					CFrameMon2 = CFrame.new(-7724.96143, 5630.62109, -1510.87366)
					CFrameMon3 = CFrame.new(-7669.97656, 5630.33398, -1379.02832)
					CFrameMon4 = CFrame.new(-7513.9126, 5630.75098, -1420.87598)
					CFrameMon5 = CFrame.new(-7528.86475, 5630.06201, -1537.9574)
					CFrameMon6 = CFrame.new(-7841.7041, 5630.08496, -1403.62402)
					CFrameMon7 = CFrame.new(-7724.96143, 5630.62109, -1510.87366)
					CFrameMon8 = CFrame.new(-7669.97656, 5630.33398, -1379.02832)
					TelePBoss(CFrameQ) 
					SelectMonster = "Shanda [Lv. 475]"
				elseif Lv == 550 or Lv <= 624 or SelectMonster == "Royal Soldier [Lv. 550]" then -- Royal Soldier
					 
					Ms = "Royal Soldier [Lv. 550]"
					NameQuest = "SkyExp2Quest"
					QuestLv = 2
					NameMon = "Royal Soldier"
					CFrameQ = CFrame.new(-7906.81592, 5634.6626, -1411.99194, 0, 0, -1, 0, 1, 0, 1, 0, 0)
					CFrameMon = CFrame.new(-7935.60889, 5630.03613, -1624.62866)
					CFrameMon2 = CFrame.new(-7916.33789, 5630.62305, -1719.72119)
					CFrameMon3 = CFrame.new(-7946.00195, 5630.05859, -1822.9917)
					CFrameMon4 = CFrame.new(-7759.49854, 5630.90527, -1862.73206)
					CFrameMon5 = CFrame.new(-7761.07422, 5630.06641, -1720.46008)
					CFrameMon6 = CFrame.new(-7935.60889, 5630.03613, -1624.62866)
					CFrameMon7 = CFrame.new(-7916.33789, 5630.62305, -1719.72119)
					CFrameMon8 = CFrame.new(-7946.00195, 5630.05859, -1822.9917)
					TelePBoss(CFrameQ)
					if Lv >= 575 then
						_G.SelectBoss = "Thunder God [Lv. 575] [Boss]"
					end
					SelectMonster = "Royal Squad [Lv. 525]"
				elseif Lv == 625 or Lv <= 649 or SelectMonster == "Galley Pirate [Lv. 625]" then -- Galley Pirate
					 
					Ms = "Galley Pirate [Lv. 625]"
					NameQuest = "FountainQuest"
					QuestLv = 1
					NameMon = "Galley Pirate"
					CFrameQ = CFrame.new(5259.81982, 37.3500175, 4050.0293, 0.087131381, 0, 0.996196866, 0, 1, 0, -0.996196866, 0, 0.087131381)
					CFrameMon = CFrame.new(5348.28906, 70.2900734, 3953.27271)
					CFrameMon2 = CFrame.new(5522.05127, 70.2985611, 3934.32764)
					CFrameMon3 = CFrame.new(5483.07275, 80.2408676, 4059.32227)
					CFrameMon4 = CFrame.new(5654.06592, 70.2936058, 3914.33545)
					CFrameMon5 = CFrame.new(5717.08154, 80.5104256, 4042.30713)
					CFrameMon6 = CFrame.new(5838.05615, 75.3037033, 3914.26831)
					CFrameMon7 = CFrame.new(5348.28906, 70.2900734, 3953.27271)
					CFrameMon8 = CFrame.new(5522.05127, 70.2985611, 3934.32764)
					TelePBoss(CFrameQ)
				elseif Lv >= 650 or SelectMonster == "Galley Captain [Lv. 650]" then -- Galley Captain
					 
					Ms = "Galley Captain [Lv. 650]"
					NameQuest = "FountainQuest"
					QuestLv = 2
					NameMon = "Galley Captain"
					CFrameQ = CFrame.new(5259.81982, 37.3500175, 4050.0293, 0.087131381, 0, 0.996196866, 0, 1, 0, -0.996196866, 0, 0.087131381)
					CFrameMon = CFrame.new(5416.99805, 80.5530357, 4780.41553)
					CFrameMon2 = CFrame.new(5352.02979, 60.6015701, 4929.40381)
					CFrameMon3 = CFrame.new(5580.05811, 70.2926521, 4887.41357)
					CFrameMon4 = CFrame.new(5557.02441, 60.6046066, 4996.39062)
					CFrameMon5 = CFrame.new(5792.35107, 80.9391937, 4823.94287)
					CFrameMon6 = CFrame.new(5892.34326, 60.6050987, 4951.91113)
					CFrameMon7 = CFrame.new(5954.96387, 60.5344315, 4882.104)
					CFrameMon8 = CFrame.new(5922.35742, 80.6824799, 4765.85303)
					TelePBoss(CFrameQ)
					
					if Lv >= 675 then
						_G.SelectBoss = "Cyborg [Lv. 675] [Boss]"
					end
					SelectMonster = "Galley Pirate [Lv. 625]"
				end
			end
			if New_World and not Auto_Raid then
				 
				if Lv == 700 or Lv <= 724 or SelectMonster == "Raider [Lv. 700]" then -- Raider [Lv. 700]
					Ms = "Raider [Lv. 700]"
					NameQuest = "Area1Quest"
					QuestLv = 1
					NameMon = "Raider"
					CFrameQ = CFrame.new(-429.543518, 71.7699966, 1836.18188, -0.22495985, 0, -0.974368095, 0, 1, 0, 0.974368095, 0, -0.22495985)
					CFrameMon = CFrame.new(265.562622, 50.051445, 2497.43481)
					CFrameMon2 = CFrame.new(475.539307, 50.7705688, 2433.41528)
					CFrameMon3 = CFrame.new(549.550598, 50.7821999, 2190.44897)
					CFrameMon4 = CFrame.new(241.562622, 50.9522018, 2195.46753)
					CFrameMon5 = CFrame.new(-612.431946, 50.7861061, 2557.42017)
					CFrameMon6 = CFrame.new(-607.841309, 50.2306099, 2204.09521)
					CFrameMon7 = CFrame.new(-917.401367, 50.7533951, 2250.45459)
					CFrameMon8 = CFrame.new(-904.317383, 50.7743683, 2501.42383)
					TelePBoss(CFrameQ)
				elseif Lv == 725 or Lv <= 774 or SelectMonster == "Mercenary [Lv. 725]" then -- Mercenary [Lv. 725]
					Ms = "Mercenary [Lv. 725]"
					NameQuest = "Area1Quest"
					QuestLv = 2
					NameMon = "Mercenary"
					CFrameQ = CFrame.new(-429.543518, 71.7699966, 1836.18188, -0.22495985, 0, -0.974368095, 0, 1, 0, 0.974368095, 0, -0.22495985)
					CFrameMon = CFrame.new(-924.691284, 90.7750931, 1788.09863)
					CFrameMon2 = CFrame.new(-1085.13818, 90.7490768, 1696.39294)
					CFrameMon3 = CFrame.new(-915.357422, 90.0287857, 1574.66357)
					CFrameMon4 = CFrame.new(-1135.89746, 90.1187363, 1246.63953)
					CFrameMon5 = CFrame.new(-1209.23328, 90.7195435, 1073.02075)
					CFrameMon6 = CFrame.new(-988.285217, 90.1274414, 1087.69702)
					CFrameMon7 = CFrame.new(-924.691284, 90.7750931, 1788.09863)
					CFrameMon8 = CFrame.new(-1085.13818, 90.7490768, 1696.39294)
					TelePBoss(CFrameQ)
					SelectMonster = "Raider [Lv. 700]"
				elseif Lv == 775 or Lv <= 799 or SelectMonster == "Swan Pirate [Lv. 775]" then -- Swan Pirate [Lv. 775]
					Ms = "Swan Pirate [Lv. 775]"
					NameQuest = "Area2Quest"
					QuestLv = 1
					NameMon = "Swan Pirate"
					CFrameQ = CFrame.new(638.43811, 71.769989, 918.282898, 0.139203906, 0, 0.99026376, 0, 1, 0, -0.99026376, 0, 0.139203906)
					CFrameMon = CFrame.new(823.615295, 90.7710724, 1162.20508)
					CFrameMon2 = CFrame.new(967.173828, 90.8330917, 1180.75647)
					CFrameMon3 = CFrame.new(1066.99438, 90.8330917, 1080.91797)
					CFrameMon4 = CFrame.new(1063.20959, 90.7636032, 1399.74609)
					CFrameMon5 = CFrame.new(984.6474, 90.7639771, 1401.67834)
					CFrameMon6 = CFrame.new(827.783386, 90.7645111, 1326.89404)
					CFrameMon7 = CFrame.new(823.615295, 90.7710724, 1162.20508)
					CFrameMon8 = CFrame.new(967.173828, 90.8330917, 1180.75647)
					TelePBoss(CFrameQ)
				elseif Lv == 800 or Lv <= 874 or SelectMonster == "Factory Staff [Lv. 800]" then -- Factory Staff [Lv. 800]
					Ms = "Factory Staff [Lv. 800]"
					NameQuest = "Area2Quest"
					QuestLv = 2
					NameMon = "Factory Staff"
					CFrameQ = CFrame.new(638.43811, 71.769989, 918.282898, 0.139203906, 0, 0.99026376, 0, 1, 0, -0.99026376, 0, 0.139203906)
					CFrameMon = CFrame.new(936.100891, 90.7891922, -71.2398453)
					CFrameMon2 = CFrame.new(692.110413, 90.8410339, 227.752106)
					CFrameMon3 = CFrame.new(386.107452, 90.8410339, 91.7514038)
					CFrameMon4 = CFrame.new(-92.731041, 90.1639786, -32.960495)
					CFrameMon5 = CFrame.new(-426.878845, 90.8410339, -367.267761)
					CFrameMon6 = CFrame.new(-105.888847, 90.7819061, -670.231934)
					CFrameMon7 = CFrame.new(936.100891, 90.7891922, -71.2398453)
					CFrameMon8 = CFrame.new(692.110413, 90.8410339, 227.752106)
					TelePBoss(CFrameQ)
					SelectMonster = "Swan Pirate [Lv. 775]"
				elseif Lv == 875 or Lv <= 899 or SelectMonster == "Marine Lieutenant [Lv. 875]" then -- Marine Lieutenant [Lv. 875]
					Ms = "Marine Lieutenant [Lv. 875]"
					NameQuest = "MarineQuest3"
					QuestLv = 1
					NameMon = "Marine Lieutenant"
					CFrameQ = CFrame.new(-2440.79639, 71.7140732, -3216.06812, 0.866007268, 0, 0.500031412, 0, 1, 0, -0.500031412, 0, 0.866007268)
					CFrameMon = CFrame.new(-2583.93091, 90.8043213, -3039.63013)
					CFrameMon2 = CFrame.new(-2766.0686, 90.8153305, -3144.73267)
					CFrameMon3 = CFrame.new(-3012.86523, 90.8052673, -2921.84399)
					CFrameMon4 = CFrame.new(-3258.53369, 90.8076172, -2990.86768)
					CFrameMon5 = CFrame.new(-2932.48462, 90.8056259, -2604.10669)
					CFrameMon6 = CFrame.new(-2583.93091, 90.8043213, -3039.63013)
					CFrameMon7 = CFrame.new(-2766.0686, 90.8153305, -3144.73267)
					CFrameMon8 = CFrame.new(-3012.86523, 90.8052673, -2921.84399)
					TelePBoss(CFrameQ)
				elseif Lv == 900 or Lv <= 949 or SelectMonster == "Marine Captain [Lv. 900]" then -- Marine Captain [Lv. 900]
					Ms = "Marine Captain [Lv. 900]"
					NameQuest = "MarineQuest3"
					QuestLv = 2
					NameMon = "Marine Captain"
					CFrameQ = CFrame.new(-2440.79639, 71.7140732, -3216.06812, 0.866007268, 0, 0.500031412, 0, 1, 0, -0.500031412, 0, 0.866007268)
					CFrameMon = CFrame.new(-2105.40601, 90.6410751, -3260.68042)
					CFrameMon2 = CFrame.new(-2030.24768, 90.9695282, -3477.63477)
					CFrameMon3 = CFrame.new(-1928.38892, 90.9695282, -3119.57959)
					CFrameMon4 = CFrame.new(-1808.03503, 90.2457352, -3313.89746)
					CFrameMon5 = CFrame.new(-1603.00159, 90.1955719, -3314.84521)
					CFrameMon6 = CFrame.new(-2105.40601, 90.6410751, -3260.68042)
					CFrameMon7 = CFrame.new(-2030.24768, 90.9695282, -3477.63477)
					CFrameMon8 = CFrame.new(-1928.38892, 90.9695282, -3119.57959)
					TelePBoss(CFrameQ)
					SelectMonster = "Marine Lieutenant [Lv. 875]"
				elseif Lv == 950 or Lv <= 974 or SelectMonster == "Zombie [Lv. 950]" then -- Zombie [Lv. 950]
					Ms = "Zombie [Lv. 950]"
					NameQuest = "ZombieQuest"
					QuestLv = 1
					NameMon = "Zombie"
					CFrameQ = CFrame.new(-5497.06152, 47.5923004, -795.237061, -0.29242146, 0, -0.95628953, 0, 1, 0, 0.95628953, 0, -0.29242146)
					CFrameMon = CFrame.new(-5510.59229, 60.6537132, -847.672302)
					CFrameMon2 = CFrame.new(-5613.43359, 60.1997719, -937.974243)
					CFrameMon3 = CFrame.new(-5765.74951, 60.6884003, -826.096375)
					CFrameMon4 = CFrame.new(-5855.54834, 90.018486, -740.286621)
					CFrameMon5 = CFrame.new(-5761.98535, 60.35355, -654.943359)
					CFrameMon6 = CFrame.new(-5595.59229, 60.256424, -524.287292)
					CFrameMon7 = CFrame.new(-5510.59229, 60.6537132, -847.672302)
					CFrameMon8 = CFrame.new(-5613.43359, 60.1997719, -937.974243)
					TelePBoss(CFrameQ)
				elseif Lv == 975 or Lv <= 999 or SelectMonster == "Vampire [Lv. 975]" then -- Vampire [Lv. 975]
					Ms = "Vampire [Lv. 975]"
					NameQuest = "ZombieQuest"
					QuestLv = 2
					NameMon = "Vampire"
					CFrameQ = CFrame.new(-5497.06152, 47.5923004, -795.237061, -0.29242146, 0, -0.95628953, 0, 1, 0, 0.95628953, 0, -0.29242146)
					CFrameMon = CFrame.new(-6038.21533, 30.60701132, -1100.01733)
					CFrameMon2 = CFrame.new(-5776.56689, 30.19985104, -1373.43335)
					CFrameMon3 = CFrame.new(-5952.97754, 30.70087671, -1568.36951)
					CFrameMon4 = CFrame.new(-6130.99219, 30.06086016, -1465.32556)
					CFrameMon5 = CFrame.new(-6276.0293, 30.6362915, -1270.61499)
					CFrameMon6 = CFrame.new(-6038.21533, 30.60701132, -1100.01733)
					CFrameMon7 = CFrame.new(-5776.56689, 30.19985104, -1373.43335)
					CFrameMon8 = CFrame.new(-5952.97754, 30.70087671, -1568.36951)
					TelePBoss(CFrameQ)
					SelectMonster = "Zombie [Lv. 950]"
				elseif Lv == 1000 or Lv <= 1049 or SelectMonster == "Snow Trooper [Lv. 1000]" then -- Snow Trooper [Lv. 1000] **
					Ms = "Snow Trooper [Lv. 1000]"
					NameQuest = "SnowMountainQuest"
					QuestLv = 1
					NameMon = "Snow Trooper"
					CFrameQ = CFrame.new(609.858826, 400.119904, -5372.25928, -0.374604106, 0, 0.92718488, 0, 1, 0, -0.92718488, 0, -0.374604106)
					CFrameMon = CFrame.new(430.4216, 430.745422, -5069.31396)
					CFrameMon2 = CFrame.new(392.417816, 430.660065, -5207.88477)
					CFrameMon3 = CFrame.new(436.43045, 450.987854, -5467.16504)
					CFrameMon4 = CFrame.new(484.540863, 430.748322, -5472.30225)
					CFrameMon5 = CFrame.new(641.43457, 430.701202, -5453.10303)
					CFrameMon6 = CFrame.new(572.734924, 430.165436, -5605.1333)
					CFrameMon7 = CFrame.new(716.612183, 430.156342, -5706.35547)
					CFrameMon8 = CFrame.new(392.417816, 430.660065, -5207.88477)
					TelePBoss(CFrameQ)
				elseif Lv == 1050 or Lv <= 1099 or SelectMonster == "Winter Warrior [Lv. 1050]" then -- Winter Warrior [Lv. 1050]
					Ms = "Winter Warrior [Lv. 1050]"
					NameQuest = "SnowMountainQuest"
					QuestLv = 2
					NameMon = "Winter Warrior"
					CFrameQ = CFrame.new(609.858826, 400.119904, -5372.25928, -0.374604106, 0, 0.92718488, 0, 1, 0, -0.92718488, 0, -0.374604106)
					CFrameMon = CFrame.new(1044.96838, 450.593323, -5049.94287)
					CFrameMon2 = CFrame.new(1142.43262, 450.232819, -5043.06494)
					CFrameMon3 = CFrame.new(1226.46851, 450.477966, -5216.06689)
					CFrameMon4 = CFrame.new(1205.46912, 450.21579, -5397.3418)
					CFrameMon5 = CFrame.new(1446.13562, 450.495361, -5369.10449)
					CFrameMon6 = CFrame.new(1371.82556, 450.545044, -5196.37695)
					CFrameMon7 = CFrame.new(1044.96838, 450.593323, -5049.94287)
					CFrameMon8 = CFrame.new(1142.43262, 450.232819, -5043.06494)
					TelePBoss(CFrameQ)
					SelectMonster = "Snow Trooper [Lv. 1000]"
				elseif Lv == 1100 or Lv <= 1124 or SelectMonster == "Lab Subordinate [Lv. 1100]" then -- Lab Subordinate [Lv. 1100]
					Ms = "Lab Subordinate [Lv. 1100]"
					NameQuest = "IceSideQuest"
					QuestLv = 1
					NameMon = "Lab Subordinate"
					CFrameQ = CFrame.new(-6064.06885, 15.2422857, -4902.97852, 0.453972578, -0, -0.891015649, 0, 1, -0, 0.891015649, 0, 0.453972578)
					CFrameMon = CFrame.new(-5640.40674, 30.7589941, -4680.94629)
					CFrameMon2 = CFrame.new(-5897.82178, 30.2995815, -4554.60498)
					CFrameMon3 = CFrame.new(-5963.45996, 30.7573175, -4340.27393)
					CFrameMon4 = CFrame.new(-5766.34863, 30.7593508, -4249.68555)
					CFrameMon5 = CFrame.new(-5590.31738, 30.7585506, -4436.54688)
					CFrameMon6 = CFrame.new(-5640.40674, 30.7589941, -4680.94629)
					CFrameMon7 = CFrame.new(-5897.82178, 30.2995815, -4554.60498)
					CFrameMon8 = CFrame.new(-5963.45996, 30.7573175, -4340.27393)
					TelePBoss(CFrameQ)
				elseif Lv == 1125 or Lv <= 1174 or SelectMonster == "Horned Warrior [Lv. 1125]" then -- Horned Warrior [Lv. 1125]
					Ms = "Horned Warrior [Lv. 1125]"
					NameQuest = "IceSideQuest"
					QuestLv = 2
					NameMon = "Horned Warrior"
					CFrameQ = CFrame.new(-6064.06885, 15.2422857, -4902.97852, 0.453972578, -0, -0.891015649, 0, 1, -0, 0.891015649, 0, 0.453972578)
					CFrameMon = CFrame.new(-6499.00146, 30.6707783, -5514.1167)
					CFrameMon2 = CFrame.new(-6588.12061, 30.6189499, -5719.7002)
					CFrameMon3 = CFrame.new(-6516.33154, 30.7509747, -5868.68945)
					CFrameMon4 = CFrame.new(-6331.74854, 30.7566242, -5778.93115)
					CFrameMon5 = CFrame.new(-6221.72314, 30.7332659, -5951.27881)
					CFrameMon6 = CFrame.new(-6093.67139, 30.5871658, -6061.11035)
					CFrameMon7 = CFrame.new(-6499.00146, 30.6707783, -5514.1167)
					CFrameMon8 = CFrame.new(-6588.12061, 30.6189499, -5719.7002)
					TelePBoss(CFrameQ)
					SelectMonster = "Lab Subordinate [Lv. 1100]"
				elseif Lv == 1175 or Lv <= 1199 or SelectMonster == "Magma Ninja [Lv. 1175]" then -- Magma Ninja [Lv. 1175]
					Ms = "Magma Ninja [Lv. 1175]"
					NameQuest = "FireSideQuest"
					QuestLv = 1
					NameMon = "Magma Ninja"
					CFrameQ = CFrame.new(-5428.03174, 15.0622921, -5299.43457, -0.882952213, 0, 0.469463557, 0, 1, 0, -0.469463557, 0, -0.882952213)
					CFrameMon = CFrame.new(-5803.59277, 40.6432133, -5710.04443)
					CFrameMon2 = CFrame.new(-5768.63623, 40.7313824, -5945.5708)
					CFrameMon3 = CFrame.new(-5560.96436, 40.92278, -5804.56348)
					CFrameMon4 = CFrame.new(-5206.89893, 40.0855122, -5977.41162)
					CFrameMon5 = CFrame.new(-5099.0918, 40.9871378, -6115.96631)
					CFrameMon6 = CFrame.new(-5259.62549, 40.1081581, -6288.00146)
					CFrameMon7 = CFrame.new(-5803.59277, 40.6432133, -5710.04443)
					CFrameMon8 = CFrame.new(-5768.63623, 40.7313824, -5945.5708)
					TelePBoss(CFrameQ)
				elseif Lv == 1200 or Lv <= 1249 or SelectMonster == "Lava Pirate [Lv. 1200]" then 
					Ms = "Lava Pirate [Lv. 1200]"
					NameQuest = "FireSideQuest"
					QuestLv = 2
					NameMon = "Lava Pirate"
					CFrameQ = CFrame.new(-5431.09473, 15.9868021, -5296.53223, 0.831796765, 1.15322464e-07, -0.555080295, -1.10814341e-07, 1, 4.17010995e-08, 0.555080295, 2.68240168e-08, 0.831796765)
					CFrameMon = CFrame.new(-5340.02832, 40.195673, -4935.52588)
					CFrameMon2 = CFrame.new(-5431.78369, 40.1615105, -4642.13184)
					CFrameMon3 = CFrame.new(-5264.50244, 40.1666908, -4343.44482)
					CFrameMon4 = CFrame.new(-5159.77588, 40.1742325, -4652.88818)
					CFrameMon5 = CFrame.new(-4942.99365, 50.9293747, -4791.62109)
					CFrameMon6 = CFrame.new(-5340.02832, 40.195673, -4935.52588)
					CFrameMon7 = CFrame.new(-5431.78369, 40.1615105, -4642.13184)
					CFrameMon8 = CFrame.new(-5264.50244, 40.1666908, -4343.44482)
					TelePBoss(CFrameQ)
					SelectMonster = "Magma Ninja [Lv. 1175]"
				elseif Lv == 1250 or Lv <= 1274 or SelectMonster == "Ship Deckhand [Lv. 1250]" then 
					Ms = "Ship Deckhand [Lv. 1250]"
					NameQuest = "ShipQuest1"
					QuestLv = 1
					NameMon = "Ship Deckhand"
					CFrameQ = CFrame.new(1037.80127, 125.092171, 32911.6016, -0.244533166, -0, -0.969640911, -0, 1.00000012, -0, 0.96964103, 0, -0.244533136)
					CFrameMon = CFrame.new(1157.3252, 145.506523, 32930.1289)
					CFrameMon2 = CFrame.new(1257.60742, 145.92379, 33031.8867)
					CFrameMon3 = CFrame.new(1176.3291, 145.51265, 33119.0977)
					CFrameMon4 = CFrame.new(1247.4281, 145.89933, 33216.4453)
					CFrameMon5 = CFrame.new(719.283325, 145.464821, 33032)
					CFrameMon6 = CFrame.new(580.323303, 145.535988, 32930.1172)
					CFrameMon7 = CFrame.new(580.340881, 145.8246, 33124.2383)
					CFrameMon8 = CFrame.new(1257.60742, 145.92379, 33031.8867)
					if Auto_Farm and (CFrameMon.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 20000 then
						game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(923.21252441406, 126.9760055542, 32852.83203125))
					end
				elseif Lv == 1275 or Lv <= 1299 or SelectMonster == "Ship Engineer [Lv. 1275]" then 
					Ms = "Ship Engineer [Lv. 1275]"
					NameQuest = "ShipQuest1"
					QuestLv = 2
					NameMon = "Ship Engineer"
					CFrameQ = CFrame.new(1037.80127, 125.092171, 32911.6016, -0.244533166, -0, -0.969640911, -0, 1.00000012, -0, 0.96964103, 0, -0.244533136)
					CFrameMon = CFrame.new(1024.89197, 60.7224884, 32739.4121)
					CFrameMon2 = CFrame.new(1088.22607, 60.8481369, 32890.0977)
					CFrameMon3 = CFrame.new(1016.47278, 60.5837517, 33072.4844)
					CFrameMon4 = CFrame.new(834.826904, 60.8366547, 32720.9355)
					CFrameMon5 = CFrame.new(729.271057, 60.228653, 32950.3047)
					CFrameMon6 = CFrame.new(816.991028, 60.5993958, 33110.3555)
					CFrameMon7 = CFrame.new(1024.89197, 60.7224884, 32739.4121)
					CFrameMon8 = CFrame.new(1088.22607, 60.8481369, 32890.0977)
					if Auto_Farm and (CFrameMon.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 20000 then
						game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(923.21252441406, 126.9760055542, 32852.83203125))
					end
					SelectMonster = "Ship Deckhand [Lv. 1250]"
				elseif Lv == 1300 or Lv <= 1324 or SelectMonster == "Ship Steward [Lv. 1300]" then 
					Ms = "Ship Steward [Lv. 1300]"
					NameQuest = "ShipQuest2"
					QuestLv = 1
					NameMon = "Ship Steward"
					CFrameQ = CFrame.new(968.80957, 125.092171, 33244.125, -0.869560242, 1.51905191e-08, -0.493826836, 1.44108379e-08, 1, 5.38534195e-09, 0.493826836, -2.43357912e-09, -0.869560242)
					CFrameMon = CFrame.new(986.858826, 150.990578, 33366.9492)
					CFrameMon2 = CFrame.new(1032.4696, 150.000481, 33512.3984)
					CFrameMon3 = CFrame.new(920.477234, 150.321541, 33506.7812)
					CFrameMon4 = CFrame.new(801.389832, 150.996452, 33505.1836)
					CFrameMon5 = CFrame.new(815.020813, 150.999084, 33376.2148)
					CFrameMon6 = CFrame.new(986.858826, 150.990578, 33366.9492)
					CFrameMon7 = CFrame.new(1032.4696, 150.000481, 33512.3984)
					CFrameMon8 = CFrame.new(920.477234, 150.321541, 33506.7812)
					if Auto_Farm and (CFrameMon.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 20000 then
						game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(923.21252441406, 126.9760055542, 32852.83203125))
					end
				elseif Lv == 1325 or Lv <= 1349 or SelectMonster == "Ship Officer [Lv. 1325]" then 
					Ms = "Ship Officer [Lv. 1325]"
					NameQuest = "ShipQuest2"
					QuestLv = 2
					NameMon = "Ship Officer"
					CFrameQ = CFrame.new(968.80957, 125.092171, 33244.125, -0.869560242, 1.51905191e-08, -0.493826836, 1.44108379e-08, 1, 5.38534195e-09, 0.493826836, -2.43357912e-09, -0.869560242)
					CFrameMon = CFrame.new(1162.54968, 200.86264, 33445.6016)
					CFrameMon2 = CFrame.new(1320.52185, 200.869965, 33294.5977)
					CFrameMon3 = CFrame.new(1144.53174, 200.930923, 33112.6094)
					CFrameMon4 = CFrame.new(657.546753, 200.869415, 33460.6367)
					CFrameMon5 = CFrame.new(505.5177, 200.86937, 33263.5586)
					CFrameMon6 = CFrame.new(694.507202, 200.600266, 33112.6406)
					CFrameMon7 = CFrame.new(1162.54968, 200.86264, 33445.6016)
					CFrameMon8 = CFrame.new(1320.52185, 200.869965, 33294.5977)
					if Auto_Farm and (CFrameMon.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 20000 then
						game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(923.21252441406, 126.9760055542, 32852.83203125))
					end
					SelectMonster = "Ship Steward [Lv. 1300]"
				elseif Lv == 1350 or Lv <= 1374 or SelectMonster == "Arctic Warrior [Lv. 1350]" then 
					Ms = "Arctic Warrior [Lv. 1350]"
					NameQuest = "FrostQuest"
					QuestLv = 1
					NameMon = "Arctic Warrior"
					CFrameQ = CFrame.new(5667.6582, 26.7997818, -6486.08984, -0.933587909, 0, -0.358349502, 0, 1, 0, 0.358349502, 0, -0.933587909)
					CFrameMon = CFrame.new(5878.23486, 81.3886948, -6136.35596, -0.451037169, 2.3908234e-07, 0.892505825, -1.08168464e-07, 1, -3.22542007e-07, -0.892505825, -2.4201924e-07, -0.451037169)
					if Auto_Farm and (CFrameMon.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 20000 then
						game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(-6508.5581054688, 89.034996032715, -132.83953857422))
					end
				elseif Lv == 1375 or Lv <= 1424 or SelectMonster == "Snow Lurker [Lv. 1375]" then -- Snow Lurker [Lv. 1375]
					Ms = "Snow Lurker [Lv. 1375]"
					NameQuest = "FrostQuest"
					QuestLv = 2
					NameMon = "Snow Lurker"
					CFrameQ = CFrame.new(5667.6582, 26.7997818, -6486.08984, -0.933587909, 0, -0.358349502, 0, 1, 0, 0.358349502, 0, -0.933587909)
					CFrameMon = CFrame.new(5513.36865, 60.546711, -6809.94971, -0.958693981, -1.65617333e-08, 0.284439981, -4.07668654e-09, 1, 4.44854642e-08, -0.284439981, 4.14883701e-08, -0.958693981)
					if Auto_Farm and (CFrameMon.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 20000 then
						game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(-6508.5581054688, 89.034996032715, -132.83953857422))
					end
					SelectMonster = "Arctic Warrior [Lv. 1350]"
				elseif Lv == 1425 or Lv <= 1449 or SelectMonster == "Sea Soldier [Lv. 1425]" then -- Sea Soldier [Lv. 1425]
					Ms = "Sea Soldier [Lv. 1425]"
					NameQuest = "ForgottenQuest"
					QuestLv = 1
					NameMon = "Sea Soldier"
					CFrameQ = CFrame.new(-3054.44458, 235.544281, -10142.8193, 0.990270376, -0, -0.13915664, 0, 1, -0, 0.13915664, 0, 0.990270376)
					CFrameMon = CFrame.new(-3499.34546, 50.1113892, -9712.00488)
					CFrameMon2 = CFrame.new(-3292.8894, 50.41152239, -9640.78223)
					CFrameMon3 = CFrame.new(-3240.32959, 50.8411598, -9813.96582)
					CFrameMon4 = CFrame.new(-3457.94263, 50.0302029, -9933.0752)
					CFrameMon5 = CFrame.new(-2838.66821, 50.2311764, -9813.09473)
					CFrameMon6 = CFrame.new(-2550.9231, 50.8412743, -9839.99707)
					CFrameMon7 = CFrame.new(-2550.9231, 50.8412743, -9839.99707)
					CFrameMon8 = CFrame.new(-2550.9231, 50.8412743, -9839.99707)
					TelePBoss(CFrameQ)
				elseif Lv >= 1450 or SelectMonster == "Water Fighter [Lv. 1450]" then -- Water Fighter [Lv. 1450]
					Ms = "Water Fighter [Lv. 1450]"
					NameQuest = "ForgottenQuest"
					QuestLv = 2
					NameMon = "Water Fighter"
					CFrameQ = CFrame.new(-3054.5827636719, 236.87213134766, -10147.790039063)
					CFrameMon = CFrame.new(-3316.75146, 260.719513, -10323.1689)
					CFrameMon2 = CFrame.new(-3511.88721, 260.592819, -10347.0479)
					CFrameMon3 = CFrame.new(-3655.82471, 260.921265, -10589.9717)
					CFrameMon4 = CFrame.new(-3396.36108, 260.280075, -10745.1064)
					CFrameMon5 = CFrame.new(-3396.36108, 260.280075, -10745.1064)
					CFrameMon6 = CFrame.new(-3267.715576171875, 299.0077209472656)
					CFrameMon7 = CFrame.new(-3446.317626953125, 299.18936157226562)
					CFrameMon8 = CFrame.new(-3640.9677734375, 299.18931579589844)
					TelePBoss(CFrameQ)
					SelectMonster = "Sea Soldier [Lv. 1425]"
					if Lv >= 1475 then
						_G.SelectBoss = "Tide Keeper [Lv. 1475] [Boss]"
					end
				end
			end
			if Three_World and not Auto_Raid then
				if Lv >= 1500 and Lv <= 1524 or SelectMonster == "Pirate Millionaire [Lv. 1500]" then -- Pirate Millionaire [Lv. 1500]
					Ms = "Pirate Millionaire [Lv. 1500]"
					NameQuest = "PiratePortQuest"
					QuestLv = 1
					NameMon = "Pirate Millionaire"
					CFrameQ = CFrame.new(-290.074677, 42.9034653, 5581.58984, 0.965929627, -0, -0.258804798, 0, 1, -0, 0.258804798, 0, 0.965929627)
					CFrameMon = CFrame.new(81.164993286133, 43.755737304688, 5724.7021484375)
					TelePBoss(CFrameQ)
				elseif Lv >= 1525 and Lv <= 1574 or SelectMonster == "Pistol Billionaire [Lv. 1525]" then -- Pistol Billionaire [Lv. 1525]
					Ms = "Pistol Billionaire [Lv. 1525]"
					NameQuest = "PiratePortQuest"
					QuestLv = 2
					NameMon = "Pistol Billionaire"
					CFrameQ = CFrame.new(-290.074677, 42.9034653, 5581.58984, 0.965929627, -0, -0.258804798, 0, 1, -0, 0.258804798, 0, 0.965929627)
					CFrameMon = CFrame.new(81.164993286133, 43.755737304688, 5724.7021484375)
					TelePBoss(CFrameQ)
					SelectMonster = "Pirate Millionaire [Lv. 1500]"
				elseif Lv >= 1575 and Lv <= 1599 or SelectMonster == "Dragon Crew Warrior [Lv. 1575]" then -- Dragon Crew Warrior [Lv. 1575]
					Ms = "Dragon Crew Warrior [Lv. 1575]"
					NameQuest = "AmazonQuest"
					QuestLv = 1
					NameMon = "Dragon Crew Warrior"
					CFrameQ = CFrame.new(5832.83594, 51.6806107, -1101.51563, 0.898790359, -0, -0.438378751, 0, 1, -0, 0.438378751, 0, 0.898790359)
					CFrameMon = CFrame.new(6241.9951171875, 51.522083282471, -1243.9771728516)
					TelePBoss(CFrameQ)
				elseif Lv >= 1600 and Lv <= 1624 or SelectMonster == "Dragon Crew Archer [Lv. 1600]" then -- Dragon Crew Archer [Lv. 1600]
					Ms = "Dragon Crew Archer [Lv. 1600]"
					NameQuest = "AmazonQuest"
					QuestLv = 2
					NameMon = "Dragon Crew Archer"
					CFrameQ = CFrame.new(5832.83594, 51.6806107, -1101.51563, 0.898790359, -0, -0.438378751, 0, 1, -0, 0.438378751, 0, 0.898790359)
					CFrameMon = CFrame.new(6488.9155273438, 383.38375854492, -110.66246032715)
					TelePBoss(CFrameQ)
					SelectMonster = "Dragon Crew Warrior [Lv. 1575]"
				elseif Lv >= 1625 and Lv <= 1649 or SelectMonster == "Female Islander [Lv. 1625]" then -- Female Islander [Lv. 1625]
					Ms = "Female Islander [Lv. 1625]"
					NameQuest = "AmazonQuest2"
					QuestLv = 1
					NameMon = "Female Islander"
					CFrameQ = CFrame.new(5448.86133, 601.516174, 751.130676, 0, 0, 1, 0, 1, -0, -1, 0, 0)
					CFrameMon = CFrame.new(4770.4990234375, 758.95520019531, 1069.8680419922)
					TelePBoss(CFrameQ)
				elseif Lv >= 1650 and Lv <= 1699 or SelectMonster == "Giant Islander [Lv. 1650]" then -- Giant Islander [Lv. 1650]
					Ms = "Giant Islander [Lv. 1650]"
					NameQuest = "AmazonQuest2"
					QuestLv = 2
					NameMon = "Giant Islander"
					CFrameQ = CFrame.new(5448.86133, 601.516174, 751.130676, 0, 0, 1, 0, 1, -0, -1, 0, 0)
					CFrameMon = CFrame.new(4530.3540039063, 656.75695800781, -131.60952758789)
					TelePBoss(CFrameQ)
					SelectMonster = "Female Islander [Lv. 1625]"
				elseif Lv >= 1700 and Lv <= 1724 or SelectMonster == "Marine Commodore [Lv. 1700]" then -- Marine Commodore [Lv. 1700]
					Ms = "Marine Commodore [Lv. 1700]"
					NameQuest = "MarineTreeIsland"
					QuestLv = 1
					NameMon = "Marine Commodore"
					CFrameQ = CFrame.new(2180.54126, 27.8156815, -6741.5498, -0.965929747, 0, 0.258804798, 0, 1, 0, -0.258804798, 0, -0.965929747)
					CFrameMon = CFrame.new(2490.0844726563, 190.4232635498, -7160.0502929688)
					TelePBoss(CFrameQ)
				elseif Lv >= 1725 and Lv <= 1774 or SelectMonster == "Marine Rear Admiral [Lv. 1725]" then -- Marine Rear Admiral [Lv. 1725]
					Ms = "Marine Rear Admiral [Lv. 1725]"
					NameQuest = "MarineTreeIsland"
					QuestLv = 2
					NameMon = "Marine Rear Admiral"
					CFrameQ = CFrame.new(2180.54126, 27.8156815, -6741.5498, -0.965929747, 0, 0.258804798, 0, 1, 0, -0.258804798, 0, -0.965929747)
					CFrameMon = CFrame.new(3951.3903808594, 229.11549377441, -6912.81640625)
					TelePBoss(CFrameQ)
					SelectMonster = "Marine Commodore [Lv. 1700]"
				elseif Lv >= 1775 and Lv <= 1799 or SelectMonster == "Fishman Raider [Lv. 1775]" then -- Fishman Raider [Lv. 1775]
					Ms = "Fishman Raider [Lv. 1775]"
					NameQuest = "DeepForestIsland3"
					QuestLv = 1
					NameMon = "Fishman Raider"
					CFrameQ = CFrame.new(-10581.6563, 330.872955, -8761.18652, -0.882952213, 0, 0.469463557, 0, 1, 0, -0.469463557, 0, -0.882952213)
					CFrameMon = CFrame.new(-10322.400390625, 390.94473266602, -8580.0908203125)
					TelePBoss(CFrameQ)
				elseif Lv >= 1800 and Lv <= 1824 or SelectMonster == "Fishman Captain [Lv. 1800]" then -- Fishman Captain [Lv. 1800]
					Ms = "Fishman Captain [Lv. 1800]"
					NameQuest = "DeepForestIsland3"
					QuestLv = 2
					NameMon = "Fishman Captain"
					CFrameQ = CFrame.new(-10581.6563, 330.872955, -8761.18652, -0.882952213, 0, 0.469463557, 0, 1, 0, -0.469463557, 0, -0.882952213)
					CFrameMon = CFrame.new(-11194.541992188, 442.02795410156, -8608.806640625)
					TelePBoss(CFrameQ)
					SelectMonster = "Fishman Raider [Lv. 1775]"
				elseif Lv >= 1825 and Lv <= 1849 or SelectMonster == "Forest Pirate [Lv. 1825]" then -- Forest Pirate [Lv. 1825]
					Ms = "Forest Pirate [Lv. 1825]"
					NameQuest = "DeepForestIsland"
					QuestLv = 1
					NameMon = "Forest Pirate"
					CFrameQ = CFrame.new(-13234.04, 331.488495, -7625.40137, 0.707134247, -0, -0.707079291, 0, 1, -0, 0.707079291, 0, 0.707134247)
					CFrameMon = CFrame.new(-13225.809570313, 428.19387817383, -7753.1245117188)
					if Auto_Farm and (CFrameMon.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 3000 then
						_G.Stop_Tween = true
						TP(CFrameQ)
						wait(.5)
						game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(-12476.080078125, 374.9144592285156, -7566.93701171875))
						wait(.5)
						_G.Stop_Tween = nil
					end
					TelePBoss(CFrameQ)
				elseif Lv >= 1850 and Lv <= 1899 or SelectMonster == "Mythological Pirate [Lv. 1850]" then -- Mythological Pirate [Lv. 1850]
					Ms = "Mythological Pirate [Lv. 1850]"
					NameQuest = "DeepForestIsland"
					QuestLv = 2
					NameMon = "Mythological Pirate"
					CFrameQ = CFrame.new(-13234.04, 331.488495, -7625.40137, 0.707134247, -0, -0.707079291, 0, 1, -0, 0.707079291, 0, 0.707134247)
					CFrameMon = CFrame.new(-13869.172851563, 564.95251464844, -7084.4135742188)
					TelePBoss(CFrameQ)
					if Auto_Farm and (CFrameMon.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 3000 then
						_G.Stop_Tween = true
						TP(CFrameQ)
						wait(.5)
						game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(-12476.080078125, 374.9144592285156, -7566.93701171875))
						wait(.5)
						_G.Stop_Tween = nil
					end
					SelectMonster = "Forest Pirate [Lv. 1825]"
				elseif Lv >= 1900 and Lv <= 1924 or SelectMonster == "Jungle Pirate [Lv. 1900]" then -- Jungle Pirate [Lv. 1900]
					Ms = "Jungle Pirate [Lv. 1900]"
					NameQuest = "DeepForestIsland2"
					QuestLv = 1
					NameMon = "Jungle Pirate"
					CFrameQ = CFrame.new(-12680.3818, 389.971039, -9902.01953, -0.0871315002, 0, 0.996196866, 0, 1, 0, -0.996196866, 0, -0.0871315002)
					CFrameMon = CFrame.new(-11982.221679688, 376.32522583008, -10451.415039063)
					TelePBoss(CFrameQ)
					if Auto_Farm and (CFrameMon.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 3000 then
						_G.Stop_Tween = true
						TP(CFrameQ)
						wait(.5)
						game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(-11993.580078125, 331.8077087402344, -8844.1826171875))
						wait(.5)
						_G.Stop_Tween = nil
					end
				elseif Lv >= 1925 and Lv <= 1974 or SelectMonster == "Musketeer Pirate [Lv. 1925]" then -- Musketeer Pirate [Lv. 1925]
					Ms = "Musketeer Pirate [Lv. 1925]"
					NameQuest = "DeepForestIsland2"
					QuestLv = 2
					NameMon = "Musketeer Pirate"
					CFrameQ = CFrame.new(-12680.3818, 389.971039, -9902.01953, -0.0871315002, 0, 0.996196866, 0, 1, 0, -0.996196866, 0, -0.0871315002)
					CFrameMon = CFrame.new(-13282.3046875, 496.23684692383, -9565.150390625)
					TelePBoss(CFrameQ)
					if Auto_Farm and (CFrameMon.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 3000 then
						_G.Stop_Tween = true
						TP(CFrameQ)
						wait(.5)
						game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(-11993.580078125, 331.8077087402344, -8844.1826171875))
						wait(.5)
						_G.Stop_Tween = nil
					end
					SelectMonster = "Jungle Pirate [Lv. 1900]"
				elseif Lv >= 1975 and Lv <= 1999 or SelectMonster == "Reborn Skeleton [Lv. 1975]" then
					Ms = "Reborn Skeleton [Lv. 1975]"
					NameQuest = "HauntedQuest1"
					QuestLv = 1
					NameMon = "Reborn Skeleton"
					CFrameQ = CFrame.new(-9480.8271484375, 142.13066101074, 5566.0712890625)
					CFrameMon = CFrame.new(-8817.880859375, 191.16761779785, 6298.6557617188)
					TelePBoss(CFrameQ)
				elseif Lv >= 2000 and Lv <= 2024 or SelectMonster == "Living Zombie [Lv. 2000]" then
					Ms = "Living Zombie [Lv. 2000]"
					NameQuest = "HauntedQuest1"
					QuestLv = 2
					NameMon = "Living Zombie"
					CFrameQ = CFrame.new(-9480.8271484375, 142.13066101074, 5566.0712890625)
					CFrameMon = CFrame.new(-10125.234375, 183.94705200195, 6242.013671875)
					TelePBoss(CFrameQ)
					SelectMonster = "Reborn Skeleton [Lv. 1975]"
				elseif Lv >= 2025 and Lv <= 2049  or  SelectMonster == "Demonic Soul [Lv. 2025]" then
					Ms = "Demonic Soul [Lv. 2025]"
					NameQuest = "HauntedQuest2"
					QuestLv = 1
					NameMon = "Demonic"
					CFrameQ = CFrame.new(-9516.9931640625, 178.00651550293, 6078.4653320313)
					CFrameMon = CFrame.new(-9712.03125, 204.69589233398, 6193.322265625)
					TelePBoss(CFrameQ)
					SelectMonster = "Living Zombie [Lv. 2000]"
				elseif Lv >= 2050 and Lv <= 2074 or SelectMonster == "Posessed Mummy [Lv. 2050]" then
					Ms = "Posessed Mummy [Lv. 2050]"
					NameQuest = "HauntedQuest2"
					QuestLv = 2
					NameMon = "Posessed Mummy"
					CFrameQ = CFrame.new(-9516.9931640625, 178.00651550293, 6078.4653320313)
					CFrameMon = CFrame.new(-9545.7763671875, 69.619895935059, 6339.5615234375)    
					TelePBoss(CFrameQ)
					SelectMonster = "Demonic Soul [Lv. 2025]"
				elseif Lv >= 2075 and Lv <= 2099 or SelectMonster == "Peanut Scout [Lv. 2075]" then
					Ms = "Peanut Scout [Lv. 2075]"
					NameQuest = "NutsIslandQuest"
					QuestLv = 1
					NameMon = "Peanut Scout"
					CFrameQ = CFrame.new(-2104.17163, 38.1299706, -10194.418, 0.758814394, -1.38604395e-09, 0.651306927, 2.85280208e-08, 1, -3.1108879e-08, -0.651306927, 4.21863646e-08, 0.758814394)
					CFrameMon = CFrame.new(-2098.07544, 192.611862, -10248.8867, 0.983392298, -9.57031787e-08, 0.181492642, 8.7276355e-08, 1, 5.44169616e-08, -0.181492642, -3.76732068e-08, 0.983392298)
					TelePBoss(CFrameQ)
				elseif Lv >= 2100 and Lv <= 2124 or SelectMonster == "Peanut President [Lv. 2100]" then
					Ms = "Peanut President [Lv. 2100]"
					NameQuest = "NutsIslandQuest"
					QuestLv = 2
					NameMon = "Peanut President"
					CFrameQ = CFrame.new(-2104.17163, 38.1299706, -10194.418, 0.758814394, -1.38604395e-09, 0.651306927, 2.85280208e-08, 1, -3.1108879e-08, -0.651306927, 4.21863646e-08, 0.758814394)
					CFrameMon = CFrame.new(-1876.95959, 192.610947, -10542.2939, 0.0553516336, -2.83836812e-08, 0.998466909, -6.89634405e-10, 1, 2.84654931e-08, -0.998466909, -2.26418861e-09, 0.0553516336)
					SelectMonster = "Peanut Scout [Lv. 2075]"
					TelePBoss(CFrameQ)
				elseif Lv >= 2125 and Lv <= 2149 or SelectMonster == "Ice Cream Chef [Lv. 2125]" then
					Ms = "Ice Cream Chef [Lv. 2125]"
					NameQuest = "IceCreamIslandQuest"
					QuestLv = 1
					NameMon = "Ice Cream Chef"
					CFrameQ = CFrame.new(-820.404358, 65.8453293, -10965.5654, 0.822534859, 5.24448502e-08, -0.568714678, -2.08336317e-08, 1, 6.20846663e-08, 0.568714678, -3.92184099e-08, 0.822534859)
					CFrameMon = CFrame.new(-821.614075, 208.39537, -10990.7617, -0.870096624, 3.18909272e-08, 0.492881238, -1.8357893e-08, 1, -9.71107568e-08, -0.492881238, -9.35439957e-08, -0.870096624)
					TelePBoss(CFrameQ)
				elseif Lv >= 2150 and Lv <= 2199 or SelectMonster == "Ice Cream Commander [Lv. 2150]" then 
					Ms = "Ice Cream Commander [Lv. 2150]"
					NameQuest = "IceCreamIslandQuest"
					QuestLv = 2
					NameMon = "Ice Cream Commander"
					CFrameQ = CFrame.new(-819.376526, 67.4634171, -10967.2832)
					CFrameMon = CFrame.new(-610.11669921875, 208.26904296875, -11253.686523438)
					TelePBoss(CFrameQ)
					SelectMonster = "Ice Cream Chef [Lv. 2125]"
				elseif Lv >= 2200 and Lv <= 2224 or SelectMonster == "Cookie Crafter [Lv. 2200]" then 
					Ms = "Cookie Crafter [Lv. 2200]"
					NameQuest = "CakeQuest1"
					QuestLv = 1
					NameMon = "Cookie Crafter"
					CFrameQ = CFrame.new(-2020.6068115234375, 37.82400894165039, -12027.80859375)
					CFrameMon = CFrame.new(-2286.684326171875, 146.5656280517578, -12226.8818359375)
					TelePBoss(CFrameQ)
				elseif Lv >= 2225 and Lv <= 2249 or SelectMonster == "Cake Guard [Lv. 2225]" then 
					Ms = "Cake Guard [Lv. 2225]"
					NameQuest = "CakeQuest1"
					QuestLv = 2
					NameMon = "Cake Guard"
					CFrameQ = CFrame.new(-2020.6068115234375, 37.82400894165039, -12027.80859375)
					CFrameMon = CFrame.new(-1817.9747314453125, 209.5632781982422, -12288.9228515625)
					SelectMonster = "Cookie Crafter [Lv. 2200]"
					TelePBoss(CFrameQ)
				elseif Lv >= 2250 and Lv <= 2299 or SelectMonster == "Baking Staff [Lv. 2250]" then 
					Ms = "Baking Staff [Lv. 2250]"
					NameQuest = "CakeQuest2"
					QuestLv = 1
					NameMon = "Baking Staff"
					CFrameQ = CFrame.new(-1928.31763, 37.7296638, -12840.626)
					CFrameMon = CFrame.new(-1818.347900390625, 93.41275787353516, -12887.66015625)
					TelePBoss(CFrameQ)
				elseif Lv >= 2300 and Lv <= 2324 or SelectMonster == "Cocoa Warrior [Lv. 2300]" then
					Ms = "Cocoa Warrior [Lv. 2300]"
					NameQuest = "ChocQuest1"
					QuestLv = 1
					NameMon = "Cocoa Warrior"
					CFrameMon = CFrame.new(53.17967224121094, 43.44169998168945, -12286.28515625)
					CFrameQ = CFrame.new(231.68377685546875, 25.077497482299805, -12196.4892578125)
					TelePBoss(CFrameQ)
				elseif Lv >= 2325 and Lv <= 2349 or SelectMonster == "Chocolate Bar Battler [Lv. 2325]" then
					Ms = "Chocolate Bar Battler [Lv. 2325]"
					NameQuest = "ChocQuest1"
					QuestLv = 2
					NameMon = "Chocolate Bar Battler"
					CFrameMon = CFrame.new(616.9508666992188, 82.83536529541016, -12574.2841796875)
					CFrameQ = CFrame.new(231.68377685546875, 25.077497482299805, -12196.4892578125)
					SelectMonster = "Cocoa Warrior [Lv. 2300]"
					TelePBoss(CFrameQ)
				elseif Lv >= 2350 and Lv <= 2374 or SelectMonster == "Sweet Thief [Lv. 2350]" then
					Ms = "Sweet Thief [Lv. 2350]"
					NameQuest = "ChocQuest2"
					QuestLv = 1
					NameMon = "Sweet Thief"
					CFrameMon = CFrame.new(12.077109336853027, 88.81404113769531, -12822.841796875)
					CFrameQ = CFrame.new(148.7130584716797, 25.137081146240234, -12774.9052734375)
					SelectMonster = "Chocolate Bar Battler [Lv. 2325]"
					TelePBoss(CFrameQ)
				elseif Lv >= 2375 and Lv <= 2399 or SelectMonster == "Candy Rebel [Lv. 2375]" then
					Ms = "Candy Rebel [Lv. 2375]"
					NameQuest = "ChocQuest2"
					QuestLv = 2
					NameMon = "Candy Rebel"
					CFrameMon = CFrame.new(12.077109336853027, 88.81404113769531, -12822.841796875)
					CFrameQ = CFrame.new(148.7130584716797, 25.137081146240234, -12774.9052734375)
					SelectMonster = "Sweet Thief [Lv. 2350]"
					TelePBoss(CFrameQ)
				elseif Lv >= 2400 and Lv <= 2424 or SelectMonster == "Candy Pirate [Lv. 2400]" then
					Ms = "Candy Pirate [Lv. 2400]"
					NameQuest = "CandyQuest1"
					QuestLv = 1
					NameMon = "Candy Pirate"
					CFrameMon = CFrame.new(-1225.8407, 40.70440292, -14702.5811)
					CFrameMon2 = CFrame.new(-1299.79883, 40.0102119, -14801.2295)
					CFrameMon3 = CFrame.new(-1411.04895, 40.2383375, -14703.4199)
					CFrameMon4 = CFrame.new(-1370.88086, 40.9806051, -14477.8525)
					CFrameMon5 = CFrame.new(-1291.07166, 40.8216858, -14385.0557)
					CFrameMon6 = CFrame.new(-1436.48059, 40.6319561, -14386.876)
					CFrameMon7 = CFrame.new(-1436.48059, 40.6319561, -14386.876)
					CFrameMon8 = CFrame.new(-1436.48059, 40.6319561, -14386.876)
					CFrameQ = CFrame.new(-1147.0028076171875, 14.450505256652832, -14445.3818359375)
					TelePBoss(CFrameQ)
				elseif Lv >= 2425 or SelectMonster == "Snow Demon [Lv. 2425]" then
					Ms = "Snow Demon [Lv. 2425]"
					NameQuest = "CandyQuest1"
					QuestLv = 2
					NameMon = "Snow Demon"
					CFrameMon = CFrame.new(-849.702454, 40.2957001, -14407.29)
					CFrameMon2 = CFrame.new(-902.147339, 40.2959757, -14309.4268)
					CFrameMon3 = CFrame.new(-800.331482, 40.7142744, -14291.1357)
					CFrameMon4 = CFrame.new(-896.080078, 40.70440292, -14624.3779)
					CFrameMon5 = CFrame.new(-809.856934, 40.6076746, -14687.751)
					CFrameMon6 = CFrame.new(-928.158264, 40.0589685, -14762.2178)
					CFrameMon7 = CFrame.new(-928.158264, 40.0589685, -14762.2178)
					CFrameMon8 = CFrame.new(-928.158264, 40.0589685, -14762.2178)
					CFrameQ = CFrame.new(-1147.0028076171875, 14.450505256652832, -14445.3818359375)
					SelectMonster = "Candy Pirate [Lv. 2400]"
					TelePBoss(CFrameQ)
				end
			end
		end --Fix not Complete

		function TP(P1)
			if not _G.Stop_Tween then
				local Distance = (P1.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude
				if Distance < 50 then
		Speed = 100
	elseif Distance < 250 then
	    Speed = 2400
	elseif Distance < 550 then
	    Speed = 400
	elseif Distance < 700 then
		Speed = 1000
	elseif Distance < 1000 then
	    Speed = 350
	elseif Distance > 3000 then
		Speed = 250
	end				Tween = game:GetService("TweenService"):Create(game.Players.LocalPlayer.Character.HumanoidRootPart,TweenInfo.new(Distance/Speed, Enum.EasingStyle.Linear),{CFrame = P1})
				if _G.Stop_Tween or Auto_Raid then
					Tween:Cancel()
				elseif game.Players.LocalPlayer.Character.Humanoid.Health > 0 then
					Tween:Play()
				end
			end
		end
		
function TP3(P1)
	local Distance = (P1.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude
	if Distance < 350 then
		Speed = 50000
	elseif Distance < 350 then
	    Speed = 400
	elseif Distance < 500 then
	    Speed = 350
	elseif Distance > 1000 then
		Speed = 300
	end
	game:GetService("TweenService"):Create(
		game.Players.LocalPlayer.Character.HumanoidRootPart,
		TweenInfo.new(Distance/Speed, Enum.EasingStyle.Linear),
		{CFrame = P1}
	):Play()
	if _G.Stop_Tween then
		game:GetService("TweenService"):Create(
		game.Players.LocalPlayer.Character.HumanoidRootPart,
		TweenInfo.new(Distance/Speed, Enum.EasingStyle.Linear),
			{CFrame = P1}
		):Cancel()
	end
end

function TP2(P1)
	local Distance = (P1.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude
	if Distance < 350 then
	    Speed = 700
	elseif Distance < 550 then
	    Speed = 350
	elseif Distance < 700 then
		Speed = 350
	elseif Distance < 1000 then
	    Speed = 350
	elseif Distance > 1000 then
		Speed = 350
	end
	game:GetService("TweenService"):Create(
		game.Players.LocalPlayer.Character.HumanoidRootPart,
		TweenInfo.new(Distance/Speed, Enum.EasingStyle.Linear),
		{CFrame = P1}
	):Play()
	if _G.Stop_Tween then
		game:GetService("TweenService"):Create(
		game.Players.LocalPlayer.Character.HumanoidRootPart,
		TweenInfo.new(Distance/Speed, Enum.EasingStyle.Linear),
			{CFrame = P1}
		):Cancel()
	end
	_G.Clip = true
	wait(Distance/Speed)
	_G.Clip = false
end

spawn(function()
   while wait() do
    if Methodnow == 1 then
        Methodnow = 2
        Method = CFrameMon
        wait(.5)
        Method = CFrameMon2
        wait(.5)
        Method = CFrameMon3
        wait(.5)
        Method = CFrameMon4
        wait(.5)
        Method = CFrameMon5
        wait(1)
        Method = CFrameMon6
        wait(.5)
        Method = CFrameMon7
        wait(.5)
        Method = CFrameMon8
    else
        Methodnow = 1
        Method = CFrameMon
        wait(.5)
        Method = CFrameMon2
        wait(.5)
        Method = CFrameMon3
        wait(.5)
        Method = CFrameMon4
        wait(.5)
        Method = CFrameMon5
        wait(1)
        Method = CFrameMon6
        wait(.5)
        Method = CFrameMon7
        wait(.5)
        Method = CFrameMon8
       end
   end
end)

spawn(function()
   while wait() do
    if Cnow == 1 then
        Cnow = 2
        Cethod = CFrame.new(-45,0,0)
        wait()
        Cethod = CFrame.new(0,0,-45)
        wait()
        Cethod = CFrame.new(45,0,0)
        wait()
        Cethod = CFrame.new(0,0,45)
        wait()
        Cethod = CFrame.new(0,45,0)
    else
        Cnow = 1
        Cethod = CFrame.new(-45,0,0)
        wait()
        Cethod = CFrame.new(0,0,-45)
        wait()
        Cethod = CFrame.new(45,0,0)
        wait()
        Cethod = CFrame.new(0,0,45)
        wait()
        Cethod = CFrame.new(0,45,0)
       end
   end
end)

function EquipWeapon(ToolSe)
	if game.Players.LocalPlayer.Backpack:FindFirstChild(ToolSe) then
		local tool = game.Players.LocalPlayer.Backpack:FindFirstChild(ToolSe)
		wait(.4)
		game.Players.LocalPlayer.Character.Humanoid:EquipTool(tool)
	end
end

spawn(function()
    while wait(.1) do
        pcall(function()
            if _G.Clip or Auto_Farm_Bounty or Auto_Twin_Hooks or Auto_Canvander or Auto_Buddy_Sword or Auto_Hallow_Scryte or Auto_Spikey_Trident or Auto_Dark_Dagger or Auto_Serpent_Bow or Auto_Acidum_Rifle or Auto_Swan_Glass or Auto_Pale_Scarf or Auto_Valkyrie_Helmet or Saber_Farm or Pole_Farm or Rengoku_A or Auto_Dragon_Trident or Triple_A or Auto_Yama or Auto_Tushita or Auto_Dark_Coat or _G.Setting_table.Human_Evo or _G.Setting_table.Mink_Evo or _G.Setting_table.Death_Step or _G.Setting_table.Sharkman_Karate or _G.Setting_table.Electric_Claw or _G.Setting_table.Dragon_Talon or _G.Setting_table.Superhuman or Auto_Three_World or Bartlio_Farm or Auto_New_A or Auto_Elite_Hunter or Auto_Phoenix_Awaken or Auto_Raid or _G.Setting_table.Farm_Ken_Hop or _G.Setting_table.Auto_Farm_Boss_Hop or _G.Setting_table.Auto_Farm_Boss_All_Hop or Open_Color_Haki or Auto_Holy_Torch or Grab_Chest or Auto_Farm_Monster or Farm_Ken or Auto_Farm_Bone or Farm_Ken_V2 or Auto_Farm_Melee or Auto_Farm_Sword or Auto_Farm or Auto_Farm_Gun or Auto_Farm_Boss_All or Auto_Farm_Boss or Auto_Farm_Fruit then
				if game.Players.LocalPlayer.Character.Humanoid.Sit == true then
					game.Players.LocalPlayer.Character.Humanoid:ChangeState(15)
					wait(5)
				end
				PIO = false
                if not game.Players.LocalPlayer.Character.HumanoidRootPart:FindFirstChild("BodyVelocity") then 
					local L_1 = Instance.new("BodyVelocity")
                    L_1.Name = "BodyGyrozz"
                    L_1.Parent = game.Players.LocalPlayer.Character.HumanoidRootPart 
                    L_1.MaxForce=Vector3.new(1000000000,1000000000,1000000000)
                    L_1.Velocity=Vector3.new(0,0,0) 
                end
            elseif PIO == false then
				for i,v in pairs(game.Players.LocalPlayer.Character.HumanoidRootPart:GetChildren()) do
					if v.Name == "BodyGyrozz" then
						v:Destroy()
						PIO = true
					end
				end
            end
        end)
    end
end)

local library = loadstring(game:HttpGet("https://raw.githubusercontent.com/garnoog/Guia/main/README.md" , true))()

game.StarterGui:SetCore("SendNotification", {
	Title = "King of god hub", 
	Text = "Gay Kong",
	Duration = 8
})

local win = library:CreateWindow({Name = "Dummy hub [Premium]",Themeable = {info = "Doing by SharkDShop"}})
local General_Tab = win:Tab("General")
local Quest_Tab = win:Tab("Quest")
local PvP_Tab = win:Tab("Combat")
local Raid_Tab = win:Tab("Raid")
local Shop_Tab = win:Tab("Shop")
local Island_Tab = win:Tab("Island")
local Status_Tab = win:Tab("Status")

local yname = game:GetService("Players").LocalPlayer.Name
local IN = General_Tab:CreateSection({Name = "Info"})
IN:AddLabel({
    Name = "Your Name : "..tostring(yname)
})
if Old_World then
    IN:AddLabel({
        Name = "Your World : 1"
    })
elseif New_World then
    IN:AddLabel({
        Name = "Your World : 2"
    })
elseif Three_World then
    IN:AddLabel({
        Name = "Your World : 3"
    })
end

local St = General_Tab:CreateSection({
    Name = "Setting",
    Side = "Right"
})
St:AddLabel("Setting Server")
function FPSBooster()
    local decalsyeeted = true
    local g = game
    local w = g.Workspace
    local l = g.Lighting
    local t = w.Terrain
    sethiddenproperty(l,"Technology",2)
    sethiddenproperty(t,"Decoration",false)
    t.WaterWaveSize = 0
    t.WaterWaveSpeed = 0
    t.WaterReflectance = 0
    t.WaterTransparency = 0
    l.GlobalShadows = false
    l.FogEnd = 9e9
    l.Brightness = 0
    settings().Rendering.QualityLevel = "Level01"
    for i, v in pairs(g:GetDescendants()) do
        if v:IsA("Part") or v:IsA("Union") or v:IsA("CornerWedgePart") or v:IsA("TrussPart") then
            v.Material = "Plastic"
            v.Reflectance = 0
        elseif v:IsA("Decal") or v:IsA("Texture") and decalsyeeted then
            v.Transparency = 1
        elseif v:IsA("ParticleEmitter") or v:IsA("Trail") then
            v.Lifetime = NumberRange.new(0)
        elseif v:IsA("Explosion") then
            v.BlastPressure = 1
            v.BlastRadius = 1
        elseif v:IsA("Fire") or v:IsA("SpotLight") or v:IsA("Smoke") or v:IsA("Sparkles") then
            v.Enabled = false
        elseif v:IsA("MeshPart") then
            v.Material = "Plastic"
            v.Reflectance = 0
            v.TextureID = 10385902758728957
        end
    end
    for i, e in pairs(l:GetChildren()) do
        if e:IsA("BlurEffect") or e:IsA("SunRaysEffect") or e:IsA("ColorCorrectionEffect") or e:IsA("BloomEffect") or e:IsA("DepthOfFieldEffect") then
            e.Enabled = false
        end
    end
end
St:AddToggle({
    Name = "White Screen",
    _G.Setting_table.White_Screen,
    Callback = function(vu)
	_G.Setting_table.White_Screen = vu
    if _G.Setting_table.White_Screen then
        game:GetService("RunService"):Set3dRenderingEnabled(false)
    else
        game:GetService("RunService"):Set3dRenderingEnabled(true)
    end
end})
St:AddButton({
    Name = "FPS Booster",
    Callback = function()
	FPSBooster()
end})
St:AddButton({
    Name = "Redeem All Code",
    Callback = function()
	function UseCode(Text)
        game:GetService("ReplicatedStorage").Remotes.Redeem:InvokeServer(Text)
    end
    UseCode("NOOB_REFUND")
    UseCode("SUB2GAMERROBOT_RESET1")
    UseCode("kittgaming")
    UseCode("Sub2Fer999")
    UseCode("Enyu_is_Pro")
    UseCode("Magicbus")
    UseCode("JCWK")
    UseCode("Starcodeheo")
    UseCode("Bluxxy")
    UseCode("fudd10_v2")
    UseCode("FUDD10")
    UseCode("BIGNEWS")
    UseCode("THEGREATACE")
    UseCode("SUB2GAMERROBOT_EXP1")
    UseCode("Sub2OfficialNoobie")
    UseCode("StrawHatMaine")
    UseCode("SUB2NOOBMASTER123")
    UseCode("Sub2Daigrock")
    UseCode("Sub2UncleKizaru")
    UseCode("Axiore")
    UseCode("TantaiGaming")
end})
St:AddToggle({
    Name = "Auto Rejoin On Kick",
    _G.Setting_table.Rejoin,
    Value = true,
    Callback = function(vu)
	_G.Rejoin = vu
	_G.Setting_table.Rejoin = vu
	Update_Setting(getgenv()['MyName'])
end})
St:AddToggle({
    Name = "Anti AFK",
    _G.Setting_table.Anti_AFK,
    Value = true,
    Callback = function(vu)
	_G.Setting_table.Anti_AFK = vu
	Update_Setting(getgenv()['MyName'])
end})

spawn(function()
	while wait(2) do
		pcall(function()
			if _G.Setting_table.Auto_Ken then
				game:GetService("ReplicatedStorage").Remotes.CommE:FireServer("Ken",true)
				wait(7)
			end
		end)
	end
end)
St:AddToggle({
    Name = "No Clip",
    _G.Setting_table.NoClip,
    Value = true,
    Callback = function(vu)
	_G.Setting_table.NoClip = vu
	Update_Setting(getgenv()['MyName'])
end})
spawn(function()
    while game:GetService("RunService").Stepped:wait() do
		pcall(function()
        	if _G.Setting_table.NoClip then
				local character = game.Players.LocalPlayer.Character
				for _, v in pairs(character:GetChildren()) do
					if v:IsA("BasePart") then
						v.CanCollide = false
					end
				end
			end
        end)
    end
end)
St:AddToggle({
    Name = "Show Damage",
    _G.Setting_table.Show_Damage,
    Callback = function(vu)
	game:GetService("ReplicatedStorage").Assets.GUI.DamageCounter.Enabled = vu
	_G.Setting_table.Show_Damage = vu
	Update_Setting(getgenv()['MyName'])
end})
St:AddButton({
    Name = "Delete Effect Slash Hit",
    Callback = function()
    if game:GetService("ReplicatedStorage").Assets:FindFirstChild('SlashHit') then
        game:GetService("ReplicatedStorage").Assets:FindFirstChild('SlashHit'):Destroy()
	end
end})
if game:GetService("ReplicatedStorage").Assets:FindFirstChild('SlashHit') then
	game:GetService("ReplicatedStorage").Assets:FindFirstChild('SlashHit'):Destroy()
end

St:AddButton({
    Name = "Copy Hwid",
    Callback = function()
	setclipboard((syn and syn.request or request)({Url = 'https://api.luauth.xyz/hwid', Method = syn and "Get" or "GET"}).Body)
end})

--[[St:AddLabel("Save Setting")
St:AddToggle({
    Name = "Save Setting",
    _G.Setting_table.Save_All_Member,
    Value = true,
    Callback = function(vu)
	_G.Setting_table.Save_All_Member = vu
	if vu then
		_G.Dis = nil
	end
	Update_Setting(_G.Check_Save_Setting)
	if _G.Setting_table.Save_All_Member then
		getgenv()['MyName'] = "AllMember"
		Update_Setting(getgenv()['MyName'])
		Check_Setting(getgenv()['MyName'])
		Get_Setting(getgenv()['MyName'])
	end
end})]]--

spawn(function()
    while wait(1) do
		pcall(function()
			if _G.Setting_table.Auto_Buso then
				if not game.Players.LocalPlayer.Character:FindFirstChild("HasBuso") then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Buso")
				else
					wait(3)
				end
			end
		end)
    end
end)

local AutoF = General_Tab:CreateSection({Name = "Auto Farm"})
AutoF:AddToggle({
    Name = "Auto Farm",
    _G.Setting_table.AutoFarm,
    Callback = function(vu)
	Auto_Farm = vu
	_G.Setting_table.AutoFarm = vu
	Update_Setting(getgenv()['MyName'])
end})
	local plr = game.Players.LocalPlayer
	local CbFw = getupvalues(require(plr.PlayerScripts.CombatFramework))
	local CbFw2 = CbFw[2]

    function GetCurrentBlade() 
        local p13 = CbFw2.activeController
        local ret = p13.blades[1]
        if not ret then return end
        while ret.Parent~=game.Players.LocalPlayer.Character do ret=ret.Parent end
        return ret
    end
    
    function AttackNoCD()
        if not Auto_Farm_Bounty and not Auto_Farm_Fruit or Mix_Farm then
            if not Auto_Raid then
                local AC = CbFw2.activeController
                for i = 1, 1 do 
                    local bladehit = require(game.ReplicatedStorage.CombatFramework.RigLib).getBladeHits(
                        plr.Character,
                        {plr.Character.HumanoidRootPart},
                        60
                    )
                    local cac = {}
                    local hash = {}
                    for k, v in pairs(bladehit) do
                        if v.Parent:FindFirstChild("HumanoidRootPart") and not hash[v.Parent] then
                            table.insert(cac, v.Parent.HumanoidRootPart)
                            hash[v.Parent] = true
                        end
                    end
                    bladehit = cac
                    if #bladehit > 0 then
                        local u8 = debug.getupvalue(AC.attack, 5)
                        local u9 = debug.getupvalue(AC.attack, 6)
                        local u7 = debug.getupvalue(AC.attack, 4)
                        local u10 = debug.getupvalue(AC.attack, 7)
                        local u12 = (u8 * 798405 + u7 * 727595) % u9
                        local u13 = u7 * 798405
                        (function()
                            u12 = (u12 * u9 + u13) % 1099511627776
                            u8 = math.floor(u12 / u9)
                            u7 = u12 - u8 * u9
                        end)()
                        u10 = u10 + 1
                        debug.setupvalue(AC.attack, 5, u8)
                        debug.setupvalue(AC.attack, 6, u9)
                        debug.setupvalue(AC.attack, 4, u7)
                        debug.setupvalue(AC.attack, 7, u10)
                        pcall(function()
                            if plr.Character:FindFirstChildOfClass("Tool") and AC.blades and AC.blades[1] then
                                AC.animator.anims.basic[1]:Play(0.01,0.01,0.01)
                                game:GetService("ReplicatedStorage").RigControllerEvent:FireServer("weaponChange",tostring(GetCurrentBlade()))
                                game.ReplicatedStorage.Remotes.Validator:FireServer(math.floor(u12 / 1099511627776 * 16777215), u10)
                                game:GetService("ReplicatedStorage").RigControllerEvent:FireServer("hit", bladehit, i, "")
                            end
                        end)
                    end
                end
            end
        end
        if Auto_Farm_Bounty or Auto_Farm_Fruit and not Mix_Farm then
            local Fast = getupvalues(require(game:GetService("Players").LocalPlayer.PlayerScripts.CombatFramework))
            local Lop = Fast[2]
            Lop.activeController.timeToNextAttack = (-math.huge^math.huge*math.huge)
            Lop.activeController.attacking = false
            Lop.activeController.timeToNextBlock = 0
            Lop.activeController.humanoid.AutoRotate = 80
            Lop.activeController.increment = 3
            Lop.activeController.blocking = false
            Lop.activeController.hitboxMagnitude = 80
        end
    end
spawn(function()
	while wait(.1) do
		pcall(function()
			if Auto_Farm then
				if not Mix_Farm then
					if game.Players.LocalPlayer.PlayerGui.Main.Quest.Visible == false then
						if _G.Farm_Boss then
							_G.SelectBoss = nil
							_G.Farm_Boss = nil
							SelectMonster = nil
							_G.Farm_Mon = nil
						end
						if _G.SelectBoss ~= nil and game.Workspace.Enemies:FindFirstChild(_G.SelectBoss) or _G.SelectBoss ~= nil and game.ReplicatedStorage:FindFirstChild(_G.SelectBoss) then
							CheckQuestBoss()
							repeat wait()
							until (CFrameQBoss.Position-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude < 7000000000000000000000000000
							game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StartQuest", NameQuestBoss, QuestLvBoss)
							game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("SetSpawnPoint")
							_G.Farm_Boss = true
						elseif SelectMonster ~= nil then
							CheckLevel2()
							repeat wait()
							until (CFrameQ.Position-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude < 7000000000000000000000000000
							game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StartQuest", NameQuest, QuestLv)
							game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("SetSpawnPoint")
							SelectMonster = nil
							_G.Farm_Mon = nil
						else
							StatrMagnet = nil
							CheckLevel2()
							repeat wait()
							until (CFrameQ.Position-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude < 7000000000000000000000000000
							game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StartQuest", NameQuest, QuestLv)
							game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("SetSpawnPoint")
						end
					elseif game.Players.LocalPlayer.PlayerGui.Main.Quest.Visible == true then
						if _G.Farm_Boss then
							if game.Workspace.Enemies:FindFirstChild(_G.SelectBoss) then
								for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
									if v.Name == _G.SelectBoss and v.Humanoid.Health > 0 then
										if v.Humanoid:FindFirstChild("Animator") then
											v.Humanoid.Animator:Destroy()
										end
										v.Humanoid:ChangeState(11)
										v.Humanoid.JumpPower = 0
										v.Humanoid.WalkSpeed = 0
										v.HumanoidRootPart.CanCollide = false
										v.HumanoidRootPart.Size = Vector3.new(5,5,5)
										StatrMagnet = nil
										repeat wait(1)
										    wait(_G.Fast_Delay)
											EquipWeapon(_G.Setting_table.Weapon)
									TP3(v.HumanoidRootPart.CFrame * Cethod)
											AttackNoCD()
										until game.Players.LocalPlayer.PlayerGui.Main.Quest.Visible == false or not string.find(game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text, NameBoss) or not v.Parent or v.Humanoid.Health <= 0 or not Auto_Farm or Mix_Farm
										if not string.find(game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text, NameBoss) then
											game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("AbandonQuest")
										end
									end
								end
							else
								TP(CFrameBoss*CFrame.new(0,30,0))
								TelePBoss(CFrameBoss)
							end
						else
							if game.Workspace.Enemies:FindFirstChild(Ms) then
								for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
									if v.Name == Ms and v.Humanoid.Health > 0 then
										_G.PosMon = v.HumanoidRootPart.CFrame
										StatrMagnet = true
										if v.Humanoid:FindFirstChild("Animator") then
											v.Humanoid.Animator:Destroy()
										end
										v.Humanoid:ChangeState(11)
										v.Humanoid.JumpPower = 0
										v.Humanoid.WalkSpeed = 0
										v.HumanoidRootPart.CanCollide = false
										v.HumanoidRootPart.Size = Vector3.new(5,5,5)
										repeat wait(1) 
										    wait(_G.Fast_Delay)
										EquipWeapon(_G.Setting_table.Weapon)
									TP3(v.HumanoidRootPart.CFrame * CFrame.new(0,30,0))
											AttackNoCD()
								      StatrMagnet = false
										until game.Players.LocalPlayer.PlayerGui.Main.Quest.Visible == false or not string.find(game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text, NameMon) or not v.Parent or v.Humanoid.Health <= 0 or not Auto_Farm or Mix_Farm
										if not string.find(game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text, NameMon) then
											game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("AbandonQuest")
										end
										Attack = nil
										repeat game.Workspace.Enemies:FindFirstChild(Ms)
										until 
										function()
										    for i2,v2 in pairs(game.Players.LocalPlayer.Backpack:GetChildren()) do
										        if v2:IsA("Tool") then
										            if tostring(v2.ToolTip) == "Wear" then
										                _G.Setting_table.Weapon = v2.Name
										                end
										                end
										                end
										                end
										                end
										                end
							elseif game.ReplicatedStorage:FindFirstChild(Ms) then
								TP3(game.ReplicatedStorage:FindFirstChild(Ms).HumanoidRootPart.CFrame * CFrame.new(0,30,0))
								else
								    Fast_Delay = 20
								    TP3(Method)
							end
						end
					end
				end
			else
				wait(2)
			end
		end)
	end
end)

spawn(function()
	while task.wait() do
		pcall(function()
			if StatrMagnet then
				if Auto_Farm then
					if game.Players.LocalPlayer.PlayerGui.Main.Quest.Visible == true then
						for i,v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
							if v.Name == Ms and (v.HumanoidRootPart.Position-_G.PosMon.Position).Magnitude <= 350 then
								if v.Humanoid:FindFirstChild("Animator") then
									v.Humanoid.Animator:Destroy()
								end
								v.Humanoid:ChangeState(11)
								v.Humanoid.JumpPower = 0
								v.Humanoid.WalkSpeed = 0
								v.HumanoidRootPart.CanCollide = false
								v.HumanoidRootPart.Size = Vector3.new(5,5,5)
								v.HumanoidRootPart.CFrame = _G.PosMon
								sethiddenproperty(game.Players.LocalPlayer, "SimulationRadius",  math.huge)
								Attack = true
							end
						end
					end
				else
					for i,v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
						if (v.HumanoidRootPart.Position-_G.PosMon.Position).Magnitude <= 350 then
							if v.Humanoid:FindFirstChild("Animator") then
								v.Humanoid.Animator:Destroy()
							end
							v.Humanoid:ChangeState(11)
							v.Humanoid.JumpPower = 0
							v.Humanoid.WalkSpeed = 0
							v.HumanoidRootPart.CanCollide = false
							v.HumanoidRootPart.Size = Vector3.new(5,5,5)
							v.HumanoidRootPart.CFrame = _G.PosMon
							sethiddenproperty(game.Players.LocalPlayer, "MaximumSimulationRadius",  math.huge)
							sethiddenproperty(game.Players.LocalPlayer, "SimulationRadius",  9e20)
						end
					end
				end
			end
		end)
	end
end)

if _G.Setting_table.FastAttack_Mode == nil then
	_G.Setting_table.FastAttack_Mode = "Fast"
end
MIo = {
	"Fast",
	"Smooth",
	"Slow",
	"Super Fast"
}

SW = {
    "Melee",
    "Sword",
    "Gun",
    "Fruit"
}

AutoF:AddToggle({
    Name = "Fast Attack",
    _G.Setting_table.FastAttack,
    Value = true,
    Callback = function(vu)
	_G.Setting_table.FastAttack = vu
	Update_Setting(getgenv()['MyName'])
end})
spawn(function()
	while wait() do
		pcall(function()
			if _G.Setting_table.FastAttack then
				repeat wait(1.8)
				    wait(_G.Fast_Delay)
					AttackNoCD()
				until not _G.Setting_table.FastAttack
			end
		end)
	end
end)

AutoF:AddDropdown({
    Name = "Fast Delay",
    List = MIo,
    Value = "Fast"
    Callback = function(vu)
	_G.Setting_table.FastAttack_Mode = vu
	Update_Setting(getgenv()['MyName'])
	if _G.Setting_table.FastAttack_Mode == "Fast" then
		_G.Fast_Delay = 0.1
	elseif _G.Setting_table.FastAttack_Mode == "Smooth" then
		_G.Fast_Delay = 0.3
	elseif _G.Setting_table.FastAttack_Mode == "Super Fast" then
		_G.Fast_Delay = 0
	elseif _G.Setting_table.FastAttack_Mode == "Slow" then
		_G.Fast_Delay = 0.175
	end
end})

if Old_World then
AutoF:AddToggle({
    Name = "Auto Second World",
    _G.Setting_table.Second_Farm,
    Callback = function(vu)
	Auto_New_A = vu
	_G.Setting_table.Second_Farm = vu
	Update_Setting(getgenv()['MyName'])
end})
spawn(function()
    while wait(.2) do
        if Auto_New_A then
            if Mix_Farm == nil or Auto_New_Farm then
                local Lv = game:GetService("Players").LocalPlayer.Data.Level.Value
                local Beli = game:GetService("Players").LocalPlayer.Data.Beli.Value
                local FG = game:GetService("Players").LocalPlayer.Data.Fragments.Value
                if Lv >= 700 then
                    Mix_Farm = true
                    Auto_New_Farm = true
                    if game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("DressrosaQuestProgress","Detective") == 1 then
                    else
                        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("DressrosaQuestProgress","Detective")
                        wait(2)
                        EquipWeapon("Key")
                    end
                    repeat wait()
                        TP2(CFrame.new(1347.32947, 37.349369, -1325.44922, 0.538348913, 8.57539106e-08, 0.842722058, 8.61935634e-10, 1, -1.0230886e-07, -0.842722058, 5.58042359e-08, 0.538348913))
                    until (Vector3.new(1347.32947, 37.349369, -1325.44922)-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude < 1 or Auto_New_A == false
                    wait(2)
                    for i,v in pairs(game.workspace.Enemies:GetChildren()) do
                        if v.Name == "Ice Admiral [Lv. 700] [Boss]" then
                            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("SetSpawnPoint")
                             
                            repeat wait(1)
                                wait(_G.Fast_Delay)
                                EquipWeapon(_G.Setting_table.Weapon)
                                v.HumanoidRootPart.Size = Vector3.new(50,50,50)
                                TP(v.HumanoidRootPart.CFrame*CFrame.new(0,25,15))
                                AttackNoCD()
                            until v.Humanoid.Health <= 0 or not v.Parent or Auto_New_A == false
                            wait(2)
                            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("TravelDressrosa")
                            wait(25)
                        end
                    end
                end
            end
        end
    end
end)
end
if New_World then
    AutoF:AddToggle({
        Name = "Auto Third World",
        Callback = function(vu)
	Auto_Three_World = vu
end})
spawn(function()
	while wait(.5) do
		pcall(function()
			if Auto_Three_World then
				if game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("TalkTrevor","1") == 0 and game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("TalkTrevor","1") ~= 0 then
					if game:GetService("Workspace").Enemies:FindFirstChild("rip_indra [Lv. 1500] [Boss]") then
						for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
							if v.Name == "rip_indra [Lv. 1500] [Boss]" and v.Humanoid.Health > 0 then
								if v.Humanoid:FindFirstChild("Animator") then
									v.Humanoid.Animator:Destroy()
								end
								repeat wait(.1)
									EquipWeapon(_G.Setting_table.Weapon)
									TP(v.HumanoidRootPart.CFrame*CFrame.new(0,30,0))
									game:GetService'VirtualUser':Button1Down(Vector2.new(1280,600))
								until v.Humanoid.Health <= 0 or not v.Parent or not Auto_Three_World or game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("TalkTrevor","1") == 0
								game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("ZQuestProgress","Zou")
								if not YUHJO then
									Text("ทำเควสโลก 3 เสร็จสิ้น")
									YUHJO = true
								end
							end
						end
					elseif not game:GetService("Workspace").Enemies:FindFirstChild("rip_indra [Lv. 1500] [Boss]") then
						game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("ZQuestProgress","Check")
						game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("ZQuestProgress","Begin")
						repeat wait(1)
						until game:GetService("Workspace").Enemies:FindFirstChild("rip_indra [Lv. 1500] [Boss]") or game.ReplicatedStorage:FindFirstChild("rip_indra [Lv. 1500] [Boss]")
					end
				elseif game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("TalkTrevor","1") == 0 then
					if not IJOIJD then
						Text("คุณทำเควสโลก 3 เสร็จแล้ว")
						IJOIJD = true
					end
				else
					if not JUO then
						Text("คุณยังไม่เปิดประตูโดฟา\nไม่สามารถทำได้!!")
						JUO = true
					end
				end
			else
				wait(2)
			end
		end)
	end
end)
    end

if Three_World then
local CFrameBone = CFrame.new(-9514.9453125, 164.32366943359375, 5786.96044921875)
local Fb = General_Tab:CreateSection("Farm Bone")
Fb:AddToggle({
    Name = "Auto Farm Bone",
    _G.Setting_table.Farm_Bone,
    Callback = function(vu)
	Auto_Farm_Bone = vu
	_G.Setting_table.Farm_Bone = vu
	Update_Setting(getgenv()['MyName'])
end})
spawn(function()
	while wait(.5) do
		pcall(function()
			if Auto_Farm_Bone then
				if not Mix_Farm then
					if game.Workspace.Enemies:FindFirstChild("Reborn Skeleton [Lv. 1975]") then
						game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("SetSpawnPoint")
						for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
							if v.Name == "Reborn Skeleton [Lv. 1975]" and v.Humanoid.Health > 0 then
								if v.Humanoid:FindFirstChild("Animator") then
									v.Humanoid.Animator:Destroy()
								end
								_G.PosMon = v.HumanoidRootPart.CFrame
								StatrMagnet = true
								repeat wait(.3)
								    wait(_G.Fast_Delay)
									EquipWeapon(_G.Setting_table.Weapon)
									TP3(v.HumanoidRootPart.CFrame * Cethod)
									AttackNoCD()
								until v.Humanoid.Health <= 0 or not v.Parent or Mix_Farm or not Auto_Farm_Bone 
								StatrMagnet = false
							end
						end
					elseif game.ReplicatedStorage:FindFirstChild("Reborn Skeleton [Lv. 1975]") then
						TP3(game.ReplicatedStorage:FindFirstChild("Reborn Skeleton [Lv. 1975]").HumanoidRootPart.CFrame*CFrame.new(0,60,0))
					else
						for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
							if not string.find(v.Name,"Boss") and v.Humanoid.Health > 0 and (v.HumanoidRootPart.Position-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 1000 then
								if v.Humanoid:FindFirstChild("Animator") then
									v.Humanoid.Animator:Destroy()
								end
								_G.PosMon = v.HumanoidRootPart.CFrame
								StatrMagnet = true
								repeat wait(_G.Fast_Delay)
									EquipWeapon(_G.Setting_table.Weapon)
									TP3(v.HumanoidRootPart.CFrame * Cethod)
									AttackNoCD()
								until v.Humanoid.Health <= 0 or not v.Parent or Mix_Farm or not Auto_Farm_Bone
								StatrMagnet = false
								else
								    TP2(CFrameBone)
							end
						end
					end
				end
			end
		end)
	end
end)
Fb:AddToggle({
    Name = "Auto Buy Random Surprise",
    _G.Setting_table.Farm_Random_S,
    Callback = function(vu)
	Farm_Random_S = vu
	_G.Setting_table.Farm_Random_S = vu
	Update_Setting(getgenv()['MyName'])
end})
spawn(function()
	while wait(.5) do
		pcall(function()
			if Farm_Random_S then
				game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Bones","Check")
				game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Bones","Buy",1,1)
			end
		end)
	end
end)
Fb:AddButton({
    Name = "Teleport To Haunted Castle",
    Callback = function()
        TP2(CFrameBone)
        end
})
end

local Is = Island_Tab:CreateSection({
    Name = "Server",
    Side = "Right"
})
Is:AddButton({
    Name = "Hop Server",
    Callback = function()
	HopServer()
end})
function HopServer()
    if not _G.TP_Ser then
		_G.TP_Ser = true
		game.StarterGui:SetCore("SendNotification", {
			Title = "Hop Low Server ", 
			Text = "กำลังหาเซิฟ",
			Duration = 25
		})
		local PlaceID = game.PlaceId
		local AllIDs = {}
		local foundAnything = ""
		local actualHour = os.date("!*t").hour
		local Deleted = false
		function TPReturner()
			local Site;
			if foundAnything == "" then
				Site = game.HttpService:JSONDecode(game:HttpGet('https://games.roblox.com/v1/games/' .. PlaceID .. '/servers/Public?sortOrder=Asc&limit=100'))
			else
				Site = game.HttpService:JSONDecode(game:HttpGet('https://games.roblox.com/v1/games/' .. PlaceID .. '/servers/Public?sortOrder=Asc&limit=100&cursor=' .. foundAnything))
			end
			local ID = ""
			if Site.nextPageCursor and Site.nextPageCursor ~= "null" and Site.nextPageCursor ~= nil then
				foundAnything = Site.nextPageCursor
			end
			local num = 0;
			for i,v in pairs(Site.data) do
				local Possible = true
				ID = tostring(v.id)
				game.StarterGui:SetCore("SendNotification", {
					Title = "Hop Low Server ", 
					Text = "Players : " ..tonumber(v.playing),
					Duration = 1.5
				})
				if tonumber(v.maxPlayers) > tonumber(v.playing) then
					for _,Existing in pairs(AllIDs) do
						if num ~= 0 then
							if ID == tostring(Existing) then
								Possible = false
							end
						else
							if tonumber(actualHour) ~= tonumber(Existing) then
								local delFile = pcall(function()
									-- delfile("NotSameServers.json")
									AllIDs = {}
									table.insert(AllIDs, actualHour)
								end)
							end
						end
						num = num + 1
					end
					if Possible == true then
						table.insert(AllIDs, ID)
						wait()
						pcall(function()
							_G.Setting_table.Hop_Server = true 
							Update_Setting(getgenv()['MyName'])
							_G.TP_Ser = true
							-- writefile("NotSameServers.json", game:GetService('HttpService'):JSONEncode(AllIDs))
							wait()
							game:GetService("TeleportService"):TeleportToPlaceInstance(PlaceID, ID, game.Players.LocalPlayer)
						end)
						wait(.1)
					end
				end
			end
		end
		function Bring()
			while wait(.2) do
				pcall(function()
					TPReturner()
					if foundAnything ~= "" then
						TPReturner()
					end
				end)
			end
		end
		Bring()
	end
end
function HopLowServer()
	if not _G.TP_Ser then
		_G.TP_Ser = true
		game.StarterGui:SetCore("SendNotification", {
			Title = "Hop Server S", 
			Text = "กำลังหาเซิฟ",
			Duration = 25
		})
		local PlaceID = game.PlaceId
		local AllIDs = {}
		local foundAnything = ""
		local actualHour = os.date("!*t").hour
		local Deleted = false
		function TPReturner()
			local Site;
			if foundAnything == "" then
				Site = game.HttpService:JSONDecode(game:HttpGet('https://games.roblox.com/v1/games/' .. PlaceID .. '/servers/Public?sortOrder=Asc&limit=100'))
			else
				Site = game.HttpService:JSONDecode(game:HttpGet('https://games.roblox.com/v1/games/' .. PlaceID .. '/servers/Public?sortOrder=Asc&limit=100&cursor=' .. foundAnything))
			end
			local ID = ""
			if Site.nextPageCursor and Site.nextPageCursor ~= "null" and Site.nextPageCursor ~= nil then
				foundAnything = Site.nextPageCursor
			end
			local num = 0;
			for i,v in pairs(Site.data) do
				local Possible = true
				ID = tostring(v.id)
				game.StarterGui:SetCore("SendNotification", {
					Title = "HopServer", 
					Text = "Players : " ..tonumber(v.playing),
					Duration = 1.5
				})
				if tonumber(v.maxPlayers) > tonumber(v.playing) then
					for _,Existing in pairs(AllIDs) do
						if num ~= 0 then
							if ID == tostring(Existing) then
								Possible = false
							end
						else
							if tonumber(actualHour) ~= tonumber(Existing) then
								local delFile = pcall(function()
									-- delfile("NotSameServers.json")
									AllIDs = {}
									table.insert(AllIDs, actualHour)
								end)
							end
						end
						num = num + 1
					end
					if Possible == true then
						table.insert(AllIDs, ID)
						wait()
						pcall(function()
							_G.Setting_table.Hop_Server = true 
							Update_Setting(getgenv()['MyName'])
							_G.TP_Ser = true
							-- writefile("NotSameServers.json", game:GetService('HttpService'):JSONEncode(AllIDs))
							wait()
							game:GetService("TeleportService"):TeleportToPlaceInstance(PlaceID, ID, game.Players.LocalPlayer)
						end)
						wait(.1)
					end
				end
			end
		end
		function Bring()
			while wait(.2) do
				pcall(function()
					TPReturner()
					if foundAnything ~= "" then
						TPReturner()
					end
				end)
			end
		end
		Bring()
	end
end
Is:AddButton({
    Name = "Hop Low Server",
    Callback = function()
	HopLowServer()
end})
Is:AddButton({
    Name = "Re join Server",
    Callback = function()
	game.StarterGui:SetCore("SendNotification", {
        Title = "Re Join Server", 
        Text = "Ready Go!",
        Duration = 10
    })
	_G.TP_Ser = true
	wait(1)
	game:GetService("TeleportService"):Teleport(game.PlaceId)
	wait(50)
end})

function TP_World1()
	_G.TP_Ser = true
	game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("TravelMain")
end
function TP_World2()
	_G.TP_Ser = true
	game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("TravelDressrosa")	
end
function TP_World3()
	_G.TP_Ser = true
	game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("TravelZou")
end

local Iw = Island_Tab:CreateSection({
    Name = "World",
    Side = "Right"
})
Iw:AddButton({
    Name = "Teleport to World 1",
    Callback = function()
	Com()
	TP_World1()
end})
Iw:AddButton({
    Name = "Teleport to World 2", 
    Callback = function()
	Com()
	TP_World2()
end})

Iw:AddButton({"Teleport to World 3", function()
	Com()
	TP_World3()
end})

local m = Island_Tab:CreateSection("Map")
if Old_World then

    m:AddButton({
        Name = "Jones Salad", 
        Callback = function()
        TP2(CFrame.new(1042.1501464844, 16.299360275269, 1444.3442382813))
    end})

    m:AddButton({
        Name = "Marine1", 
        Callback = function()
        TP2(CFrame.new(-2599.6655273438, 6.9146227836609, 2062.2216796875))
    end})

    m:AddButton({
        Name = "Marine2", 
        Callback = function()
        TP2(CFrame.new(-5081.3452148438, 85.221641540527, 4257.3588867188))
    end})

    m:AddButton({
        Name = "Midle Town", 
        Callback = function()
        TP2(CFrame.new(-655.97088623047, 7.878026008606, 1573.7612304688))
    end})

    m:AddButton({
        Name = "Jungle", 
        Callback = function()
        TP2(CFrame.new(-1499.9877929688, 22.877912521362, 353.87060546875))
    end})

    m:AddButton({
        Name = "Pirate Village", 
        Callback = function()
        TP2(CFrame.new(-1163.3889160156, 44.777843475342, 3842.8276367188))
    end})

    m:AddButton({
        Name = "Desert", 
        Callback = function()
        TP2(CFrame.new(954.02056884766, 6.6275520324707, 4262.611328125))
    end})

    m:AddButton({
        Name = "Frozen Village", 
        Callback = function()
        TP2(CFrame.new(1144.5270996094, 7.3292083740234, -1164.7322998047))
    end})

    m:AddButton({
        Name = "Colosseum", 
        Callback = function()
        TP2(CFrame.new(-1667.5869140625, 39.385631561279, -3135.5817871094))
    end})

    m:AddButton({
        Name = "Prison", 
        Callback = function()
        TP2(CFrame.new(4857.6982421875, 5.6780304908752, 732.75750732422))
    end})

    m:AddButton({
        Name = "Mob Leader", 
        Callback = function()
        TP2(CFrame.new(-2841.9604492188, 7.3560485839844, 5318.1040039063))
    end})

    m:AddButton({
        Name = "Magma Village", 
        Callback = function()
        TP2(CFrame.new(-5328.8740234375, 8.6164798736572, 8427.3994140625))
    end})

    m:AddButton({
        Name = "UnderWater Gate", 
        Callback = function()
        TP2(CFrame.new(3893.953125, 5.3989524841309, -1893.4851074219))
    end})

    m:AddButton({
        Name = "UnderWater City", 
        Callback = function()
        TP2(CFrame.new(61191.12109375, 18.497436523438, 1561.8873291016))
    end})

    m:AddButton({
        Name = "Fountain City", 
        Callback = function()
        TP2(CFrame.new(5244.7133789063, 38.526943206787, 4073.4987792969))
    end})

    m:AddButton({
        Name = "Sky1", 
        Callback = function()
        TP2(CFrame.new(-4878.0415039063, 717.71246337891, -2637.7294921875))
    end})

    m:AddButton({
        Name = "Sky2", 
        Callback = function()
        TP2(CFrame.new(-7899.6157226563, 5545.6030273438, -422.21798706055))
    end})

    m:AddButton({
        Name = "Sky3", 
        Callback = function()
        TP2(CFrame.new(-7868.5288085938, 5638.205078125, -1482.5548095703))
    end})

elseif New_World then

    m:AddButton({
        Name = "Dock", 
        Callback = function()
        TP2(CFrame.new(-12.519311904907, 19.302536010742, 2827.853515625))
    end})

    m:AddButton({
        Name = "Mansion", 
        Callback = function()
        TP2(CFrame.new(-390.34829711914, 321.89730834961, 869.00506591797))
    end})

    m:AddButton({
        Name = "Kingdom Of Rose",
        Callback = function()
        TP2(CFrame.new(-388.29895019531, 138.35575866699, 1132.1662597656))
    end})

    m:AddButton({
        Name = "Cafe", 
        Callback = function()
        TP2(CFrame.new(-379.70889282227, 73.0458984375, 304.84692382813))
    end})

    m:AddButton({
        Name = "Sunflower Field", 
        Callback = function()
        TP2(CFrame.new(-1576.7171630859, 198.61849975586, 13.725157737732))
    end})

    m:AddButton({
        Name = "Jeramy Mountain", 
        Callback = function()
        TP2(CFrame.new(1986.3519287109, 448.95678710938, 796.70239257813))
    end})

    m:AddButton({
        Name = "Colossuem", 
        Callback = function()
        TP2(CFrame.new(-1871.8974609375, 45.820514678955, 1359.6843261719))
    end})

    m:AddButton({
        Name = "Factory",
        Callback = function()
        TP2(CFrame.new(349.53750610352, 74.446998596191, -355.62420654297))
    end})

    m:AddButton({
        Name = "The Bridge", 
        Callback = function()
        TP2(CFrame.new(-1860.6354980469, 88.384948730469, -1859.1593017578))
    end})

    m:AddButton({
        Name = "Green Bit",
        Callback = function()
        TP2(CFrame.new(-2202.3706054688, 73.097663879395, -2819.2687988281))
    end})

    m:AddButton({
        Name = "Graveyard",
        Callback = function()
        TP2(CFrame.new(-5617.5927734375, 492.22183227539, -778.3017578125))
    end})

    m:AddButton({
        Name = "Dark Area", 
        Callback = function()
        TP2(CFrame.new(3464.7700195313, 13.375151634216, -3368.90234375))
    end})

    m:AddButton({
        Name = "Snow Mountain",
        Callback = function()
        TP2(CFrame.new(561.23834228516, 401.44781494141, -5297.14453125))
    end})

    m:AddButton({
        Name = "Hot Island", 
        Callback = function()
        TP2(CFrame.new(-5505.9633789063, 15.977565765381, -5366.6123046875))
    end})

    m:AddButton({
        Name = "Cold Island", 
        Callback = function()
        TP2(CFrame.new(-5924.716796875, 15.977565765381, -4996.427734375))
    end})

    m:AddButton({
        Name = "Ice Castle", 
        Callback = function()
        TP2(CFrame.new(6111.7109375, 294.41259765625, -6716.4829101563))
    end})

    m:AddButton({
        Name = "Usopp's Island", 
        Callback = function()
        TP2(CFrame.new(4760.4985351563, 8.3444719314575, 2849.2426757813))
    end})

    m:AddButton({
        Name = "inscription Island", 
        Callback = function()
        TP2(CFrame.new(-5099.01171875, 98.241539001465, 2424.4035644531))
    end})

    m:AddButton({
        Name = "Forgotten Island", 
        Callback = function()
        TP2(CFrame.new(-3051.9514160156, 238.87203979492, -10250.807617188))
    end})

    m:AddButton({
        Name = "Ghost Ship", 
        Callback = function()
        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(923.21252441406, 126.9760055542, 32852.83203125))
    end})

    m:AddButton({
        Name = "Mini Sky",
        Callback = function()
        TP2(CFrame.new(-262.11901855469, 49325.69140625, -35272.49609375))
    end})

elseif Three_World  then
    m:AddButton({
        Name = "Port Town", 
        Callback = function()
        TP2(CFrame.new(-275.21615600586, 43.755737304688, 5451.0659179688))
    end})

    m:AddButton({
        Name = "Hydra Island", 
        Callback = function()
        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(5741.71875, 610.4240112304688, -270.9977722167969))
        TP2(CFrame.new(5541.2685546875, 668.30456542969, 195.48069763184))
    end})
    
    m:AddButton({
        Name = "Gaint Tree", 
        Callback = function()
        TP2(CFrame.new(2276.0859375, 25.87850189209, -6493.03125))
    end})
    
    m:AddButton({
        Name = "Zou Island", 
        Callback = function()
        TP2(CFrame.new(-10034.40234375, 331.78845214844, -8319.6923828125))
    end})
    
    m:AddButton({
        Name = "PineApple Village", 
        Callback = function()
        TP2(CFrame.new(-11172.950195313, 331.8049621582, -10151.033203125))
    end})
    
    m:AddButton({
        Name = "Mansion", 
        Callback = function()
        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(-12463.740234375, 374.9144592285156, -7553.33984375))
        TP2(CFrame.new(-12550.7373046875, 337.16827392578125, -7507.8759765625))
    end})

    m:AddButton({
        Name = "Castle on the Sea", 
        Callback = function()
        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(-5076.65087890625, 314.5155029296875, -3151.17431640625))
        TP2(CFrame.new(-4976.94677734375, 314.5155029296875, -3018.078369140625))
    end})

    m:AddButton({
        Name = "Graveyard Island", 
        Callback = function()
        TP2(CFrame.new(-9515.07324, 142.130615, 5537.58398))
    end})
    m:AddButton({
        Name = "Haunted Castle",
        Callback = function()
        TP2(CFrame.new(-8932.86, 143.258, 6063.31))
    end})
    m:AddButton({
        Name = "Raid Lab", 
        Callback = function()
        TP2(CFrame.new(-5057.146484375, 314.54132080078, -2934.7995605469))
    end})

    m:AddButton({
        Name = "Mini Sky",
        Callback = function()
        TP2(CFrame.new(-263.66668701172, 49325.49609375, -35260))
    end})
    m:AddButton({
        Name = "Ice Cream Island",
        Callback = function()
        TP2(CFrame.new(-691.829, 371.943, -11106.4))
    end})
    m:AddButton({
        Name = "Soa of Cake",
        Callback = function()
        TP2(CFrame.new(-2073.262451171875, 37.16134262084961, -10183.3271484375))
    end})
    m:AddButton({
        Name = "Cake Loaf",
        Callback = function()
        TP2(CFrame.new(-2099.33, 66.9971, -12128.6))
    end})
    m:AddButton({
        Name = "On Tree",
        Callback = function()
        TP2(CFrame.new(2952.8408203125, 2282.0048828125, -7216.93701171875))
        end})
    end

--[[for i2,v2 in pairs(game.Players.LocalPlayer.Backpack:GetChildren()) do
		if v2:IsA("Tool") then
			if tostring(v2.ToolTip) == "Melee" then
		_G.Setting_table.Weapon = v2.Name
			end
			end
		end
		]]--
AutoF:AddToggle({
    Name = "Auto Use Race V4",
    _G.Setting_table.Autorace,
    Callback = function(vu)
    Autorace = vu
	_G.Setting_table.Autorace = vu
	Update_Setting(getgenv()['MyName'])
	while wait() do
	game:service('VirtualInputManager'):SendKeyEvent(true, "Y", false, game)
	wait(.1)
	game:service('VirtualInputManager'):SendKeyEvent(false, "Y", false, game)
	end
end})

local Camera = require(game.ReplicatedStorage.Util.CameraShaker)
Camera:Stop()

Waspon = {}
for i,v in pairs(game.Players.LocalPlayer.Backpack:GetChildren()) do  
    if v:IsA("Tool") then
        table.insert(Waspon ,v.Name)
    end
end
for i,v in pairs(game.Players.LocalPlayer.Character:GetChildren()) do  
    if v:IsA("Tool") then
        table.insert(Waspon ,v.Name)
    end
end
if type(_G.Setting_table.Weapon) == 'string' then
else
	_G.Setting_table.Weapon = ""
end

local WE = General_Tab:CreateSection({
    Name = "Select Weapon",
    Side = "Right"
})
local Select_W = WE:AddDropdown({
    Name = "Select Weapon",
    _G.Setting_table.Weapon,
    List = SW,
    Callback = function(vu)
    _G.Setting_table.Weapon = vu
	Update_Setting(getgenv()['MyName'])
	if _G.Setting_table.Weapon == "Melee" then
		for i2,v2 in pairs(game.Players.LocalPlayer.Backpack:GetChildren()) do
		if v2:IsA("Tool") then
			if tostring(v2.ToolTip) == "Melee" then
		_G.Setting_table.Weapon = v2.Name
			end
			end
		end
	elseif _G.Setting_table.Weapon == "Sword" then
		for i2,v2 in pairs(game.Players.LocalPlayer.Backpack:GetChildren()) do
		if v2:IsA("Tool") then
			if tostring(v2.ToolTip) == "Sword" then
		_G.Setting_table.Weapon = v2.Name
			end
			end
		end
	elseif _G.Setting_table.Weapon == "Gun" then
		for i2,v2 in pairs(game.Players.LocalPlayer.Backpack:GetChildren()) do
		if v2:IsA("Tool") then
			if tostring(v2.ToolTip) == "Gun" then
		_G.Setting_table.Weapon = v2.Name
			end
			end
		end
	elseif _G.Setting_table.Weapon == "Fruit" then
		for i2,v2 in pairs(game.Players.LocalPlayer.Backpack:GetChildren()) do
		if v2:IsA("Tool") then
			if tostring(v2.ToolTip) == "Fruit" then
		_G.Setting_table.Weapon = v2.Name
			end
			end
		end
	end
end})

local mel = Quest_Tab:CreateSection("Melee")
mel:AddToggle({
    Name = "Auto Superhuman",
    _G.Setting_table.Superhuman,
    Callback = function(vu)
	_G.Setting_table.Superhuman = vu
	Update_Setting(getgenv()['MyName'])
end})
mel:AddToggle({
    Name = "Auto Death Step",
    _G.Setting_table.Death_Step,
    Callback = function(vu)
	_G.Setting_table.Death_Step = vu
	
	Update_Setting(getgenv()['MyName'])
end})
mel:AddToggle({
    Name = "Auto Sharkman Karate",
    _G.Setting_table.Sharkman_Karate,
    Callback = function(vu)
	_G.Setting_table.Sharkman_Karate = vu
	
	Update_Setting(getgenv()['MyName'])
end})
mel:AddToggle({
    Name = "Auto Electric Claw",
    _G.Setting_table.Electric_Claw,
    Callback = function(vu)
	_G.Setting_table.Electric_Claw = vu
	
	Update_Setting(getgenv()['MyName'])
end})
mel:AddToggle({
    Name = "Auto Dragon Talon",
    _G.Setting_table.Dragon_Talon,
    Callback = function(vu)
	_G.Setting_table.Dragon_Talon = vu
	
	Update_Setting(getgenv()['MyName'])
end})

mel:AddToggle({
    Name = "Auto GodHuman",
    _G.Setting_table.Superhuman,
    Callback = function(vu)
    text("ยังไม่ได้ทำนะรอก่อน")
	_G.Setting_table.Superhuman = vu
	Update_Setting(getgenv()['MyName'])
end})

mel:AddToggle({
    Name = "Next Melee",
    _G.Setting_table.Next_Melee,
    Callback = function(vu)
	_G.Setting_table.Next_Melee = vu
	Update_Setting(getgenv()['MyName'])
	-- Auto Exc
end})

spawn(function()
	while wait(.5) do
		pcall(function()
			if not Mix_Farm or Farm_Melee_Ex then
				if _G.Setting_table.Superhuman and not Superhuman_H then
					if game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuySuperhuman") == 1 or game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuySuperhuman") == 2 then
						_G.Setting_table.Weapon = "Superhuman"
						
						if _G.Setting_table.Next_Melee then
							Superhuman_H = true
						end
					else
						if game.Players.LocalPlayer.Backpack:FindFirstChild("Combat") or game.Players.LocalPlayer.Character:FindFirstChild("Combat") then
							_G.Setting_table.Weapon = "Combat"
							if game:GetService("Players").LocalPlayer.Data.Beli.Value > 500000 then
								local args = {
									[1] = "BuyElectro"
								}
								game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
							end
							
						end
						
						if game.Players.LocalPlayer.Backpack:FindFirstChild("Black Leg") and game.Players.LocalPlayer.Backpack:FindFirstChild("Black Leg").Level.Value <= 299 and game.Players.LocalPlayer.Character.Humanoid.Health > 0 then
						    while wait() do
	game:service('VirtualInputManager'):SendKeyEvent(true, "V", false, game)
	wait(.1)
	game:service('VirtualInputManager'):SendKeyEvent(false, "V", false, game)
	end
							_G.Setting_table.Weapon = "Black Leg"
							
						end
						if game.Players.LocalPlayer.Backpack:FindFirstChild("Electro") and game.Players.LocalPlayer.Backpack:FindFirstChild("Electro").Level.Value <= 300 and game.Players.LocalPlayer.Character.Humanoid.Health > 0 then
							_G.Setting_table.Weapon = "Electro"
							
						end
						if game.Players.LocalPlayer.Backpack:FindFirstChild("Fishman Karate") and game.Players.LocalPlayer.Backpack:FindFirstChild("Fishman Karate").Level.Value <= 299 and game.Players.LocalPlayer.Character.Humanoid.Health > 0 then
							_G.Setting_table.Weapon = "Fishman Karate"
							
						end
						if game.Players.LocalPlayer.Backpack:FindFirstChild("Dragon Claw") and game.Players.LocalPlayer.Backpack:FindFirstChild("Dragon Claw").Level.Value <= 300 and game.Players.LocalPlayer.Character.Humanoid.Health > 0 then
							_G.Setting_table.Weapon = "Dragon Claw"
							
						end
						if game.Players.LocalPlayer.Backpack:FindFirstChild("Black Leg") and game.Players.LocalPlayer.Backpack:FindFirstChild("Black Leg").Level.Value >= 300 and game.Players.LocalPlayer.Character.Humanoid.Health > 0 then
							
							local args = {
								[1] = "BuyFishmanKarate"
							}
							game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
						end
						if game.Players.LocalPlayer.Character:FindFirstChild("Black Leg") and game.Players.LocalPlayer.Character:FindFirstChild("Black Leg").Level.Value >= 300 and game.Players.LocalPlayer.Character.Humanoid.Health > 0 then
							local args = {
								[1] = "BuyFishmanKarate"
							}
							game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
						end
						
						if game.Players.LocalPlayer.Backpack:FindFirstChild("Electro") and game.Players.LocalPlayer.Backpack:FindFirstChild("Electro").Level.Value >= 300 and game.Players.LocalPlayer.Character.Humanoid.Health > 0 then
							
							local args = {
								[1] = "BuyBlackLeg"
							}
							game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
						end
						if game.Players.LocalPlayer.Character:FindFirstChild("Electro") and game.Players.LocalPlayer.Character:FindFirstChild("Electro").Level.Value >= 300 and game.Players.LocalPlayer.Character.Humanoid.Health > 0 then
							
							local args = {
								[1] = "BuyBlackLeg"
							}
							game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
						end
						if game.Players.LocalPlayer.Backpack:FindFirstChild("Fishman Karate") and game.Players.LocalPlayer.Backpack:FindFirstChild("Fishman Karate").Level.Value >= 300 and game.Players.LocalPlayer.Character.Humanoid.Health > 0 then
							local FG = game:GetService("Players").LocalPlayer.Data.Fragments.Value
							if FG >= 1500 then
								local args = {
									[1] = "BlackbeardReward",
									[2] = "DragonClaw",
									[3] = "2"
								}
								game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
							elseif _G.Setting_table.Melee_Hop and not Mix_Farm then
								Raid_FG()
							end
						end
						if game.Players.LocalPlayer.Character:FindFirstChild("Fishman Karate") and game.Players.LocalPlayer.Character:FindFirstChild("Fishman Karate").Level.Value >= 300 and game.Players.LocalPlayer.Character.Humanoid.Health > 0 then
							local FG = game:GetService("Players").LocalPlayer.Data.Fragments.Value
							if FG >= 1500 then
								local args = {
									[1] = "BlackbeardReward",
									[2] = "DragonClaw",
									[3] = "2"
								}
								game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
							elseif _G.Setting_table.Melee_Hop and not Mix_Farm then
								Raid_FG()
							end
						end
						if game.Players.LocalPlayer.Backpack:FindFirstChild("Dragon Claw") and game.Players.LocalPlayer.Backpack:FindFirstChild("Dragon Claw").Level.Value >= 300 and game.Players.LocalPlayer.Character.Humanoid.Health > 0 then
							local Beli = game:GetService("Players").LocalPlayer.Data.Beli.Value
							if Beli >= 300000 then
								local args = {
									[1] = "BuySuperhuman"
								}
								game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
							else
								
								_G.Setting_table.Weapon = "Dragon Claw"
							end
						end
						if game.Players.LocalPlayer.Character:FindFirstChild("Dragon Claw") and game.Players.LocalPlayer.Character:FindFirstChild("Dragon Claw").Level.Value >= 300 and game.Players.LocalPlayer.Character.Humanoid.Health > 0 then
							local Beli = game:GetService("Players").LocalPlayer.Data.Beli.Value
							if Beli >= 300000 then
								local args = {
									[1] = "BuySuperhuman"
								}
								game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
							else
								
								_G.Setting_table.Weapon = "Dragon Claw"
							end
						end
					end
				elseif _G.Setting_table.Death_Step and not Death_Step_H then
					if game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyDeathStep") == 1 or game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyDeathStep") == 2 then
						_G.Setting_table.Weapon = "Death Step"
						
						if _G.Setting_table.Next_Melee then
							Death_Step_H = true
						end
					else
						if not New_World and _G.Setting_table.Next_Melee then
							TP_World2()
							wait(50)
						end
						if game.Players.LocalPlayer.Backpack:FindFirstChild("Black Leg") and game.Players.LocalPlayer.Backpack:FindFirstChild("Black Leg").Level.Value <= 400 and game.Players.LocalPlayer.Character.Humanoid.Health > 0 then
							_G.Setting_table.Weapon = "Black Leg"
							
						elseif not game.Players.LocalPlayer.Backpack:FindFirstChild("Black Leg") and not game.Players.LocalPlayer.Character:FindFirstChild("Black Leg") and not game.Players.LocalPlayer.Backpack:FindFirstChild("Death Step") and not game.Players.LocalPlayer.Character:FindFirstChild("Death Step") and game.Players.LocalPlayer.Character.Humanoid.Health > 0 then
							wait(4)
							if not game.Players.LocalPlayer.Backpack:FindFirstChild("Black Leg") and not game.Players.LocalPlayer.Character:FindFirstChild("Black Leg") and not game.Players.LocalPlayer.Backpack:FindFirstChild("Death Step") and not game.Players.LocalPlayer.Character:FindFirstChild("Death Step") then
								local args = {
									[1] = "BuyBlackLeg"
								}
								game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
							end
						end
						if game.Players.LocalPlayer.Backpack:FindFirstChild("Black Leg") and game.Players.LocalPlayer.Backpack:FindFirstChild("Black Leg").Level.Value >= 400 then
							local Beli = game:GetService("Players").LocalPlayer.Data.Beli.Value
							local FG = game:GetService("Players").LocalPlayer.Data.Fragments.Value
							if FG >= 5000 and Beli >= 3000000 then
								if game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyDeathStep") ~= 1 then
									if game.Players.LocalPlayer.Backpack:FindFirstChild("Library Key") or game.Players.LocalPlayer.Character:FindFirstChild("Library Key") then
										Mix_Farm = true
										repeat wait(1)
											EquipWeapon("Library Key")
											TP(CFrame.new(6377.12549, 296.634735, -6843.76025, -0.860993743, 1.17677516e-07, -0.508615494, 1.31121894e-07, 1, 9.40274347e-09, 0.508615494, -5.8594928e-08, -0.860993743))
										until not game.Players.LocalPlayer.Backpack:FindFirstChild("Library Key") and not game.Players.LocalPlayer.Character:FindFirstChild("Library Key")
										Mix_Farm = nil
									else
										if game:GetService("ReplicatedStorage"):FindFirstChild("Awakened Ice Admiral [Lv. 1400] [Boss]") or game:GetService("Workspace").Enemies:FindFirstChild("Awakened Ice Admiral [Lv. 1400] [Boss]") then
											Mix_Farm = true
											Farm_Melee_Ex = true
											if game:GetService("Workspace").Enemies:FindFirstChild("Awakened Ice Admiral [Lv. 1400] [Boss]") and not AutoRaid then
												repeat wait()
													TP(game:GetService("Workspace").Enemies:FindFirstChild("Awakened Ice Admiral [Lv. 1400] [Boss]").HumanoidRootPart.CFrame*CFrame.new(0,30,0))
													EquipWeapon(_G.Setting_table.Weapon)
													game:GetService'VirtualUser':CaptureController()
													game:GetService'VirtualUser':Button1Down(Vector2.new(1280,700))
												until not game:GetService("Workspace").Enemies:FindFirstChild("Awakened Ice Admiral [Lv. 1400] [Boss]") or game:GetService("Workspace").Enemies:FindFirstChild("Awakened Ice Admiral [Lv. 1400] [Boss]").Humanoid.Health <= 0 
												Mix_Farm = nil
												Farm_Melee_Ex = nil
											elseif game:GetService("ReplicatedStorage"):FindFirstChild("Awakened Ice Admiral [Lv. 1400] [Boss]") then
												TP(game:GetService("ReplicatedStorage"):FindFirstChild("Awakened Ice Admiral [Lv. 1400] [Boss]").HumanoidRootPart.CFrame*CFrame.new(0,50,0))
											end
										elseif _G.Setting_table.Melee_Hop then
											wait(5)
											if not game:GetService("ReplicatedStorage"):FindFirstChild("Awakened Ice Admiral [Lv. 1400] [Boss]") and not game:GetService("Workspace").Enemies:FindFirstChild("Awakened Ice Admiral [Lv. 1400] [Boss]") then
												HopServer()
												wait(50)
											end
										end
									end
								elseif Farm_Melee_Ex then
									Farm_Melee_Ex = nil
									Mix_Farm = nil
								elseif game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyDeathStep") == 1 then
									game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyDeathStep")
								end
							elseif FG < 5000 and not Mix_Farm and _G.Setting_table.Melee_Hop then
								Raid_FG()
							end
						end
						if game.Players.LocalPlayer.Character:FindFirstChild("Black Leg") and game.Players.LocalPlayer.Character:FindFirstChild("Black Leg").Level.Value >= 400 then
							local Beli = game:GetService("Players").LocalPlayer.Data.Beli.Value
							local FG = game:GetService("Players").LocalPlayer.Data.Fragments.Value
							if FG >= 5000 and Beli >= 3000000 then
								if game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyDeathStep") ~= 1 then
									if game.Players.LocalPlayer.Backpack:FindFirstChild("Library Key") or game.Players.LocalPlayer.Character:FindFirstChild("Library Key") then
										Mix_Farm = true
										repeat wait(1)
											EquipWeapon("Library Key")
											TP(CFrame.new(6377.12549, 296.634735, -6843.76025, -0.860993743, 1.17677516e-07, -0.508615494, 1.31121894e-07, 1, 9.40274347e-09, 0.508615494, -5.8594928e-08, -0.860993743))
										until not game.Players.LocalPlayer.Backpack:FindFirstChild("Library Key") and not game.Players.LocalPlayer.Character:FindFirstChild("Library Key")
										Mix_Farm = nil
									else
										if game:GetService("ReplicatedStorage"):FindFirstChild("Awakened Ice Admiral [Lv. 1400] [Boss]") or game:GetService("Workspace").Enemies:FindFirstChild("Awakened Ice Admiral [Lv. 1400] [Boss]") then
											Mix_Farm = true
											Farm_Melee_Ex = true
											if game:GetService("Workspace").Enemies:FindFirstChild("Awakened Ice Admiral [Lv. 1400] [Boss]") and not AutoRaid then
												repeat wait()
													TP(game:GetService("Workspace").Enemies:FindFirstChild("Awakened Ice Admiral [Lv. 1400] [Boss]").HumanoidRootPart.CFrame*CFrame.new(0,30,0))
													EquipWeapon(_G.Setting_table.Weapon)
													game:GetService'VirtualUser':CaptureController()
													game:GetService'VirtualUser':Button1Down(Vector2.new(1280,700))
												until not game:GetService("Workspace").Enemies:FindFirstChild("Awakened Ice Admiral [Lv. 1400] [Boss]") or game:GetService("Workspace").Enemies:FindFirstChild("Awakened Ice Admiral [Lv. 1400] [Boss]").Humanoid.Health <= 0 
												Mix_Farm = nil
												Farm_Melee_Ex = nil
											elseif game:GetService("ReplicatedStorage"):FindFirstChild("Awakened Ice Admiral [Lv. 1400] [Boss]") then
												TP(game:GetService("ReplicatedStorage"):FindFirstChild("Awakened Ice Admiral [Lv. 1400] [Boss]").HumanoidRootPart.CFrame*CFrame.new(0,50,0))
											end
										elseif _G.Setting_table.Melee_Hop then
											wait(5)
											if not game:GetService("ReplicatedStorage"):FindFirstChild("Awakened Ice Admiral [Lv. 1400] [Boss]") and not game:GetService("Workspace").Enemies:FindFirstChild("Awakened Ice Admiral [Lv. 1400] [Boss]") then
												HopServer()
												wait(50)
											end
										end
									end
								elseif Farm_Melee_Ex then
									Farm_Melee_Ex = nil
									Mix_Farm = nil
								elseif game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyDeathStep") == 1 then
									game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyDeathStep")
								end
							elseif FG < 5000 and not Mix_Farm and _G.Setting_table.Melee_Hop then
								Raid_FG()
							end
						end
					end	
				elseif _G.Setting_table.Sharkman_Karate and not Sharkman_Karate_H then
					if game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuySharkmanKarate") == 1 or game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuySharkmanKarate") == 2 then
						_G.Setting_table.Weapon = "Sharkman Karate"
						if _G.Setting_table.Next_Melee then
							Sharkman_Karate_H = true
						end
					else
						if not New_World and _G.Setting_table.Next_Melee then
							TP_World2()
							wait(50)
						end
						if game.Players.LocalPlayer.Backpack:FindFirstChild("Fishman Karate") and game.Players.LocalPlayer.Backpack:FindFirstChild("Fishman Karate").Level.Value <= 400 and game.Players.LocalPlayer.Character.Humanoid.Health > 0 then
							_G.Setting_table.Weapon  = "Fishman Karate"
							
						elseif not game.Players.LocalPlayer.Backpack:FindFirstChild("Fishman Karate") and not game.Players.LocalPlayer.Character:FindFirstChild("Fishman Karate") and not game.Players.LocalPlayer.Backpack:FindFirstChild("Sharkman Karate") and not game.Players.LocalPlayer.Character:FindFirstChild("Sharkman Karate") and game.Players.LocalPlayer.Character.Humanoid.Health > 0 then
							wait(5)
							if not game.Players.LocalPlayer.Backpack:FindFirstChild("Fishman Karate") and not game.Players.LocalPlayer.Character:FindFirstChild("Fishman Karate") and not game.Players.LocalPlayer.Backpack:FindFirstChild("Sharkman Karate") and not game.Players.LocalPlayer.Character:FindFirstChild("Sharkman Karate") then
								local args = {
										[1] = "BuyFishmanKarate"
									}
								game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
							end
						end
						if game.Players.LocalPlayer.Backpack:FindFirstChild("Fishman Karate") and game.Players.LocalPlayer.Backpack:FindFirstChild("Fishman Karate").Level.Value >= 400 then
							if string.find(game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuySharkmanKarate"), "keys") then
								if game.Players.LocalPlayer.Character:FindFirstChild("Water Key") or game.Players.LocalPlayer.Backpack:FindFirstChild("Water Key") then
									EquipWeapon("Water Key")
									wait(0.5)
									game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuySharkmanKarate",true)
								else
									if game:GetService("ReplicatedStorage"):FindFirstChild("Tide Keeper [Lv. 1475] [Boss]") or game:GetService("Workspace").Enemies:FindFirstChild("Tide Keeper [Lv. 1475] [Boss]") then
										Mix_Farm = true
										Farm_Melee_Ex = true
										if game:GetService("Workspace").Enemies:FindFirstChild("Tide Keeper [Lv. 1475] [Boss]") and not AutoRaid then
											for i,v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
												if v.Name == "Tide Keeper [Lv. 1475] [Boss]" then
													repeat wait(_G.Fast_Delay)
														EquipWeapon(_G.Setting_table.Weapon)
														TP(v.HumanoidRootPart.CFrame * CFrame.new(0,25,0))
														AttackNoCD()
													until v.Humanoid.Health <= 0 or not v.Parent or not _G.Setting_table.Sharkman_Karate
													Mix_Farm = nil
													Farm_Melee_Ex = nil
												end
											end
										elseif game:GetService("ReplicatedStorage"):FindFirstChild("Tide Keeper [Lv. 1475] [Boss]") then
											TP(game:GetService("ReplicatedStorage"):FindFirstChild("Tide Keeper [Lv. 1475] [Boss]").HumanoidRootPart.CFrame*CFrame.new(0,50,0))
										end
									elseif _G.Setting_table.Melee_Hop then
										wait(5)
										if not game:GetService("ReplicatedStorage"):FindFirstChild("Tide Keeper [Lv. 1475] [Boss]") and not game:GetService("Workspace").Enemies:FindFirstChild("Tide Keeper [Lv. 1475] [Boss]") then
											HopServer()
											wait(50)
										end
									end
								end
							elseif FG >= 5000 and Beli >= 3000000 and game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuySharkmanKarate",true) == 1 then
								local args = {
									[1] = "BuySharkmanKarate",
									[2] = true
								}
								game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
								local args = {
									[1] = "BuySharkmanKarate"
								}
								game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
							elseif Farm_Melee_Ex then
								Farm_Melee_Ex = nil
								Mix_Farm = nil
							elseif FG < 5000 and not Mix_Farm and _G.Setting_table.Melee_Hop then
								Raid_FG()
							end
						end
						if game.Players.LocalPlayer.Character:FindFirstChild("Fishman Karate") and game.Players.LocalPlayer.Character:FindFirstChild("Fishman Karate").Level.Value >= 400 then
							if string.find(game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuySharkmanKarate"), "keys") then
								if game.Players.LocalPlayer.Character:FindFirstChild("Water Key") or game.Players.LocalPlayer.Backpack:FindFirstChild("Water Key") then
									EquipWeapon("Water Key")
									wait(0.5)
									game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuySharkmanKarate",true)
								else
									if game:GetService("ReplicatedStorage"):FindFirstChild("Tide Keeper [Lv. 1475] [Boss]") or game:GetService("Workspace").Enemies:FindFirstChild("Tide Keeper [Lv. 1475] [Boss]") then
										Mix_Farm = true
										Farm_Melee_Ex = true
										if game:GetService("Workspace").Enemies:FindFirstChild("Tide Keeper [Lv. 1475] [Boss]") and not AutoRaid then
											for i,v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
												if v.Name == "Tide Keeper [Lv. 1475] [Boss]" then
													repeat wait(_G.Fast_Delay)
														EquipWeapon(_G.Setting_table.Weapon)
														TP(v.HumanoidRootPart.CFrame * CFrame.new(0,25,0))
														AttackNoCD()
													until v.Humanoid.Health <= 0 or not v.Parent or not _G.Setting_table.Sharkman_Karate
													Mix_Farm = nil
													Farm_Melee_Ex = nil
												end
											end
										elseif game:GetService("ReplicatedStorage"):FindFirstChild("Tide Keeper [Lv. 1475] [Boss]") then
											TP(game:GetService("ReplicatedStorage"):FindFirstChild("Tide Keeper [Lv. 1475] [Boss]").HumanoidRootPart.CFrame*CFrame.new(0,50,0))
										end
									elseif _G.Setting_table.Melee_Hop then
										wait(5)
										if not game:GetService("ReplicatedStorage"):FindFirstChild("Tide Keeper [Lv. 1475] [Boss]") and not game:GetService("Workspace").Enemies:FindFirstChild("Tide Keeper [Lv. 1475] [Boss]") then
											HopServer()
											wait(50)
										end
									end
								end
							elseif FG >= 5000 and Beli >= 3000000 and game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuySharkmanKarate",true) == 1 then
								local args = {
									[1] = "BuySharkmanKarate",
									[2] = true
								}
								game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
								local args = {
									[1] = "BuySharkmanKarate"
								}
								game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
							elseif Farm_Melee_Ex then
								Farm_Melee_Ex = nil
								Mix_Farm = nil
							elseif FG < 5000 and not Mix_Farm and _G.Setting_table.Melee_Hop then
								Raid_FG()
							end
						end
					end
				elseif _G.Setting_table.Electric_Claw and not Electric_Claw_H then
					if game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyElectricClaw") == 1 or game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyElectricClaw") == 2 then
						_G.Setting_table.Weapon = "Electric Claw"
						if _G.Setting_table.Next_Melee then
							Electric_Claw_H = true
						end
					else
						if game.Players.LocalPlayer.Backpack:FindFirstChild("Electro") and game.Players.LocalPlayer.Backpack:FindFirstChild("Electro").Level.Value <= 400 and game.Players.LocalPlayer.Character.Humanoid.Health > 0 then
							_G.Setting_table.Weapon  = "Electro"
							
						elseif not game.Players.LocalPlayer.Backpack:FindFirstChild("Electro") and not game.Players.LocalPlayer.Character:FindFirstChild("Electro") and not game.Players.LocalPlayer.Backpack:FindFirstChild("Electric Claw") and not game.Players.LocalPlayer.Character:FindFirstChild("Electric Claw") then
							wait(5)
							if not game.Players.LocalPlayer.Backpack:FindFirstChild("Electro") and not game.Players.LocalPlayer.Character:FindFirstChild("Electro") and not game.Players.LocalPlayer.Backpack:FindFirstChild("Electric Claw") and not game.Players.LocalPlayer.Character:FindFirstChild("Electric Claw") then
								local args = {
										[1] = "BuyElectro"
									}
								game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
							end
						end
						if game.Players.LocalPlayer.Backpack:FindFirstChild("Electro") and game.Players.LocalPlayer.Backpack:FindFirstChild("Electro").Level.Value >= 400 and Three_World then
							local Beli = game:GetService("Players").LocalPlayer.Data.Beli.Value
							local FG = game:GetService("Players").LocalPlayer.Data.Fragments.Value
							if FG >= 5000 and Beli >= 3000000 then
								if game.ReplicatedStorage.Remotes.CommF_:InvokeServer("BuyElectricClaw", true) == 4 then
									if game.ReplicatedStorage.Remotes.CommF_:InvokeServer("BuyElectricClaw", "Start") == nil and not AutoRaid then
										Mix_Farm = true
										repeat wait(1)
											TP2(CFrame.new(-12548, 337, -7481))
										until (Vector3.new(-12548, 337, -7481)-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 10
										Mix_Farm = nil
									end
								else
									game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyElectricClaw")
								end
							elseif FG < 5000 and not Mix_Farm and _G.Setting_table.Melee_Hop then
								Raid_FG()
							end
						end
						if game.Players.LocalPlayer.Character:FindFirstChild("Electro") and game.Players.LocalPlayer.Character:FindFirstChild("Electro").Level.Value >= 400 and Three_World then
							local Beli = game:GetService("Players").LocalPlayer.Data.Beli.Value
							local FG = game:GetService("Players").LocalPlayer.Data.Fragments.Value
							if FG >= 5000 and Beli >= 3000000 then
								if game.ReplicatedStorage.Remotes.CommF_:InvokeServer("BuyElectricClaw", true) == 4 then
									if game.ReplicatedStorage.Remotes.CommF_:InvokeServer("BuyElectricClaw", "Start") == nil and not AutoRaid then
										Mix_Farm = true
										repeat wait(1)
											TP2(CFrame.new(-12548, 337, -7481))
										until (Vector3.new(-12548, 337, -7481)-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 10
										Mix_Farm = nil
									end
								else
									game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyElectricClaw")
								end
							elseif FG < 5000 and not Mix_Farm and _G.Setting_table.Melee_Hop then
								Raid_FG()
							end
						end
					end
				elseif _G.Setting_table.Dragon_Talon and not Dragon_Talon_H then
					if game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyDragonTalon") == 1 or game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyDragonTalon") == 2 then
						_G.Setting_table.Weapon = "Dragon Talon"
						if _G.Setting_table.Next_Melee then
							Dragon_Talon_H = true
						end
					else
						if game.Players.LocalPlayer.Backpack:FindFirstChild("Dragon Claw") and game.Players.LocalPlayer.Backpack:FindFirstChild("Dragon Claw").Level.Value <= 400 and game.Players.LocalPlayer.Character.Humanoid.Health > 0 then
							_G.Setting_table.Weapon = "Dragon Claw"
							
						elseif not game.Players.LocalPlayer.Backpack:FindFirstChild("Dragon Claw") and not game.Players.LocalPlayer.Character:FindFirstChild("Dragon Claw") and not game.Players.LocalPlayer.Backpack:FindFirstChild("Dragon Talon") and not game.Players.LocalPlayer.Character:FindFirstChild("Dragon Talon") and game.Players.LocalPlayer.Character.Humanoid.Health > 0 then
							wait(5)
							if not game.Players.LocalPlayer.Backpack:FindFirstChild("Dragon Claw") and not game.Players.LocalPlayer.Character:FindFirstChild("Dragon Claw") and not game.Players.LocalPlayer.Backpack:FindFirstChild("Dragon Talon") and not game.Players.LocalPlayer.Character:FindFirstChild("Dragon Talon") then
								local args = {
									[1] = "BlackbeardReward",
									[2] = "DragonClaw",
									[3] = "2"
								}
								game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
							end
						end
						if game.Players.LocalPlayer.Backpack:FindFirstChild("Dragon Claw") and game.Players.LocalPlayer.Backpack:FindFirstChild("Dragon Claw").Level.Value >= 400 then
							local Lv = game:GetService("Players").LocalPlayer.Data.Level.Value
							local Beli = game:GetService("Players").LocalPlayer.Data.Beli.Value
							local FG = game:GetService("Players").LocalPlayer.Data.Fragments.Value
							if FG >= 5000 and Beli >= 3000000 and Lv >= 1950 then
								local B_H = game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Bones","Check")
								Auto_Farm_Melee = false
								Auto_Farm_Bone = true
								if tonumber(B_H) >= 500 then
									spawn(function()
										repeat wait(1)
											wait(15)
											IKAIP = true
										until IKAIP == true
									end)
									repeat wait(.1)
										local args = {
											[1] = "Bones",
											[2] = "Check"
										}
										game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
										local args = {
											[1] = "Bones",
											[2] = "Buy",
											[3] = 1,
											[4] = 1
										}
										game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
									until IKAIP == true or game.Players.LocalPlayer.Backpack:FindFirstChild("Fire Essence") or game.Players.LocalPlayer.Character:FindFirstChild("Fire Essence")
								end
								if game.Players.LocalPlayer.Backpack:FindFirstChild("Fire Essence") or game.Players.LocalPlayer.Character:FindFirstChild("Fire Essence") then
									game.ReplicatedStorage.Remotes.CommF_:InvokeServer("BuyDragonTalon",true)
								end
								if game.ReplicatedStorage.Remotes.CommF_:InvokeServer("BuyDragonTalon", true) == 3 then
									game.ReplicatedStorage.Remotes.CommF_:InvokeServer("Bones", "Buy",1,1)
									game.ReplicatedStorage.Remotes.CommF_:InvokeServer("BuyDragonTalon",true)
								elseif game.ReplicatedStorage.Remotes.CommF_:InvokeServer("BuyDragonTalon", true) == 1 then
									game.ReplicatedStorage.Remotes.CommF_:InvokeServer("BuyDragonTalon")
								else
									game.ReplicatedStorage.Remotes.CommF_:InvokeServer("BuyDragonTalon",true)
									game.ReplicatedStorage.Remotes.CommF_:InvokeServer("BuyDragonTalon")
								end
								wait(2)
							elseif FG < 5000 and not Mix_Farm and _G.Setting_table.Melee_Hop then
								Raid_FG()
							end
						end
						if game.Players.LocalPlayer.Character:FindFirstChild("Dragon Claw") and game.Players.LocalPlayer.Character:FindFirstChild("Dragon Claw").Level.Value >= 400 then
							local Lv = game:GetService("Players").LocalPlayer.Data.Level.Value
							local Beli = game:GetService("Players").LocalPlayer.Data.Beli.Value
							local FG = game:GetService("Players").LocalPlayer.Data.Fragments.Value
							if FG >= 5000 and Beli >= 3000000 and Lv >= 1950 then
								local B_H = game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Bones","Check")
								Auto_Farm_Melee = false
								Auto_Farm_Bone = true
								if tonumber(B_H) >= 500 then
									spawn(function()
										repeat wait(1)
											wait(15)
											IKAIP = true
										until IKAIP == true
									end)
									repeat wait(.1)
										local args = {
											[1] = "Bones",
											[2] = "Check"
										}
										game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
										local args = {
											[1] = "Bones",
											[2] = "Buy",
											[3] = 1,
											[4] = 1
										}
										game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
									until IKAIP == true or game.Players.LocalPlayer.Backpack:FindFirstChild("Fire Essence") or game.Players.LocalPlayer.Character:FindFirstChild("Fire Essence")
								end
								if game.Players.LocalPlayer.Backpack:FindFirstChild("Fire Essence") or game.Players.LocalPlayer.Character:FindFirstChild("Fire Essence") then
									game.ReplicatedStorage.Remotes.CommF_:InvokeServer("BuyDragonTalon",true)
								end
								if game.ReplicatedStorage.Remotes.CommF_:InvokeServer("BuyDragonTalon", true) == 3 then
									game.ReplicatedStorage.Remotes.CommF_:InvokeServer("Bones", "Buy",1,1)
									game.ReplicatedStorage.Remotes.CommF_:InvokeServer("BuyDragonTalon",true)
								elseif game.ReplicatedStorage.Remotes.CommF_:InvokeServer("BuyDragonTalon", true) == 1 then
									game.ReplicatedStorage.Remotes.CommF_:InvokeServer("BuyDragonTalon")
								else
									game.ReplicatedStorage.Remotes.CommF_:InvokeServer("BuyDragonTalon",true)
									game.ReplicatedStorage.Remotes.CommF_:InvokeServer("BuyDragonTalon")
								end
								wait(2)
							elseif FG < 5000 and not Mix_Farm and _G.Setting_table.Melee_Hop then
								Raid_FG()
							end
						end
					end
				else
					wait(2)
				end
			else
				wait(3)
			end
		end)
	end
end)

local el = Quest_Tab:CreateSection({Name = "EliteHunter",Side = "Right"})
local Kill_Elite_Hunter_ST = el:AddLabel("Kill Elite Hunter : 0")
local es = el:AddLabel("Elite : 🔴")
el:AddToggle({
    Name = "Auto Elite Hunter",
    _G.Setting_table.Auto_Elite_Hunter,
    Callback = function(vu)
	Auto_Elite_Hunter = vu
	_G.Setting_table.Auto_Elite_Hunter = vu
	Update_Setting(getgenv()['MyName'])
end})
spawn(function()
	while wait(.5) do
		pcall(function()
			if Auto_Elite_Hunter then
				if not Mix_Farm or Auto_Elite_Hunter_Farm then
					if game:GetService("ReplicatedStorage"):FindFirstChild("Urban [Lv. 1750]") or game:GetService("Workspace").Enemies:FindFirstChild("Urban [Lv. 1750]") then
						Mix_Farm = true
						Auto_Elite_Hunter_Farm = true
						game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("EliteHunter")
						if game:GetService("Workspace").Enemies:FindFirstChild("Urban [Lv. 1750]") then
							for i,v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
								if v.Name == "Urban [Lv. 1750]" then
									repeat wait(Fast_Delay)
										EquipWeapon(_G.Setting_table.Weapon)
										TP(v.HumanoidRootPart.CFrame * Cethod)
										game:GetService'VirtualUser':CaptureController()
										game:GetService'VirtualUser':Button1Down(Vector2.new(1280,630))
									until v.Humanoid.Health <= 0 or not v.Parent or not Auto_Elite_Hunter
									Mix_Farm = nil
									Auto_Elite_Hunter_Farm = nil
								end
							end
						elseif game:GetService("ReplicatedStorage"):FindFirstChild("Urban [Lv. 1750]") then
							TP(game:GetService("ReplicatedStorage"):FindFirstChild("Urban [Lv. 1750]").HumanoidRootPart.CFrame*CFrame.new(0,30,0))
						end
					elseif game:GetService("ReplicatedStorage"):FindFirstChild("Diablo [Lv. 1750]") or game:GetService("Workspace").Enemies:FindFirstChild("Diablo [Lv. 1750]") then
						Mix_Farm = true
						Auto_Elite_Hunter_Farm = true
						game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("EliteHunter")
						if game:GetService("Workspace").Enemies:FindFirstChild("Diablo [Lv. 1750]") then
							for i,v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
								if v.Name == "Diablo [Lv. 1750]" then
									repeat wait(Fast_Delay)
										EquipWeapon(_G.Setting_table.Weapon)
										TP(v.HumanoidRootPart.CFrame * Cethod)
										game:GetService'VirtualUser':CaptureController()
										game:GetService'VirtualUser':Button1Down(Vector2.new(1280,630))
									until v.Humanoid.Health <= 0 or not v.Parent or not Auto_Elite_Hunter
									Mix_Farm = nil
									Auto_Elite_Hunter_Farm = nil
								end
							end
						elseif game:GetService("ReplicatedStorage"):FindFirstChild("Diablo [Lv. 1750]") then
							TP(game:GetService("ReplicatedStorage"):FindFirstChild("Diablo [Lv. 1750]").HumanoidRootPart.CFrame*CFrame.new(0,30,0))
						end
					elseif game:GetService("ReplicatedStorage"):FindFirstChild("Deandre [Lv. 1750]") or game:GetService("Workspace").Enemies:FindFirstChild("Deandre [Lv. 1750]") then
						Mix_Farm = true
						Auto_Elite_Hunter_Farm = true
						game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("EliteHunter")
						if game:GetService("Workspace").Enemies:FindFirstChild("Deandre [Lv. 1750]") then
							for i,v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
								if v.Name == "Deandre [Lv. 1750]" then
									repeat wait(Fast_Delay)
										EquipWeapon(_G.Setting_table.Weapon)
									TP(v.HumanoidRootPart.CFrame * Cethod)
										game:GetService'VirtualUser':CaptureController()
										game:GetService'VirtualUser':Button1Down(Vector2.new(1280,630))
									until v.Humanoid.Health <= 0 or not v.Parent or not Auto_Elite_Hunter
									Mix_Farm = nil
									Auto_Elite_Hunter_Farm = nil
								end
							end
						elseif game:GetService("ReplicatedStorage"):FindFirstChild("Deandre [Lv. 1750]") then
							TP(game:GetService("ReplicatedStorage"):FindFirstChild("Deandre [Lv. 1750]").HumanoidRootPart.CFrame*CFrame.new(0,30,0))
						end
					elseif _G.Setting_table.Auto_Elite_Hunter_Hop then
						wait(5)
						if not game:GetService("ReplicatedStorage"):FindFirstChild("Urban [Lv. 1750]") and not game:GetService("Workspace").Enemies:FindFirstChild("Urban [Lv. 1750]") and not game:GetService("ReplicatedStorage"):FindFirstChild("Diablo [Lv. 1750]") and not game:GetService("Workspace").Enemies:FindFirstChild("Diablo [Lv. 1750]") and not game:GetService("ReplicatedStorage"):FindFirstChild("Deandre [Lv. 1750]") and not game:GetService("Workspace").Enemies:FindFirstChild("Deandre [Lv. 1750]") then
							HopServer()
							wait(50)
						end
					elseif game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text == "Defeat  Urban (0/1)" or game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text == "Defeat  Deandre (0/1)" or game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text == "Defeat  Diablo (0/1)" then
						Mix_Farm = nil
						Auto_Elite_Hunter_Farm = nil
					elseif Auto_Elite_Hunter_Farm then
						Mix_Farm = nil
						Auto_Elite_Hunter_Farm = nil
					else
						wait(3)
					end
				end
			else
				wait(2)
			end
		end)
	end
end)

local rd = Raid_Tab:CreateSection({Name = "Raid"})
--[[Raid_Tab:Toggle("Auto Raid Hop",_G.Setting_table.Auto_Raid_Hop,function(vu)
	Auto_Raid = vu
	_G.Setting_table.Auto_Raid_Hop = vu
	Update_Setting(getgenv()['MyName'])
end)]]--
rd:AddToggle({
    Name = "Auto Raid",
    _G.Setting_table.Auto_Raid,
    Callback = function(vu)
	Auto_Raid = vu
	_G.Setting_table.Auto_Raid = vu
	Update_Setting(getgenv()['MyName'])
end})
rd:AddToggle({
    Name = "Next Islands",
    _G.Setting_table.Next_Islands,
    Callback = function(vu)
	Next_Islands = vu
	_G.Setting_table.Next_Islands = vu
	Update_Setting(getgenv()['MyName'])
end})
if _G.Setting_table.Auto_Raid_Hop then
	Auto_Raid = true
end

if type(_G.Setting_table.Select_Map) ~= 'string' then
    _G.Setting_table.Select_Map = "Flame"
end
function Buy_Chip()
	game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("RaidsNpc", "Select", _G.Setting_table.Select_Map)
end
spawn(function()
	while wait(.5) do
		pcall(function()
			if Auto_Raid then
				if game:GetService("Players")["LocalPlayer"].PlayerGui.Main.Timer.Visible == true then
					for i,v in pairs(game.Workspace.Enemies:GetDescendants()) do
						if v:FindFirstChild("Humanoid") and v:FindFirstChild("HumanoidRootPart") and v.Humanoid.Health > 0 then
							repeat wait(.1)
								sethiddenproperty(game.Players.LocalPlayer, "SimulationRadius", math.huge)
								v.Humanoid.Health = 0
								v.HumanoidRootPart.CanCollide = false
								v.HumanoidRootPart.Size = Vector3.new(50,50,50)
								v.HumanoidRootPart.Transparency = 0.5
							until not Auto_Raid or not v.Parent or v.Humanoid.Health <= 0
						end
					end
				end
			else
				wait(3)
			end
		end)
	end
end)
spawn(function()
	while wait(.5) do
		pcall(function()
			if Next_Islands then
				if game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 5") then
					for i,v in pairs(game:GetService("Workspace")["_WorldOrigin"].Locations:GetChildren()) do
						if v.Name == "Island 5" and (v.Position-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 2300 then
							TP3(v.CFrame*CFrame.new(0,70,0))
						end
					end
				elseif game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 4") then
					for i,v in pairs(game:GetService("Workspace")["_WorldOrigin"].Locations:GetChildren()) do
						if v.Name == "Island 4" and (v.Position-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 2000 then
							TP3(v.CFrame*CFrame.new(0,70,0))
						--wait(2)
						end
					end
				elseif game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 3") then
					for i,v in pairs(game:GetService("Workspace")["_WorldOrigin"].Locations:GetChildren()) do
						if v.Name == "Island 3" and (v.Position-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 2100 then
							TP3(v.CFrame*CFrame.new(0,70,0))
							--wait(2)
						end
					end
				elseif game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 2") then
					for i,v in pairs(game:GetService("Workspace")["_WorldOrigin"].Locations:GetChildren()) do
						if v.Name == "Island 2" and (v.Position-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 2000 then
							TP3(v.CFrame*CFrame.new(0,70,0))
							--wait(2)
						end
					end
				elseif game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 1") then
					for i,v in pairs(game:GetService("Workspace")["_WorldOrigin"].Locations:GetChildren()) do
						if v.Name == "Island 1" and (v.Position-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 2000 then
							TP3(v.CFrame*CFrame.new(0,70,0))
							--wait(2)
						end
					end
				else
					wait(1)
				end
			else
				wait(2)
			end
		end)
	end
end)
rd:AddToggle({
    Name = "Auto Awaken",
    _G.Setting_table.Auto_Awaken,
    Callback = function(vu)
	_G.Setting_table.Auto_Awaken = vu
	Update_Setting(getgenv()['MyName'])
end})
Map = {
    "Dark",
    "Sand",
    "Magma",
    "Rumble",
    "Flame",
    "Ice",
    "Light",
    "Quake",
    "Human: Buddha",
    "Flame",
    "Bird: Phoenix",
    "Dough"
}
rd:AddDropdown({
    Name = "Select Dungeon",
    _G.Setting_table.Select_Map,
    List = Map,
    Callback = function(vu)
	_G.Setting_table.Select_Map = vu
	Update_Setting(getgenv()['MyName'])
end})

rd:AddLabel("Misc")
rd:AddToggle({
    Name = "Bring Fruit (risk)",
    _G.Setting_table.BringFruit,
    Callback = function(vu)
	BringFruit = vu
	_G.Setting_table.BringFruit = vu
	Update_Setting(getgenv()['MyName'])
end})
rd:AddToggle({
    Name = "Get Fruit Inventory",
    _G.Setting_table.Get_Fruit,
    Callback = function(vu)
	_G.Setting_table.Get_Fruit = vu
	Update_Setting(getgenv()['MyName'])
end})
spawn(function()
    while wait(.5) do
        pcall(function()
            if _G.Setting_table.Get_Fruit then
                if Inventory_Fruit then
                    Inventory_Fruit = nil
                end
                fruit = game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("getInventoryFruits")
                for i,v in pairs(fruit) do
                    if v["Price"] < 10000000 then
                        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("LoadFruit",v["Name"])
                    end
                end
			else
				wait(2)
            end
        end)
    end
end)


local stat = General_Tab:CreateSection({
    Name = "Stats",
    Side = "Right"
})
stat:AddToggle({
    Name = "Melee",
    _G.Setting_table.Melee_A,
    Value = true,
    Callback = function(vu)
	Melee_A = vu
	_G.Setting_table.Melee_A = vu
	Update_Setting(getgenv()['MyName'])
end})
stat:AddToggle({
    Name = "Defense",
    _G.Setting_table.Defense_A,
    Callback = function(vu)
	Defense_A = vu
	_G.Setting_table.Defense_A = vu
	Update_Setting(getgenv()['MyName'])
end})
stat:AddToggle({
    Name = "Sword",
    _G.Setting_table.Sword_A,
    Callback = function(vu)
	Sword_A = vu
	_G.Setting_table.Sword_A = vu
	Update_Setting(getgenv()['MyName'])
end})
stat:AddToggle({
    Name = "Fruit",
    _G.Setting_table.Fruit_A,
    Callback = function(vu)
	Fruit_A = vu
	_G.Setting_table.Fruit_A = vu
	Update_Setting(getgenv()['MyName'])
end})
stat:AddToggle({
    Name = "Gun",
    _G.Setting_table.Gun_A,
    Callback = function(vu)
	Gun_A = vu
	_G.Setting_table.Gun_A = vu
	Update_Setting(getgenv()['MyName'])
end})
stat:AddSlider({
    Name = "Point",
    Value = 3,
    Min = 1,
    Max = 2450,
    Callback = function(vu)
	Points = vu
end})

spawn(function()
    while wait() do
        if Melee_A then
            if game:GetService("Players").LocalPlayer.Data.Points.Value > 0 then
                game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("AddPoint", "Melee", Points)
            end
        end
    end
end)

spawn(function()
    while wait() do
        if Defense_A then
            if game:GetService("Players").LocalPlayer.Data.Points.Value > 0 then
                game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("AddPoint", "Defense", Points)
            end
        end
    end
end)

spawn(function()
    while wait() do
        if Sword_A then
            if game:GetService("Players").LocalPlayer.Data.Points.Value > 0 then
                game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("AddPoint", "Sword", Points)
            end
        end
    end
end)

spawn(function()
    while wait() do
        if Gun_A then
            if game:GetService("Players").LocalPlayer.Data.Points.Value > 0 then
                game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("AddPoint", "Gun", Points)
            end
        end
    end
end)

spawn(function()
    while wait() do
        if Fruit_A then
            if game:GetService("Players").LocalPlayer.Data.Points.Value > 0 then
                game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("AddPoint", "Demon Fruit", Points)
            end
        end
    end
end)


local FBss = General_Tab:CreateSection("Farm Boss")
FBss:AddToggle({
    Name = "Auto Farm",
    _G.Setting_table.Farm_Boss,
    Callback = function(vu)
	Auto_Farm_Boss = vu
	_G.Setting_table.Farm_Boss = vu
	Update_Setting(getgenv()['MyName'])
end})
spawn(function()
	while wait() do
		pcall(function()
			if Auto_Farm_Boss then
				if not Mix_Farm or Auto_Farm_Boss_Ex then
					if game.Workspace.Enemies:FindFirstChild(_G.Setting_table.Boss_Name) or game.ReplicatedStorage:FindFirstChild(_G.Setting_table.Boss_Name) then
						Mix_Farm = true
						Auto_Farm_Boss_Ex = true
						if game.Workspace.Enemies:FindFirstChild(_G.Setting_table.Boss_Name) then
							for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
								if v.Name == _G.Setting_table.Boss_Name and v.Humanoid.Health > 0 then
									game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("SetSpawnPoint")
									if v.Humanoid:FindFirstChild("Animator") then
										v.Humanoid.Animator:Destroy()
									end
									repeat wait(_G.Fast_Delay)
										EquipWeapon(_G.Setting_table.Weapon)
										
										wait()
									TP3(v.HumanoidRootPart.CFrame * Cethod)
										AttackNoCD()
									until v.Humanoid.Health <= 0 or not v.Parent or Auto_Farm_Boss == false
									Mix_Farm = nil
									Auto_Farm_Boss_Ex = nil
								end
							end
						elseif game.ReplicatedStorage:FindFirstChild(_G.Setting_table.Boss_Name) then
							TP3(game.ReplicatedStorage:FindFirstChild(_G.Setting_table.Boss_Name).HumanoidRootPart.CFrame * Cethod)
						end
					elseif game.Workspace.Enemies:FindFirstChild(_G.Setting_table.Boss_Lock) or game.ReplicatedStorage:FindFirstChild(_G.Setting_table.Boss_Lock) then
						Mix_Farm = true
						Auto_Farm_Boss_Ex = true
						if game.Workspace.Enemies:FindFirstChild(_G.Setting_table.Boss_Lock) then
							for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
								if v.Name == _G.Setting_table.Boss_Lock and v.Humanoid.Health > 0 then
									game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("SetSpawnPoint")
									if v.Humanoid:FindFirstChild("Animator") then
										v.Humanoid.Animator:Destroy()
									end
									repeat wait(_G.Fast_Delay)
									TP3(v.HumanoidRootPart.CFrame*CFrame.new(0,30,0))
										AttackNoCD()
									until v.Humanoid.Health <= 0 or not v.Parent or Auto_Farm_Boss == false
									Mix_Farm = nil
									Auto_Farm_Boss_Ex = nil
								end
							end
						elseif game.ReplicatedStorage:FindFirstChild(_G.Setting_table.Boss_Lock) then
							TP(game.ReplicatedStorage:FindFirstChild(_G.Setting_table.Boss_Lock).HumanoidRootPart.CFrame*CFrame.new(0,30,0))
						end
					elseif Auto_Farm_Boss_Ex then
						Mix_Farm = nil
						Auto_Farm_Boss_Ex = nil
					else
						wait(3)
					end
				end
			elseif _G.Setting_table.Auto_Farm_Boss_Hop then
				if Ping == nil then
					Hop_Boss()
					wait(1)
					print("....".._G.Setting_table.Boss_Name)
					Ping = true
				end
				if game.Workspace.Enemies:FindFirstChild(_G.Setting_table.Boss_Name) or game.ReplicatedStorage:FindFirstChild(_G.Setting_table.Boss_Name) then
					Mix_Farm = true
					Auto_Farm_Boss_Ex = true
					if game.Workspace.Enemies:FindFirstChild(_G.Setting_table.Boss_Name) then
						for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
							if v.Name == _G.Setting_table.Boss_Name and v.Humanoid.Health > 0 then
								game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("SetSpawnPoint")
								if v.Humanoid:FindFirstChild("Animator") then
									v.Humanoid.Animator:Destroy()
								end
								repeat wait(_G.Fast_Delay)
									EquipWeapon(_G.Setting_table.Weapon)
									TP(v.HumanoidRootPart.CFrame*CFrame.new(0,0,30))
									AttackNoCD()
								until v.Humanoid.Health <= 0 or not v.Parent or _G.Setting_table.Auto_Farm_Boss_Hop == false
								Mix_Farm = nil
								Auto_Farm_Boss_Ex = nil
								Ping = nil
							end
						end
					elseif game.ReplicatedStorage:FindFirstChild(_G.Setting_table.Boss_Name) then
						TP(game.ReplicatedStorage:FindFirstChild(_G.Setting_table.Boss_Name).HumanoidRootPart.CFrame*CFrame.new(0,30,0))
					end
				elseif Auto_Farm_Boss_Ex then
					Mix_Farm = nil
					Auto_Farm_Boss_Ex = nil
					Ping = nil
				else
					wait(5)
					if not game.Workspace.Enemies:FindFirstChild(_G.Setting_table.Boss_Name) and not game.ReplicatedStorage:FindFirstChild(_G.Setting_table.Boss_Name) then
						Hop_Boss()
						wait(1)
						print("....".._G.Setting_table.Boss_Name)
						wait(3)
						if not game.Workspace.Enemies:FindFirstChild(_G.Setting_table.Boss_Name) and not game.ReplicatedStorage:FindFirstChild(_G.Setting_table.Boss_Name) then
							HopServer()
							wait(50)
						end
					end
				end
			elseif Auto_Farm_Boss_Ex then
				Mix_Farm = nil
				Auto_Farm_Boss_Ex = nil
			else
				wait(3)
			end
		end)
	end
end)
FBss:AddToggle({
    Name = "Auto Farm All Boss",
    _G.Setting_table.Farm_All_Boss,
    Callback = function(vu)
	Auto_Farm_Boss_All = vu
	_G.Setting_table.Farm_All_Boss = vu
	Update_Setting(getgenv()['MyName'])
end})
function Hop_Boss()
	CheckBoss()
	for i,v in pairs(Boss_A) do
		for i2,v2 in pairs(_G.Setting_table.Boss_All_Select) do
			if v == v2 then
				print(v)
				_G.Setting_table.Boss_Name = v
				return 
			end
		end
	end
end
function H_B()
	CheckBoss()
	for i,v in pairs(Boss_A) do
		if type(v) == 'string' then
			print(v)
			_G.Setting_table.Boss_Name = v
			return
		end
	end
end
spawn(function()
	while wait() do
		pcall(function()
			if Auto_Farm_Boss_All then
				if not Mix_Farm or Auto_Farm_Boss_All_Ex then
					if Ping == nil then
						H_B()
						wait(1)
						print("....".._G.Setting_table.Boss_Name)
						Ping = true
					end
					if game.Workspace.Enemies:FindFirstChild(_G.Setting_table.Boss_Name) or game.ReplicatedStorage:FindFirstChild(_G.Setting_table.Boss_Name) then
						Mix_Farm = true
						Auto_Farm_Boss_All_Ex = true
						if game.Workspace.Enemies:FindFirstChild(_G.Setting_table.Boss_Name) then
							for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
								if v.Name == _G.Setting_table.Boss_Name and v.Humanoid.Health > 0 then
									game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("SetSpawnPoint")
									if v.Humanoid:FindFirstChild("Animator") then
										v.Humanoid.Animator:Destroy()
									end
									repeat wait(_G.Fast_Delay)
										EquipWeapon(_G.Setting_table.Weapon)
										TP(v.HumanoidRootPart.CFrame*CFrame.new(0,30,0))
									until v.Humanoid.Health <= 0 or not v.Parent or Auto_Farm_Boss_All == false
									Mix_Farm = nil
									Auto_Farm_Boss_All_Ex = nil
									Ping = nil
								end
							end
						elseif game.ReplicatedStorage:FindFirstChild(_G.Setting_table.Boss_Name) then
							TP(game.ReplicatedStorage:FindFirstChild(_G.Setting_table.Boss_Name).HumanoidRootPart.CFrame*CFrame.new(0,30,0))
						end
					elseif Auto_Farm_Boss_All_Ex then
						Mix_Farm = nil
						Auto_Farm_Boss_All_Ex = nil
						Ping = nil
					else
						Ping = nil
						wait(5)
					end
				end
			elseif _G.Setting_table.Auto_Farm_Boss_All_Hop then
				if not Mix_Farm or Auto_Farm_Boss_All_Ex then
					if Ping == nil then
						H_B()
						wait(1)
						print("....".._G.Setting_table.Boss_Name)
						Ping = true
					end
					if game.Workspace.Enemies:FindFirstChild(_G.Setting_table.Boss_Name) or game.ReplicatedStorage:FindFirstChild(_G.Setting_table.Boss_Name) then
						Mix_Farm = true
						Auto_Farm_Boss_All_Ex = true
						if game.Workspace.Enemies:FindFirstChild(_G.Setting_table.Boss_Name) then
							for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
								if v.Name == _G.Setting_table.Boss_Name and v.Humanoid.Health > 0 then
									game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("SetSpawnPoint")
									if v.Humanoid:FindFirstChild("Animator") then
										v.Humanoid.Animator:Destroy()
									end
									repeat wait(_G.Fast_Delay)
										EquipWeapon(_G.Setting_table.Weapon)
										TP(v.HumanoidRootPart.CFrame*CFrame.new(0,30,0))
										AttackNoCD()
									until v.Humanoid.Health <= 0 or not v.Parent or _G.Setting_table.Auto_Farm_Boss_All_Hop == false
									Mix_Farm = nil
									Auto_Farm_Boss_All_Ex = nil
									Ping = nil
								end
							end
						elseif game.ReplicatedStorage:FindFirstChild(_G.Setting_table.Boss_Name) then
							TP(game.ReplicatedStorage:FindFirstChild(_G.Setting_table.Boss_Name).HumanoidRootPart.CFrame*CFrame.new(0,30,0))
						end
					elseif Auto_Farm_Boss_All_Ex then
						Mix_Farm = nil
						Auto_Farm_Boss_All_Ex = nil
						Ping = nil
					else
						Ping = nil
						wait(5)
						if not game.Workspace.Enemies:FindFirstChild(_G.Setting_table.Boss_Name) and not game.ReplicatedStorage:FindFirstChild(_G.Setting_table.Boss_Name) then
							if Ping == nil then
								H_B()
								wait(1)
								print("....".._G.Setting_table.Boss_Name)
								Ping = true
							end
							wait(3)
							if not game.Workspace.Enemies:FindFirstChild(_G.Setting_table.Boss_Name) and not game.ReplicatedStorage:FindFirstChild(_G.Setting_table.Boss_Name) then
								HopServer()
								wait(50)
							end
						end
					end
				end
			elseif Auto_Farm_Boss_All_Ex then
				Mix_Farm = nil
				Auto_Farm_Boss_All_Ex = nil
				Ping = nil
			else
				wait(2)
			end
		end)
	end
end)

Boss_A = {}
function CheckBoss()
	for i,v in pairs(Boss_A) do
		table.remove(Boss_A,i)
	end
	for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
		if string.find(v.Name,"Boss") then
			table.insert(Boss_A,v.Name)
		end
	end
	for i,v in pairs(game.ReplicatedStorage:GetChildren()) do
		if string.find(v.Name,"Boss") then
			table.insert(Boss_A,v.Name)
		end
	end
end
Boss = {}
for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
	if string.find(v.Name,"Boss") then
		table.insert(Boss,v.Name)
	end
end
for i,v in pairs(game.ReplicatedStorage:GetChildren()) do
	if string.find(v.Name,"Boss") then
		table.insert(Boss,v.Name)
	end
end
if type(_G.Setting_table.Boss_Name) == 'string' then
else
	_G.Setting_table.Boss_Name = ""
end
Boss_List = {
	"Saber Expert [Lv. 200] [Boss]" ,
	"Thunder God [Lv. 575] [Boss]",
	"Diamond [Lv. 750] [Boss]",
	"Jeremy [Lv. 850] [Boss]",
	"Fajita [Lv. 925] [Boss]",
	"Don Swan [Lv. 1000] [Boss]",
	"Darkbeard [Lv. 1000] [Raid Boss]",
	"Tide Keeper [Lv. 1475] [Boss]",
	"Island Empress [Lv. 1675] [Boss]",
	"Captain Elephant [Lv. 1875] [Boss]",
	"rip_indra True Form [Lv. 5000] [Raid Boss]",
	"Longma [Lv. 2000] [Boss]",
	"Soul Reaper [Lv. 2100] [Raid Boss]",
	"Cake Queen [Lv. 2175] [Boss]"
}
local Select_BK = FBss:AddDropdown({
    Name = "Select Lock Boss",
    _G.Setting_table.Boss_Lock,Boss_List,
    List = Boss_List,
    Callback = function(vu)
	_G.Setting_table.Boss_Lock = vu
	Update_Setting(getgenv()['MyName'])
end})
local Select_B = FBss:AddDropdown({
    Name = "Select Boss",
    _G.Setting_table.Boss_Name,Boss,
    List = Boss,
    Callback = function(vu)
	_G.Setting_table.Boss_Name = vu
	Update_Setting(getgenv()['MyName'])
end})
FBss:AddButton({
    Name = "Refresh Boss",
    Callback = function(vu)
	Select_B:Clear()
	for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
		if string.find(v.Name,"Boss") then
			Select_B:Add(v.Name)
		end
	end
	for i,v in pairs(game.ReplicatedStorage:GetChildren()) do
		if string.find(v.Name,"Boss") then
			Select_B:Add(v.Name)
		end
	end
end})

MT = {
    " ",
    "Angel Wings",
    "Magma Ore",
    "Yati",
    "Scrap Metal",
    "Leader",
    "Vampire Fang",
    "Gunpowder",
    "Mini Tusk",
    "Radioactive Material",
    "Mystic Droplet",
    "Fish Tail",
    "Ectoplasm",
    "Conjured Cocao",
    "Candy",
    "Dragon Scale",
    "Demonic Wisp",
    "Meteorite",
    "Dark Fragment"
}

spawn(function()
   while wait() do
    if CFnow == 1 then
        CFnow = 2
        CT = CF
        wait(1)
        CT = CF2
    else
        CFnow = 1
        CT = CF
        wait(1)
        CT = CF2
       end
   end
end)

--[[local SMTS = Quest_Tab:CreateSection({Name = "Materias",Side = "Right"})
SMTS:AddToggle({
    Name = "Auto Farm",
    _G.Setting_table.Materia,
    Callback = function(vu)
	Auto_Materia = vu
	_G.Setting_table.Materia = vu
	Update_Setting(getgenv()['MyName'])
	if _G.Setting_table.Materia == "Angel Wings" then
	    Materia = "Royal Squad [Lv. 525]"
	    end
end})
SMTS:AddDropdown({
    Name = "Select Materias",
    _G.Setting_table.Materia,
    List = MT,
    Callback = function(vu)
	_G.Setting_table.Materia = vu
	Update_Setting(getgenv()['MyName'])
end})
spawn(function()
	while wait(.5) do
		pcall(function()
			if Auto_Materia then
				if not Mix_Farm then
					if game.Workspace.Enemies:FindFirstChild(Materia) or game.ReplicatedStorage:FindFirstChild(Materia) then
						if game.Workspace.Enemies:FindFirstChild(Materia) then
							game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("SetSpawnPoint")
							for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
								if v.Name == Materia and v.Humanoid.Health > 0 then
									_G.PosMon = v.HumanoidRootPart.CFrame
									StatrMagnet = true
									repeat wait(_G.Fast_Delay)
										EquipWeapon(_G.Setting_table.Weapon)
										TP(v.HumanoidRootPart.CFrame * CFrame.new(0, 30, 0))
										AttackNoCD()
									until v.Humanoid.Health <= 0 or not v.Parent or Mix_Farm or not Auto_Farm_Monster
									StatrMagnet = false
								end
							end
						elseif game.ReplicatedStorage:FindFirstChild(Materia) then
							TP(game.ReplicatedStorage:FindFirstChild(Materia).HumanoidRootPart.CFrame*CFrame.new(0,30,0))
						end
					end
				end
			else
				wait(2)
			end
		end)
	end
end)]]--
spawn(function()
	while wait(.5) do
		pcall(function()
				CheckStatus()
		end)
	end
end)

local CFrameCake = CFrame.new(-1990.672607421875, 4532.998046875, -14973.6748046875)

local CP = Quest_Tab:CreateSection({Name = "Cake Pirnce",Side = "Right"})
local Kill_Cake_Monster_ST = CP:AddLabel("Kill Cake Monster : 0/500")
local CAKESPAWN = CP:AddLabel("Cake Prince : 🔴")
CP:AddToggle({
    Name = "Auto Cake Prince",
    _G.Setting_table.Auto_Spikey_Trident,
    Callback = function(vu)
	Auto_Spikey_Trident = vu
	_G.Setting_table.Auto_Spikey_Trident = vu
	Update_Setting(getgenv()['MyName'])
end})


spawn(function()
	while wait(.5) do
		pcall(function()
			if Auto_Spikey_Trident then
				if not Mix_Farm or Auto_Spikey_Trident_Farm then
					if game.Workspace.Enemies:FindFirstChild("Cake Prince [Lv. 2300] [Raid Boss]") or game.ReplicatedStorage:FindFirstChild("Cake Prince [Lv. 2300] [Raid Boss]") then
						Auto_Spikey_Trident_Farm = true
						Mix_Farm = true
						if game.Workspace.Enemies:FindFirstChild("Cake Prince [Lv. 2300] [Raid Boss]") then
							game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("SetSpawnPoint")
							for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
								if v.Name == "Cake Prince [Lv. 2300] [Raid Boss]" and v.Humanoid.Health > 0 then
									if v.Humanoid:FindFirstChild("Animator") then
										v.Humanoid.Animator:Destroy()
									end
									repeat wait(_G.Fast_Delay)
										EquipWeapon(_G.Setting_table.Weapon)
										TP3(v.HumanoidRootPart.CFrame * Cethod)
										AttackNoCD()
									until v.Humanoid.Health <= 0 or not v.Parent or not Auto_Spikey_Trident
								end
							end
							
						elseif game.ReplicatedStorage:FindFirstChild("Cake Prince [Lv. 2300] [Raid Boss]") then
						    if Auto_Spikey_Trident and (CFrameCake.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 700 then
						game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-2149.209228515625, 80.00882720947266, -12402.974609375)
						    else
						    TP3(game.ReplicatedStorage:FindFirstChild("Cake Prince [Lv. 2300] [Raid Boss]").HumanoidRootPart.CFrame * Cethod)
						    end
					end
					elseif Auto_Spikey_Trident_Farm then
						Auto_Spikey_Trident_Farm = nil
						Mix_Farm = nil
					else
						if (Vector3.new(-2017.4874267578125, 36.85276412963867, -12027.53515625)-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 1200 then
							CFrameMon = CFrame.new(-2017.4874267578125, 36.85276412963867, -12027.53515625)
							for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
								if not string.find(v.Name,"Boss") and v.Humanoid.Health > 0 and (v.HumanoidRootPart.Position-CFrameMon.Position).Magnitude <= 1000 then
									if v.Humanoid:FindFirstChild("Animator") then
										v.Humanoid.Animator:Destroy()
									end
									_G.PosMon = v.HumanoidRootPart.CFrame
									StatrMagnet = true
									repeat wait(_G.Fast_Delay)
										EquipWeapon(_G.Setting_table.Weapon)
										TP3(v.HumanoidRootPart.CFrame * Cethod)
										AttackNoCD()
									until v.Humanoid.Health <= 0 or not v.Parent or not Auto_Spikey_Trident
									StatrMagnet = false
								end
							end
						else
							TP2(CFrame.new(-2017.4874267578125, 36.85276412963867, -12027.53515625))
						end
					end
				end
			else
				wait(2)
		end
		end)
	end
end)

-- 🔴
-- 🟢
local Status = Status_Tab:CreateSection("Status Quest")
local Check_Bile = IN:AddLabel("Your Bile : 0")
local Check_Frag = IN:AddLabel("Your Fragment : 0")
local YLV = IN:AddLabel("Your Level : 1")
local Bartlio_ST = Status:AddLabel("❌ : Quest Bartlio")
local Open_Don_Swan_ST = Status:AddLabel("❌ : Quest Open Don Swan")
local Observation_Haki_ST = Status:AddLabel("❌ : Quest Observation Haki")
local Observation_Haki_V2_ST = Status:AddLabel("❌ : Quest Observation Haki V2")
Status:AddLabel({Name = "Status Player"})
local YS = Status:AddLabel("SetSpawnPoint : ")
local DF = Status:AddLabel("Devil Fruit : ")
function CheckStatus()
	Kill_Elite_Hunter_ST:Set("Kill Elite Hunter : "..tostring(game.ReplicatedStorage.Remotes.CommF_:InvokeServer("EliteHunter","Progress")))
	local OP = game.ReplicatedStorage.Remotes.CommF_:InvokeServer("CakePrinceSpawner")
    local Lp = tonumber(string.match(tostring(OP), "%d+"))
	Kill_Cake_Monster_ST:Set("Kill Cake Monster : "..tostring(Lp).."/500")
	Check_Bile:Set("Your Bile : "..tostring(game:GetService("Players").LocalPlayer.Data.Beli.Value))
	Check_Frag:Set("Your Fragment : "..tostring(game:GetService("Players").LocalPlayer.Data.Fragments.Value))
	YS:Set("SetSpawnPoint : "..tostring(game:GetService("Players").LocalPlayer.Data.SpawnPoint.Value))
	DF:Set("Devil Fruit : "..tostring(game:GetService("Players").LocalPlayer.Data.DevilFruit.Value))
	YLV:Set("Your Level : "..tostring(game:GetService("Players").LocalPlayer.Data.Level.Value))
	if game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("TalkTrevor","1") == 0 then
		Open_Don_Swan_ST:Set("✅ : Open Don Swan Quest")
	end
	if game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BartiloQuestProgress","Bartilo") == 3 then
		Bartlio_ST:Set("✅ : Bartilo Quest") 
	end
	if game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("ProQuestProgress","SickMan") == 0 then
		Observation_Haki_ST:Set('✅ : Quest Observation Haki')
	end
	if game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("CitizenQuestProgress","Citizen") == 3 then
		Observation_Haki_V2_ST:Set('✅ : Quest Observation Haki V2')
	end
	if game.ReplicatedStorage:FindFirstChild("Cake Prince [Lv. 2300] [Raid Boss]") then
	    CAKESPAWN:Set("Cake Pirnce : ✅")
	    else
	    CAKESPAWN:Set("Cake Pirnce : ❌")
	end
    if game:GetService("ReplicatedStorage"):FindFirstChild("Urban [Lv. 1750]") then
        es:Set("Elite : ✅")
    elseif game:GetService("ReplicatedStorage"):FindFirstChild("Diablo [Lv. 1750]") then
        es:Set("Elite : ✅")
    elseif game:GetService("ReplicatedStorage"):FindFirstChild("Deandre [Lv. 1750]") then
        es:Set("Elite : ✅")
    else
        es:Set("Elite : ❌")
       end
	--[[for i,x in pairs(I_W) do
		v = {
			Name = x["Name"]
		}
		if v.Name == "Shisui" then
			ST_Shisui:Set("🟢 : Shisui")
		end
		if v.Name == "Wando" then
			ST_Wando:Set("🟢 : Wando")
		end
		if v.Name == "Saddi" then
			ST_Saddi:Set("🟢 : Saddi")
		end
	end
	for i,v in pairs(game.Players.LocalPlayer.Backpack:GetChildren()) do
		if v:IsA("Tool") then
			if v.Name == "Shisui" then
				ST_Shisui:Set("🟢 : Shisui")
			end
			if v.Name == "Wando" then
				ST_Wando:Set("🟢 : Wando")
			end
			if v.Name == "Saddi" then
				ST_Saddi:Set("🟢 : Saddi")
			end
		end
	end
	for i,v in pairs(game.Players.LocalPlayer.Character:GetChildren()) do
		if v:IsA("Tool") then
			if v.Name == "Shisui" then
				ST_Shisui:Set("🟢 : Shisui")
			end
			if v.Name == "Wando" then
				ST_Wando:Set("🟢 : Wando")
			end
			if v.Name == "Saddi" then
				ST_Saddi:Set("🟢 : Saddi")
			end
		end
	end]]--
end
CheckStatus()


--[[General_Tab:Label("Farm Monster")
General_Tab:Toggle("Auto Farm","9606294253",_G.Setting_table.Auto_Farm_Monster,function(vu)
	Auto_Farm_Monster = vu
	_G.Setting_table.Auto_Farm_Monster = vu
	Update_Setting(getgenv()['MyName'])
end)



spawn(function()
	while wait(.5) do
		pcall(function()
			if Auto_Farm_Monster then
				if not Mix_Farm then
					if game.Workspace.Enemies:FindFirstChild(_G.Setting_table.Mon_Name) or game.ReplicatedStorage:FindFirstChild(_G.Setting_table.Mon_Name) then
						if game.Workspace.Enemies:FindFirstChild(_G.Setting_table.Mon_Name) then
							game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("SetSpawnPoint")
							for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
								if v.Name == _G.Setting_table.Mon_Name and v.Humanoid.Health > 0 then
									_G.PosMon = v.HumanoidRootPart.CFrame
									StatrMagnet = true
									repeat wait(_G.Fast_Delay)
										EquipWeapon(_G.Setting_table.Weapon)
										TP(v.HumanoidRootPart.CFrame * CFrame.new(0, 30, 0))
										AttackNoCD()
									until v.Humanoid.Health <= 0 or not v.Parent or Mix_Farm or not Auto_Farm_Monster
									StatrMagnet = false
								end
							end
						elseif game.ReplicatedStorage:FindFirstChild(_G.Setting_table.Mon_Name) then
							TP(game.ReplicatedStorage:FindFirstChild(_G.Setting_table.Mon_Name).HumanoidRootPart.CFrame*CFrame.new(0,30,0))
						end
					end
				end
			else
				wait(2)
			end
		end)
	end
end)
local Mons = {}
local xx = {}

for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
    if string.find(v.Name , "Lv.") then
        table.insert(xx, v.Name)
    end
end

for i,v in pairs(game:GetService("ReplicatedStorage"):GetChildren()) do
    if string.find(v.Name , "Lv.") then
        table.insert(xx, v.Name)
    end
end

table.sort(xx)
local result = {}

for key,value in ipairs(xx) do
    if value ~=xx[key+1] then
        table.insert(result,value)
    end
end
for key,value in ipairs(result) do
    table.insert(Mons, value)
end
local Select_M = General_Tab:Dropdown("Select Monster",_G.Setting_table.Mon_Name,Mons,function(vu)
	_G.Setting_table.Mon_Name = vu
	Update_Setting(getgenv()['MyName'])
end)
General_Tab:Button("Refresh Monster",function(vu)
	Select_M:Clear()
	local xx = {}

	for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
		if string.find(v.Name , "Lv.") then
			table.insert(xx, v.Name)
		end
	end

	for i,v in pairs(game:GetService("ReplicatedStorage"):GetChildren()) do
		if string.find(v.Name , "Lv.") then
			table.insert(xx, v.Name)
		end
	end

	table.sort(xx)
	local result = {}

	for key,value in ipairs(xx) do
		if value ~=xx[key+1] then
			table.insert(result,value)
		end
	end
	for key,value in ipairs(result) do
		Select_M:Add(value)
	end
end)]]--

local FarmM = Quest_Tab:CreateSection("Farm Mastery")
FarmM:AddToggle({
    Name = "Auto Farm Fruit",
    _G.Setting_table.Farm_Fruit,
    Callback = function(vu)
	Auto_Farm_Fruit = vu
	_G.Setting_table.Farm_Fruit = vu
	Update_Setting(getgenv()['MyName'])
end})
if _G.Setting_table.MinHealth == nil then
	_G.Setting_table.MinHealth = 20
end

FarmM:AddToggle({
    Name = "Auto Farm Gun",
    _G.Setting_table.Farm_Gun,
    Callback = function(vu)
	Auto_Farm_Gun = vu
	_G.Setting_table.Farm_Gun = vu
	Update_Setting(getgenv()['MyName'])
end})

FarmM:Slider({
    Name = "Health %",
    Value = 25,
    Min = 1,
    Max = 100,
    _G.Setting_table.MinHealth,
    Callback = function(vu)
	MinHealth = vu
	_G.Setting_table.MinHealth = vu
	Update_Setting(getgenv()['MyName'])
end})
spawn(function()
	while wait(.5) do
		pcall(function()
			if Auto_Farm_Fruit then
				if not Mix_Farm then
					if game.Players.LocalPlayer.PlayerGui.Main.Quest.Visible == false then
						CheckLevel()
						if (CFrameQ.Position-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 1000000 then
                        else
                            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StartQuest", NameQuest, QuestLv)
                            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("SetSpawnPoint")
                        end
					elseif game.Players.LocalPlayer.PlayerGui.Main.Quest.Visible == true then
						CheckLevel()
						TP(CFrameQ)
						if string.find(game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text, NameMon) then
							if game.Workspace.Enemies:FindFirstChild(Ms) then
								for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
									if not string.find(v.Name,"Boss") and v.Humanoid.Health > 0 and (v.HumanoidRootPart.Position-CFrameMon.Position).Magnitude <= 1000 then
										_G.PosMon = v.HumanoidRootPart.CFrame
										StatrMagnet = true
										repeat wait(.2)
											local health = v.Humanoid.Health
											local maxhealth = v.Humanoid.MaxHealth
											local percent = (health / maxhealth) * 100
											if percent <= MinHealth then
												EquipWeapon(game.Players.LocalPlayer.Data.DevilFruit.Value)
												TP(v.HumanoidRootPart.CFrame * CFrame.new(0, 30, 1))
												PositionSkillMasteryDevilFruit = v.HumanoidRootPart.Position
												UseSkillMasteryDevilFruit = true
												FastAttack = true
												if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Dragon-Dragon") then
													if SkillZ  and v.Humanoid.Health > 0 then
														game:service('VirtualInputManager'):SendKeyEvent(true, "Z", false, game)
														wait(.1)
														game:service('VirtualInputManager'):SendKeyEvent(false, "Z", false, game)
													end
													if SkillX  and v.Humanoid.Health > 0 then
														game:service('VirtualInputManager'):SendKeyEvent(true, "X", false, game)
														wait(.1)
														game:service('VirtualInputManager'):SendKeyEvent(false, "X", false, game)
													end   
												elseif game:GetService("Players").LocalPlayer.Character:FindFirstChild("Human-Human: Buddha") then
													if SkillZ  and v.Humanoid.Health > 0 and game.Players.LocalPlayer.Character.HumanoidRootPart.Size == Vector3.new(7.6, 7.676, 3.686) then
													else
														game:service('VirtualInputManager'):SendKeyEvent(true, "Z", false, game)
														wait(.1)
														game:service('VirtualInputManager'):SendKeyEvent(false, "Z", false, game)
													end
													if SkillX  and v.Humanoid.Health > 0 then
														game:service('VirtualInputManager'):SendKeyEvent(true, "X", false, game)
														wait(.1)
														game:service('VirtualInputManager'):SendKeyEvent(false, "X", false, game)
													end
													if SkillC  and v.Humanoid.Health > 0 then
														game:service('VirtualInputManager'):SendKeyEvent(true, "C", false, game)
														wait(.1)
														game:service('VirtualInputManager'):SendKeyEvent(false, "C", false, game)
													end  
												elseif game:GetService("Players").LocalPlayer.Character:FindFirstChild(game.Players.LocalPlayer.Data.DevilFruit.Value) then
													game:GetService("Players").LocalPlayer.Character:FindFirstChild(game.Players.LocalPlayer.Data.DevilFruit.Value).MousePos.Value = v.HumanoidRootPart.Position
													if SkillZ  and v.Humanoid.Health > 0 then
														game:service('VirtualInputManager'):SendKeyEvent(true, "Z", false, game)
														wait(.1)
														game:service('VirtualInputManager'):SendKeyEvent(false, "Z", false, game)
													end
													if SkillX  and v.Humanoid.Health > 0 then
														game:service('VirtualInputManager'):SendKeyEvent(true, "X", false, game)
														wait(.1)
														game:service('VirtualInputManager'):SendKeyEvent(false, "X", false, game)
													end
													if SkillC  and v.Humanoid.Health > 0 then
														game:service('VirtualInputManager'):SendKeyEvent(true, "C", false, game)
														wait(.1)
														game:service('VirtualInputManager'):SendKeyEvent(false, "C", false, game)
													end
													if SkillV  and v.Humanoid.Health > 0 then
														game:service('VirtualInputManager'):SendKeyEvent(true, "V", false, game)
														wait(.1)
														game:service('VirtualInputManager'):SendKeyEvent(false, "V", false, game)
													end
												end
											elseif percent > MinHealth and v.Humanoid.Health > 0 then
												if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Human-Human: Buddha") then
													if game.Players.LocalPlayer.Character.HumanoidRootPart.Size.Y >= 6 then
														game:service('VirtualInputManager'):SendKeyEvent(true, "Z", false, game)
														wait(.1)
														game:service('VirtualInputManager'):SendKeyEvent(false, "Z", false, game)
													end
												end
												UseSkillMasteryDevilFruit = false
												EquipWeapon(_G.Setting_table.Weapon)
												TP(v.HumanoidRootPart.CFrame * CFrame.new(0, 30, 1))
												local health = v.Humanoid.Health
												local maxhealth = v.Humanoid.MaxHealth
												local percent = (health / maxhealth) * 100
												if percent > MinHealth and v.Humanoid.Health > 0 then
													game:GetService'VirtualUser':Button1Down(Vector2.new(1280,600))
												else
													EquipWeapon(game.Players.LocalPlayer.Data.DevilFruit.Value)
													wait(1)
												end
											end
										until v.Humanoid.Health <= 0 or not v.Parent or Mix_Farm or not Auto_Farm_Fruit
										StatrMagnet = false
									end
								end
							elseif game.ReplicatedStorage:FindFirstChild(Ms) then
								TP(CFrameMon)
							else
								for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
									if not string.find(v.Name,"Boss") and v.Humanoid.Health > 0 and (v.HumanoidRootPart.Position-CFrameMon.Position).Magnitude <= 1000 then
										_G.PosMon = v.HumanoidRootPart.CFrame
										StatrMagnet = true
										repeat wait(.2)
											local MinHealth = 17
											local health = v.Humanoid.Health
											local maxhealth = v.Humanoid.MaxHealth
											local percent = (health / maxhealth) * 100
											if percent <= MinHealth then
												EquipWeapon(game.Players.LocalPlayer.Data.DevilFruit.Value)
												TP(v.HumanoidRootPart.CFrame * CFrame.new(0, 30, 1))
												PositionSkillMasteryDevilFruit = v.HumanoidRootPart.Position
												UseSkillMasteryDevilFruit = true
												if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Dragon-Dragon") then
													if SkillZ  and v.Humanoid.Health > 0 then
														game:service('VirtualInputManager'):SendKeyEvent(true, "Z", false, game)
														wait(.1)
														game:service('VirtualInputManager'):SendKeyEvent(false, "Z", false, game)
													end
													if SkillX  and v.Humanoid.Health > 0 then
														game:service('VirtualInputManager'):SendKeyEvent(true, "X", false, game)
														wait(.1)
														game:service('VirtualInputManager'):SendKeyEvent(false, "X", false, game)
													end   
												elseif game:GetService("Players").LocalPlayer.Character:FindFirstChild("Human-Human: Buddha") then
													if SkillZ  and v.Humanoid.Health > 0 and game.Players.LocalPlayer.Character.HumanoidRootPart.Size == Vector3.new(7.6, 7.676, 3.686) then
													else
														game:service('VirtualInputManager'):SendKeyEvent(true, "Z", false, game)
														wait(.1)
														game:service('VirtualInputManager'):SendKeyEvent(false, "Z", false, game)
													end
													if SkillX  and v.Humanoid.Health > 0 then
														game:service('VirtualInputManager'):SendKeyEvent(true, "X", false, game)
														wait(.1)
														game:service('VirtualInputManager'):SendKeyEvent(false, "X", false, game)
													end
													if SkillC  and v.Humanoid.Health > 0 then
														game:service('VirtualInputManager'):SendKeyEvent(true, "C", false, game)
														wait(.1)
														game:service('VirtualInputManager'):SendKeyEvent(false, "C", false, game)
													end  
												elseif game:GetService("Players").LocalPlayer.Character:FindFirstChild(game.Players.LocalPlayer.Data.DevilFruit.Value) then
													game:GetService("Players").LocalPlayer.Character:FindFirstChild(game.Players.LocalPlayer.Data.DevilFruit.Value).MousePos.Value = v.HumanoidRootPart.Position
													if SkillZ  and v.Humanoid.Health > 0 then
														game:service('VirtualInputManager'):SendKeyEvent(true, "Z", false, game)
														wait(.1)
														game:service('VirtualInputManager'):SendKeyEvent(false, "Z", false, game)
													end
													if SkillX  and v.Humanoid.Health > 0 then
														game:service('VirtualInputManager'):SendKeyEvent(true, "X", false, game)
														wait(.1)
														game:service('VirtualInputManager'):SendKeyEvent(false, "X", false, game)
													end
													if SkillC  and v.Humanoid.Health > 0 then
														game:service('VirtualInputManager'):SendKeyEvent(true, "C", false, game)
														wait(.1)
														game:service('VirtualInputManager'):SendKeyEvent(false, "C", false, game)
													end
													if SkillV  and v.Humanoid.Health > 0 then
														game:service('VirtualInputManager'):SendKeyEvent(true, "V", false, game)
														wait(.1)
														game:service('VirtualInputManager'):SendKeyEvent(false, "V", false, game)
													end
												end
											elseif percent > MinHealth and v.Humanoid.Health > 0 then
												if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Human-Human: Buddha") then
													if SkillZ  and v.Humanoid.Health > 0 and game.Players.LocalPlayer.Character.HumanoidRootPart.Size == Vector3.new(7.6, 7.676, 3.686) then
														game:service('VirtualInputManager'):SendKeyEvent(true, "Z", false, game)
														wait(.1)
														game:service('VirtualInputManager'):SendKeyEvent(false, "Z", false, game)
													end
												end
												UseSkillMasteryDevilFruit = false
												EquipWeapon(_G.Setting_table.Weapon)
												TP(v.HumanoidRootPart.CFrame * CFrame.new(0, 30, 1))
												local health = v.Humanoid.Health
												local maxhealth = v.Humanoid.MaxHealth
												local percent = (health / maxhealth) * 100
												if percent > MinHealth and v.Humanoid.Health > 0 then
													game:GetService'VirtualUser':Button1Down(Vector2.new(1280,600))
												else
													EquipWeapon(game.Players.LocalPlayer.Data.DevilFruit.Value)
													wait(1)
												end
											end
										until v.Humanoid.Health <= 0 or not v.Parent or Mix_Farm or not Auto_Farm_Fruit
										StatrMagnet = false
									end
								end
							end
						end
					end
				end
			end
		end)
	end
end)

spawn(function()
	while wait(.5) do
		pcall(function()
			if game.Players.LocalPlayer.Character.Humanoid.Health <= 0 or not game.Players.LocalPlayer then
				_G.Stop_Tween = true
				wait(3)
				_G.Stop_Tween = nil
			end
		end)
	end
end)

spawn(function()
	while wait(.5) do
		pcall(function()
			if Auto_Farm_Gun then
				if not Mix_Farm then
					if game.Players.LocalPlayer.PlayerGui.Main.Quest.Visible == false then
						CheckLevel()
						if (CFrameQ.Position-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 10 then
                            TP(CFrameQ)
                        else
                            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StartQuest", NameQuest, QuestLv)
                            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("SetSpawnPoint")
                        end
					elseif game.Players.LocalPlayer.PlayerGui.Main.Quest.Visible == true then
						CheckLevel()
						if string.find(game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text, NameMon) then
							if game.Workspace.Enemies:FindFirstChild(Ms) then
								for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
									if not string.find(v.Name,"Boss") and v.Humanoid.Health > 0 and (v.HumanoidRootPart.Position-CFrameMon.Position).Magnitude <= 1000 then
										for i2,v2 in pairs(game.Players.LocalPlayer.Backpack:GetChildren()) do
											if v2:IsA("Tool") then
												if tostring(v2.ToolTip) == "Gun" then
													SelectToolWeaponGun = v2.Name
												end
											end
										end
										_G.PosMon = v.HumanoidRootPart.CFrame
										_G.Mon = v
										StatrMagnet = true
										repeat wait(.2)
											local MinHealth = 17
											local health = v.Humanoid.Health
											local maxhealth = v.Humanoid.MaxHealth
											local percent = (health / maxhealth) * 100
											if percent <= MinHealth then
												EquipWeapon(SelectToolWeaponGun)
												TP(v.HumanoidRootPart.CFrame * CFrame.new(0, 30, 1))
												_G.Mon = v
												game:GetService("Players").LocalPlayer.Character:FindFirstChild(SelectToolWeaponGun).MousePos.Value = v.HumanoidRootPart.Position
												PositionSkillMasteryDevilFruit = v.HumanoidRootPart.Position
												game:GetService'VirtualUser':Button1Down(Vector2.new(1280,600))
												Aimbot_G = true
												game:GetService'VirtualUser':Button1Down(Vector2.new(1280,600))
												UseSkillMasteryDevilFruit = true
												if SkillZ  and v.Humanoid.Health > 0 then
													game:service('VirtualInputManager'):SendKeyEvent(true, "Z", false, game)
													wait(.1)
													game:service('VirtualInputManager'):SendKeyEvent(false, "Z", false, game)
												end
												if SkillX  and v.Humanoid.Health > 0 then
													game:service('VirtualInputManager'):SendKeyEvent(true, "X", false, game)
													wait(.1)
													game:service('VirtualInputManager'):SendKeyEvent(false, "X", false, game)
												end
											elseif percent > MinHealth and v.Humanoid.Health > 0 then
												UseSkillMasteryDevilFruit = false
												EquipWeapon(_G.Setting_table.Weapon)
												TP(v.HumanoidRootPart.CFrame * CFrame.new(0, 30, 1))
												local health = v.Humanoid.Health
												local maxhealth = v.Humanoid.MaxHealth
												local percent = (health / maxhealth) * 100
												if percent > MinHealth and v.Humanoid.Health > 0 then
													game:GetService'VirtualUser':Button1Down(Vector2.new(1280,600))
												else
													EquipWeapon(game.Players.LocalPlayer.Data.DevilFruit.Value)
													wait(1)
												end
											end
										until v.Humanoid.Health <= 0 or not v.Parent or Mix_Farm or not Auto_Farm_Gun
										StatrMagnet = false
									end
								end
							elseif game.ReplicatedStorage:FindFirstChild(Ms) then
								TP(CFrameMon)
							else
								for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
									if not string.find(v.Name,"Boss") and v.Humanoid.Health > 0 and (v.HumanoidRootPart.Position-CFrameMon.Position).Magnitude <= 1000 then
										for i2,v2 in pairs(game.Players.LocalPlayer.Backpack:GetChildren()) do
											if v2:IsA("Tool") then
												if tostring(v2.ToolTip) == "Gun" then
													SelectToolWeaponGun = v2.Name
												end
											end
										end
										_G.PosMon = v.HumanoidRootPart.CFrame
										_G.Mon = v
										StatrMagnet = true
										repeat wait(.2)
											local MinHealth = 17
											local health = v.Humanoid.Health
											local maxhealth = v.Humanoid.MaxHealth
											local percent = (health / maxhealth) * 100
											if percent <= MinHealth then
												EquipWeapon(SelectToolWeaponGun)
												TP(v.HumanoidRootPart.CFrame * CFrame.new(0, 30, 1))
												_G.Mon = v.Name
												game:GetService("Players").LocalPlayer.Character:FindFirstChild(SelectToolWeaponGun).MousePos.Value = v.HumanoidRootPart.Position
												game:GetService'VirtualUser':Button1Down(Vector2.new(9,9))
												game:GetService("Players").LocalPlayer.Character:FindFirstChild(SelectToolWeaponGun).MousePos.Value = v.HumanoidRootPart.Position
												PositionSkillMasteryDevilFruit = v.HumanoidRootPart.Position
												UseSkillMasteryDevilFruit = true
												if SkillZ  and v.Humanoid.Health > 0 then
													game:service('VirtualInputManager'):SendKeyEvent(true, "Z", false, game)
													wait(.1)
													game:service('VirtualInputManager'):SendKeyEvent(false, "Z", false, game)
												end
												if SkillX  and v.Humanoid.Health > 0 then
													game:service('VirtualInputManager'):SendKeyEvent(true, "X", false, game)
													wait(.1)
													game:service('VirtualInputManager'):SendKeyEvent(false, "X", false, game)
												end
											elseif percent > MinHealth and v.Humanoid.Health > 0 then
												UseSkillMasteryDevilFruit = false
												EquipWeapon(_G.Setting_table.Weapon)
												TP(v.HumanoidRootPart.CFrame * CFrame.new(0, 30, 1))
												local health = v.Humanoid.Health
												local maxhealth = v.Humanoid.MaxHealth
												local percent = (health / maxhealth) * 100
												if percent > MinHealth and v.Humanoid.Health > 0 then
													game:GetService'VirtualUser':Button1Down(Vector2.new(1280,600))
												else
													EquipWeapon(game.Players.LocalPlayer.Data.DevilFruit.Value)
													wait(1)
												end
											end
										until v.Humanoid.Health <= 0 or not v.Parent or Mix_Farm or not Auto_Farm_Gun
										StatrMagnet = false
									end
								end
							end
						end
					end
				end
			end
		end)
	end
end)
local lp = game:GetService('Players').LocalPlayer
local mouse = lp:GetMouse()
mouse.Button1Down:Connect(function()
    if SelectToolWeaponGun ~= nil then
        if game:GetService("Players").LocalPlayer.Character:FindFirstChild(SelectToolWeaponGun) and game:GetService("Players").LocalPlayer.Character:FindFirstChild(SelectToolWeaponGun):FindFirstChild("RemoteFunctionShoot") then
            tool = game:GetService("Players").LocalPlayer.Character[SelectToolWeaponGun]
            v17 = workspace:FindPartOnRayWithIgnoreList(Ray.new(tool.Handle.CFrame.p, (_G.Mon.HumanoidRootPart.Position - tool.Handle.CFrame.p).unit * 100), { game.Players.LocalPlayer.Character, workspace._WorldOrigin });
            game:GetService("Players").LocalPlayer.Character:FindFirstChild(SelectToolWeaponGun).RemoteFunctionShoot:InvokeServer(_G.Mon.HumanoidRootPart.Position, (ReplicatedStorage_Util.Other.hrpFromPart(v17)));
        end
    end
end)
FarmM:AddLabel({
    Name = "Setting"
})
FarmM:AddToggle({
    Name = "Skill Z",
    _G.Setting_table.Skill_Z,
    Callback = function(vu)
	SkillZ = vu
	_G.Setting_table.Skill_Z = vu
	Update_Setting(getgenv()['MyName'])
end})
FarmM:AddToggle({
    Name = "Skill X",
    _G.Setting_table.Skill_X,
    Callback = function(vu)
	SkillX = vu
	_G.Setting_table.Skill_Z = vu
	Update_Setting(getgenv()['MyName'])
end})
FarmM:AddToggle({
    Name = "Skill C",
    _G.Setting_table.Skill_C,
    Callback = function(vu)
	SkillC = vu
	_G.Setting_table.Skill_Z = vu
	Update_Setting(getgenv()['MyName'])
end})
FarmM:AddToggle({
    Name = "Skill V",
    _G.Setting_table.Skill_V,
    Callback = function(vu)
	SkillV = vu
	_G.Setting_table.Skill_Z = vu
	Update_Setting(getgenv()['MyName'])
end})
FarmM:AddToggle({
    Name = "Auto Farm Melee",
    _G.Setting_table.Farm_Melee,
    Callback = function(vu)
	Auto_Farm_Melee = vu
	_G.Setting_table.Farm_Melee = vu
	Update_Setting(getgenv()['MyName'])
end})
spawn(function()
	while wait(.2) do
		pcall(function()
			if Auto_Farm_Melee then
				if not Mix_Farm then
					if game.Players.LocalPlayer.PlayerGui.Main.Quest.Visible == false then
						CheckLevel()
						if (CFrameQ.Position-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 10 then
                            TP(CFrameQ)
                        else
                            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StartQuest", NameQuest, QuestLv)
                            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("SetSpawnPoint")
                        end
					elseif game.Players.LocalPlayer.PlayerGui.Main.Quest.Visible == true then
						CheckLevel()
						if string.find(game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text, NameMon) then
							if game.Workspace.Enemies:FindFirstChild(Ms) then
								for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
									if not string.find(v.Name,"Boss") and v.Humanoid.Health > 0 and (v.HumanoidRootPart.Position-CFrameMon.Position).Magnitude <= 1000 then
										if v.Humanoid:FindFirstChild("Animator") then
											v.Humanoid.Animator:Destroy()
										end
										for i2,v2 in pairs(game.Players.LocalPlayer.Backpack:GetChildren()) do
											if v2:IsA("Tool") then
												if tostring(v2.ToolTip) == "Melee" then
													_G.Setting_table.Weapon = v2.Name
												end
											end
										end
										_G.PosMon = v.HumanoidRootPart.CFrame
										StatrMagnet = true
										repeat wait(_G.Fast_Delay)
											EquipWeapon(_G.Setting_table.Weapon)
											TP(v.HumanoidRootPart.CFrame * CFrame.new(0, 30, 1))
											AttackNoCD()
										until v.Humanoid.Health <= 0 or not v.Parent or Mix_Farm or not Auto_Farm_Melee
										StatrMagnet = false
									end
								end
							elseif game.ReplicatedStorage:FindFirstChild(Ms) then
								TP(CFrameMon)
							else
								for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
									if not string.find(v.Name,"Boss") and v.Humanoid.Health > 0 and (v.HumanoidRootPart.Position-CFrameMon.Position).Magnitude <= 1000 then
										if v.Humanoid:FindFirstChild("Animator") then
											v.Humanoid.Animator:Destroy()
										end
										for i2,v2 in pairs(game.Players.LocalPlayer.Backpack:GetChildren()) do
											if v2:IsA("Tool") then
												if tostring(v2.ToolTip) == "Melee" then
													_G.Setting_table.Weapon = v2.Name
												end
											end
										end
										_G.PosMon = v.HumanoidRootPart.CFrame
										StatrMagnet = true
										repeat wait(_G.Fast_Delay)
											EquipWeapon(_G.Setting_table.Weapon)
											TP(v.HumanoidRootPart.CFrame * CFrame.new(0, 30, 1))
											AttackNoCD()
										until v.Humanoid.Health <= 0 or not v.Parent or Mix_Farm or not Auto_Farm_Melee
										StatrMagnet = false
									end
								end
							end
						end
					end
				end
			end
		end)
	end
end)
FarmM:AddLabel("Farm Sword")
FarmM:AddToggle({
    Name = "Auto Farm Sword",
    _G.Setting_table.Farm_Sword,
    Callback = function(vu)
	Auto_Farm_Sword = vu
	_G.Setting_table.Farm_Sword = vu
	Update_Setting(getgenv()['MyName'])
end})
spawn(function()
	while wait(.2) do
		pcall(function()
			if Auto_Farm_Sword then
				if not Mix_Farm then
					if game.Players.LocalPlayer.PlayerGui.Main.Quest.Visible == false then
						CheckLevel()
						if (CFrameQ.Position-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 10 then
                            TP(CFrameQ)
                        else
                            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StartQuest", NameQuest, QuestLv)
                            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("SetSpawnPoint")
                        end
					elseif game.Players.LocalPlayer.PlayerGui.Main.Quest.Visible == true then
						CheckLevel()
						if string.find(game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text, NameMon) then
							if game.Workspace.Enemies:FindFirstChild(Ms) then
								for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
									if not string.find(v.Name,"Boss") and v.Humanoid.Health > 0 and (v.HumanoidRootPart.Position-CFrameMon.Position).Magnitude <= 1000 then
										if v.Humanoid:FindFirstChild("Animator") then
											v.Humanoid.Animator:Destroy()
										end
										for i2,v2 in pairs(game.Players.LocalPlayer.Backpack:GetChildren()) do
											if v2:IsA("Tool") then
												if tostring(v2.ToolTip) == "Sword" then
													_G.Setting_table.Weapon = v2.Name
												end
											end
										end
										_G.PosMon = v.HumanoidRootPart.CFrame
										StatrMagnet = true
										repeat wait(_G.Fast_Delay)
											EquipWeapon(_G.Setting_table.Weapon)
											TP(v.HumanoidRootPart.CFrame * CFrame.new(0, 30, 1))
											AttackNoCD()
										until v.Humanoid.Health <= 0 or not v.Parent or Mix_Farm or not Auto_Farm_Sword
										StatrMagnet = false
									end
								end
							elseif game.ReplicatedStorage:FindFirstChild(Ms) then
								TP(CFrameMon)
							else
								for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
									if not string.find(v.Name,"Boss") and v.Humanoid.Health > 0 and (v.HumanoidRootPart.Position-CFrameMon.Position).Magnitude <= 1000 then
										if v.Humanoid:FindFirstChild("Animator") then
											v.Humanoid.Animator:Destroy()
										end
										for i2,v2 in pairs(game.Players.LocalPlayer.Backpack:GetChildren()) do
											if v2:IsA("Tool") then
												if tostring(v2.ToolTip) == "Sword" then
													_G.Setting_table.Weapon = v2.Name
												end
											end
										end
										_G.PosMon = v.HumanoidRootPart.CFrame
										StatrMagnet = true
										repeat wait(_G.Fast_Delay)
											EquipWeapon(_G.Setting_table.Weapon)
											TP(v.HumanoidRootPart.CFrame * CFrame.new(0, 30, 1))
											AttackNoCD()
										until v.Humanoid.Health <= 0 or not v.Parent or Mix_Farm or not Auto_Farm_Sword
										StatrMagnet = false
									end
								end
							end
						end
					end
				end
			end
		end)
	end
end)

local FO = Quest_Tab:CreateSection({Name = "Auto Observation",Side = "Right"})
FO:AddLabel('Observation Haki')
FO:Toggle({
    Name = "Auto Farm Observation Haki",
    _G.Setting_table.Farm_Ken,
    Callback = function(vu)
	Farm_Ken = vu
	_G.Setting_table.Farm_Ken = vu
	Update_Setting(getgenv()['MyName'])
end})
spawn(function()
	while wait(.5) do
		pcall(function()
			if Farm_Ken then
				if not Mix_Farm then
					if game.Players.LocalPlayer.PlayerGui.Main.Quest.Visible == false then
						CheckLevel()
						if (CFrameQ.Position-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 10 then
                            TP(CFrameQ)
                        else
                            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StartQuest", NameQuest, QuestLv)
                            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("SetSpawnPoint")
                        end
					elseif game.Players.LocalPlayer.PlayerGui.Main.Quest.Visible == true then
						CheckLevel()
						if string.find(game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text, NameMon) then
							if game.Workspace.Enemies:FindFirstChild(Ms) then
								for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
									if not string.find(v.Name,"Boss") and v.Humanoid.Health > 0 and (v.HumanoidRootPart.Position-CFrameMon.Position).Magnitude <= 1000 then
										if v.Humanoid:FindFirstChild("Animator") then
											v.Humanoid.Animator:Destroy()
										end
										_G.PosMon = v.HumanoidRootPart.CFrame
										spawn(function()
											repeat wait(1)
												if (v.HumanoidRootPart.Position-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 7 then
													wait(7)
													if game.Players.LocalPlayer.Character.Humanoid.Health == game.Players.LocalPlayer.Character.Humanoid.MaxHealth then
														_G.IKAI = true
														--break
													end
												end
											until _G.IKAI == true or StatrMagnet
										end)
										repeat wait(.2)
											local health = game.Players.LocalPlayer.Character.Humanoid.Health
											local maxhealth = game.Players.LocalPlayer.Character.Humanoid.MaxHealth
											local percent = (health / maxhealth) * 100
											if percent >= 90 then
												TP(v.HumanoidRootPart.CFrame*CFrame.new(0,0,2))
											else
												TP(v.HumanoidRootPart.CFrame*CFrame.new(0,30,0))
											end
										until _G.IKAI or percent < 90 or v.Humanoid.Health <= 0 or not v.Parent or Mix_Farm or not Farm_Ken
										TP(v.HumanoidRootPart.CFrame*CFrame.new(0,30,0))
										_G.IKAI = false
										StatrMagnet = true
										repeat wait(_G.Fast_Delay)
											TP(v.HumanoidRootPart.CFrame*CFrame.new(0,30,0))
											EquipWeapon(_G.Setting_table.Weapon)
											AttackNoCD()
										until v.Humanoid.Health <= 0 or not v.Parent or Mix_Farm or not Farm_Ken 
										StatrMagnet = false
									end
								end
							elseif game.ReplicatedStorage:FindFirstChild(Ms) then
								TP(game.ReplicatedStorage:FindFirstChild(Ms).HumanoidRootPart.CFrame*CFrame.new(0,30,0))
							else
								for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
									if not string.find(v.Name,"Boss") and v.Humanoid.Health > 0 and (v.HumanoidRootPart.Position-CFrameMon.Position).Magnitude <= 1000 then
										if v.Humanoid:FindFirstChild("Animator") then
											v.Humanoid.Animator:Destroy()
										end
										_G.PosMon = v.HumanoidRootPart.CFrame
										StatrMagnet = false
										spawn(function()
											repeat wait(1)
												if (v.HumanoidRootPart.Position-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 7 then
													wait(7)
													if game.Players.LocalPlayer.Character.Humanoid.Health == game.Players.LocalPlayer.Character.Humanoid.MaxHealth then
														_G.IKAI = true
														--break
													end
												end
											until _G.IKAI == true or StatrMagnet
										end)
										repeat wait(.2)
											local health = game.Players.LocalPlayer.Character.Humanoid.Health
											local maxhealth = game.Players.LocalPlayer.Character.Humanoid.MaxHealth
											local percent = (health / maxhealth) * 100
											if percent >= 90 then
												TP(v.HumanoidRootPart.CFrame*CFrame.new(0,0,2))
											else
												TP(v.HumanoidRootPart.CFrame*CFrame.new(0,30,0))
											end
										until _G.IKAI or percent < 90 or v.Humanoid.Health <= 0 or not v.Parent or Mix_Farm or not _G.Setting_table.Farm_Ken_Hop
										TP(v.HumanoidRootPart.CFrame*CFrame.new(0,30,0))
										_G.IKAI = false
										StatrMagnet = true
										repeat wait(_G.Fast_Delay)
											TP(v.HumanoidRootPart.CFrame*CFrame.new(0,30,0))
											EquipWeapon(_G.Setting_table.Weapon)
											AttackNoCD()
										until v.Humanoid.Health <= 0 or not v.Parent or Mix_Farm or not Farm_Ken 
										StatrMagnet = false
									end
								end
							end
						end
					end
				end
			elseif _G.Setting_table.Farm_Ken_Hop then
				if not Mix_Farm then
					if game.Players.LocalPlayer.PlayerGui.Main.Quest.Visible == false then
						CheckLevel()
						if (CFrameQ.Position-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 10 then
                            TP(CFrameQ)
                        else
                            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StartQuest", NameQuest, QuestLv)
                            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("SetSpawnPoint")
                        end
					elseif game.Players.LocalPlayer.PlayerGui.Main.Quest.Visible == true then
						CheckLevel()
						if string.find(game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text, NameMon) then
							if game.Workspace.Enemies:FindFirstChild(Ms) then
								for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
									if not string.find(v.Name,"Boss") and v.Humanoid.Health > 0 and (v.HumanoidRootPart.Position-CFrameMon.Position).Magnitude <= 1000 then
										if v.Humanoid:FindFirstChild("Animator") then
											v.Humanoid.Animator:Destroy()
										end
										spawn(function()
											repeat wait(1)
												if (v.HumanoidRootPart.Position-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 7 then
													wait(15)
													if game.Players.LocalPlayer.Character.Humanoid.Health == game.Players.LocalPlayer.Character.Humanoid.MaxHealth then
														_G.IKAI = true
														--break
													end
												end
											until _G.IKAI == true
										end)
										repeat wait(.2)
											local health = game.Players.LocalPlayer.Character.Humanoid.Health
											local maxhealth = game.Players.LocalPlayer.Character.Humanoid.MaxHealth
											local percent = (health / maxhealth) * 100
											if percent >= 90 then
												TP(v.HumanoidRootPart.CFrame*CFrame.new(0,0,2))
											else
												TP(v.HumanoidRootPart.CFrame*CFrame.new(0,30,0))
											end
										until _G.IKAI or percent < 90 or v.Humanoid.Health <= 0 or not v.Parent or Mix_Farm or not _G.Setting_table.Farm_Ken_Hop
										TP(v.HumanoidRootPart.CFrame*CFrame.new(0,30,0))
										if _G.IKAI then
											_G.Upto = true
											_G.IKAI = false
										else
											_G.TP_Ser = true
											game:GetService("TeleportService"):Teleport(game.PlaceId)
											wait(50)
										end
									end
								end
							elseif game.ReplicatedStorage:FindFirstChild(Ms) then
								TP(game.ReplicatedStorage:FindFirstChild(Ms).HumanoidRootPart.CFrame*CFrame.new(0,30,0))
							else
								for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
									if not string.find(v.Name,"Boss") and v.Humanoid.Health > 0 and (v.HumanoidRootPart.Position-CFrameMon.Position).Magnitude <= 1000 then
										if v.Humanoid:FindFirstChild("Animator") then
											v.Humanoid.Animator:Destroy()
										end
										spawn(function()
											repeat wait(1)
												if (v.HumanoidRootPart.Position-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 7 then
													wait(15)
													if game.Players.LocalPlayer.Character.Humanoid.Health == game.Players.LocalPlayer.Character.Humanoid.MaxHealth then
														_G.IKAI = true
														--break
													end
												end
											until _G.IKAI == true 
										end)
										repeat wait(.2)
											local health = game.Players.LocalPlayer.Character.Humanoid.Health
											local maxhealth = game.Players.LocalPlayer.Character.Humanoid.MaxHealth
											local percent = (health / maxhealth) * 100
											if percent >= 90 then
												TP(v.HumanoidRootPart.CFrame*CFrame.new(0,0,2))
											else
												TP(v.HumanoidRootPart.CFrame*CFrame.new(0,30,0))
											end
										until _G.IKAI or percent < 90 or v.Humanoid.Health <= 0 or not v.Parent or Mix_Farm or not _G.Setting_table.Farm_Ken_Hop
										TP(v.HumanoidRootPart.CFrame*CFrame.new(0,30,0))
										if _G.IKAI then
											_G.Upto = true
											_G.IKAI = false
										else
											_G.TP_Ser = true
											game:GetService("TeleportService"):Teleport(game.PlaceId)
											wait(50)
										end
									end
								end
							end
						end
					end
				end
			else
				wait(2)
			end
		end)
	end
end)


local Sh = Quest_Tab:CreateSection({Name = "Legendary Sword",Side = "Right"})
Sh:AddToggle({
    Name = "Auto Buy Legendary Sword",
    _G.Setting_table.Auto_Buy_Legendary_Sword,
    Callback = function(vu)
	_G.Setting_table.Auto_Buy_Legendary_Sword = vu
	Update_Setting(getgenv()['MyName'])
end})
spawn(function()
    while wait(.1) do
        pcall(function()
            if _G.Setting_table.Auto_Buy_Legendary_Sword or Triple_A then
                local args = {
                    [1] = "LegendarySwordDealer",
                    [2] = "2"
                }
                -- Triple_A
                game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
            else
				wait(2)
			end
        end)
    end
end)


if New_World or Three_World then
	local OPP = game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("KenTalk","Status")
	local Lpp = string.match(tostring(OPP), "%d+")
	_G.Lv_Ken = tonumber(Lpp)
end

spawn(function()
    while wait(2) do
        pcall(function()
            if CH_K then
                local OPP = game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("KenTalk","Status")
                local Lpp = string.match(tostring(OPP), "%d+")
                _G.Lv_Ken = tonumber(Lpp)
                wait(5)
            end
        end)
    end
end)

spawn(function()
    while wait(.3) do
        pcall(function()
            if Farm_Ken_V2 then
                if not Mix_Farm or Farm_Ken_Ex then
                    local Lv = game:GetService("Players").LocalPlayer.Data.Level.Value
                    local Beli = game:GetService("Players").LocalPlayer.Data.Beli.Value
                    if Lv >= 1800 and Beli >= 5000000 then
                        CH_K = true
                        if _G.Lv_Ken >= 5000 then
                            if game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("CitizenQuestProgress","Citizen") == 3 then
                                game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("KenTalk2","Start")
                                if not game.Players.LocalPlayer.Backpack:FindFirstChild("Pineapple") and not game.Players.LocalPlayer.Character:FindFirstChild("Pineapple") then
                                    for i,v in pairs(game.Workspace.PineappleSpawner:GetChildren()) do
                                        if v.Name == "Pineapple" then
                                            game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = v.Handle.CFrame
                                            wait(1)
                                        end
                                    end
                                    if not GPIJdz then
                                        Text("wait Fruit Spawn\nรอผลไม้เกิด")
                                        GPIJdz = true
                                    end
                                elseif not game.Players.LocalPlayer.Backpack:FindFirstChild("Banana") and not game.Players.LocalPlayer.Character:FindFirstChild("Banana") then
                                    for i,v in pairs(game.Workspace.BananaSpawner:GetChildren()) do
                                        if v.Name == "Banana" then
                                            game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = v.Handle.CFrame
                                            wait(1)
                                        end
                                    end
                                    if not GPIJdx then
                                        Text("wait Fruit Spawn\nรอผลไม้เกิด")
                                        GPIJdx = true
                                    end
                                elseif not game.Players.LocalPlayer.Backpack:FindFirstChild("Apple") and not game.Players.LocalPlayer.Character:FindFirstChild("Apple") then
                                    for i,v in pairs(game.Workspace.AppleSpawner:GetChildren()) do
                                        if v.Name == "Apple" then
                                            game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = v.Handle.CFrame
                                            wait(1)
                                        end
                                    end
                                    if not GPIJdcw then
                                        Text("wait Fruit Spawn\nรอผลไม้เกิด")
                                        GPIJdcw = true
                                    end
                                elseif not game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Fruit Bowl") and not  game:GetService("Players").LocalPlayer.Character:FindFirstChild("Fruit Bowl") then
                                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("CitizenQuestProgress","Citizen")
                                else
                                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("KenTalk2","Buy")
                                end
                            elseif game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("CitizenQuestProgress","Citizen") == 2 then
                                Mix_Farm = true
                                Farm_Ken_Ex = true
								TP(CFrame.new(-12512.6533203125, 336.21612548828125, -9872.841796875))
                            elseif game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("CitizenQuestProgress","Citizen") == 1 then
                                if game.Workspace.Enemies:FindFirstChild("Captain Elephant [Lv. 1875] [Boss]") then
                                    Mix_Farm = true
                                    Farm_Ken_Ex = true
                                    for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
                                        if v.Name == "Captain Elephant [Lv. 1875] [Boss]" and v.Humanoid.Health > 0 then
											repeat wait(_G.Fast_Delay)
												EquipWeapon(_G.Setting_table.Weapon)
                                                TP(v.HumanoidRootPart.CFrame*CFrame.new(0,30,0))
                                                AttackNoCD()
                                            until v.Humanoid.Health <= 0 or not v.Parent or Farm_Ken_V2 == false
                                        end
                                    end
                                elseif game.ReplicatedStorage:FindFirstChild("Captain Elephant [Lv. 1875] [Boss]") then
                                    Mix_Farm = true
                                    Farm_Ken_Ex = true
									TP(CFrame.new(-13400.6103515625, 317.9277648925781, -8409.9853515625)*CFrame.new(0,200,0))
                                elseif Farm_Ken_Ex then
                                    Mix_Farm = nil
                                    Farm_Ken_Ex = nil
                                end
                            elseif game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("CitizenQuestProgress","Citizen") == 0 then
                                if LIPO == nil then
                                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StartQuest","CitizenQuest",1)
                                    LIPO = true
                                end
                                if game.Workspace.Enemies:FindFirstChild("Forest Pirate [Lv. 1825]") then
                                    Mix_Farm = true
                                    Farm_Ken_Ex = true
                                    for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
                                        if v.Name == "Forest Pirate [Lv. 1825]" and v.Humanoid.Health > 0 then
                                            _G.PosMon = v.HumanoidRootPart.CFrame
                                            StatrMagnet = true
                                            repeat wait(_G.Fast_Delay)
												EquipWeapon(_G.Setting_table.Weapon)
                                                TP(v.HumanoidRootPart.CFrame*CFrame.new(0,30,0))
                                                AttackNoCD()
                                            until v.Humanoid.Health <= 0 or not v.Parent or Farm_Ken_V2 == false
                                            StatrMagnet = false
                                        end
                                    end
                                elseif game.ReplicatedStorage:FindFirstChild("Forest Pirate [Lv. 1825]") then
                                    Mix_Farm = true
                                    Farm_Ken_Ex = true
									TP(game.ReplicatedStorage:FindFirstChild("Forest Pirate [Lv. 1825]").HumanoidRootPart.CFrame*CFrame.new(0,30,0))
								elseif Farm_Ken_Ex then
									Farm_Ken_Ex = nil
									Mix_Farm = nil
								end
							elseif Farm_Ken_Ex then
								Farm_Ken_Ex = nil
								Mix_Farm = nil
                            end
                        elseif _G.Lv_Ken < 5000 then
                            if XER == nil then
								if Lv < 1800 then
									Text("❌ Level < 1800")
									_G.Have_Lv = "0"
								else
									Text("✅ Level >= 1800")
									_G.Have_Lv = "1"
								end
								if Beli < 5000000 then
									Text("❌ Money < 5M")
									_G.Have_B = "0"
								else
									Text("✅ Money >= 5M")
									_G.Have_B = "1"
								end
								if _G.Lv_Ken < 5000 then
									Text("❌ Ken Level < 5000")
								else
									Text("✅ Ken Level == 5000")
								end
								XER = true
							end
							--Farm_Ken = true
                        end
                    else
                        if XER == nil then
                            if Lv < 1800 then
                                Text("❌ Level < 1800")
                                _G.Have_Lv = "0"
                            else
                                Text("✅ Level >= 1800")
                                _G.Have_Lv = "1"
                            end
                            if Beli < 5000000 then
                                Text("❌ Money < 5M")
                                _G.Have_B = "0"
                            else
                                Text("✅ Money >= 5M")
                                _G.Have_B = "1"
                            end
                            if _G.Lv_Ken < 5000 then
                                Text("❌ Ken Level < 5000")
                            else
                                Text("✅ Ken Level == 5000")
                            end
                            XER = true
                        end
                        --Farm_Ken = true
                    end
                end
			elseif Farm_Ken_Ex then
				Farm_Ken_Ex = nil
				Mix_Farm = nil
			else
				wait(2)
            end
        end)
    end
end)

local INDRA = Quest_Tab:CreateSection("Farm Object")
INDRA:AddToggle({
    Name = "Auto Color Haki Indra",
    _G.Setting_table.Farm_Ob_Color,
    Callback = function(vu)
	Open_Color_Haki = vu
	_G.Setting_table.Farm_Ob_Color = vu
	Update_Setting(getgenv()['MyName'])
end})
spawn(function()
    while wait(.3) do
        pcall(function()
            if Open_Color_Haki then
                game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("activateColor","Winter Sky")
            	wait(0.5)
            	repeat TP2(CFrame.new(-5420.16602, 1084.9657, -2666.8208)) wait() 
                until _G.StopTween == true or Open_Color_Haki == false or (game.Players.LocalPlayer.Character.HumanoidRootPart.Position-Vector3.new(-5420.16602, 1084.9657, -2666.8208)).Magnitude <= 10
                wait(0.5)
                game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("activateColor","Pure Red")
                wait(0.5)
                repeat TP2(CFrame.new(-5414.41357, 309.865753, -2212.45776)) wait() 
                until _G.StopTween == true or Open_Color_Haki == false or (game.Players.LocalPlayer.Character.HumanoidRootPart.Position-Vector3.new(-5414.41357, 309.865753, -2212.45776)).Magnitude <= 10
                wait(0.5)
                game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("activateColor","Snow White")
                wait(0.5)
                repeat TP2(CFrame.new(-4971.47559, 331.565765, -3720.02954)) wait() 
                until _G.StopTween == true or Open_Color_Haki == false or (game.Players.LocalPlayer.Character.HumanoidRootPart.Position-Vector3.new(-4971.47559, 331.565765, -3720.02954)).Magnitude <= 10
                wait(0.5)
                game:GetService'VirtualUser':Button1Down(Vector2.new(1280,600))
                wait(3)
                game:GetService'VirtualUser':Button1Down(Vector2.new(1280,600))
            end
        end) 
    end
end)
INDRA:AddToggle({
    Name = "Auto Holy Torch",
    _G.Setting_table.Auto_Holy_Torch,
    Callback = function(vu)
	Auto_Holy_Torch = vu
	_G.Setting_table.Auto_Holy_Torch = vu
	Update_Setting(getgenv()['MyName'])
end})
INDRA:AddToggle({
    Name = "Auto Grab Chest",
    _G.Setting_table.Grab_Chest,
    Callback = function(vu)
	Grab_Chest = vu
	_G.Setting_table.Grab_Chest = vu
	Update_Setting(getgenv()['MyName'])
end})
INDRA:AddToggle({
    Name = "Auto Grab Chest Stop Torch",
    _G.Setting_table.STP,
    Callback = function(vu)
	Grab_Chest = vu
	T_P_H = vu
	_G.Setting_table.STP = vu
	Update_Setting(getgenv()['MyName'])
end})
INDRA:AddToggle({
    Name = "Hop Chest Lock",
    _G.Setting_table.Hop_Chest,
    Callback = function(vu)
	_G.Setting_table.Hop_Chest = vu
	Update_Setting(getgenv()['MyName'])
end})
INDRA:AddSlider({
    Name = "Chest Lock",
    Value = 30,
    Min = 1,
    Max = 100,
    _G.Setting_table.K_MAX,
    Callback = function(vu)
	_G.Setting_table.K_MAX = vu
	Update_Setting(getgenv()['MyName'])
end})
local K_C = INDRA:AddLabel('Chest Lock : 0')
if _G.Setting_table.Grab_Chest then
	Grab_Chest = true
end
spawn(function()
	while wait(2) do
		pcall(function()
			if _G.Setting_table.Hop_Chest then
				if K_CH >= _G.Setting_table.K_MAX and not H_F then
					if game.Players.LocalPlayer.Backpack:FindFirstChild("Fist of Darkness") or game.Players.LocalPlayer.Character:FindFirstChild("Fist of Darkness") then
						H_F = true
					else
						HopServer()
						wait(50)
					end
				end
			end
		end)
	end
end)
K_CH = 0
K_C:Set('Chest : '..tostring(K_CH).."/".._G.Setting_table.K_MAX)
spawn(function()
    while wait(.2) do
        pcall(function()
            if Grab_Chest then
                if T_P_H then
                    if game.Players.LocalPlayer.Backpack:FindFirstChild("Fist of Darkness") or game.Players.LocalPlayer.Character:FindFirstChild("Fist of Darkness") then
                        TP2(CFrame.new(-379.70889282227, 73.0458984375, 304.84692382813))
                        H_F = true
						game:GetService'VirtualUser':Button1Down(Vector2.new(1280,600))
                        wait(3)
                    else
						_G.Chest_100 = nil
						_G.Chest_500 = nil
						_G.Chest_1000 = nil
						_G.Chest_1500 = nil
						_G.Chest_2000 = nil
						_G.Chest_2500 = nil
						_G.Chest_3500 = nil
						_G.Chest_4500 = nil
						_G.Chest_5500 = nil
						_G.Chest_6500 = nil
						_G.Chest_7500 = nil
						_G.Chest_9500 = nil
						_G.Chest_10500 = nil
						_G.Chest_12500 = nil
						_G.Chest_15500 = nil
						_G.Chest_17500 = nil
						Chest_100()
						Chest_500()
						Chest_1000()
						Chest_1500()
						Chest_2000()
						Chest_2500()
						Chest_3500()
						Chest_4500()
						Chest_5500()
						Chest_6500()
						Chest_7500()
						Chest_9500()
						Chest_10500()
						Chest_12500()
						Chest_15500()
						Chest_17500()
						if _G.Chest_100 ~= nil then
							repeat wait(.3)
								TP(_G.Chest_100.CFrame)
							until not _G.Chest_100.Parent or not Grab_Chest
							if Grab_Chest then
								K_CH = K_CH + 1
								K_C:Set('Chest : '..tostring(K_CH).."/".._G.Setting_table.K_MAX)
							end
						elseif _G.Chest_500 ~= nil then
							repeat wait(.3)
								TP(_G.Chest_500.CFrame)
							until not _G.Chest_500.Parent or not Grab_Chest
							if Grab_Chest then
								K_CH = K_CH + 1
								K_C:Set('Chest : '..tostring(K_CH).."/".._G.Setting_table.K_MAX)
							end
						elseif _G.Chest_1000 ~= nil then
							repeat wait(.3)
								TP(_G.Chest_1000.CFrame)
							until not _G.Chest_1000.Parent or not Grab_Chest
							if Grab_Chest then
								K_CH = K_CH + 1
								K_C:Set('Chest : '..tostring(K_CH).."/".._G.Setting_table.K_MAX)
							end
						elseif _G.Chest_1500 ~= nil then
							repeat wait(.3)
								TP(_G.Chest_1500.CFrame)
							until not _G.Chest_1500.Parent or not Grab_Chest
							if Grab_Chest then
								K_CH = K_CH + 1
								K_C:Set('Chest : '..tostring(K_CH).."/".._G.Setting_table.K_MAX)
							end
						elseif _G.Chest_2000 ~= nil then
							repeat wait(.3)
								TP(_G.Chest_2000.CFrame)
							until not _G.Chest_2000.Parent or not Grab_Chest
							if Grab_Chest then
								K_CH = K_CH + 1
								K_C:Set('Chest : '..tostring(K_CH).."/".._G.Setting_table.K_MAX)
							end
						elseif _G.Chest_2500 ~= nil then
							repeat wait(.3)
								TP(_G.Chest_2500.CFrame)
							until not _G.Chest_2500.Parent or not Grab_Chest
							if Grab_Chest then
								K_CH = K_CH + 1
								K_C:Set('Chest : '..tostring(K_CH).."/".._G.Setting_table.K_MAX)
							end
						elseif _G.Chest_3500 ~= nil then
							repeat wait(.3)
								TP(_G.Chest_3500.CFrame)
							until not _G.Chest_3500.Parent or not Grab_Chest
							if Grab_Chest then
								K_CH = K_CH + 1
								K_C:Set('Chest : '..tostring(K_CH).."/".._G.Setting_table.K_MAX)
							end
						elseif _G.Chest_4500 ~= nil then
							repeat wait(.3)
								TP(_G.Chest_4500.CFrame)
							until not _G.Chest_4500.Parent or not Grab_Chest
							if Grab_Chest then
								K_CH = K_CH + 1
								K_C:Set('Chest : '..tostring(K_CH).."/".._G.Setting_table.K_MAX)
							end
						elseif _G.Chest_5500 ~= nil then
							repeat wait(.3)
								TP(_G.Chest_5500.CFrame)
							until not _G.Chest_5500.Parent or not Grab_Chest
							if Grab_Chest then
								K_CH = K_CH + 1
								K_C:Set('Chest : '..tostring(K_CH).."/".._G.Setting_table.K_MAX)
							end
						elseif _G.Chest_6500 ~= nil then
							repeat wait(.3)
								TP(_G.Chest_6500.CFrame)
							until not _G.Chest_6500.Parent or not Grab_Chest
							if Grab_Chest then
								K_CH = K_CH + 1
								K_C:Set('Chest : '..tostring(K_CH).."/".._G.Setting_table.K_MAX)
							end
						elseif _G.Chest_7500 ~= nil then
							repeat wait(.3)
								TP(_G.Chest_7500.CFrame)
							until not _G.Chest_7500.Parent or not Grab_Chest
							if Grab_Chest then
								K_CH = K_CH + 1
								K_C:Set('Chest : '..tostring(K_CH).."/".._G.Setting_table.K_MAX)
							end
						elseif _G.Chest_9500 ~= nil then
							repeat wait(.3)
								TP(_G.Chest_9500.CFrame)
							until not _G.Chest_9500.Parent or not Grab_Chest
							if Grab_Chest then
								K_CH = K_CH + 1
								K_C:Set('Chest : '..tostring(K_CH).."/".._G.Setting_table.K_MAX)
							end
						elseif _G.Chest_10500 ~= nil then
							repeat wait(.3)
								TP(_G.Chest_10500.CFrame)
							until not _G.Chest_10500.Parent or not Grab_Chest
							if Grab_Chest then
								K_CH = K_CH + 1
								K_C:Set('Chest : '..tostring(K_CH).."/".._G.Setting_table.K_MAX)
							end
						elseif _G.Chest_12500 ~= nil then
							repeat wait(.3)
								TP(_G.Chest_12500.CFrame)
							until not _G.Chest_12500.Parent or not Grab_Chest
							if Grab_Chest then
								K_CH = K_CH + 1
								K_C:Set('Chest : '..tostring(K_CH).."/".._G.Setting_table.K_MAX)
							end
						elseif _G.Chest_15500 ~= nil then
							repeat wait(.3)
								TP(_G.Chest_15500.CFrame)
							until not _G.Chest_15500.Parent or not Grab_Chest
							if Grab_Chest then
								K_CH = K_CH + 1
								K_C:Set('Chest : '..tostring(K_CH).."/".._G.Setting_table.K_MAX)
							end
						elseif _G.Chest_17500 ~= nil then
							repeat wait(.3)
								TP(_G.Chest_17500.CFrame)
							until not _G.Chest_17500.Parent or not Grab_Chest
							if Grab_Chest then
								K_CH = K_CH + 1
								K_C:Set('Chest : '..tostring(K_CH).."/".._G.Setting_table.K_MAX)
							end
						end
                    end
                else
					
                    _G.Chest_100 = nil
						_G.Chest_500 = nil
						_G.Chest_1000 = nil
						_G.Chest_1500 = nil
						_G.Chest_2000 = nil
						_G.Chest_2500 = nil
						_G.Chest_3500 = nil
						_G.Chest_4500 = nil
						_G.Chest_5500 = nil
						_G.Chest_6500 = nil
						_G.Chest_7500 = nil
						_G.Chest_9500 = nil
						_G.Chest_10500 = nil
						_G.Chest_12500 = nil
						_G.Chest_15500 = nil
						_G.Chest_17500 = nil
						Chest_100()
						Chest_500()
						Chest_1000()
						Chest_1500()
						Chest_2000()
						Chest_2500()
						Chest_3500()
						Chest_4500()
						Chest_5500()
						Chest_6500()
						Chest_7500()
						Chest_9500()
						Chest_10500()
						Chest_12500()
						Chest_15500()
						Chest_17500()
						if _G.Chest_100 ~= nil then
							repeat wait(.3)
								TP(_G.Chest_100.CFrame)
							until not _G.Chest_100.Parent or not Grab_Chest
							if Grab_Chest then
								K_CH = K_CH + 1
								K_C:Set('Chest : '..tostring(K_CH).."/".._G.Setting_table.K_MAX)
							end
						elseif _G.Chest_500 ~= nil then
							repeat wait(.3)
								TP(_G.Chest_500.CFrame)
							until not _G.Chest_500.Parent or not Grab_Chest
							if Grab_Chest then
								K_CH = K_CH + 1
								K_C:Set('Chest : '..tostring(K_CH).."/".._G.Setting_table.K_MAX)
							end
						elseif _G.Chest_1000 ~= nil then
							repeat wait(.3)
								TP(_G.Chest_1000.CFrame)
							until not _G.Chest_1000.Parent or not Grab_Chest
							if Grab_Chest then
								K_CH = K_CH + 1
								K_C:Set('Chest : '..tostring(K_CH).."/".._G.Setting_table.K_MAX)
							end
						elseif _G.Chest_1500 ~= nil then
							repeat wait(.3)
								TP(_G.Chest_1500.CFrame)
							until not _G.Chest_1500.Parent or not Grab_Chest
							if Grab_Chest then
								K_CH = K_CH + 1
								K_C:Set('Chest : '..tostring(K_CH).."/".._G.Setting_table.K_MAX)
							end
						elseif _G.Chest_2000 ~= nil then
							repeat wait(.3)
								TP(_G.Chest_2000.CFrame)
							until not _G.Chest_2000.Parent or not Grab_Chest
							if Grab_Chest then
								K_CH = K_CH + 1
								K_C:Set('Chest : '..tostring(K_CH).."/".._G.Setting_table.K_MAX)
							end
						elseif _G.Chest_2500 ~= nil then
							repeat wait(.3)
								TP(_G.Chest_2500.CFrame)
							until not _G.Chest_2500.Parent or not Grab_Chest
							if Grab_Chest then
								K_CH = K_CH + 1
								K_C:Set('Chest : '..tostring(K_CH).."/".._G.Setting_table.K_MAX)
							end
						elseif _G.Chest_3500 ~= nil then
							repeat wait(.3)
								TP(_G.Chest_3500.CFrame)
							until not _G.Chest_3500.Parent or not Grab_Chest
							if Grab_Chest then
								K_CH = K_CH + 1
								K_C:Set('Chest : '..tostring(K_CH).."/".._G.Setting_table.K_MAX)
							end
						elseif _G.Chest_4500 ~= nil then
							repeat wait(.3)
								TP(_G.Chest_4500.CFrame)
							until not _G.Chest_4500.Parent or not Grab_Chest
							if Grab_Chest then
								K_CH = K_CH + 1
								K_C:Set('Chest : '..tostring(K_CH).."/".._G.Setting_table.K_MAX)
							end
						elseif _G.Chest_5500 ~= nil then
							repeat wait(.3)
								TP(_G.Chest_5500.CFrame)
							until not _G.Chest_5500.Parent or not Grab_Chest
							if Grab_Chest then
								K_CH = K_CH + 1
								K_C:Set('Chest : '..tostring(K_CH).."/".._G.Setting_table.K_MAX)
							end
						elseif _G.Chest_6500 ~= nil then
							repeat wait(.3)
								TP(_G.Chest_6500.CFrame)
							until not _G.Chest_6500.Parent or not Grab_Chest
							if Grab_Chest then
								K_CH = K_CH + 1
								K_C:Set('Chest : '..tostring(K_CH).."/".._G.Setting_table.K_MAX)
							end
						elseif _G.Chest_7500 ~= nil then
							repeat wait(.3)
								TP(_G.Chest_7500.CFrame)
							until not _G.Chest_7500.Parent or not Grab_Chest
							if Grab_Chest then
								K_CH = K_CH + 1
								K_C:Set('Chest : '..tostring(K_CH).."/".._G.Setting_table.K_MAX)
							end
						elseif _G.Chest_9500 ~= nil then
							repeat wait(.3)
								TP(_G.Chest_9500.CFrame)
							until not _G.Chest_9500.Parent or not Grab_Chest
							if Grab_Chest then
								K_CH = K_CH + 1
								K_C:Set('Chest : '..tostring(K_CH).."/".._G.Setting_table.K_MAX)
							end
						elseif _G.Chest_10500 ~= nil then
							repeat wait(.3)
								TP(_G.Chest_10500.CFrame)
							until not _G.Chest_10500.Parent or not Grab_Chest
							if Grab_Chest then
								K_CH = K_CH + 1
								K_C:Set('Chest : '..tostring(K_CH).."/".._G.Setting_table.K_MAX)
							end
						elseif _G.Chest_12500 ~= nil then
							repeat wait(.3)
								TP(_G.Chest_12500.CFrame)
							until not _G.Chest_12500.Parent or not Grab_Chest
							if Grab_Chest then
								K_CH = K_CH + 1
								K_C:Set('Chest : '..tostring(K_CH).."/".._G.Setting_table.K_MAX)
							end
						elseif _G.Chest_15500 ~= nil then
							repeat wait(.3)
								TP(_G.Chest_15500.CFrame)
							until not _G.Chest_15500.Parent or not Grab_Chest
							if Grab_Chest then
								K_CH = K_CH + 1
								K_C:Set('Chest : '..tostring(K_CH).."/".._G.Setting_table.K_MAX)
							end
						elseif _G.Chest_17500 ~= nil then
							repeat wait(.3)
								TP(_G.Chest_17500.CFrame)
							until not _G.Chest_17500.Parent or not Grab_Chest
							if Grab_Chest then
								K_CH = K_CH + 1
								K_C:Set('Chest : '..tostring(K_CH).."/".._G.Setting_table.K_MAX)
							end
						end
                end
            end
        end)
    end
end)

spawn(function()
    while wait(.5) do
        pcall(function()
            if Auto_Holy_Torch then
                if game.Players.LocalPlayer.Backpack:FindFirstChild("Holy Torch") or game.Players.LocalPlayer.Character:FindFirstChild("Holy Torch") then
                    repeat wait(.2)
                        EquipWeapon("Holy Torch")
                        TP2(CFrame.new(-10752.4434, 415.261749, -9367.43848, 1, 0, 0, 0, 1, 0, 0, 0, 1))
                    until (Vector3.new(-10752.4434, 415.261749, -9367.43848)-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude < 5
                    wait(2)
                    repeat wait(.2)
                        EquipWeapon("Holy Torch")
                        TP2(CFrame.new(-11671.6289, 333.78125, -9474.31934, 0.300932229, 0, -0.953645527, 0, 1, 0, 0.953645527, 0, 0.300932229))
                    until (Vector3.new(-11671.6289, 333.78125, -9474.31934)-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude < 5
                    wait(2)
                    repeat wait(.2)
                        EquipWeapon("Holy Torch")
                        TP2(CFrame.new(-12133.1406, 521.507446, -10654.292, 0.80428642, 0, -0.594241858, 0, 1, 0, 0.594241858, 0, 0.80428642))
                    until (Vector3.new(-12133.1406, 521.507446, -10654.292)-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude < 5
                    wait(2)
                    repeat wait(.2)
                        EquipWeapon("Holy Torch")
                        TP2(CFrame.new(-13336.127, 484.521179, -6985.31689, 0.853732228, 0, -0.520712316, 0, 1, 0, 0.520712316, 0, 0.853732228))
                    until (Vector3.new(-13336.127, 484.521179, -6985.31689)-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude < 5
                    wait(2)
                    EquipWeapon("Holy Torch")
                    repeat wait(.2)
                        TP2(CFrame.new(-13487.623, 336.436188, -7924.53857, -0.982848108, 0, 0.184417039, 0, 1, 0, -0.184417039, 0, -0.982848108))
                    until (Vector3.new(-13487.623, 336.436188, -7924.53857)-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude < 5
                    wait(2)
                    Com()
                    wait(20)
                elseif not game.Players.LocalPlayer.Backpack:FindFirstChild("Holy Torch") and not game.Players.LocalPlayer.Character:FindFirstChild("Holy Torch") then
                    if Uiio == nil then
						Text("No Have Holy Torch")
						Uiio = true
					end
                    wait(3)
                end
            end
        end)
    end
end)
--[[ST:AddButton({
    Name = "Copy Hwid",
    Callback = function()
	setclipboard((syn and syn.request or request)({Url = 'https://api.luauth.xyz/hwid', Method = syn and "Get" or "GET"}).Body)
end})]]--

local Qs = Quest_Tab:CreateSection({
    Name = "Quest",
    Side = "Right"
})
Qs:AddToggle({
    Name = "Auto Bartlio",
    _G.Setting_table.Bartlio_Farm,
    Callback = function(vu)
	Bartlio_Farm = vu
	_G.Setting_table.Bartlio_Farm = vu
	Update_Setting(getgenv()['MyName'])
end})
spawn(function()
    while wait(1) do
		pcall(function()
			if Bartlio_Farm and New_World then
				local Lv = game:GetService("Players").LocalPlayer.Data.Level.Value
				if Lv >= 900 then
					if game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BartiloQuestProgress","Bartilo") == 0 then
						if string.find(game.Players.LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text, "Swan Pirates") and string.find(game.Players.LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text, "50") and game.Players.LocalPlayer.PlayerGui.Main.Quest.Visible == true then
							if game.workspace.Enemies:FindFirstChild("Swan Pirate [Lv. 775]") then
								for i,v in pairs(game.workspace.Enemies:GetChildren()) do
									if v.Name == "Swan Pirate [Lv. 775]" then
										CFrameMon = v.HumanoidRootPart.CFrame
										_G.PosMon = v.HumanoidRootPart.CFrame
										StatrMagnet = true
										repeat wait()
											EquipWeapon(_G.Setting_table.Weapon)
											v.HumanoidRootPart.Size = Vector3.new(50,50,50)
											TP(v.HumanoidRootPart.CFrame*CFrame.new(0,25,0))
											game:GetService'VirtualUser':CaptureController()
											game:GetService'VirtualUser':Button1Down(Vector2.new(1280,900))
										until v.Humanoid.Health <= 0 or not v.Parent or Bartlio_Farm ==false
										StatrMagnet = false
									end
								end
							elseif game:GetService("ReplicatedStorage"):FindFirstChild("Swan Pirate [Lv. 775]") then
								TP2(game:GetService("ReplicatedStorage"):FindFirstChild("Swan Pirate [Lv. 775]").HumanoidRootPart.CFrame*CFrame.new(0,20,0))
							end
						else
							game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StartQuest","BartiloQuest",1)
						end
					elseif game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BartiloQuestProgress","Bartilo") == 1 then
						_G.SelectBoss = "Jeremy [Lv. 850] [Boss]"
						CheckQuestBoss()
						if game.workspace.Enemies:FindFirstChild("Jeremy [Lv. 850] [Boss]") then
							for i,v in pairs(game.workspace.Enemies:GetChildren()) do
								if v.Name == "Jeremy [Lv. 850] [Boss]" then
									repeat wait()
										EquipWeapon(_G.Setting_table.Weapon)
										v.HumanoidRootPart.Size = Vector3.new(50,50,50)
										TP(v.HumanoidRootPart.CFrame*CFrame.new(0,25,0))
										game:GetService'VirtualUser':CaptureController()
										game:GetService'VirtualUser':Button1Down(Vector2.new(1280,900))
									until v.Humanoid.Health <= 0 or not v.Parent or Bartlio_Farm == false
								end
							end
						else
							TP(CFrameBoss)
						end
					elseif game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BartiloQuestProgress","Bartilo") == 2 then
						repeat wait()
							TP2(CFrame.new(-1836, 11, 1714))
						until (Vector3.new(-1836, 11, 1714)-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 2
						game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-1836, 11, 1714)
						wait(1)
						game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-1850.49329, 13.1789551, 1750.89685)
						wait(1)
						game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-1858.87305, 19.3777466, 1712.01807)
						wait(1)
						game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-1803.94324, 16.5789185, 1750.89685)
						wait(1)
						game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-1858.55835, 16.8604317, 1724.79541)
						wait(1)
						game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-1869.54224, 15.987854, 1681.00659)
						wait(1)
						game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-1800.0979, 16.4978027, 1684.52368)
						wait(1)
						game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-1819.26343, 14.795166, 1717.90625)
						wait(1)
						game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-1813.51843, 14.8604736, 1724.79541)
					end
				end
			end
		end)
    end
end)
Qs:AddToggle({
    Name = "Auto Open Don Swan",
    _G.Setting_table.Open_Don_Swan,
    Callback = function(vu)
	Inventory_Fruit = vu
	BringFruit = vu
	Don_Swan_Quest = vu
	_G.Setting_table.Open_Don_Swan = vu
	Update_Setting(getgenv()['MyName'])
end})

local function split(str, sep)
	local result = {}
	local regex = ("([^%s]+)"):format(sep)
	for each in str:gmatch(regex) do
	   table.insert(result, each)
	end
	return result
 end

spawn(function()
    while wait(.5) do
        pcall(function()
            if Don_Swan_Quest then
                if New_World then
                    local Lv = game:GetService("Players").LocalPlayer.Data.Level.Value
                    if Lv >= 1200 then
                        if game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("TalkTrevor","1") ~= 0 then
                            wait(2)
							local fruit = game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("getInventoryFruits")
                            for i,v in pairs(fruit) do
                                if v["Price"] >= 1000000 then
                                    Inventory_Fruit = false
                                    Mix_Farm = true
                                    wait(1)
                                    local NameFruit = split(v["Name"], "-")[2] .. " Fruit"
                                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("LoadFruit",v["Name"])
                                    wait(2)
                                    EquipWeapon(NameFruit)
                                    wait(2)
                                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("TalkTrevor","1")
                                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("TalkTrevor","2")
                                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("TalkTrevor","3")
                                    Mix_Farm = nil
                                    Inventory_Fruit = true
									return
                                end
                            end
                        end
                    end
                end
			else
				wait(2)
            end
        end)
    end
end)

Qs:AddLabel("Third World")
Qs:AddToggle({
    Name = "Auto Phoenix Awaken",
    _G.Setting_table.Auto_Phoenix_Awaken,
    Callback = function(vu)
	Auto_Phoenix_Awaken = vu
	Auto_Farm_Fruit = vu
	SkillZ = vu
	_G.Setting_table.Auto_Phoenix_Awaken = vu
end})
if _G.Setting_table.Farm_Fruit then
	Auto_Farm_Fruit = true
end
if _G.Setting_table.Skill_Z then
	SkillZ = true
end
function Get_Fruit_Backpack()
	for i,v in pairs(game.Players.LocalPlayer.Backpack:GetChildren()) do
		if v:IsA("Tool") then
			if string.find(v.Name,"Fruit") then
				_G.Have_Fruit = true
				return
			end
		end
	end
end
function Get_Fruit_Character()
	for i,v in pairs(game.Players.LocalPlayer.Character:GetChildren()) do
		if v:IsA("Tool") then
			if string.find(v.Name,"Fruit") then
				_G.Have_Fruit = true
				return
			end
		end
	end
end
function Get_Fruit_Inventory()
	local fruit = game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("getInventoryFruits")
	for i,v in pairs(fruit) do
		if _G.Phoenix_R then
			if v["Price"] < 1000000 then
				game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("LoadFruit",v["Name"])
				_G.Have_Fruit = true
				return
			end
		elseif _G.Phoenix_XR then
			if v["Price"] >= 1000000 then
				game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("LoadFruit",v["Name"])
				_G.Have_Fruit = true
				return
			end
		elseif v["Price"] >= 10 then
			game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("LoadFruit",v["Name"])
			_G.Have_Fruit = true
			return
		end
	end
end
function Raid_FG()
	for i,v6 in pairs(game:GetService("Workspace"):GetChildren()) do
		if v6:IsA ("Tool") and (v6.Handle.Position-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude < 13000 then
			game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = v6.Handle.CFrame
			v6.Handle.CFrame = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame
		end
	end
	wait(1)
	Inventory_Fruit = nil
	Get_Fruit_Inventory()
	Get_Fruit_Backpack()
	Get_Fruit_Character()
	if _G.Have_Fruit then
		Mix_Farm = true
		Raid_FG_Ex = true
		Auto_Raid = true
	elseif _G.Setting_table.Melee_Hop then
		HopServer()
		wait(50)
	elseif _G.Setting_table.Phoenix_Hop then
		HopServer()
		wait(50)
	elseif _G.Setting_table.Race_Hop then
		HopServer()
		wait(50)
	elseif _G.Setting_table.Auto_Pole_V2_Hop then
		HopServer()
		wait(50)
	elseif Raid_FG_Ex then
		Mix_Farm = nil
		Raid_FG_Ex = nil
		Auto_Raid = nil
	elseif not _G.Have_Fruit then
		Text("ไม่มีผลปีศาจเหลือ\nไม่สามารถลงดันได้")
	end
end
spawn(function()
	while wait(.5) do
		pcall(function()
			if Auto_Phoenix_Awaken then
				if not Mix_Farm or Auto_Phoenix_Awaken_Ex then
					if game.Players.LocalPlayer.Character:FindFirstChild("Bird-Bird: Phoenix") or game.Players.LocalPlayer.Backpack:FindFirstChild("Bird-Bird: Phoenix") then
						if game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("SickScientist","Check") ~= false then
							if not UHuHI then
								Text("กำลังฟามมาสเตอรี่ผลปีศาจ")
								UHuHI = true
							end
							Auto_Farm_Fruit = true
						elseif game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("SickScientist","Check") == false then
							Auto_Farm_Fruit = false
							if game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("SickScientist","Heal") == 1 then
								local Beli = game:GetService("Players").LocalPlayer.Data.Beli.Value
								local FG = game:GetService("Players").LocalPlayer.Data.Fragments.Value
								if FG >= 6000 then
									_G.Have_Fruit = nil
									_G.Phoenix_R = nil
									_G.Phoenix_XR = true
									Get_Fruit_Inventory()
									_G.Phoenix_XR = nil
									wait(1)
									if _G.Have_Fruit then
										if game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("RaidsNpc", "Select", "Bird: Phoenix") == 1 then
											_G.Setting_table.Select_Map = "Bird: Phoenix"
											_G.Setting_table.Auto_Awaken = true
											Mix_Farm = true
											Auto_Phoenix_Awaken_Ex = true
											Auto_Raid = true
											TP(game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame*CFrame.new(0,30,0))
											Text("กำลังลงดันฟีนิกตื่น")
											repeat wait(1)
											until game:GetService("Players")["LocalPlayer"].PlayerGui.Main.Timer.Visible == true
											repeat wait(1)
											until game:GetService("Players")["LocalPlayer"].PlayerGui.Main.Timer.Visible == false
										elseif game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("RaidsNpc", "Select", "Bird: Phoenix") == '[You already have a Special Microchip.]' then
											_G.Setting_table.Select_Map = "Flame"
											Mix_Farm = true
											Auto_Phoenix_Awaken_Ex = true
											Auto_Raid = true
											TP(game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame*CFrame.new(0,30,0))
											Text("กำลังลงดันหาเงินม่วง")
											repeat wait(1)
											until game:GetService("Players")["LocalPlayer"].PlayerGui.Main.Timer.Visible == true
											repeat wait(1)
											until game:GetService("Players")["LocalPlayer"].PlayerGui.Main.Timer.Visible == false
										elseif Auto_Phoenix_Awaken_Ex then
											Auto_Phoenix_Awaken_Ex = nil
											Mix_Farm = nil
											Auto_Raid = nil
										elseif _G.Setting_table.Phoenix_Hop then
											if not UHIkx then
												Text("รอ2ช.มถึงจะซื้อชิปลงดันได้\nฟามเงินม่วงรอดีกว่า")
												UHIkx = true
											end
											_G.Phoenix_R = true
											Raid_FG()
										else
											if not UHIkz then
												Text("รอ2ช.มถึงจะซื้อชิปลงดันได้")
												UHIkz = true
											end
										end
									elseif Beli >= 1000000 then
										if game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("RaidsNpc", "Select", "Bird: Phoenix") == 1 then
											_G.Setting_table.Select_Map = "Bird: Phoenix"
											_G.Setting_table.Auto_Awaken = true
											Mix_Farm = true
											Auto_Phoenix_Awaken_Ex = true
											Auto_Raid = true
											TP(game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame*CFrame.new(0,30,0))
											Text("กำลังลงดันฟีนิกตื่น")
											repeat wait(1)
											until game:GetService("Players")["LocalPlayer"].PlayerGui.Main.Timer.Visible == true
											repeat wait(1)
											until game:GetService("Players")["LocalPlayer"].PlayerGui.Main.Timer.Visible == false
										elseif game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("RaidsNpc", "Select", "Bird: Phoenix") == '[You already have a Special Microchip.]' then
											_G.Setting_table.Select_Map = "Flame"
											Mix_Farm = true
											Auto_Phoenix_Awaken_Ex = true
											Auto_Raid = true
											TP(game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame*CFrame.new(0,30,0))
											Text("กำลังลงดันหาเงินม่วง")
											repeat wait(1)
											until game:GetService("Players")["LocalPlayer"].PlayerGui.Main.Timer.Visible == true
											repeat wait(1)
											until game:GetService("Players")["LocalPlayer"].PlayerGui.Main.Timer.Visible == false
										elseif Auto_Phoenix_Awaken_Ex then
											Auto_Phoenix_Awaken_Ex = nil
											Mix_Farm = nil
											Auto_Raid = nil
										elseif _G.Setting_table.Phoenix_Hop then
											if not UHIkxz then
												Text("รอ2ช.มถึงจะซื้อชิปลงดันได้\nฟามเงินม่วงรอดีกว่า")
												UHIkxz = true
											end
											_G.Phoenix_R = true
											Raid_FG()
										else
											if not UHIk then
												Text("รอ2ช.มถึงจะซื้อชิปลงดันได้")
												UHIk = true
											end
										end
									elseif Auto_Phoenix_Awaken_Ex then
										Auto_Phoenix_Awaken_Ex = nil
										Mix_Farm = nil
									else
										Text("กำลังฟามเงินไห้ถึง 1ล้าน\nเพื่อซื้อชิปลงดันฟีนิก")
										wait(10)
									end
								elseif Auto_Phoenix_Awaken_Ex then
									Auto_Phoenix_Awaken_Ex = nil
									Mix_Farm = nil
									Auto_Raid = nil
								else
									_G.Phoenix_R = true
									Raid_FG()
									Text("เงินม่วงไม่ถึง 6000\nไม่สามารถลงดันได้")
									Text("กำลังหาผลมาลงดัน!")
									wait(10)
								end
							elseif FG < 1500 then
								if not LPOJO then
									Text("เงินม่วงไม่ถึง 1500\nไม่สามารถทำเควสได้")
									Text("กำลังหาผลมาลงดัน!")
									LPOJO = true
								end
								_G.Phoenix_R = true
								Raid_FG()
							end
						end
					else
						wait(2)
					end
				else
					wait(2)
				end
			else
				wait(2)
			end
		end)
	end
end)

Qs:AddToggle({
    Name = "Auto Observation Haki V2",
    _G.Setting_table.Farm_Ken_V2,
    Callback = function(vu)
	Farm_Ken = vu
	Farm_Ken_V2 = vu
	_G.Setting_table.Farm_Ken_V2 = vu
	Update_Setting(getgenv()['MyName'])
end})
if _G.Setting_table.Farm_Ken or _G.Setting_table.Farm_Ken_V2 then
	Farm_Ken = true
end

Qs:AddToggle({
    Name = "Observation Haki V2 Hop",
    _G.Setting_table.Melee_Hop,
    Callback = function(vu)
	_G.Setting_table.Melee_Hop = vu
	Update_Setting(getgenv()['MyName'])
	-- Auto Exc
end})

local evr = Quest_Tab:CreateSection({Name = "Evo Race",Side = "Right"})
evr:AddToggle({
    Name = "Auto Mink",
    _G.Setting_table.Mink_Evo,
    Callback = function(vu)
	_G.Setting_table.Mink_Evo = vu
	Update_Setting(getgenv()['MyName'])
end})
evr:AddToggle({
    Name = "Auto Human",
    _G.Setting_table.Human_Evo,
    Callback = function(vu)
	_G.Setting_table.Human_Evo = vu
	Update_Setting(getgenv()['MyName'])
end})
evr:AddToggle({
    Name = "Auto Skypiea",
    _G.Setting_table.Skypiea_Evo,
    Callback = function(vu)
	_G.Setting_table.Skypiea_Evo = vu
	Update_Setting(getgenv()['MyName'])
end})
evr:AddToggle({
    Name = "Auto Fish",
    _G.Setting_table.Fishman_Evo,
    Callback = function(vu)
	_G.Setting_table.Fishman_Evo = vu
	Update_Setting(getgenv()['MyName'])
end})
evr:AddToggle({
    Name = "Next Race",
    _G.Setting_table.Next_Race,
    Callback = function(vu)
	_G.Setting_table.Next_Race = vu
	Update_Setting(getgenv()['MyName'])
end})
evr:AddToggle({
    Name = "Hop",
    _G.Setting_table.Race_Hop,
    Callback = function(vu)
	_G.Setting_table.Race_Hop = vu
	Update_Setting(getgenv()['MyName'])
end})
if game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Wenlocktoad","1") == -2 then
	if game.Players.LocalPlayer.Data.Race.Value == 'Mink' then
		_G.Setting_table.Mink_Evo_H = true
	elseif game.Players.LocalPlayer.Data.Race.Value == 'Human' then
		_G.Setting_table.Human_Evo_H = true
	elseif game.Players.LocalPlayer.Data.Race.Value == 'Skypiea' then
		_G.Setting_table.Skypiea_Evo_H = true
	elseif game.Players.LocalPlayer.Data.Race.Value == 'Fishman' then
		_G.Setting_table.Fishman_Evo_H = true
	end
end
spawn(function()
	while wait(.5) do
		pcall(function()
			if _G.Setting_table.Mink_Evo and not _G.Setting_table.Mink_Evo_H and game.Players.LocalPlayer.Data.Race.Value == 'Mink' then
				if game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Wenlocktoad","1") == -2 then
					if game.Players.LocalPlayer.Data.Race.Value == 'Mink' then
						_G.Setting_table.Mink_Evo_H = true
						return
					elseif game.Players.LocalPlayer.Data.Race.Value == 'Human' then
						_G.Setting_table.Human_Evo_H = true
						return
					elseif game.Players.LocalPlayer.Data.Race.Value == 'Skypiea' then
						_G.Setting_table.Skypiea_Evo_H = true
						return
					elseif game.Players.LocalPlayer.Data.Race.Value == 'Fishman' then
						_G.Setting_table.Fishman_Evo_H = true
						return
					end
				end
				if game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("TalkTrevor","1") == 0 then
					if game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Alchemist","1") ~= -2 then
						if not UIhjdk then
							Text("กำลังทำเผ่ามิงค์วี 1")
							UIhjdk = true
						end
						pcall(function()
							game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Alchemist","1")
							game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Alchemist","2")
						end)
						if not game.Players.LocalPlayer.Backpack:FindFirstChild("Flower 1") and not game.Players.LocalPlayer.Character:FindFirstChild("Flower 1") and game:GetService("Workspace"):FindFirstChild("Flower1") then
							if not YUIk then
								Text("กำลังหา ดอกไม้น้ำเงิน")
								YUIk = true
							end
							repeat wait(1)
								TP2(game:GetService("Workspace"):FindFirstChild("Flower1").CFrame)
							until game.Players.LocalPlayer.Backpack:FindFirstChild("Flower 1") or game.Players.LocalPlayer.Character:FindFirstChild("Flower 1") or not _G.Setting_table.Mink_Evo
						elseif not game.Players.LocalPlayer.Backpack:FindFirstChild("Flower 2") and not game.Players.LocalPlayer.Character:FindFirstChild("Flower 2") and game:GetService("Workspace"):FindFirstChild("Flower2") then
							if not YUIkx then
								Text("กำลังหา ดอกไม้แดง")
								YUIkx = true
							end
							repeat wait(1)
								TP2(game:GetService("Workspace"):FindFirstChild("Flower2").CFrame)
							until game.Players.LocalPlayer.Backpack:FindFirstChild("Flower 2") or game.Players.LocalPlayer.Character:FindFirstChild("Flower 2") or not _G.Setting_table.Mink_Evo
						elseif not game.Players.LocalPlayer.Backpack:FindFirstChild("Flower 3") and not game.Players.LocalPlayer.Character:FindFirstChild("Flower 3") then
							if PO == nil then
								Text("กำลังหา ดอกไม้เหลือง")
								PO = true
							end
							if game:GetService("Workspace").Enemies:FindFirstChild("Marine Captain [Lv. 900]") then
								for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
									if v.Name == "Marine Captain [Lv. 900]" then
										repeat wait(_G.Fast_Delay)
											EquipWeapon(_G.Setting_table.Weapon)
											TP(v.HumanoidRootPart.CFrame*CFrame.new(0,30,0))
											AttackNoCD()
										until v.Humanoid.Health <= 0 or not v.Parent or game.Players.LocalPlayer.Backpack:FindFirstChild("Flower 3") or not _G.Setting_table.Mink_Evo
									end
								end
							else
								TP2(CFrame.new(-2335.2026367188, 79.786659240723, -3245.8674316406))
							end
						elseif game.Players.LocalPlayer.Backpack:FindFirstChild("Flower 3") and game.Players.LocalPlayer.Backpack:FindFirstChild("Flower 1") and game.Players.LocalPlayer.Backpack:FindFirstChild("Flower 2") then
							game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Alchemist","1")
							game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Alchemist","3")
							wait(2)
						else
							if not UHuit then
								Text("รอดอกไม้เกิด")
								TP2(CFrame.new(-379.70889282227, 73.0458984375, 304.84692382813))
								UHuit = true
							end
							wait(2)
						end
					elseif _G.Setting_table.Mink_Evo_V2 ~= true then
						if not UIjfiz then
							Text("กำลังทำเผ่ามิงค์วี 2")
							UIjfiz = true
						end
						if game.Workspace.Enemies:FindFirstChild("Don Swan [Lv. 1000] [Boss]") then
							repeat wait(_G.Fast_Delay)
								EquipWeapon(_G.Setting_table.Weapon)
								TP(game.Workspace.Enemies:FindFirstChild("Don Swan [Lv. 1000] [Boss]").HumanoidRootPart.CFrame*CFrame.new(0,30,0))
								AttackNoCD()
							until not game.Workspace.Enemies:FindFirstChild("Don Swan [Lv. 1000] [Boss]") or game.Workspace.Enemies:FindFirstChild("Don Swan [Lv. 1000] [Boss]").Humanoid.Health <= 0 or not _G.Setting_table.Mink_Evo 
							_G.Setting_table.Mink_Evo_V2 = true
							Update_Setting(getgenv()['MyName'])
						elseif game.ReplicatedStorage:FindFirstChild("Don Swan [Lv. 1000] [Boss]") then
							TP(game.ReplicatedStorage:FindFirstChild("Don Swan [Lv. 1000] [Boss]").HumanoidRootPart.CFrame*CFrame.new(0,30,0))
						else
							Text("รอบอสโดฟาเกิด")
							TP(CFrame.new(2288.802, 15.1870775, 863.034607, 0.99974072, -8.41247214e-08, -0.0227668174, 8.4774733e-08, 1, 2.75850098e-08, 0.0227668174, -2.95079072e-08, 0.99974072))
							wait(10)
						end
					elseif game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Wenlocktoad","1") ~= -2 then
						if not UIjfi then
							Text("กำลังทำเผ่ามิงค์วี 3")
							UIjfi = true
						end
						if not ijoijofdga then
							game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Wenlocktoad","1")
							game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Wenlocktoad","2")
							ijoijofdga = true
						end
						game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Wenlocktoad","1")
                		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Wenlocktoad","3")
						for i,v in pairs(game:GetService("Workspace"):GetChildren()) do
                            if v.Name == "Chest1" and (v.Position-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude < 1500 then
                                repeat wait()
                                    TP2(v.CFrame)
                                until not v.Parent or not _G.Setting_table.Mink_Evo 
                            elseif v.Name == "Chest2" and (v.Position-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude < 1500 then
                                repeat wait()
                                    TP2(v.CFrame)
                                until not v.Parent or not _G.Setting_table.Mink_Evo 
                            elseif New_World then
                                TP2(CFrame.new(-379.70889282227, 73.0458984375, 304.84692382813))
                            end
                        end
					elseif game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Wenlocktoad","1") == -2 then
						if not IUHidm then
							Text("ทำเผ่ามิงค์วี 3 เสร็จสิ้น!")
							IUHidm = true
						end
						if _G.Setting_table.Next_Race then
							_G.Setting_table.Mink_Evo_H = true
							Update_Setting(getgenv()['MyName'])
						end
					end
				else
					Text("ประตูโดฟายังไม่เปิด\nไม่สามารถทำเผ่าได้")
					wait(5)
				end
			elseif _G.Setting_table.Human_Evo and not _G.Setting_table.Human_Evo_H and game.Players.LocalPlayer.Data.Race.Value == 'Human' then
				if game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("TalkTrevor","1") == 0 then
					if game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Alchemist","1") ~= -2 then
						if not UIhjdkh then
							Text("กำลังทำเผ่าคนวี 1")
							UIhjdkh = true
						end
						pcall(function()
							game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Alchemist","1")
							game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Alchemist","2")
						end)
						if not game.Players.LocalPlayer.Backpack:FindFirstChild("Flower 1") and not game.Players.LocalPlayer.Character:FindFirstChild("Flower 1") and game:GetService("Workspace"):FindFirstChild("Flower1") then
							if not YUIks then
								Text("กำลังหา ดอกไม้น้ำเงิน")
								YUIks = true
							end
							repeat wait(1)
								TP2(game:GetService("Workspace"):FindFirstChild("Flower1").CFrame)
							until game.Players.LocalPlayer.Backpack:FindFirstChild("Flower 1") or game.Players.LocalPlayer.Character:FindFirstChild("Flower 1") or not _G.Setting_table.Human_Evo
						elseif not game.Players.LocalPlayer.Backpack:FindFirstChild("Flower 2") and not game.Players.LocalPlayer.Character:FindFirstChild("Flower 2") and game:GetService("Workspace"):FindFirstChild("Flower2") then
							if not YUIkxz then
								Text("กำลังหา ดอกไม้แดง")
								YUIkxz = true
							end
							repeat wait(1)
								TP2(game:GetService("Workspace"):FindFirstChild("Flower2").CFrame)
							until game.Players.LocalPlayer.Backpack:FindFirstChild("Flower 2") or game.Players.LocalPlayer.Character:FindFirstChild("Flower 2") or not _G.Setting_table.Human_Evo
						elseif not game.Players.LocalPlayer.Backpack:FindFirstChild("Flower 3") and not game.Players.LocalPlayer.Character:FindFirstChild("Flower 3") then
							if POs == nil then
								Text("กำลังหา ดอกไม้เหลือง")
								POs = true
							end
							if game:GetService("Workspace").Enemies:FindFirstChild("Marine Captain [Lv. 900]") then
								for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
									if v.Name == "Marine Captain [Lv. 900]" then
										repeat wait(_G.Fast_Delay)
											EquipWeapon(_G.Setting_table.Weapon)
											TP(v.HumanoidRootPart.CFrame*CFrame.new(0,30,0))
											AttackNoCD()
										until v.Humanoid.Health <= 0 or not v.Parent or game.Players.LocalPlayer.Backpack:FindFirstChild("Flower 3") or not _G.Setting_table.Human_Evo
									end
								end
							else
								TP2(CFrame.new(-2335.2026367188, 79.786659240723, -3245.8674316406))
							end
						elseif game.Players.LocalPlayer.Backpack:FindFirstChild("Flower 3") and game.Players.LocalPlayer.Backpack:FindFirstChild("Flower 1") and game.Players.LocalPlayer.Backpack:FindFirstChild("Flower 2") then
							game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Alchemist","1")
							game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Alchemist","3")
							wait(2)
						else
							if not UHuits then
								Text("รอดอกไม้เกิด")
								TP2(CFrame.new(-379.70889282227, 73.0458984375, 304.84692382813))
								UHuits = true
							end
							wait(2)
						end
					elseif _G.Setting_table.Human_Evo_V2 ~= true then
						if not UIjfize then
							Text("กำลังทำเผ่าคนวี 2")
							UIjfize = true
						end
						if game.Workspace.Enemies:FindFirstChild("Don Swan [Lv. 1000] [Boss]") then
							repeat wait(_G.Fast_Delay)
								EquipWeapon(_G.Setting_table.Weapon)
								TP(game.Workspace.Enemies:FindFirstChild("Don Swan [Lv. 1000] [Boss]").HumanoidRootPart.CFrame*CFrame.new(0,30,0))
								AttackNoCD()
							until not game.Workspace.Enemies:FindFirstChild("Don Swan [Lv. 1000] [Boss]") or game.Workspace.Enemies:FindFirstChild("Don Swan [Lv. 1000] [Boss]").Humanoid.Health <= 0 or not _G.Setting_table.Human_Evo 
							_G.Setting_table.Human_Evo_V2 = true
							Update_Setting(getgenv()['MyName'])
						elseif game.ReplicatedStorage:FindFirstChild("Don Swan [Lv. 1000] [Boss]") then
							TP(game.ReplicatedStorage:FindFirstChild("Don Swan [Lv. 1000] [Boss]").HumanoidRootPart.CFrame*CFrame.new(0,30,0))
						else
							Text("รอบอสโดฟาเกิด")
							TP(CFrame.new(2288.802, 15.1870775, 863.034607, 0.99974072, -8.41247214e-08, -0.0227668174, 8.4774733e-08, 1, 2.75850098e-08, 0.0227668174, -2.95079072e-08, 0.99974072))
							wait(10)
						end
					elseif game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Wenlocktoad","1") ~= -2 then
						if not UIjfie then
							Text("กำลังทำเผ่าคนวี 3")
							UIjfie = true
						end
						if not ijoijofdga then
							game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Wenlocktoad","1")
							game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Wenlocktoad","2")
							ijoijofdga = true
						end
						game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Wenlocktoad","1")
                		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Wenlocktoad","3")
						if game.Workspace.Enemies:FindFirstChild("Fajita [Lv. 925] [Boss]") then
							for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
								if v.Name == "Fajita [Lv. 925] [Boss]" then
									repeat twait(_G.Fast_Delay)
										EquipWeapon(_G.Setting_table.Weapon)
										TP(v.HumanoidRootPart.CFrame*CFrame.new(0,30,0))
										AttackNoCD()
									until v.Humanoid.Health <= 0 or not v.Parent or not _G.Setting_table.Human_Evo
								end
							end
						elseif game.ReplicatedStorage:FindFirstChild("Fajita [Lv. 925] [Boss]") then
							TP(game.ReplicatedStorage:FindFirstChild("Fajita [Lv. 925] [Boss]").HumanoidRootPart.CFrame*CFrame.new(0,30,0))
						elseif game.Workspace.Enemies:FindFirstChild("Jeremy [Lv. 850] [Boss]") then
							for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
								if v.Name == "Jeremy [Lv. 850] [Boss]" then
									repeat wait(_G.Fast_Delay)
										EquipWeapon(_G.Setting_table.Weapon)
										TP(v.HumanoidRootPart.CFrame*CFrame.new(0,30,0))
										AttackNoCD()
									until v.Humanoid.Health <= 0 or not v.Parent or not _G.Setting_table.Human_Evo
								end
							end
						elseif game.ReplicatedStorage:FindFirstChild("Jeremy [Lv. 850] [Boss]") then
							TP(game.ReplicatedStorage:FindFirstChild("Jeremy [Lv. 850] [Boss]").HumanoidRootPart.CFrame*CFrame.new(0,30,0))
						elseif game.Workspace.Enemies:FindFirstChild("Diamond [Lv. 750] [Boss]") then
							for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
								if v.Name == "Diamond [Lv. 750] [Boss]" then
									repeat wait(_G.Fast_Delay)
										EquipWeapon(_G.Setting_table.Weapon)
										TP(v.HumanoidRootPart.CFrame*CFrame.new(0,30,0))
										AttackNoCD()
									until v.Humanoid.Health <= 0 or not v.Parent or not _G.Setting_table.Human_Evo
								end
							end
						elseif game.ReplicatedStorage:FindFirstChild("Diamond [Lv. 750] [Boss]") then
							TP(game.ReplicatedStorage:FindFirstChild("Diamond [Lv. 750] [Boss]").HumanoidRootPart.CFrame*CFrame.new(0,30,0))
						else
							if not IJOijogr then
								TP2(CFrame.new(-379.70889282227, 73.0458984375, 304.84692382813))
								IJOijogr = true
							end
							Text("รอบอสเกิด 5 - 15นาที")
							wait(10)
						end
					elseif game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Wenlocktoad","1") == -2 then
						if not IUHidmr then
							Text("ทำเผ่าคนวี 3 เสร็จสิ้น!")
							IUHidmr = true
						end
						if _G.Setting_table.Next_Race then
							_G.Setting_table.Human_Evo_H = true
							Update_Setting(getgenv()['MyName'])
						end
					end
				else
					Text("ประตูโดฟายังไม่เปิด\nไม่สามารถทำเผ่าได้")
					wait(5)
				end
			elseif _G.Setting_table.Skypiea_Evo and not _G.Setting_table.Skypiea_Evo_H and game.Players.LocalPlayer.Data.Race.Value == 'Skypiea' then
				if game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("TalkTrevor","1") == 0 then
					if game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Alchemist","1") ~= -2 then
						if not UIhjdkhz then
							Text("กำลังทำเผ่าปีกวี 1")
							UIhjdkhz = true
						end
						pcall(function()
							game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Alchemist","1")
							game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Alchemist","2")
						end)
						if not game.Players.LocalPlayer.Backpack:FindFirstChild("Flower 1") and not game.Players.LocalPlayer.Character:FindFirstChild("Flower 1") and game:GetService("Workspace"):FindFirstChild("Flower1") then
							if not YUIksz then
								Text("กำลังหา ดอกไม้น้ำเงิน")
								YUIksz = true
							end
							repeat wait(1)
								TP2(game:GetService("Workspace"):FindFirstChild("Flower1").CFrame)
							until game.Players.LocalPlayer.Backpack:FindFirstChild("Flower 1") or game.Players.LocalPlayer.Character:FindFirstChild("Flower 1") or not _G.Setting_table.Skypiea_Evo
						elseif not game.Players.LocalPlayer.Backpack:FindFirstChild("Flower 2") and not game.Players.LocalPlayer.Character:FindFirstChild("Flower 2") and game:GetService("Workspace"):FindFirstChild("Flower2") then
							if not YUIkxzx then
								Text("กำลังหา ดอกไม้แดง")
								YUIkxzx = true
							end
							repeat wait(1)
								TP2(game:GetService("Workspace"):FindFirstChild("Flower2").CFrame)
							until game.Players.LocalPlayer.Backpack:FindFirstChild("Flower 2") or game.Players.LocalPlayer.Character:FindFirstChild("Flower 2") or not _G.Setting_table.Skypiea_Evo
						elseif not game.Players.LocalPlayer.Backpack:FindFirstChild("Flower 3") and not game.Players.LocalPlayer.Character:FindFirstChild("Flower 3") then
							if POsz == nil then
								Text("กำลังหา ดอกไม้เหลือง")
								POsz = true
							end
							if game:GetService("Workspace").Enemies:FindFirstChild("Marine Captain [Lv. 900]") then
								for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
									if v.Name == "Marine Captain [Lv. 900]" then
										repeat wait(_G.Fast_Delay)
											EquipWeapon(_G.Setting_table.Weapon)
											TP(v.HumanoidRootPart.CFrame*CFrame.new(0,30,0))
											AttackNoCD()
										until v.Humanoid.Health <= 0 or not v.Parent or game.Players.LocalPlayer.Backpack:FindFirstChild("Flower 3") or not _G.Setting_table.Skypiea_Evo
									end
								end
							else
								TP2(CFrame.new(-2335.2026367188, 79.786659240723, -3245.8674316406))
							end
						elseif game.Players.LocalPlayer.Backpack:FindFirstChild("Flower 3") and game.Players.LocalPlayer.Backpack:FindFirstChild("Flower 1") and game.Players.LocalPlayer.Backpack:FindFirstChild("Flower 2") then
							game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Alchemist","1")
							game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Alchemist","3")
							wait(2)
						else
							if not UHuitsz then
								Text("รอดอกไม้เกิด")
								TP2(CFrame.new(-379.70889282227, 73.0458984375, 304.84692382813))
								UHuitsz = true
							end
							wait(2)
						end
					elseif _G.Setting_table.Skypiea_Evo_V2 ~= true then
						if not UIjfizez then
							Text("กำลังทำเผ่าปีกวี 2")
							UIjfizez = true
						end
						if game.Workspace.Enemies:FindFirstChild("Don Swan [Lv. 1000] [Boss]") then
							repeat wait(_G.Fast_Delay)
								EquipWeapon(_G.Setting_table.Weapon)
								TP(game.Workspace.Enemies:FindFirstChild("Don Swan [Lv. 1000] [Boss]").HumanoidRootPart.CFrame*CFrame.new(0,30,0))
								AttackNoCD()
							until not game.Workspace.Enemies:FindFirstChild("Don Swan [Lv. 1000] [Boss]") or game.Workspace.Enemies:FindFirstChild("Don Swan [Lv. 1000] [Boss]").Humanoid.Health <= 0 or not _G.Setting_table.Skypiea_Evo 
							_G.Setting_table.Skypiea_Evo_V2 = true
							Update_Setting(getgenv()['MyName'])
						elseif game.ReplicatedStorage:FindFirstChild("Don Swan [Lv. 1000] [Boss]") then
							TP(game.ReplicatedStorage:FindFirstChild("Don Swan [Lv. 1000] [Boss]").HumanoidRootPart.CFrame*CFrame.new(0,30,0))
						else
							Text("รอบอสโดฟาเกิด")
							TP(CFrame.new(2288.802, 15.1870775, 863.034607, 0.99974072, -8.41247214e-08, -0.0227668174, 8.4774733e-08, 1, 2.75850098e-08, 0.0227668174, -2.95079072e-08, 0.99974072))
							wait(10)
						end
					elseif game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Wenlocktoad","1") ~= -2 then
						if not UIjfiez then
							Text("กำลังทำเผ่าปีกวี 3")
							UIjfiez = true
						end
						if not ijoijofdga then
							game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Wenlocktoad","1")
							game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Wenlocktoad","2")
							ijoijofdga = true
						end
						game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Wenlocktoad","1")
                		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Wenlocktoad","3")
						_G.Select_Player = nil
						Check_Race_Skypiea()
						if _G.Select_Player ~= nil then
							print(_G.Select_Player)
							repeat wait(_G.Fast_Delay)
								EquipWeapon(_G.Setting_table.Weapon)
								TP(game.Players:FindFirstChild(_G.Select_Player).Character.HumanoidRootPart.CFrame*CFrame.new(0,0,2))
								AttackNoCD()
							until game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Wenlocktoad","1") == -2 or game.Players:FindFirstChild(_G.Select_Player).Character.Humanoid.Health <= 0 or not game.Players:FindFirstChild(_G.Select_Player) or not _G.Setting_table.Skypiea_Evo
						elseif _G.Setting_table.Race_Hop then
							Text("ไม่มีคนที่มีเผ่าสกายเปีย\nในโลกนี้เลย")
							HopServer()
							wait(50)
						else
							Text("ไม่มีคนที่มีเผ่าสกายเปีย\nในโลกนี้เลย")
							wait(7)
						end
					elseif game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Wenlocktoad","1") == -2 then
						if not IUHidmrz then
							Text("ทำเผ่าปีกวี 3 เสร็จสิ้น!")
							IUHidmrz = true
						end
						if _G.Setting_table.Next_Race then
							_G.Setting_table.Skypiea_Evo_H = true
							Update_Setting(getgenv()['MyName'])
						end
					end
				else
					Text("ประตูโดฟายังไม่เปิด\nไม่สามารถทำเผ่าได้")
					wait(5)
				end
			elseif _G.Setting_table.Fishman_Evo and not _G.Setting_table.Fishman_Evo_H and game.Players.LocalPlayer.Data.Race.Value == 'Fishman' then
				if game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("TalkTrevor","1") == 0 then
					if game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Alchemist","1") ~= -2 then
						if not UIhjdkhzt then
							Text("กำลังทำเผ่าเงือกวี 1")
							UIhjdkhzt = true
						end
						pcall(function()
							game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Alchemist","1")
							game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Alchemist","2")
						end)
						if not game.Players.LocalPlayer.Backpack:FindFirstChild("Flower 1") and not game.Players.LocalPlayer.Character:FindFirstChild("Flower 1") and game:GetService("Workspace"):FindFirstChild("Flower1") then
							if not YUIkszt then
								Text("กำลังหา ดอกไม้น้ำเงิน")
								YUIkszt = true
							end
							repeat wait(1)
								TP2(game:GetService("Workspace"):FindFirstChild("Flower1").CFrame)
							until game.Players.LocalPlayer.Backpack:FindFirstChild("Flower 1") or game.Players.LocalPlayer.Character:FindFirstChild("Flower 1") or not _G.Setting_table.Fishman_Evo
						elseif not game.Players.LocalPlayer.Backpack:FindFirstChild("Flower 2") and not game.Players.LocalPlayer.Character:FindFirstChild("Flower 2") and game:GetService("Workspace"):FindFirstChild("Flower2") then
							if not YUIkxzxt then
								Text("กำลังหา ดอกไม้แดง")
								YUIkxzxt = true
							end
							repeat wait(1)
								TP2(game:GetService("Workspace"):FindFirstChild("Flower2").CFrame)
							until game.Players.LocalPlayer.Backpack:FindFirstChild("Flower 2") or game.Players.LocalPlayer.Character:FindFirstChild("Flower 2") or not _G.Setting_table.Fishman_Evo
						elseif not game.Players.LocalPlayer.Backpack:FindFirstChild("Flower 3") and not game.Players.LocalPlayer.Character:FindFirstChild("Flower 3") then
							if POszt == nil then
								Text("กำลังหา ดอกไม้เหลือง")
								POszt = true
							end
							if game:GetService("Workspace").Enemies:FindFirstChild("Marine Captain [Lv. 900]") then
								for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
									if v.Name == "Marine Captain [Lv. 900]" then
										repeat wait(_G.Fast_Delay)
											EquipWeapon(_G.Setting_table.Weapon)
											TP(v.HumanoidRootPart.CFrame*CFrame.new(0,30,0))
											AttackNoCD()
										until v.Humanoid.Health <= 0 or not v.Parent or game.Players.LocalPlayer.Backpack:FindFirstChild("Flower 3") or not _G.Setting_table.Fishman_Evo
									end
								end
							else
								TP2(CFrame.new(-2335.2026367188, 79.786659240723, -3245.8674316406))
							end
						elseif game.Players.LocalPlayer.Backpack:FindFirstChild("Flower 3") and game.Players.LocalPlayer.Backpack:FindFirstChild("Flower 1") and game.Players.LocalPlayer.Backpack:FindFirstChild("Flower 2") then
							game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Alchemist","1")
							game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Alchemist","3")
							wait(2)
						else
							if not UHuitszt then
								Text("รอดอกไม้เกิด")
								TP2(CFrame.new(-379.70889282227, 73.0458984375, 304.84692382813))
								UHuitszt = true
							end
							wait(2)
						end
					elseif _G.Setting_table.Fishman_Evo_V2 ~= true then
						if not UIjfizezt then
							Text("กำลังทำเผ่าเงือกวี 2")
							UIjfizezt = true
						end
						if game.Workspace.Enemies:FindFirstChild("Don Swan [Lv. 1000] [Boss]") then
							repeat wait(_G.Fast_Delay)
								EquipWeapon(_G.Setting_table.Weapon)
								TP(game.Workspace.Enemies:FindFirstChild("Don Swan [Lv. 1000] [Boss]").HumanoidRootPart.CFrame*CFrame.new(0,30,0))
								AttackNoCD()
							until not game.Workspace.Enemies:FindFirstChild("Don Swan [Lv. 1000] [Boss]") or game.Workspace.Enemies:FindFirstChild("Don Swan [Lv. 1000] [Boss]").Humanoid.Health <= 0 or not _G.Setting_table.Fishman_Evo 
							_G.Setting_table.Fishman_Evo_V2 = true
							Update_Setting(getgenv()['MyName'])
						elseif game.ReplicatedStorage:FindFirstChild("Don Swan [Lv. 1000] [Boss]") then
							TP(game.ReplicatedStorage:FindFirstChild("Don Swan [Lv. 1000] [Boss]").HumanoidRootPart.CFrame*CFrame.new(0,30,0))
						else
							Text("รอบอสโดฟาเกิด")
							TP(CFrame.new(2288.802, 15.1870775, 863.034607, 0.99974072, -8.41247214e-08, -0.0227668174, 8.4774733e-08, 1, 2.75850098e-08, 0.0227668174, -2.95079072e-08, 0.99974072))
							wait(10)
						end
					elseif game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Wenlocktoad","1") ~= -2 then
						if not UIjfiezt then
							Text("กำลังทำเผ่าเงือกวี 3")
							UIjfiezt = true
						end
						if not ijoijofdg then
							game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Wenlocktoad","1")
							game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Wenlocktoad","2")
							ijoijofdg = true
						end
						for i,v in pairs(game:GetService("Workspace").SeaBeasts:GetChildren()) do
							if v:FindFirstChild("HumanoidRootPart") then
								_G.Ping = true
								repeat wait(_G.Fast_Delay)
									EquipWeapon(_G.Setting_table.Weapon)
									TP(v.HumanoidRootPart.CFrame * CFrame.new(0,30,0))
									AttackNoCD()
								until not v.Parent or not _G.Setting_table.Fishman_Evo or game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Wenlocktoad","1") == -2
							end
						end
						Text("เจ้าทะเลยังไม่เกิด")
						if _G.Setting_table.Race_Hop and not _G.Ping then
							HopServer()
							wait(50)
						end
						wait(9)
					elseif game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Wenlocktoad","1") == -2 then
						if not IUHidmrzt then
							Text("ทำเผ่าเงือกวี 3 เสร็จสิ้น!")
							IUHidmrzt = true
						end
						if _G.Setting_table.Next_Race then
							_G.Setting_table.Fishman_Evo_H = true
							Update_Setting(getgenv()['MyName'])
						end
					end
				else
					Text("ประตูโดฟายังไม่เปิด\nไม่สามารถทำเผ่าได้")
					wait(5)
				end
			elseif _G.Setting_table.Next_Race and _G.Setting_table.Mink_Evo and not _G.Setting_table.Mink_Evo_H and game.Players.LocalPlayer.Data.Race.Value ~= 'Mink' then
				local FG = game:GetService("Players").LocalPlayer.Data.Fragments.Value
				if FG >= 3000 then
					local args = {
						[1] = "BlackbeardReward",
						[2] = "Reroll",
						[3] = "2"
					}
					
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
					wait(5)
				elseif not Mix_Farm then
					_G.Have_Fruit = nil
					Raid_FG()
				end
			elseif _G.Setting_table.Next_Race and _G.Setting_table.Human_Evo and not _G.Setting_table.Human_Evo_H and game.Players.LocalPlayer.Data.Race.Value ~= 'Human' then
				local FG = game:GetService("Players").LocalPlayer.Data.Fragments.Value
				if FG >= 3000 then
					local args = {
						[1] = "BlackbeardReward",
						[2] = "Reroll",
						[3] = "2"
					}
					
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
					wait(5)
				elseif not Mix_Farm then
					_G.Have_Fruit = nil
					Raid_FG()
				end
			elseif _G.Setting_table.Next_Race and _G.Setting_table.Skypiea_Evo and not _G.Setting_table.Skypiea_Evo_H and game.Players.LocalPlayer.Data.Race.Value ~= 'Skypiea' then
				local FG = game:GetService("Players").LocalPlayer.Data.Fragments.Value
				if FG >= 3000 then
					local args = {
						[1] = "BlackbeardReward",
						[2] = "Reroll",
						[3] = "2"
					}
					
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
					wait(5)
				elseif not Mix_Farm then
					_G.Have_Fruit = nil
					Raid_FG()
				end
			elseif _G.Setting_table.Next_Race and _G.Setting_table.Fishman_Evo and not _G.Setting_table.Fishman_Evo_H and game.Players.LocalPlayer.Data.Race.Value ~= 'Fishman' then
				local FG = game:GetService("Players").LocalPlayer.Data.Fragments.Value
				if FG >= 3000 then
					local args = {
						[1] = "BlackbeardReward",
						[2] = "Reroll",
						[3] = "2"
					}
					
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
					wait(5)
				elseif not Mix_Farm then
					_G.Have_Fruit = nil
					Raid_FG()
				end
			elseif _G.Setting_table.Mink_Evo_H and _G.Setting_table.Fishman_Evo_H and _G.Setting_table.Skypiea_Evo_H and _G.Setting_table.Human_Evo_H then
				Text("อีโวเผ่าขั้น 3 ครบทั้ง4เผ่าแล้ว")
				wait(10)
			else
				wait(2)
			end
		end)
	end
end)

function Check_Race_Skypiea()
	for i,v in pairs(game.Players:GetChildren()) do
		if v.Name ~= game.Players.LocalPlayer.Name and tostring(v.Data.Race.Value) == "Skypiea" then
			print(v.Name)
			_G.Select_Player = v.Name
			return
		end
	end
end

local QG = Quest_Tab:CreateSection({
    Name = "Gun",
    Side = "Right"
})
QG:AddToggle({
    Name = "Auto Acidum Rifle",
    _G.Setting_table.Auto_Acidum_Rifle,
    Callback = function(vu)
	Auto_Acidum_Rifle = vu
	_G.Setting_table.Auto_Acidum_Rifle = vu
	Update_Setting(getgenv()['MyName'])
end})
spawn(function()
	while wait(.5) do
		pcall(function()
			if Auto_Acidum_Rifle then
				if not Mix_Farm or Auto_Acidum_Rifle_Farm then
					if game.Workspace.Enemies:FindFirstChild("Core") or game.ReplicatedStorage:FindFirstChild("Core") then
						Mix_Farm = true
						Auto_Acidum_Rifle_Farm = true
						if game.Workspace.Enemies:FindFirstChild("Core") then
							game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("SetSpawnPoint")
							for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
								if v.Name == "Core" then
									repeat wait(_G.Fast_Delay)
										EquipWeapon(_G.Setting_table.Weapon)
										TP(CFrame.new(402.404296875, 182.53373718262, -414.73394775391))
										AttackNoCD()
									until not game.Workspace.Enemies:FindFirstChild("Core") or not Auto_Acidum_Rifle
									Mix_Farm = nil
									Auto_Acidum_Rifle_Farm = nil
								end
							end
						else
							TP(CFrame.new(402.404296875, 182.53373718262, -414.73394775391))
						end
					elseif _G.Setting_table.Auto_Acidum_Rifle_Hop then
						wait(5)
						if not game.Workspace.Enemies:FindFirstChild("Core") and not game.ReplicatedStorage:FindFirstChild("Core") then
							HopServer()
							wait(50)
						end
					elseif Auto_Acidum_Rifle_Farm then
						Auto_Acidum_Rifle_Farm = nil
						Mix_Farm = nil
					end
				end
			else
				wait(2)
			end
		end)
	end
end)
QG:AddToggle({
    Name = "Auto Serpent Bow",
    _G.Setting_table.Auto_Serpent_Bow,
    Callback = function(vu)
	Auto_Serpent_Bow = vu
	_G.Setting_table.Auto_Serpent_Bow = vu
	Update_Setting(getgenv()['MyName'])
end})
spawn(function()
	while wait(.5) do
		pcall(function()
			if Auto_Serpent_Bow then
				if not Mix_Farm or Auto_Serpent_Bow_Farm then
					if game.Workspace.Enemies:FindFirstChild("Island Empress [Lv. 1675] [Boss]") or game.ReplicatedStorage:FindFirstChild("Island Empress [Lv. 1675] [Boss]") then
						Auto_Serpent_Bow_Farm = true
						Mix_Farm = true
						if game.Workspace.Enemies:FindFirstChild("Island Empress [Lv. 1675] [Boss]") then
							game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("SetSpawnPoint")
							for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
								if v.Name == "Island Empress [Lv. 1675] [Boss]" and v.Humanoid.Health > 0 then
									repeat wait(_G.Fast_Delay)
										EquipWeapon(_G.Setting_table.Weapon)
										TP(v.HumanoidRootPart.CFrame*CFrame.new(0,30,0))
										AttackNoCD()
									until v.Humanoid.Health <= 0 or not v.Parent or not Auto_Serpent_Bow
								end
							end
						elseif game.ReplicatedStorage:FindFirstChild("Island Empress [Lv. 1675] [Boss]") then
							TP(game.ReplicatedStorage:FindFirstChild("Island Empress [Lv. 1675] [Boss]").HumanoidRootPart.CFrame*CFrame.new(0,30,0))
						end
					elseif _G.Setting_table.Auto_Serpent_Bow_Hop then
						wait(5)
						if not game.Workspace.Enemies:FindFirstChild("Island Empress [Lv. 1675] [Boss]") and not game.ReplicatedStorage:FindFirstChild("Island Empress [Lv. 1675] [Boss]") then
							HopServer()
							wait(50)
						end
					elseif Auto_Serpent_Bow_Farm then
						Auto_Serpent_Bow_Farm = nil
						Mix_Farm = nil
					end
				end
			else
				wait(2)
			end
		end)
	end
end)

QG:AddLabel("Accessory")
QG:AddToggle({
    Name = "Auto Dark Coat",
    _G.Setting_table.Auto_Dark_Coat,
    Callback = function(vu)
	Auto_Dark_Coat = vu
	_G.Setting_table.Auto_Dark_Coat = vu
	Update_Setting(getgenv()['MyName'])
end})
function Chest_100()
	for i,v in pairs(game:GetService("Workspace"):GetChildren()) do
		if v.Name == "Chest1" and (v.Position-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 100 then
			_G.Chest_100 = v
			return
		elseif v.Name == "Chest2" and (v.Position-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 100 then
			_G.Chest_100 = v
			return
		end
	end
end
function Chest_500()
	for i,v in pairs(game:GetService("Workspace"):GetChildren()) do
		if v.Name == "Chest1" and (v.Position-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 500 then
			_G.Chest_500 = v
			return
		elseif v.Name == "Chest2" and (v.Position-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 500 then
			_G.Chest_500 = v
			return
		end
	end
end
function Chest_1000()
	for i,v in pairs(game:GetService("Workspace"):GetChildren()) do
		if v.Name == "Chest1" and (v.Position-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 1000 then
			_G.Chest_1000 = v
			return
		elseif v.Name == "Chest2" and (v.Position-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 1000 then
			_G.Chest_1000 = v
			return
		end
	end
end
function Chest_1500()
	for i,v in pairs(game:GetService("Workspace"):GetChildren()) do
		if v.Name == "Chest1" and (v.Position-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 1500 then
			_G.Chest_1500 = v
			return
		elseif v.Name == "Chest2" and (v.Position-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 1500 then
			_G.Chest_1500 = v
			return
		end
	end
end
function Chest_2000()
	for i,v in pairs(game:GetService("Workspace"):GetChildren()) do
		if v.Name == "Chest1" and (v.Position-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 2000 then
			_G.Chest_2000 = v
			return
		elseif v.Name == "Chest2" and (v.Position-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 2000 then
			_G.Chest_2000 = v
			return
		end
	end
end
function Chest_2500()
	for i,v in pairs(game:GetService("Workspace"):GetChildren()) do
		if v.Name == "Chest1" and (v.Position-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 2500 then
			_G.Chest_2500 = v
			return
		elseif v.Name == "Chest2" and (v.Position-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 2500 then
			_G.Chest_2500 = v
			return
		end
	end
end
function Chest_3500()
	for i,v in pairs(game:GetService("Workspace"):GetChildren()) do
		if v.Name == "Chest1" and (v.Position-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 3500 then
			_G.Chest_3500 = v
			return
		elseif v.Name == "Chest2" and (v.Position-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 3500 then
			_G.Chest_3500 = v
			return
		end
	end
end
function Chest_4500()
	for i,v in pairs(game:GetService("Workspace"):GetChildren()) do
		if v.Name == "Chest1" and (v.Position-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 4500 then
			_G.Chest_4500 = v
			return
		elseif v.Name == "Chest2" and (v.Position-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 4500 then
			_G.Chest_4500 = v
			return
		end
	end
end
function Chest_5500()
	for i,v in pairs(game:GetService("Workspace"):GetChildren()) do
		if v.Name == "Chest1" and (v.Position-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 5500 then
			_G.Chest_5500 = v
			return
		elseif v.Name == "Chest2" and (v.Position-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 5500 then
			_G.Chest_5500 = v
			return
		end
	end
end
function Chest_6500()
	for i,v in pairs(game:GetService("Workspace"):GetChildren()) do
		if v.Name == "Chest1" and (v.Position-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 6500 then
			_G.Chest_6500 = v
			return
		elseif v.Name == "Chest2" and (v.Position-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 6500 then
			_G.Chest_6500 = v
			return
		end
	end
end
function Chest_7500()
	for i,v in pairs(game:GetService("Workspace"):GetChildren()) do
		if v.Name == "Chest1" and (v.Position-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 7500 then
			_G.Chest_7500 = v
			return
		elseif v.Name == "Chest2" and (v.Position-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 7500 then
			_G.Chest_7500 = v
			return
		end
	end
end
function Chest_9500()
	for i,v in pairs(game:GetService("Workspace"):GetChildren()) do
		if v.Name == "Chest1" and (v.Position-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 9500 then
			_G.Chest_9500 = v
			return
		elseif v.Name == "Chest2" and (v.Position-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 9500 then
			_G.Chest_9500 = v
			return
		end
	end
end
function Chest_10500()
	for i,v in pairs(game:GetService("Workspace"):GetChildren()) do
		if v.Name == "Chest1" and (v.Position-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 10500 then
			_G.Chest_10500 = v
			return
		elseif v.Name == "Chest2" and (v.Position-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 10500 then
			_G.Chest_10500 = v
			return
		end
	end
end
function Chest_12500()
	for i,v in pairs(game:GetService("Workspace"):GetChildren()) do
		if v.Name == "Chest1" and (v.Position-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 12500 then
			_G.Chest_12500 = v
			return
		elseif v.Name == "Chest2" and (v.Position-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 12500 then
			_G.Chest_12500 = v
			return
		end
	end
end
function Chest_15500()
	for i,v in pairs(game:GetService("Workspace"):GetChildren()) do
		if v.Name == "Chest1" and (v.Position-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 15500 then
			_G.Chest_15500 = v
			return
		elseif v.Name == "Chest2" and (v.Position-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 15500 then
			_G.Chest_15500 = v
			return
		end
	end
end
function Chest_17500()
	for i,v in pairs(game:GetService("Workspace"):GetChildren()) do
		if v.Name == "Chest1" and (v.Position-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 17500 then
			_G.Chest_17500 = v
			return
		elseif v.Name == "Chest2" and (v.Position-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 17500 then
			_G.Chest_17500 = v
			return
		end
	end
end

QG:AddToggle({
    Name = "Auto Swan Glass",
    _G.Setting_table.Auto_Swan_Glass,
    Callback = function(vu)
	Auto_Swan_Glass = vu
	_G.Setting_table.Auto_Swan_Glass = vu
	Update_Setting(getgenv()['MyName'])
end})
spawn(function()
	while wait(.5) do
		pcall(function()
			if Auto_Swan_Glass then
				if not Mix_Farm or Auto_Swan_Glass_Farm then
					if game.Workspace.Enemies:FindFirstChild("Don Swan [Lv. 1000] [Boss]") or game.ReplicatedStorage:FindFirstChild("Don Swan [Lv. 1000] [Boss]") then
						Auto_Swan_Glass_Farm = true
						Mix_Farm = true
						if game.Workspace.Enemies:FindFirstChild("Don Swan [Lv. 1000] [Boss]") then
							game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("SetSpawnPoint")
							for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
								if v.Name == "Don Swan [Lv. 1000] [Boss]" and v.Humanoid.Health > 0 then
									repeat wait(_G.Fast_Delay)
										EquipWeapon(_G.Setting_table.Weapon)
										TP(v.HumanoidRootPart.CFrame*CFrame.new(0,30,0))
										AttackNoCD()
									until v.Humanoid.Health <= 0 or not v.Parent or not Auto_Swan_Glass
								end
							end
						elseif game.ReplicatedStorage:FindFirstChild("Don Swan [Lv. 1000] [Boss]") then
							TP(game.ReplicatedStorage:FindFirstChild("Don Swan [Lv. 1000] [Boss]").HumanoidRootPart.CFrame*CFrame.new(0,30,0))
						end
					elseif _G.Setting_table.Auto_Swan_Glass_Hop then
						wait(5)
						if not game.Workspace.Enemies:FindFirstChild("Don Swan [Lv. 1000] [Boss]") and not game.ReplicatedStorage:FindFirstChild("Don Swan [Lv. 1000] [Boss]") then
							HopServer()
							wait(50)
						end
					elseif Auto_Swan_Glass_Farm then
						Auto_Swan_Glass_Farm = nil
						Mix_Farm = nil
					end
				end
			else
				wait(3)
			end
		end)
	end
end)
QG:AddToggle({
    Name = "Auto Pale Scarf",
    _G.Setting_table.Auto_Pale_Scarf,
    Callback = function(vu)
	Auto_Pale_Scarf = vu
	_G.Setting_table.Auto_Pale_Scarf = vu
	Update_Setting(getgenv()['MyName'])
end})
spawn(function()
	while wait(.5) do
		pcall(function()
			if Auto_Pale_Scarf then
				if game.Workspace.Enemies:FindFirstChild("Cake Prince [Lv. 2300] [Raid Boss]") or game.ReplicatedStorage:FindFirstChild("Cake Prince [Lv. 2300] [Raid Boss]") then
					if game.Workspace.Enemies:FindFirstChild("Cake Prince [Lv. 2300] [Raid Boss]") then
						game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("SetSpawnPoint")
						for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
							if v.Name == "Cake Prince [Lv. 2300] [Raid Boss]" and v.Humanoid.Health > 0 then
								if v.Humanoid:FindFirstChild("Animator") then
									v.Humanoid.Animator:Destroy()
								end
								repeat wait(_G.Fast_Delay)
									EquipWeapon(_G.Setting_table.Weapon)
									TP(v.HumanoidRootPart.CFrame*CFrame.new(0,30,0))
									AttackNoCD()
								until v.Humanoid.Health <= 0 or not v.Parent or not Auto_Pale_Scarf
							end
						end
					elseif game.ReplicatedStorage:FindFirstChild("Cake Prince [Lv. 2300] [Raid Boss]") then
						TP(game.ReplicatedStorage:FindFirstChild("Cake Prince [Lv. 2300] [Raid Boss]").HumanoidRootPart.CFrame*CFrame.new(0,30,0))
					end
				elseif _G.Setting_table.Auto_Pale_Scarf_Hop then
					wait(5)
					if not game.Workspace.Enemies:FindFirstChild("Cake Prince [Lv. 2300] [Raid Boss]") and not game.ReplicatedStorage:FindFirstChild("Cake Prince [Lv. 2300] [Raid Boss]") then
						HopServer()
						wait(50)
					end
				else
					if (Vector3.new(-2017.4874267578125, 36.85276412963867, -12027.53515625)-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 1200 then
						CFrameMon = CFrame.new(-2017.4874267578125, 36.85276412963867, -12027.53515625)
						game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("SetSpawnPoint")
						for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
							if not string.find(v.Name,"Boss") and v.Humanoid.Health > 0 and (v.HumanoidRootPart.Position-CFrameMon.Position).Magnitude <= 1000 then
								if v.Humanoid:FindFirstChild("Animator") then
									v.Humanoid.Animator:Destroy()
								end
								_G.PosMon = v.HumanoidRootPart.CFrame
								StatrMagnet = true
								repeat wait(_G.Fast_Delay)
									EquipWeapon(_G.Setting_table.Weapon)
									TP(v.HumanoidRootPart.CFrame * CFrame.new(0, 30, 1))
									AttackNoCD()
								until v.Humanoid.Health <= 0 or not v.Parent or not Auto_Pale_Scarf
								StatrMagnet = false
							end
						end
					else
						TP(CFrame.new(-2017.4874267578125, 36.85276412963867, -12027.53515625))
					end
				end
			else
				wait(3)
			end
		end)
	end
end)
QG:AddToggle({
    Name = "Auto Valkyrie Helmet",
    _G.Setting_table.Auto_Valkyrie_Helmet,
    Callback = function(vu)
	Auto_Valkyrie_Helmet = vu
	_G.Setting_table.Auto_Valkyrie_Helmet = vu
	Update_Setting(getgenv()['MyName'])
end})
spawn(function()
	while wait(.5) do
		pcall(function()
			if Auto_Valkyrie_Helmet then
				if not Mix_Farm or Auto_Valkyrie_Helmet_Farm then
					if game.Workspace.Enemies:FindFirstChild("rip_indra True Form [Lv. 5000] [Raid Boss]") or game.ReplicatedStorage:FindFirstChild("rip_indra True Form [Lv. 5000] [Raid Boss]") then
						Auto_Valkyrie_Helmet_Farm = true
						Mix_Farm = true
						if game.Workspace.Enemies:FindFirstChild("rip_indra True Form [Lv. 5000] [Raid Boss]") then
							for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
								if v.Name == "rip_indra True Form [Lv. 5000] [Raid Boss]" and v.Humanoid.Health > 0 then
									if v.Humanoid:FindFirstChild("Animator") then
										v.Humanoid.Animator:Destroy()
									end
									repeat wait(_G.Fast_Delay)
										EquipWeapon(_G.Setting_table.Weapon)
										TP(v.HumanoidRootPart.CFrame*CFrame.new(0,30,0))
										AttackNoCD()
									until v.Humanoid.Health <= 0 or not v.Parent or not Auto_Valkyrie_Helmet
								end
							end
						elseif game.ReplicatedStorage:FindFirstChild("rip_indra True Form [Lv. 5000] [Raid Boss]") then
							TP(game.ReplicatedStorage:FindFirstChild("rip_indra True Form [Lv. 5000] [Raid Boss]").HumanoidRootPart.CFrame*CFrame.new(0,30,0))
						end
					elseif _G.Setting_table.Auto_Valkyrie_Helmet_Hop then
						wait(5)
						if not game.Workspace.Enemies:FindFirstChild("rip_indra True Form [Lv. 5000] [Raid Boss]") and not game.ReplicatedStorage:FindFirstChild("rip_indra True Form [Lv. 5000] [Raid Boss]") then
							HopServer()
							wait(50)
						end
					elseif Auto_Valkyrie_Helmet_Farm then
						Auto_Valkyrie_Helmet_Farm = nil
						Mix_Farm = nil
					end
				end
			else
				wait(2)
			end
		end)
	end
end)

QG:AddLabel("Sword")
QG:AddToggle({
    Name = "Auto Saber",
    _G.Setting_table.Saber_Farm,
    Callback = function(vu)
	Saber_Farm = vu
	_G.Setting_table.Saber_Farm = vu
	Update_Setting(getgenv()['MyName'])
end})
spawn(function()
    while wait(.2) do
        local Lv = game:GetService("Players").LocalPlayer.Data.Level.Value
        local Beli = game:GetService("Players").LocalPlayer.Data.Beli.Value
        local FG = game:GetService("Players").LocalPlayer.Data.Fragments.Value
        if Old_World and Saber_Farm then
            if Auto_Farm then
                Auto_Farm = false
            end
            if game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("ProQuestProgress","SickMan") ~= 0 then
                game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("AbandonQuest")
                Auto_Farm = false
                repeat wait()
                    TP(CFrame.new(-1609.29956, 40.0520697, 162.820404))
                until (Vector3.new(-1609.29956, 40.0520697, 162.820404)-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 10
                wait(3)
                for i,v in pairs(game:GetService("Workspace").Map.Jungle.QuestPlates:GetChildren()) do
                    if v.Name == "Plate1" then
                        repeat wait()
                        TP2(v.Button.CFrame)
                        until (v.Button.Position-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude < 1
                        wait(1)
                    end
                    if v.Name == "Plate2" then
                        repeat wait()
                        TP2(v.Button.CFrame)
                        until (v.Button.Position-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude < 1
                        wait(1)
                    end
                    if v.Name == "Plate3" then
                        repeat wait()
                        TP2(v.Button.CFrame)
                        until (v.Button.Position-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude < 1
                        wait(1)
                    end
                    if v.Name == "Plate4" then
                        repeat wait()
                        TP2(v.Button.CFrame)
                        until (v.Button.Position-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude < 1
                        wait(1)
                    end
                    if v.Name == "Plate5" then
                        repeat wait()
                        TP2(v.Button.CFrame)
                        until (v.Button.Position-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude < 1
                        wait(1)
                    end
                end
                wait(2)
                game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-1609.29956, 12.0520697, 162.820404, -0.993804812, 2.60902091e-08, 0.11113929, 3.47902116e-08, 1, 7.63408607e-08, -0.11113929, 7.97344768e-08, -0.993804812)
                wait(2)
                repeat wait()
                    EquipWeapon("Torch")
                    TP(CFrame.new(1113.9502, 4.92147732, 4350.91992, -0.60768199, 3.86533046e-08, 0.794180453, 6.00742425e-08, 1, -2.70375722e-09, -0.794180453, 4.60667628e-08, -0.60768199))
                until (Vector3.new(1113.9502, 4.92147732, 4350.91992)-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 1
                wait(1)
                --fireclickdetector(game:GetService("Workspace").Map.Desert.Burn.Fire.ClickDetector)
                wait(1)
                game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(1113.9502, 4.92147732, 4350.91992, -0.60768199, 3.86533046e-08, 0.794180453, 6.00742425e-08, 1, -2.70375722e-09, -0.794180453, 4.60667628e-08, -0.60768199)
                wait(1)
                game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(1113.9502, 4.92147732, 4350.91992, -0.60768199, 3.86533046e-08, 0.794180453, 6.00742425e-08, 1, -2.70375722e-09, -0.794180453, 4.60667628e-08, -0.60768199)
                wait(1)
                game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(1114.87708, 4.9214654, 4349.8501, -0.612586915, -9.68697833e-08, 0.790403247, -1.2634203e-07, 1, 2.4638446e-08, -0.790403247, -8.47679615e-08, -0.612586915)
                wait(10)
                game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(1113.33618, 7.5484705, 4365.56396, -0.618000686, 2.54492516e-08, -0.786177576, -8.16741874e-09, 1, 3.87911392e-08, 0.786177576, 3.03939913e-08, -0.618000686)
                wait(2)
                repeat wait()
                    EquipWeapon("Cup")
                    TP(CFrame.new(1397.73975, 37.3480263, -1321.54456, -0.170597032, -4.99889588e-08, 0.985340893, 2.99880867e-08, 1, 5.59246409e-08, -0.985340893, 3.90890662e-08, -0.170597032))
                until (Vector3.new(1397.73975, 37.3480263, -1321.54456)-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 2
                wait(1)
                game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(1397.73975, 37.3480263, -1321.54456, -0.170597032, -4.99889588e-08, 0.985340893, 2.99880867e-08, 1, 5.59246409e-08, -0.985340893, 3.90890662e-08, -0.170597032)
                wait(3)
                game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("ProQuestProgress","SickMan")
                wait(1)
                Mob_Boss = true
                Saber_Farm = false
                
            else
                Auto_Farm = false
                Mob_Boss = true
                Saber_Farm = false
            end
        elseif not Old_World and Saber_Farm then
            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("TravelMain")
        end
    end
end)

spawn(function()
    while wait(.2) do
        if Mob_Boss then
            if game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("ProQuestProgress","RichSon") == 1 then
                if game.Players.LocalPlayer.Backpack:FindFirstChild("Relic") or game.Players.LocalPlayer.Character:FindFirstChild("Relic") then
                    EquipWeapon("Relic")
                    repeat wait()
                        EquipWeapon("Relic")
                        TP2(CFrame.new(-1406.60925, 29.8520069, 4.5805192, 0.882920146, 3.62382622e-08, 0.469523162, -3.61928865e-09, 1, -7.03750587e-08, -0.469523162, 6.04362143e-08, 0.882920146))
                    until (Vector3.new(-1406.60925, 29.8520069, 4.5805192)-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 2
                    wait(1)
                    Saber_Kill = true
                    Mob_Boss = false
                else
                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("ProQuestProgress","RichSon")
                end
            elseif game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("ProQuestProgress","RichSon") == 0 then
                if game.Workspace.Enemies:FindFirstChild("Mob Leader [Lv. 120] [Boss]") then
                    for i,v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
                        if v.Name == "Mob Leader [Lv. 120] [Boss]" then
                            
                            repeat wait()
                                EquipWeapon(_G.Setting_table.Weapon)
                                v.HumanoidRootPart.Size = Vector3.new(50,50,50)
                                TP(v.HumanoidRootPart.CFrame*CFrame.new(0,20,0))
                                game:GetService'VirtualUser':CaptureController()
                                game:GetService'VirtualUser':Button1Down(Vector2.new(1280,900))
                            until not v.Parent or v.Humanoid.Health <= 0 or Mob_Boss == false
                        end
                    end
                elseif game:GetService("ReplicatedStorage"):FindFirstChild("Mob Leader [Lv. 120] [Boss]") then
                    TP2(game:GetService("ReplicatedStorage"):FindFirstChild("Mob Leader [Lv. 120] [Boss]").HumanoidRootPart.CFrame)
                end
            else
                game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("ProQuestProgress","RichSon")
            end
        end
    end
end)

spawn(function()
    while wait(.2) do
        pcall(function()
            if Saber_Kill then
                if game.Workspace.Enemies:FindFirstChild("Saber Expert [Lv. 200] [Boss]") then
                    for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
                        if v.Name == "Saber Expert [Lv. 200] [Boss]" then
                            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("SetSpawnPoint")
                             
                            repeat wait()
                                EquipWeapon(_G.Setting_table.Weapon)
                                v.HumanoidRootPart.Size = Vector3.new(50,50,50)
                                TP(v.HumanoidRootPart.CFrame*CFrame.new(0,25,15))
                                game:GetService'VirtualUser':CaptureController()
                                game:GetService'VirtualUser':Button1Down(Vector2.new(1280,900))
                            until not v.Parent or v.Humanoid.Health <= 0 or Saber_Kill == false
                        end
                    end
                elseif game:GetService("ReplicatedStorage"):FindFirstChild("Saber Expert [Lv. 200] [Boss]") or game.Workspace.Enemies:FindFirstChild("Saber Expert [Lv. 200] [Boss]") then
                    TP(game:GetService("ReplicatedStorage"):FindFirstChild("Saber Expert [Lv. 200] [Boss]").HumanoidRootPart.CFrame)
                elseif _G.Hop_Saber then
                    wait(5)
                    if not game.Workspace.Enemies:FindFirstChild("Saber Expert [Lv. 200] [Boss]") and not game:GetService("ReplicatedStorage"):FindFirstChild("Saber Expert [Lv. 200] [Boss]") then
                        _G.Hop_Saber_Ex = true
                    end
                else
                    TP2(CFrame.new(-1458.89502, 29.8870335, -50.633564, 0.858821094, 1.13848939e-08, 0.512275636, -4.85649254e-09, 1, -1.40823326e-08, -0.512275636, 9.6063415e-09, 0.858821094))
                end
            end
        end)
    end
end)

QG:AddToggle({
    Name = "Auto Pole V1",
    _G.Setting_table.Pole_Farm,
    Callback = function(vu)
	Pole_Farm = vu
	_G.Setting_table.Pole_Farm = vu
	Update_Setting(getgenv()['MyName'])
end})

spawn(function()
	while wait(.5) do
		pcall(function()
			if Pole_Farm then
				if not Mix_Farm or Pole_Farm_Ex then
					if game.Workspace.Enemies:FindFirstChild("Thunder God [Lv. 575] [Boss]") or game.ReplicatedStorage:FindFirstChild("Thunder God [Lv. 575] [Boss]") then
						Pole_Farm_Ex = true
						Mix_Farm = true
						if game.Workspace.Enemies:FindFirstChild("Thunder God [Lv. 575] [Boss]") then
							for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
								if v.Name == "Thunder God [Lv. 575] [Boss]" then
									repeat wait(.2)
										EquipWeapon(_G.Setting_table.Weapon)
										TP(v.HumanoidRootPart.CFrame*CFrame.new(0,30,15))
										game:GetService'VirtualUser':Button1Down(Vector2.new(1280,900))
										game:service('VirtualInputManager'):SendKeyEvent(true, "Z", false, game)
										wait(.1)
										game:service('VirtualInputManager'):SendKeyEvent(false, "Z", false, game)
										game:service('VirtualInputManager'):SendKeyEvent(true, "X", false, game)
										wait(.1)
										game:service('VirtualInputManager'):SendKeyEvent(false, "X", false, game)
										game:service('VirtualInputManager'):SendKeyEvent(true, "C", false, game)
										wait(.1)
										game:service('VirtualInputManager'):SendKeyEvent(false, "C", false, game)
									until v.Humanoid.Health <= 0 or not v.Parent or not Pole_Farm 
									Pole_Farm_Ex = nil
									Mix_Farm = nil
								end
							end
						elseif game.ReplicatedStorage:FindFirstChild("Thunder God [Lv. 575] [Boss]") then
							TP(game.ReplicatedStorage:FindFirstChild("Thunder God [Lv. 575] [Boss]").HumanoidRootPart.CFrame*CFrame.new(0,30,0))
						end
					elseif _G.Setting_table.Pole_V1_Hop then
						wait(5)
						if not game.Workspace.Enemies:FindFirstChild("Thunder God [Lv. 575] [Boss]") and not game.ReplicatedStorage:FindFirstChild("Thunder God [Lv. 575] [Boss]") then
							HopServer()
							wait(50)
						end
					elseif Pole_Farm_Ex then
						Mix_Farm = nil
						Pole_Farm_Ex = nil
					else
						wait(5)
					end
				end
			else
				wait(2)
			end
		end)
	end
end)
QG:AddToggle({
    Name = "Auto Rengoku",
    _G.Setting_table.Rengoku_A,
    Callback = function(vu)
	Rengoku_A = vu
	_G.Setting_table.Rengoku_A = vu
	Update_Setting(getgenv()['MyName'])
end})
spawn(function()
    while wait(.3) do
        pcall(function()
            if Rengoku_A then
                if not Mix_Farm or Rengoku_Farm then
                    if game.Players.LocalPlayer.Backpack:FindFirstChild("Hidden Key") or game.Players.LocalPlayer.Character:FindFirstChild("Hidden Key") then
                        repeat wait(.3)
							EquipWeapon("Hidden Key")
                            TP(CFrame.new(6572.29248, 295.712677, -6966.09961, 0.803500533, -3.27515153e-08, 0.595304072, 3.97485422e-08, 1, 1.36659384e-09, -0.595304072, 2.25644108e-08, 0.803500533))
                        until not game.Players.LocalPlayer.Backpack:FindFirstChild("Hidden Key") and not game.Players.LocalPlayer.Character:FindFirstChild("Hidden Key")
                    else
                        if game.Workspace.Enemies:FindFirstChild("Snow Lurker [Lv. 1375]") then
							for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
								if v.Name == "Snow Lurker [Lv. 1375]" and v.Humanoid.Health > 0 then
									if v.Humanoid:FindFirstChild("Animator") then
										v.Humanoid.Animator:Destroy()
									end
									_G.PosMon = v.HumanoidRootPart.CFrame
									StatrMagnet = true
									repeat wait(_G.Fast_Delay)
										EquipWeapon(_G.Setting_table.Weapon)
										TP(v.HumanoidRootPart.CFrame*CFrame.new(0,30,0))
										AttackNoCD()
									until v.Humanoid.Health <= 0 or not v.Parent or not Rengoku_A
									StatrMagnet = false
								end
							end
						elseif game.ReplicatedStorage:FindFirstChild("Snow Lurker [Lv. 1375]") then
							TP(game.ReplicatedStorage:FindFirstChild("Snow Lurker [Lv. 1375]").HumanoidRootPart.CFrame*CFrame.new(0,30,0))
						end
                    end
                end
			else
				wait(2)
            end
        end)
    end
end)
QG:AddToggle({
    Name = "Auto Ko Ko",
    Value = false,
    Callback = function(vu)
	if vu then
		Text("ยังไม่ทำ")
	end
end})
QG:AddToggle({
    Name = "Auto Dragon Trident",
    _G.Setting_table.Auto_Dragon_Trident,
    Callback = function(vu)
	Auto_Dragon_Trident = vu
	_G.Setting_table.Auto_Dragon_Trident = vu
	Update_Setting(getgenv()['MyName'])
end})
spawn(function()
	while wait(.5) do
		pcall(function()
			if Auto_Dragon_Trident then
				if not Mix_Farm or Auto_Dragon_Trident_Farm then
					if game.Workspace.Enemies:FindFirstChild("Tide Keeper [Lv. 1475] [Boss]") or game.ReplicatedStorage:FindFirstChild("Tide Keeper [Lv. 1475] [Boss]") then
						Auto_Dragon_Trident_Farm = true
						Mix_Farm = true
						if game.Workspace.Enemies:FindFirstChild("Tide Keeper [Lv. 1475] [Boss]") then
							game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("SetSpawnPoint")
							for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
								if v.Name == "Tide Keeper [Lv. 1475] [Boss]" and v.Humanoid.Health > 0 then
									if v.Humanoid:FindFirstChild("Animator") then
										v.Humanoid.Animator:Destroy()
									end
									repeat wait(_G.Fast_Delay)
										EquipWeapon(_G.Setting_table.Weapon)
										TP(v.HumanoidRootPart.CFrame*CFrame.new(0,30,0))
										AttackNoCD()
									until v.Humanoid.Health <= 0 or not v.Parent or not Auto_Dragon_Trident
								end
							end
						elseif game.ReplicatedStorage:FindFirstChild("Tide Keeper [Lv. 1475] [Boss]") then
							TP(game.ReplicatedStorage:FindFirstChild("Tide Keeper [Lv. 1475] [Boss]").HumanoidRootPart.CFrame*CFrame.new(0,30,0))
						end
					elseif Auto_Dragon_Trident_Farm then
						Auto_Dragon_Trident_Farm = nil
						Mix_Farm = nil
					elseif _G.Setting_table.Auto_Dragon_Trident_Hop then
						wait(5)
						if not game.Workspace.Enemies:FindFirstChild("Tide Keeper [Lv. 1475] [Boss]") and not game.ReplicatedStorage:FindFirstChild("Tide Keeper [Lv. 1475] [Boss]") then
							HopServer()
							wait(50)
						end
					end
				end
			else
				wait(2)
			end
		end)
	end
end)
QG:AddToggle({
    Name = "Auto True Triple Katana",
    _G.Setting_table.Triple_A,
    Callback = function(vu)
	Auto_Farm_Sword = vu
	Triple_A = vu
	_G.Setting_table.Triple_A = vu
	Update_Setting(getgenv()['MyName'])
end})
function Dis()
    if New_World then
        repeat wait(.2)
			Mix_Farm = true
            TP(CFrame.new(121.6969223022461, 18.738399505615234, 2850.1474609375))
        until (Vector3.new(121.6969223022461, 18.738399505615234, 2850.1474609375)-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude < 2
		wait(1)
		for i2,v2 in pairs(game.Players.LocalPlayer.Backpack:GetChildren()) do  
			if tostring(v2.ToolTip) == "Melee" then
				EquipWeapon(v2.Name)
			end
		end
		wait(1)
        for i2,v2 in pairs(game.Players.LocalPlayer.Backpack:GetChildren()) do  
            if tostring(v2.ToolTip) == "Sword" then
                local args = {
                    [1] = "StoreItem",
                    [2] = v2.Name
                }
                game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
            end
        end
		wait(1)
		Mix_Farm = nil
    elseif Three_World then
        repeat wait(.2)
			Mix_Farm = true
            TP(CFrame.new(-220.47975158691406, 5.787993431091309, 5324.3720703125))
        until (Vector3.new(-220.47975158691406, 5.787993431091309, 5324.3720703125)-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude < 2
        wait(1)
		for i2,v2 in pairs(game.Players.LocalPlayer.Backpack:GetChildren()) do  
			if tostring(v2.ToolTip) == "Melee" then
				EquipWeapon(v2.Name)
			end
		end
		wait(1)
        for i2,v2 in pairs(game.Players.LocalPlayer.Backpack:GetChildren()) do  
            if tostring(v2.ToolTip) == "Sword" then
                local args = {
                    [1] = "StoreItem",
                    [2] = v2.Name
                }
                game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
            end
        end
		wait(1)
		Mix_Farm = nil
    end
end
function Load(vu)
    if New_World then
        repeat wait(.2)
			Mix_Farm = true
            TP(CFrame.new(121.6969223022461, 18.738399505615234, 2850.1474609375))
        until (Vector3.new(121.6969223022461, 18.738399505615234, 2850.1474609375)-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude < 2
		wait(1)
        local args = {
            [1] = "LoadItem",
            [2] = tostring(vu)
        }
        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
		wait(2)
		Mix_Farm = nil
    elseif Three_World then
        repeat wait(.2)
			Mix_Farm = true
            TP(CFrame.new(-220.47975158691406, 5.787993431091309, 5324.3720703125))
        until (Vector3.new(-220.47975158691406, 5.787993431091309, 5324.3720703125)-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude < 2
		wait(1)
        local args = {
            [1] = "LoadItem",
            [2] = tostring(vu)
        }
        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
		wait(2)
		Mix_Farm = nil
    end
end
local I_W = game:GetService("ReplicatedStorage").Remotes["CommF_"]:InvokeServer("getInventoryWeapons")

for i,x in pairs(I_W) do
    v = {
        Name = x["Name"]
    }
	if v.Name == "Shisui" then
		_G.Setting_table.Shisui = true
	end
	if v.Name == "Wando" then
		_G.Setting_table.Wando = true
	end
		if v.Name == "Saddi" then
		_G.Setting_table.Saddi = true
	end
end
for i,v in pairs(game.Players.LocalPlayer.Backpack:GetChildren()) do
	if v:IsA("Tool") then
		if v.Name == "Shisui" then
			_G.Setting_table.Shisui = true
		end
		if v.Name == "Wando" then
			_G.Setting_table.Wando = true
		end
			if v.Name == "Saddi" then
			_G.Setting_table.Saddi = true
		end
	end
end
for i,v in pairs(game.Players.LocalPlayer.Character:GetChildren()) do
	if v:IsA("Tool") then
		if v.Name == "Shisui" then
			_G.Setting_table.Shisui = true
		end
		if v.Name == "Wando" then
			_G.Setting_table.Wando = true
		end
			if v.Name == "Saddi" then
			_G.Setting_table.Saddi = true
		end
	end
end
spawn(function()
    while wait(.1) do
        pcall(function()
            if Triple_A then
                local args = {
                    [1] = "LegendarySwordDealer",
                    [2] = "2"
                }
                game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
            end
        end)
    end
end)
spawn(function()
    while wait(.3) do
        pcall(function()
            if Triple_A then
                if game.Players.LocalPlayer.Backpack:FindFirstChild("True Triple Katana") or game.Players.LocalPlayer.Character:FindFirstChild("True Triple Katana") then
                    _G.Setting_table.Weapon = "True Triple Katana"
					Auto_Farm_Sword = true
                elseif _G.Setting_table.Shisui_H and _G.Setting_table.Wando_H and _G.Setting_table.Saddi_H then
                    local Beli = game:GetService("Players").LocalPlayer.Data.Beli.Value
                    if Beli >= 3000000 then
                        pcall(function()
                            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("MysteriousMan","1")
                            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("MysteriousMan","2")
                        end)
                    else
                        Auto_Farm_Sword = true
                    end
                elseif _G.Setting_table.Shisui and not _G.Setting_table.Shisui_H then
                    if game.Players.LocalPlayer.Backpack:FindFirstChild("Shisui") or game.Players.LocalPlayer.Character:FindFirstChild("Shisui") then
                        if game.Players.LocalPlayer.Backpack:FindFirstChild("Shisui") and game.Players.LocalPlayer.Backpack:FindFirstChild("Shisui").Level.Value >= 300 then
                            _G.Setting_table.Weapon = "Shisui"
                            _G.Setting_table.Shisui_H = true
                            Update_Setting(getgenv()['MyName'])
                        elseif game.Players.LocalPlayer.Backpack:FindFirstChild("Shisui") and game.Players.LocalPlayer.Backpack:FindFirstChild("Shisui").Level.Value < 300 then
                            _G.Setting_table.Weapon = "Shisui"
							Auto_Farm_Sword = true
                        end
						if game.Players.LocalPlayer.Character:FindFirstChild("Shisui") and game.Players.LocalPlayer.Character:FindFirstChild("Shisui").Level.Value >= 300 then
                            _G.Setting_table.Weapon = "Shisui"
                            _G.Setting_table.Shisui_H = true
                            Update_Setting(getgenv()['MyName'])
                        elseif game.Players.LocalPlayer.Character:FindFirstChild("Shisui") and game.Players.LocalPlayer.Character:FindFirstChild("Shisui").Level.Value < 300 then
                            _G.Setting_table.Weapon = "Shisui"
							Auto_Farm_Sword = true
                        end
                    else
						wait(5)
						if game.Players.LocalPlayer.Backpack:FindFirstChild("Shisui") or game.Players.LocalPlayer.Character:FindFirstChild("Shisui") then
						else
							Dis()
							Load("Shisui")
						end
                    end
                elseif _G.Setting_table.Wando and not _G.Setting_table.Wando_H then
                    if game.Players.LocalPlayer.Backpack:FindFirstChild("Wando") or game.Players.LocalPlayer.Character:FindFirstChild("Wando") then
                        if game.Players.LocalPlayer.Backpack:FindFirstChild("Wando") and game.Players.LocalPlayer.Backpack:FindFirstChild("Wando").Level.Value >= 300 then
                            _G.Setting_table.Weapon = "Wando"
                            _G.Setting_table.Wando_H = true
                            Update_Setting(getgenv()['MyName'])
                        elseif game.Players.LocalPlayer.Backpack:FindFirstChild("Wando") and game.Players.LocalPlayer.Backpack:FindFirstChild("Wando").Level.Value < 300 then
                            _G.Setting_table.Weapon = "Wando"
							Auto_Farm_Sword = true
                        end
						if game.Players.LocalPlayer.Character:FindFirstChild("Wando") and game.Players.LocalPlayer.Character:FindFirstChild("Wando").Level.Value >= 300 then
                            _G.Setting_table.Weapon = "Wando"
                            _G.Setting_table.Wando_H = true
                            Update_Setting(getgenv()['MyName'])
                        elseif game.Players.LocalPlayer.Character:FindFirstChild("Wando") and game.Players.LocalPlayer.Character:FindFirstChild("Wando").Level.Value < 300 then
                            _G.Setting_table.Weapon = "Wando"
							Auto_Farm_Sword = true
                        end
                    else
						wait(5)
						if game.Players.LocalPlayer.Backpack:FindFirstChild("Wando") or game.Players.LocalPlayer.Character:FindFirstChild("Wando") then
						else
							Dis()
							Load("Wando")
						end
                    end
                elseif _G.Setting_table.Saddi and not _G.Setting_table.Saddi_H then
                    if game.Players.LocalPlayer.Backpack:FindFirstChild("Saddi") or game.Players.LocalPlayer.Character:FindFirstChild("Saddi") then
                        if game.Players.LocalPlayer.Backpack:FindFirstChild("Saddi") and game.Players.LocalPlayer.Backpack:FindFirstChild("Saddi").Level.Value >= 300 then
                            _G.Setting_table.Weapon = "Saddi"
                            _G.Setting_table.Saddi_H = true
                            Update_Setting(getgenv()['MyName'])
                        elseif game.Players.LocalPlayer.Backpack:FindFirstChild("Saddi") and game.Players.LocalPlayer.Backpack:FindFirstChild("Saddi").Level.Value < 300 then
                            _G.Setting_table.Weapon = "Saddi"
							Auto_Farm_Sword = true
                        end
						if game.Players.LocalPlayer.Character:FindFirstChild("Saddi") and game.Players.LocalPlayer.Character:FindFirstChild("Saddi").Level.Value >= 300 then
                            _G.Setting_table.Weapon = "Saddi"
                            _G.Setting_table.Saddi_H = true
                            Update_Setting(getgenv()['MyName'])
                        elseif game.Players.LocalPlayer.Character:FindFirstChild("Saddi") and game.Players.LocalPlayer.Character:FindFirstChild("Saddi").Level.Value < 300 then
                            _G.Setting_table.Weapon = "Saddi"
							Auto_Farm_Sword = true
                        end
                    else
						wait(5)
						if game.Players.LocalPlayer.Backpack:FindFirstChild("Saddi") or game.Players.LocalPlayer.Character:FindFirstChild("Saddi") then
						else
							Dis()
							Load("Saddi")
						end
                    end
                elseif _G.Setting_table.Triple_Hop then
					local Beli = game:GetService("Players").LocalPlayer.Data.Beli.Value
					if Beli < 2000000 then
						Text("ฟามเงินรอดาบเกิด")
						Auto_Farm_Sword = true
						wait(10)
					else
						Text("กำลังหาดาบ")
						wait(10)
						HopServer()
						wait(50)
					end
				else
					Text("ฟามเงินรอดาบเกิด")
					Auto_Farm_Sword = true
					wait(10)
                end
            end
        end)
    end
end)

QG:AddToggle({
    Name = "Auto Yama",
    _G.Setting_table.Auto_Yama,
    Callback = function(vu)
	Auto_Yama = vu
	_G.Setting_table.Auto_Yama = vu
	Update_Setting(getgenv()['MyName'])
end})
spawn(function()
	while wait(.5) do
		pcall(function()
			if Auto_Yama then
				if not Mix_Farm or Auto_Yama_Farm then
					if game.ReplicatedStorage.Remotes.CommF_:InvokeServer("EliteHunter", "Progress") < 30 then
                        if game:GetService("ReplicatedStorage"):FindFirstChild("Urban [Lv. 1750]") or game:GetService("Workspace").Enemies:FindFirstChild("Urban [Lv. 1750]") then
                            Mix_Farm = true
                            Auto_Yama_Farm = true
                            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("EliteHunter")
                            if game:GetService("Workspace").Enemies:FindFirstChild("Urban [Lv. 1750]") then
                                for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
									if v.Name == "Urban [Lv. 1750]" and v.Humanoid.Health > 0 then
										if v.Humanoid:FindFirstChild("Animator") then
											v.Humanoid.Animator:Destroy()
										end
										repeat wait(_G.Fast_Delay)
											EquipWeapon(_G.Setting_table.Weapon)
											TP(v.HumanoidRootPart.CFrame*CFrame.new(0,30,0))
											AttackNoCD()
										until v.Humanoid.Health <= 0 or not v.Parent or not Auto_Yama
									end
								end
                            elseif game:GetService("ReplicatedStorage"):FindFirstChild("Urban [Lv. 1750]") then
                                TP(game:GetService("ReplicatedStorage"):FindFirstChild("Urban [Lv. 1750]").HumanoidRootPart.CFrame*CFrame.new(0,30,0))
                            end
                        elseif game:GetService("ReplicatedStorage"):FindFirstChild("Diablo [Lv. 1750]") or game:GetService("Workspace").Enemies:FindFirstChild("Diablo [Lv. 1750]") then
                            Mix_Farm = true
                            Auto_Yama_Farm = true
							game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("EliteHunter")
                            if game:GetService("Workspace").Enemies:FindFirstChild("Diablo [Lv. 1750]") then
                                for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
									if v.Name == "Diablo [Lv. 1750]" and v.Humanoid.Health > 0 then
										if v.Humanoid:FindFirstChild("Animator") then
											v.Humanoid.Animator:Destroy()
										end
										repeat wait(_G.Fast_Delay)
											EquipWeapon(_G.Setting_table.Weapon)
											TP(v.HumanoidRootPart.CFrame*CFrame.new(0,30,0))
											AttackNoCD()
										until v.Humanoid.Health <= 0 or not v.Parent or not Auto_Yama
									end
								end
                            elseif game:GetService("ReplicatedStorage"):FindFirstChild("Diablo [Lv. 1750]") then
                                TP(game:GetService("ReplicatedStorage"):FindFirstChild("Diablo [Lv. 1750]").HumanoidRootPart.CFrame*CFrame.new(0,30,0))
                            end
                        elseif game:GetService("ReplicatedStorage"):FindFirstChild("Deandre [Lv. 1750]") or game:GetService("Workspace").Enemies:FindFirstChild("Deandre [Lv. 1750]") then
							Mix_Farm = true
                            Auto_Yama_Farm = true
                            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("EliteHunter")
                            if game:GetService("Workspace").Enemies:FindFirstChild("Deandre [Lv. 1750]") then
                                for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
									if v.Name == "Deandre [Lv. 1750]" and v.Humanoid.Health > 0 then
										if v.Humanoid:FindFirstChild("Animator") then
											v.Humanoid.Animator:Destroy()
										end
										repeat wait(_G.Fast_Delay)
											EquipWeapon(_G.Setting_table.Weapon)
											TP(v.HumanoidRootPart.CFrame*CFrame.new(0,30,0))
											AttackNoCD()
										until v.Humanoid.Health <= 0 or not v.Parent or not Auto_Yama
									end
								end
                            elseif game:GetService("ReplicatedStorage"):FindFirstChild("Deandre [Lv. 1750]") then
                                TP(game:GetService("ReplicatedStorage"):FindFirstChild("Deandre [Lv. 1750]").HumanoidRootPart.CFrame*CFrame.new(0,30,0))
                            end
						elseif Auto_Yama_Farm then
							Auto_Yama_Farm = nil
							Mix_Farm = nil
                        elseif game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text == "Defeat  Urban (0/1)" or game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text == "Defeat  Deandre (0/1)" or game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text == "Defeat  Diablo (0/1)" then
                            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("AbandonQuest")
                        elseif _G.Setting_table.Auto_Yama_Hop then
                            wait(5)
                            if not game:GetService("ReplicatedStorage"):FindFirstChild("Urban [Lv. 1750]") and not game:GetService("Workspace").Enemies:FindFirstChild("Urban [Lv. 1750]") and not game:GetService("ReplicatedStorage"):FindFirstChild("Diablo [Lv. 1750]") and not game:GetService("Workspace").Enemies:FindFirstChild("Diablo [Lv. 1750]") and not game:GetService("ReplicatedStorage"):FindFirstChild("Deandre [Lv. 1750]") and not game:GetService("Workspace").Enemies:FindFirstChild("Deandre [Lv. 1750]") then
                                HopServer()
                                wait(50)
                            end
                        end
                    elseif game.ReplicatedStorage.Remotes.CommF_:InvokeServer("EliteHunter", "Progress") >= 30 and not Yama_H then
                        Auto_Yama_Farm = true
						Mix_Farm = true
                        if (game.Workspace.Map.Waterfall.SealedKatana.Handle.Position-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 300 then
                            TP(game.Workspace.Map.Waterfall.SealedKatana.Handle.CFrame)
                        end
                        if game.Workspace.Enemies:FindFirstChild("Ghost [Lv. 1500]") then
                            for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
								if v.Name == "Ghost [Lv. 1500]" and v.Humanoid.Health > 0 then
									if v.Humanoid:FindFirstChild("Animator") then
										v.Humanoid.Animator:Destroy()
									end
									repeat wait(_G.Fast_Delay)
										EquipWeapon(_G.Setting_table.Weapon)
										TP(v.HumanoidRootPart.CFrame*CFrame.new(0,30,0))
										AttackNoCD()
									until v.Humanoid.Health <= 0 or not v.Parent or not Auto_Yama
								end
							end
                        elseif not game.Workspace.Enemies:FindFirstChild("Ghost [Lv. 1500]") then
							Yama_H = true
							fireclickdetector(game.Workspace.Map.Waterfall.SealedKatana.Handle.ClickDetector)
                        end
					elseif Auto_Yama_Farm then
						Auto_Yama_Farm = nil
						Mix_Farm = nil
                    end
				end
			else
				wait(2)
			end
		end)
	end
end)
QG:AddToggle({
    Name = "Auto Tushita",
    _G.Setting_table.Auto_Tushita,
    Callback = function(vu)
	Auto_Tushita = vu
	_G.Setting_table.Auto_Tushita = vu
	Update_Setting(getgenv()['MyName'])
end})
spawn(function()
	while wait(.5) do
		pcall(function()
			if Auto_Tushita then
				if not Mix_Farm or Auto_Tushita_Farm then
					if not _G.Setting_table.Quest_Torch then
						if game.Workspace.Enemies:FindFirstChild("rip_indra True Form [Lv. 5000] [Raid Boss]") or game.ReplicatedStorage:FindFirstChild("rip_indra True Form [Lv. 5000] [Raid Boss]") then
							Auto_Tushita_Farm = true
							Mix_Farm = true
							repeat wait(1)
								game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("TushitaProgress")
							until game.Players.LocalPlayer.Backpack:FindFirstChild("Holy Torch") or game.Players.LocalPlayer.Character:FindFirstChild("Holy Torch") or not Auto_Tushita
							wait(1)
							local Q_Tushita = game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("TushitaProgress")
							local Q_Torch = game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("TushitaProgress")['Torches']
							if Q_Torch[1] == false then
								if game.Players.LocalPlayer.Backpack:FindFirstChild("Holy Torch") or game.Players.LocalPlayer.Character:FindFirstChild("Holy Torch") then
									EquipWeapon("Holy Torch")
									game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("TushitaProgress","Torch",1)
								else
									game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("TushitaProgress")
								end
							elseif Q_Torch[2] == false then
								if game.Players.LocalPlayer.Backpack:FindFirstChild("Holy Torch") or game.Players.LocalPlayer.Character:FindFirstChild("Holy Torch") then
									EquipWeapon("Holy Torch")
									game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("TushitaProgress","Torch",2)
								else
									game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("TushitaProgress")
								end
							elseif Q_Torch[3] == false then
								if game.Players.LocalPlayer.Backpack:FindFirstChild("Holy Torch") or game.Players.LocalPlayer.Character:FindFirstChild("Holy Torch") then
									EquipWeapon("Holy Torch")
									game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("TushitaProgress","Torch",3)
								else
									game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("TushitaProgress")
								end
							elseif Q_Torch[4] == false then
								if game.Players.LocalPlayer.Backpack:FindFirstChild("Holy Torch") or game.Players.LocalPlayer.Character:FindFirstChild("Holy Torch") then
									EquipWeapon("Holy Torch")
									game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("TushitaProgress","Torch",4)
								else
									game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("TushitaProgress")
								end
							elseif Q_Torch[5] == false then
								if game.Players.LocalPlayer.Backpack:FindFirstChild("Holy Torch") or game.Players.LocalPlayer.Character:FindFirstChild("Holy Torch") then
									EquipWeapon("Holy Torch")
									game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("TushitaProgress","Torch",5)
								else
									game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("TushitaProgress")
								end
							elseif Q_Tushita['KilledLongma'] == false then
								_G.Tushita_Q = true
							end
							if game.Players.LocalPlayer.Backpack:FindFirstChild("Holy Torch") or game.Players.LocalPlayer.Character:FindFirstChild("Holy Torch") then
								game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("TushitaProgress","Torch",1)
								game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("TushitaProgress","Torch",2)
								game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("TushitaProgress","Torch",3)
								game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("TushitaProgress","Torch",4)
								game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("TushitaProgress","Torch",5)
								wait(1)
								_G.Setting_table.Quest_Torch = true
								Update_Setting(getgenv()['MyName'])
							elseif game:GetService("ReplicatedStorage"):FindFirstChild("rip_indra True Form [Lv. 5000] [Raid Boss]") or game.Workspace.Enemies:FindFirstChild("rip_indra True Form [Lv. 5000] [Raid Boss]") then
								_G.Setting_table.Quest_Torch = true
								Update_Setting(getgenv()['MyName'])
							end
						elseif _G.Setting_table.No_Color_Haki_Tushita and _G.Setting_table.Auto_Tushita_Hop then
							wait(5)
							if not game.Workspace.Enemies:FindFirstChild("rip_indra True Form [Lv. 5000] [Raid Boss]") and not game.ReplicatedStorage:FindFirstChild("rip_indra True Form [Lv. 5000] [Raid Boss]") then
								HopServer()
								wait(50)
							end
						elseif not _G.Setting_table.No_Color_Haki_Tushita then
							if game.Players.LocalPlayer.Backpack:FindFirstChild("God's Chalice") or game.Players.LocalPlayer.Character:FindFirstChild("God's Chalice") then
								Mix_Farm = true
								Auto_Tushita_Farm = true
								game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("activateColor","Winter Sky")
								wait(1)
								repeat TP2(CFrame.new(-5420.16602, 1084.9657, -2666.8208)) wait() until not Auto_Tushita or (game.Players.LocalPlayer.Character.HumanoidRootPart.Position-Vector3.new(-5420.16602, 1084.9657, -2666.8208)).Magnitude <= 10
								wait(1)
								game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("activateColor","Pure Red")
								wait(1)
								repeat TP2(CFrame.new(-5414.41357, 309.865753, -2212.45776)) wait() until not Auto_Tushita or (game.Players.LocalPlayer.Character.HumanoidRootPart.Position-Vector3.new(-5414.41357, 309.865753, -2212.45776)).Magnitude <= 10
								wait(1)
								game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("activateColor","Snow White")
								wait(1)
								repeat TP2(CFrame.new(-4971.47559, 331.565765, -3720.02954)) wait() until not Auto_Tushita or (game.Players.LocalPlayer.Character.HumanoidRootPart.Position-Vector3.new(-4971.47559, 331.565765, -3720.02954)).Magnitude <= 10
								wait(1)
								repeat wait()
									EquipWeapon("God's Chalice")
									TP(CFrame.new(-5561.32471, 314.284546, -2663.39697, -0.391084909, 1.08295005e-07, 0.920354605, 4.10446699e-09, 1, -1.15922504e-07, -0.920354605, -4.15579748e-08, -0.391084909))
								until not Auto_Tushita or not game.Players.LocalPlayer.Backpack:FindFirstChild("God's Chalicee") and not game.Players.LocalPlayer.Character:FindFirstChild("God's Chalice") or game.Workspace.Enemies:FindFirstChild("rip_indra True Form [Lv. 5000] [Raid Boss]")
								wait(1)
							else
								if game:GetService("ReplicatedStorage"):FindFirstChild("Urban [Lv. 1750]") or game:GetService("Workspace").Enemies:FindFirstChild("Urban [Lv. 1750]") then
									Mix_Farm = true
									Auto_Tushita_Farm = true
									game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("EliteHunter")
									if game:GetService("Workspace").Enemies:FindFirstChild("Urban [Lv. 1750]") then
										for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
											if v.Name == "Urban [Lv. 1750]" and v.Humanoid.Health > 0 then
												if v.Humanoid:FindFirstChild("Animator") then
													v.Humanoid.Animator:Destroy()
												end
												repeat wait(_G.Fast_Delay)
													EquipWeapon(_G.Setting_table.Weapon)
													TP(v.HumanoidRootPart.CFrame*CFrame.new(0,30,0))
													AttackNoCD()
												until v.Humanoid.Health <= 0 or not v.Parent or not Auto_Tushita
											end
										end
									elseif game:GetService("ReplicatedStorage"):FindFirstChild("Urban [Lv. 1750]") then
										TP(game:GetService("ReplicatedStorage"):FindFirstChild("Urban [Lv. 1750]").HumanoidRootPart.CFrame*CFrame.new(0,30,0))
									end
								elseif game:GetService("ReplicatedStorage"):FindFirstChild("Diablo [Lv. 1750]") or game:GetService("Workspace").Enemies:FindFirstChild("Diablo [Lv. 1750]") then
									Mix_Farm = true
									Auto_Tushita_Farm = true
									game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("EliteHunter")
									if game:GetService("Workspace").Enemies:FindFirstChild("Diablo [Lv. 1750]") then
										for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
											if v.Name == "Diablo [Lv. 1750]" and v.Humanoid.Health > 0 then
												if v.Humanoid:FindFirstChild("Animator") then
													v.Humanoid.Animator:Destroy()
												end
												repeat wait(_G.Fast_Delay)
													EquipWeapon(_G.Setting_table.Weapon)
													TP(v.HumanoidRootPart.CFrame*CFrame.new(0,30,0))
													AttackNoCD()
												until v.Humanoid.Health <= 0 or not v.Parent or not Auto_Tushita
											end
										end
									elseif game:GetService("ReplicatedStorage"):FindFirstChild("Diablo [Lv. 1750]") then
										TP(game:GetService("ReplicatedStorage"):FindFirstChild("Diablo [Lv. 1750]").HumanoidRootPart.CFrame*CFrame.new(0,30,0))
									end
								elseif game:GetService("ReplicatedStorage"):FindFirstChild("Deandre [Lv. 1750]") or game:GetService("Workspace").Enemies:FindFirstChild("Deandre [Lv. 1750]") then
									Mix_Farm = true
									Auto_Tushita_Farm = true
									game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("EliteHunter")
									if game:GetService("Workspace").Enemies:FindFirstChild("Deandre [Lv. 1750]") then
										for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
											if v.Name == "Deandre [Lv. 1750]" and v.Humanoid.Health > 0 then
												if v.Humanoid:FindFirstChild("Animator") then
													v.Humanoid.Animator:Destroy()
												end
												repeat wait(_G.Fast_Delay)
													EquipWeapon(_G.Setting_table.Weapon)
													TP(v.HumanoidRootPart.CFrame*CFrame.new(0,30,0))
													AttackNoCD()
												until v.Humanoid.Health <= 0 or not v.Parent or not Auto_Tushita
											end
										end
									elseif game:GetService("ReplicatedStorage"):FindFirstChild("Deandre [Lv. 1750]") then
										TP(game:GetService("ReplicatedStorage"):FindFirstChild("Deandre [Lv. 1750]").HumanoidRootPart.CFrame*CFrame.new(0,30,0))
									end
								elseif game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text == "Defeat  Urban (0/1)" or game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text == "Defeat  Deandre (0/1)" or game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text == "Defeat  Diablo (0/1)" then
									game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("AbandonQuest")
								elseif _G.Setting_table.Auto_Tushita_Hop then
									wait(5)
									if not game:GetService("ReplicatedStorage"):FindFirstChild("Urban [Lv. 1750]") and not game:GetService("Workspace").Enemies:FindFirstChild("Urban [Lv. 1750]") and not game:GetService("ReplicatedStorage"):FindFirstChild("Diablo [Lv. 1750]") and not game:GetService("Workspace").Enemies:FindFirstChild("Diablo [Lv. 1750]") and not game:GetService("ReplicatedStorage"):FindFirstChild("Deandre [Lv. 1750]") and not game:GetService("Workspace").Enemies:FindFirstChild("Deandre [Lv. 1750]") then
										HopServer()
										wait(50)
									end
								elseif Auto_Tushita_Farm then
									Auto_Tushita_Farm = nil
									Mix_Farm = nil
								end
							end
						elseif Auto_Tushita_Farm then
							Auto_Tushita_Farm = nil
							Mix_Farm = nil
						end
					else
						if game.Workspace.Enemies:FindFirstChild("Longma [Lv. 2000] [Boss]") or game.ReplicatedStorage:FindFirstChild("Longma [Lv. 2000] [Boss]") then
							Auto_Tushita_Farm = true
							Mix_Farm = true
							if game.Workspace.Enemies:FindFirstChild("Longma [Lv. 2000] [Boss]") then
								for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
									if v.Name == "Longma [Lv. 2000] [Boss]" and v.Humanoid.Health > 0 then
										if v.Humanoid:FindFirstChild("Animator") then
											v.Humanoid.Animator:Destroy()
										end
										repeat wait(_G.Fast_Delay)
											EquipWeapon(_G.Setting_table.Weapon)
											TP(v.HumanoidRootPart.CFrame*CFrame.new(0,30,0))
											AttackNoCD()
										until v.Humanoid.Health <= 0 or not v.Parent or not Auto_Tushita
									end
								end
							elseif game.ReplicatedStorage:FindFirstChild("Longma [Lv. 2000] [Boss]") then
								TP(game.ReplicatedStorage:FindFirstChild("Longma [Lv. 2000] [Boss]").HumanoidRootPart.CFrame*CFrame.new(0,30,0))
							end
						elseif Auto_Tushita_Farm then
							Auto_Tushita_Farm = nil
							Mix_Farm = nil
						end
					end
				end
			else
				wait(2)
			end
		end)
	end
end)

local racev = General_Tab:CreateSection({Name = "Race V4"})
local statr = racev:AddLabel("Race : ")
local statt = racev:AddLabel("nil")

racev:AddButton({
        Name = "Temper Of Time", 
        Callback = function()
            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(28286.35546875, 14896.5341796875, 102.62469482421875))
        end})
racev:AddButton({
    Name = "Race Door",
    Callback = function()
        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(28286.35546875, 14896.5341796875, 102.62469482421875))
        if game.Players.LocalPlayer.Data.Race.Value == 'Mink' then
			TP3(CFrame.new(29017.560546875, 14890.658203125, -379.031494140625))
			return
		elseif game.Players.LocalPlayer.Data.Race.Value == 'Human' then
			TP3(CFrame.new(29234.44921875, 14890.658203125, -206.6354217529297))
			return
		elseif game.Players.LocalPlayer.Data.Race.Value == 'Skypiea' then
			TP3(CFrame.new(28962.34765625, 14919.306640625, 233.89907836914062))
			return
		elseif game.Players.LocalPlayer.Data.Race.Value == 'Fishman' then
			TP3(CFrame.new(28228.796875, 14890.658203125, -210.81324768066406))
			return
		elseif game.Players.LocalPlayer.Data.Race.Value == 'Cyborg' then
			TP3(CFrame.new(28497.732421875, 14895.658203125, -421.8268127441406))
			return
		elseif game.Players.LocalPlayer.Data.Race.Value == 'Ghoul' then
			TP3(CFrame.new(28672.1640625, 14890.359375, 447.9342956542969))
			return
		end
    end
})
spawn(function()
    while wait() do
        pcall(function()
            if game.Players.LocalPlayer.Data.Race.Value == 'Mink' then
			statr:Set("Race : Rabbit")
			statt:Set("Red : แดชไกล\nBule : พายุ")
			return
		elseif game.Players.LocalPlayer.Data.Race.Value == 'Human' then
			statr:Set("Race : Human")
			statt:Set("Red : ดาเมจ\nBule : หายตัว")
			return
		elseif game.Players.LocalPlayer.Data.Race.Value == 'Skypiea' then
			statr:Set("Race : Angel")
			statt:Set("Red : บิน\nBule : สตั้น")
			return
		elseif game.Players.LocalPlayer.Data.Race.Value == 'Fishman' then
			statr:Set("Race : Fish")
			statt:Set("Red : เกาะ\nBule : สโล")
			return
		elseif game.Players.LocalPlayer.Data.Race.Value == 'Cyborg' then
			statr:Set("Race : Cyborg")
			statt:Set("Red : กระโดด\nBule : ดาเมจ")
			return
		elseif game.Players.LocalPlayer.Data.Race.Value == 'Ghoul' then
			statr:Set("Race : Ghoul")
			statt:Set("Red : ดูดเลือด\nBule : ดาเมจ")
			end
            end)
        end
    end)
--[[racev:AddToggle({
    Name = "Auto Complete Race",
    Callback = function()
        if game.Players.LocalPlayer.Data.Race.Value == 'Mink' then
			TP3(CFrame.new(29022.15234375, 14890.658203125, -379.0438232421875))
			_G.Mink_C = true
			return
		elseif game.Players.LocalPlayer.Data.Race.Value == 'Human' then
			TP3(CFrame.new(29237.986328125, 14890.658203125, -205.98892211914062))
			_G.Human_C = true
			return
		elseif game.Players.LocalPlayer.Data.Race.Value == 'Skypiea' then
			TP3(CFrame.new(28969.44921875, 14919.306640625, 234.9833526611328))
			_G.Skypiea_C = true
			return
		elseif game.Players.LocalPlayer.Data.Race.Value == 'Fishman' then
			TP3(CFrame.new(28222.759765625, 14890.658203125, -212.35557556152344))
			_G.Fishman_C = true
			return
		elseif game.Players.LocalPlayer.Data.Race.Value == 'Cyborg' then
			TP3(CFrame.new(28490.703125, 14895.658203125, -422.3362731933594))
			_G.Cyborg_C = true
			return
		elseif game.Players.LocalPlayer.Data.Race.Value == 'Ghoul' then
			TP3(CFrame.new(28673.861328125, 14890.3583984375, 455.34307861328125))
			_G.Ghoul_C = true
			return
		end
    end
})
spawn(function()
    while wait() do
        pcall(function()
            if _G.Mink_C then
            if game.Players.LocalPlayer.Data.Race.Value == 'Mink' then
                _G.KillAura = true -- true/false
                while _G.KillAura do wait()
                    for i,v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
                    v.Humanoid.Health = die
                    end
                end
            end
                end
            end)
        end
end)]]--
local Sha = Shop_Tab:CreateSection({Name = "Ability"})
Sha:AddButton({
    Name = "Buy SkyJump",
    Callback = function()
    local args = {
        [1] = "BuyHaki",
        [2] = "Geppo"
    }
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
end})
Sha:AddButton({
    Name = "Buy Soru",
    Callback = function()
    local args = {
        [1] = "BuyHaki",
        [2] = "Soru"
    }
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
end})
Sha:AddButton({
    Name = "Buy Haki",
    Callback = function()
    local args = {
        [1] = "BuyHaki",
        [2] = "Buso"
    }

    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))    
end})
Sha:AddButton({
    Name = "Buy KenHaki",
    Callback = function()
    local args = {
        [1] = "KenTalk",
        [2] = "Buy"
    }
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
end})
Sha:AddLabel("Fruit")
Sha:AddToggle({
    Name = "Auto Buy Random Fruit",
    _G.Setting_table.Auto_Buy_Random_Fruit,
    Callback = function(vu)
	_G.Setting_table.Auto_Buy_Random_Fruit = vu
	Update_Setting(getgenv()['MyName'])
end})
spawn(function()
    while wait(.2) do
        if _G.Setting_table.Auto_Buy_Random_Fruit then
            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Cousin","Buy")
            wait(20)
        end
    end
end)
Sha:AddToggle({
    Name = "Fruit Inventory",
    _G.Setting_table.Inventory_Fruit,
    Callback = function(vu)
	Inventory_Fruit = vu
	_G.Setting_table.Inventory_Fruit = vu
	Update_Setting(getgenv()['MyName'])
end})
if _G.Setting_table.Open_Don_Swan then
	Inventory_Fruit = true
end

spawn(function()
    while wait(2) do
		pcall(function()
			if Inventory_Fruit then
				if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Bomb Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Bomb Fruit") then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Bomb-Bomb")
					wait(1)
				end
				if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Spike Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Spike Fruit") then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Spike-Spike")
					wait(1)
				end
				if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Chop Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Chop Fruit") then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Chop-Chop")
					wait(1)
				end
				if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Spring Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Spring Fruit") then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Spring-Spring")
					wait(1)
				end
				if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Kilo Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Kilo Fruit") then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Kilo-Kilo")
					wait(1)
				end
				if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Smoke Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Smoke Fruit") then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Smoke-Smoke")
					wait(1)
				end
				if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Spin Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Spin Fruit") then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Spin-Spin")
					wait(1)
				end
				if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Flame Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Flame Fruit") then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Flame-Flame")
					wait(1)
				end
				if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Bird: Falcon Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Bird: Falcon Fruit") then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Bird-Bird: Falcon")
					wait(1)
				end
				if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Ice Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Ice Fruit") then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Ice-Ice")
					wait(1)
				end
				if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Sand Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Sand Fruit") then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Sand-Sand")
					wait(1)
				end
				if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Dark Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Dark Fruit") then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Dark-Dark")
					wait(1)
				end
				if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Revive Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Revive Fruit") then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Revive-Revive")
					wait(1)
				end
				if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Diamond Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Diamond Fruit") then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Diamond-Diamond")
					wait(1)
				end
				if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Light Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Light Fruit") then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Light-Light")
					wait(1)
				end
				if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Love Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Love Fruit") then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Love-Love")
					wait(1)
				end
				if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Rubber Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Rubber Fruit") then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Rubber-Rubber")
					wait(1)
				end
				if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Barrier Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Barrier Fruit") then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Barrier-Barrier")
					wait(1)
				end
				if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Magma Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Magma Fruit") then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Magma-Magma")
					wait(1)
				end
				if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Door Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Door Fruit") then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Door-Door")
					wait(1)
				end
				if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Quake Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Quake Fruit") then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Quake-Quake")
					wait(1)
				end
				if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Human-Human: Buddha Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Human-Human: Buddha Fruit") then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Human-Human: Buddha")
					wait(1)
				end
				if game:GetService("Players").LocalPlayer.Character:FindFirstChild("String Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("String Fruit") then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","String-String")
					wait(1)
				end
				if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Bird: Phoenix Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Bird: Phoenix Fruit") then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Bird-Bird: Phoenix")
					wait(1)
				end
				if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Rumble Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Rumble Fruit") then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Rumble-Rumble")
					wait(1)
				end
				if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Paw Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Paw Fruit") then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Paw-Paw")
					wait(1)
				end
				if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Gravity Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Gravity Fruit") then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Gravity-Gravity")
					wait(1)
				end
				if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Dough Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Dough Fruit") then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Dough-Dough")
					wait(1)
				end
				if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Shadow Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Shadow Fruit") then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Shadow-Shadow")
					wait(1)
				end
				if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Venom Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Venom Fruit") then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Venom-Venom")
					wait(1)
				end
				if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Control Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Control Fruit") then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Control-Control")
					wait(1)
				end
				if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Dragon Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Dragon Fruit") then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Dragon-Dragon")
					wait(1)
				end
				if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Soul Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Soul Fruit") then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Soul-Soul")
					wait(1)
				end	
			end
		end)
    end
end)
Sha:AddToggle({
    Name = "Bring Fruit",
    _G.Setting_table.BringFruit,
    Callback = function(vu)
	BringFruit = vu
	_G.Setting_table.BringFruit = vu
	Update_Setting(getgenv()['MyName'])
end})
if _G.Setting_table.BringFruit then
	BringFruit = true
end
spawn(function()
    while wait(.2) do
        pcall(function()
            if BringFruit or BringFruit_P then
                for i,v6 in pairs(game:GetService("Workspace"):GetChildren()) do
                    if v6:IsA ("Tool") and (v6.Handle.Position-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude < 13000 then
                        game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = v6.Handle.CFrame
                        v6.Handle.CFrame = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame
                    end
                end
            end
        end)
    end
end)
spawn(function()
    while wait(3) do
        if _G.Hop_Bring_Fruit then
            wait(15)
            _G.Hop_Bring_Fruit_Ex = true
        end
    end
end)
Sha:AddToggle({
    Name = "Devil Fruit Sniper",
    _G.Setting_table.Sniper_Fruit,
    Callback = function(vu)
	_G.Setting_table.Sniper_Fruit = vu
	Update_Setting(getgenv()['MyName'])
end})
local l__Remotes__11 = game.ReplicatedStorage:WaitForChild("Remotes");
u45 = l__Remotes__11.CommF_:InvokeServer("GetFruits");
Table_DevilFruitSniper = {}
for i,v in next,u45 do
    table.insert(Table_DevilFruitSniper,v.Name)
end
if _G.Setting_table.Select_Fruit == nil then
    _G.Setting_table.Select_Fruit = ""
end
Sha:AddDropdown({
    Name = "Select Devil Fruit Sniper",
    _G.Setting_table.Select_Fruit,
    List = Table_DevilFruitSniper,
    Callback = function(vu)
	_G.Setting_table.Select_Fruit = vu
	Update_Setting(getgenv()['MyName'])
end})
spawn(function()
    while wait(3) do
        if _G.Setting_table.Sniper_Fruit then
            for s,f in pairs(_G.Setting_table.Select_Fruit) do
                game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("GetFruits")
                game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("PurchaseRawFruit",f)
			end
			wait(30)
        end
    end
end)

Sha:AddLabel("Melee")
Sha:AddButton({
    Name = "Buy Electro",
    Callback = function()
    local args = {
        [1] = "BuyElectro"
    }
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
end})
Sha:AddButton({
    Name = "Buy Black Leg",
    Callback = function()
    local args = {
        [1] = "BuyBlackLeg"
    }
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
end})
Sha:AddButton({
    Name = "Buy Fishman Karate",
    Callback = function()
    local args = {
        [1] = "BuyFishmanKarate"
    }
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
end})

Sha:AddButton({
    Name = "Buy Dragon Claw",
    Callback = function()
    local args = {
        [1] = "BlackbeardReward",
        [2] = "DragonClaw",
        [3] = "1"
    }
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
    local args = {
        [1] = "BlackbeardReward",
        [2] = "DragonClaw",
        [3] = "2"
    }
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
end})
Sha:AddLabel("Melee v2")
Sha:AddButton({
    Name = "Buy Superhuman",
    Callback = function()
    local args = {
        [1] = "BuySuperhuman"
    }

    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
end})

Sha:AddButton({
    Name = "Buy Death Step",
    Callback = function()
    local args = {
        [1] = "BuyDeathStep"
    }

    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
end})

Sha:AddButton({
    Name = "Buy Shakman Karate",
    Callback = function()
    local args = {
        [1] = "BuySharkmanKarate",
        [2] = true
    }
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
    local args = {
        [1] = "BuySharkmanKarate"
    }
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
end})
Sha:AddButton({
    Name = "Buy ElectricClaw",
    Callback = function()
    local args = {
        [1] = "BuyElectricClaw"
        }
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
end})

    Sha:AddButton({
        Name = "Buy Dragon Talon",
        Callback = function()
        local args = {
            [1] = "BuyDragonTalon",
            [2] = true
            }
        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
        local args = {
            [1] = "BuyDragonTalon"
            }
        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
    end})
    
    Sha:AddButton({
        Name = "Buy GodHuman",
        Callback = function()

    local args = {
        [1] = "BuyGodhuman",
        [2] = true
    }
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
    local args = {
        [1] = "BuyGodhuman"
    }
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
    end})

	Sha:AddLabel("Sword")
Sha:AddButton({
    Name = "Buy Katana",
    Callback = function()
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Katana")
end})
Sha:AddButton({
    Name = "Buy Cutlass",
    Callback = function()
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Cutlass")
end})
Sha:AddButton({
    Name = "Buy Duel Katana",
    Callback = function()
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Duel Katana")
end})
Sha:AddButton({
    Name = "Buy Iron Mace",
    Callback = function()
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Iron Mace")
end})
Sha:AddButton({
    Name = "Buy Pipe",
    Callback = function()
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Pipe")
end})
Sha:AddButton({
    Name = "Buy Triple Katana",
    Callback = function()
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Triple Katana")
end})
Sha:AddButton({
    Name = "Buy Dual-Headed Blade",
    Callback = function()
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Dual-Headed Blade")
end})
Sha:AddButton({
    Name = "Buy Bisento",
    Callback = function()
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Bisento")
end})
Sha:AddButton({
    Name = "Buy Soul Cane",
    Callback = function()
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Soul Cane")
end})

Sha:AddLabel("Gun")
Sha:AddButton({
    Name = "Buy Slingshot",
    Callback = function()
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Slingshot")
end})
Sha:AddButton({
    Name = "Buy Musket",
    Callback = function()
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Musket")
end})
Sha:AddButton({
    Name = "Buy Fintlock",
    Callback = function()
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Flintlock")
end})
Sha:AddButton({
    Name = "Buy Refined Flintlock",
    Callback = function()
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Refined Flintlock")
end})
Sha:AddButton({
    Name = "Buy Cannon",
    Callback = function()
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Cannon")
end})
Sha:AddButton({
    Name = "Buy Kabucha",
    Callback = function()
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BlackbeardReward","Slingshot","1")
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BlackbeardReward","Slingshot","2")
end})

Sha:AddLabel("Fragments")
Sha:AddButton({
    Name = "Buy Refund Stat",
    Callback = function()
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BlackbeardReward","Refund","1")
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BlackbeardReward","Refund","2")
end})
Sha:AddButton({
    Name = "Buy Random Race",
    Callback = function()
    local args = {
        [1] = "BlackbeardReward",
        [2] = "Reroll",
        [3] = "2"
    }
    
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
end})
Sha:AddButton({
    Name = "Buy Color Buso Haki",
    Callback = function()
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("ColorsDealer", "2")
end})
Sha:AddToggle({
    Name = "Auto Buy Color Buso Haki",
    _G.Setting_table.Buso_Haki,
    Callback = function(vu)
	_G.Setting_table.Buso_Haki = vu
	Buso_Haki_Buy = vu
	Update_Setting(getgenv()['MyName'])
end})

spawn(function()
	while wait(.5) do
		pcall(function()
			if Buso_Haki_Buy then
				game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("ColorsDealer", "2")
			else
				wait(3)
			end
		end)
	end
end)

spawn(function()
	while wait(2) do
		pcall(function()
			if _G.Setting_table.Buso_Haki_Hop then
				wait(10)
				HopServer()
				wait(50)
			else
				wait(3)
			end
		end)
	end
end)




Quest_Tab:Toggle("No Color Haki","9610159123",_G.Setting_table.No_Color_Haki_Tushita,function(vu)
	_G.Setting_table.No_Color_Haki_Tushita = vu
	Update_Setting(getgenv()['MyName'])
end)
Quest_Tab:Toggle("Auto Twin Hooks","9610159123",_G.Setting_table.Auto_Twin_Hooks,function(vu)
	Auto_Twin_Hooks = vu
	_G.Setting_table.Auto_Twin_Hooks = vu
	Update_Setting(getgenv()['MyName'])
end)
spawn(function()
	while wait(.5) do
		pcall(function()
			if Auto_Twin_Hooks then
				if not Mix_Farm or Auto_Twin_Hooks_Farm then
					if game.Workspace.Enemies:FindFirstChild("Captain Elephant [Lv. 1875] [Boss]") or game.ReplicatedStorage:FindFirstChild("Captain Elephant [Lv. 1875] [Boss]") then
						Auto_Twin_Hooks_Farm = true
						Mix_Farm = true
						if game.Workspace.Enemies:FindFirstChild("Captain Elephant [Lv. 1875] [Boss]") then
							game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("SetSpawnPoint")
							for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
								if v.Name == "Captain Elephant [Lv. 1875] [Boss]" and v.Humanoid.Health > 0 then
									if v.Humanoid:FindFirstChild("Animator") then
										v.Humanoid.Animator:Destroy()
									end
									repeat wait(_G.Fast_Delay)
										EquipWeapon(_G.Setting_table.Weapon)
										TP(v.HumanoidRootPart.CFrame*CFrame.new(0,30,0))
										AttackNoCD()
									until v.Humanoid.Health <= 0 or not v.Parent or not Auto_Twin_Hooks
								end
							end
						elseif game.ReplicatedStorage:FindFirstChild("Captain Elephant [Lv. 1875] [Boss]") then
							TP(game.ReplicatedStorage:FindFirstChild("Captain Elephant [Lv. 1875] [Boss]").HumanoidRootPart.CFrame*CFrame.new(0,30,0))
						end
					elseif _G.Setting_table.Auto_Twin_Hooks_Hop then
						wait(5)
						if not game.Workspace.Enemies:FindFirstChild("Captain Elephant [Lv. 1875] [Boss]") and not game.ReplicatedStorage:FindFirstChild("Captain Elephant [Lv. 1875] [Boss]") then
							HopServer()
							wait(50)
						end
					elseif Auto_Twin_Hooks_Farm then
						Auto_Twin_Hooks_Farm = nil
						Mix_Farm = nil
					end
				end
			else
				wait(2)
			end
		end)
	end
end)
Quest_Tab:Toggle("Auto Canvander","9610159123",_G.Setting_table.Auto_Canvander,function(vu)
	Auto_Canvander = vu
	_G.Setting_table.Auto_Canvander = vu
	Update_Setting(getgenv()['MyName'])
end)
spawn(function()
	while wait(.5) do
		pcall(function()
			if Auto_Canvander then
				if not Mix_Farm or Auto_Canvander_Farm then
					if game.Workspace.Enemies:FindFirstChild("Beautiful Pirate [Lv. 1950] [Boss]") or game.ReplicatedStorage:FindFirstChild("Beautiful Pirate [Lv. 1950] [Boss]") then
						Auto_Canvander_Farm = true
						Mix_Farm = true
						if game.Workspace.Enemies:FindFirstChild("Beautiful Pirate [Lv. 1950] [Boss]") then
							game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("SetSpawnPoint")
							for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
								if v.Name == "Beautiful Pirate [Lv. 1950] [Boss]" and v.Humanoid.Health > 0 then
									if v.Humanoid:FindFirstChild("Animator") then
										v.Humanoid.Animator:Destroy()
									end
									repeat wait(_G.Fast_Delay)
										EquipWeapon(_G.Setting_table.Weapon)
										TP(v.HumanoidRootPart.CFrame*CFrame.new(0,30,0))
										AttackNoCD()
									until v.Humanoid.Health <= 0 or not v.Parent or not Auto_Canvander
								end
							end
						elseif game.ReplicatedStorage:FindFirstChild("Beautiful Pirate [Lv. 1950] [Boss]") then
							TP(game.ReplicatedStorage:FindFirstChild("Beautiful Pirate [Lv. 1950] [Boss]").HumanoidRootPart.CFrame*CFrame.new(0,30,0))
						end
					elseif _G.Setting_table.Auto_Canvander_Hop then
						wait(5)
						if not game.Workspace.Enemies:FindFirstChild("Beautiful Pirate [Lv. 1950] [Boss]") and not game.ReplicatedStorage:FindFirstChild("Beautiful Pirate [Lv. 1950] [Boss]") then
							HopServer()
							wait(50)
						end
					elseif Auto_Canvander_Farm then
						Auto_Canvander_Farm = nil
						Mix_Farm = nil
					end
				end
			else
				wait(2)
			end
		end)
	end
end)
Quest_Tab:Toggle("Auto Buddy Sword","9610159123",_G.Setting_table.Auto_Buddy_Sword,function(vu)
	Auto_Buddy_Sword = vu
	_G.Setting_table.Auto_Buddy_Sword = vu
	Update_Setting(getgenv()['MyName'])
end)
spawn(function()
	while wait(.5) do
		pcall(function()
			if Auto_Buddy_Sword then
				if not Mix_Farm or Auto_Buddy_Sword_Farm then
					if game.Workspace.Enemies:FindFirstChild("Cake Queen [Lv. 2175] [Boss]") or game.ReplicatedStorage:FindFirstChild("Cake Queen [Lv. 2175] [Boss]") then
						Auto_Buddy_Sword_Farm = true
						Mix_Farm = true
						if game.Workspace.Enemies:FindFirstChild("Cake Queen [Lv. 2175] [Boss]") then
							game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("SetSpawnPoint")
							for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
								if v.Name == "Cake Queen [Lv. 2175] [Boss]" and v.Humanoid.Health > 0 then
									if v.Humanoid:FindFirstChild("Animator") then
										v.Humanoid.Animator:Destroy()
									end
									repeat wait(_G.Fast_Delay)
										EquipWeapon(_G.Setting_table.Weapon)
										TP(v.HumanoidRootPart.CFrame*CFrame.new(0,30,0))
										AttackNoCD()
									until v.Humanoid.Health <= 0 or not v.Parent or not Auto_Buddy_Sword
								end
							end
						elseif game.ReplicatedStorage:FindFirstChild("Cake Queen [Lv. 2175] [Boss]") then
							TP(game.ReplicatedStorage:FindFirstChild("Cake Queen [Lv. 2175] [Boss]").HumanoidRootPart.CFrame*CFrame.new(0,30,0))
						end
					elseif _G.Setting_table.Auto_Buddy_Sword_Hop then
						wait(5)
						if not game.Workspace.Enemies:FindFirstChild("Cake Queen [Lv. 2175] [Boss]") and not game.ReplicatedStorage:FindFirstChild("Cake Queen [Lv. 2175] [Boss]") then
							HopServer()
							wait(50)
						end
					elseif Auto_Buddy_Sword_Farm then
						Auto_Buddy_Sword_Farm = nil
						Mix_Farm = nil
					end
				end
			else
				wait(2)
			end
		end)
	end
end)
Quest_Tab:Toggle("Auto Hallow Scryte","9606294253",_G.Setting_table.Auto_Hallow_Scryte,function(vu)
	Auto_Hallow_Scryte = vu
	_G.Setting_table.Auto_Hallow_Scryte = vu
	Update_Setting(getgenv()['MyName'])
end)
spawn(function()
	while wait(.5) do
		pcall(function()
			if Auto_Hallow_Scryte then
				if game.Workspace.Enemies:FindFirstChild("Soul Reaper [Lv. 2100] [Raid Boss]") or game.ReplicatedStorage:FindFirstChild("Soul Reaper [Lv. 2100] [Raid Boss]") then
					if game.Workspace.Enemies:FindFirstChild("Soul Reaper [Lv. 2100] [Raid Boss]") then
						game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("SetSpawnPoint")
						for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
							if v.Name == "Soul Reaper [Lv. 2100] [Raid Boss]" and v.Humanoid.Health > 0 then
								if v.Humanoid:FindFirstChild("Animator") then
									v.Humanoid.Animator:Destroy()
								end
								repeat wait(_G.Fast_Delay)
									EquipWeapon(_G.Setting_table.Weapon)
									TP(v.HumanoidRootPart.CFrame*CFrame.new(0,30,0))
									AttackNoCD()
								until v.Humanoid.Health <= 0 or not v.Parent or not Auto_Hallow_Scryte
							end
						end
					elseif game.ReplicatedStorage:FindFirstChild("Soul Reaper [Lv. 2100] [Raid Boss]") then
						TP(game.ReplicatedStorage:FindFirstChild("Soul Reaper [Lv. 2100] [Raid Boss]").HumanoidRootPart.CFrame*CFrame.new(0,30,0))
					end
				elseif game.Players.LocalPlayer.Character:FindFirstChild("Hallow Essence") or game.Players.LocalPlayer.Backpack:FindFirstChild("Hallow Essence") then
					repeat wait(.3)
						EquipWeapon("Hallow Essence")
						TP2(CFrame.new(-8932.86, 143.258, 6063.31))
					until not game.Players.LocalPlayer.Character:FindFirstChild("Hallow Essence") and not game.Players.LocalPlayer.Backpack:FindFirstChild("Hallow Essence") or game.Workspace.Enemies:FindFirstChild("Soul Reaper [Lv. 2100] [Raid Boss]") or game.ReplicatedStorage:FindFirstChild("Soul Reaper [Lv. 2100] [Raid Boss]") 
				elseif _G.Setting_table.Hallow_Scryte_Hop then
					wait(5)
					if not game.Workspace.Enemies:FindFirstChild("Soul Reaper [Lv. 2100] [Raid Boss]") and not game.ReplicatedStorage:FindFirstChild("Soul Reaper [Lv. 2100] [Raid Boss]") then
						HopServer()
						wait(50)
					end
				else
					local args = {
						[1] = "Bones",
						[2] = "Check"
					}
					
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
			
					local args = {
						[1] = "Bones",
						[2] = "Buy",
						[3] = 1,
						[4] = 1
					}
					
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
					if game.Workspace.Enemies:FindFirstChild("Reborn Skeleton [Lv. 1975]") then
						game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("SetSpawnPoint")
						for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
							if v.Name == "Reborn Skeleton [Lv. 1975]" and v.Humanoid.Health > 0 then
								if v.Humanoid:FindFirstChild("Animator") then
									v.Humanoid.Animator:Destroy()
								end
								_G.PosMon = v.HumanoidRootPart.CFrame
								StatrMagnet = true
								repeat wait(_G.Fast_Delay)
									EquipWeapon(_G.Setting_table.Weapon)
									TP(v.HumanoidRootPart.CFrame*CFrame.new(0,30,0))
									AttackNoCD()
								until v.Humanoid.Health <= 0 or not v.Parent or not Auto_Hallow_Scryte
								StatrMagnet = false
							end
						end
					elseif game.ReplicatedStorage:FindFirstChild("Reborn Skeleton [Lv. 1975]") then
						TP(game.ReplicatedStorage:FindFirstChild("Reborn Skeleton [Lv. 1975]").HumanoidRootPart.CFrame*CFrame.new(0,30,0))
					end
				end
			else
				wait(2)
			end
		end)
	end
end)
Quest_Tab:Toggle("Auto Dark Dagger","9610159123",_G.Setting_table.Auto_Dark_Dagger,function(vu)
	Auto_Dark_Dagger = vu
	_G.Setting_table.Auto_Dark_Dagger = vu
	Update_Setting(getgenv()['MyName'])
end)
function TelePQ(p)
	if (p.Position-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude >= 3000 and not Auto_Raid then
		if game.Players.LocalPlayer.Data.SpawnPoint.Value == 'Fountain' then
			_G.Stop_Tween = true
			Tween:Cancel()
			game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(61163.8515625, 11.6796875, 1819.7841796875))
			wait(1)
			_G.Stop_Tween = nil
		else
			_G.Stop_Tween = true
			local Speed = 100
			local Distance = 100
			game:GetService("TweenService"):Create(
				game.Players.LocalPlayer.Character.HumanoidRootPart,
				TweenInfo.new(Distance/Speed, Enum.EasingStyle.Linear),
				{CFrame = P1}
			):Cancel()
			TP(game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame*CFrame.new(0,30,0))
			wait(1)
			if not Auto_Raid then
				game.Players.LocalPlayer.Character.Humanoid:ChangeState(15)
				wait(.5)
				repeat wait(.2)
					game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = p
					wait()
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("SetSpawnPoint")
				until game.Players.LocalPlayer.Character.Humanoid.Health > 0
				wait(2)
				_G.Stop_Tween = nil
			end
		end
	end
end
spawn(function()
	while wait(.5) do
		pcall(function()
			if Auto_Dark_Dagger then
                if game.Workspace.Enemies:FindFirstChild("rip_indra True Form [Lv. 5000] [Raid Boss]") or game.ReplicatedStorage:FindFirstChild("rip_indra True Form [Lv. 5000] [Raid Boss]") then
                    if game.Workspace.Enemies:FindFirstChild("rip_indra True Form [Lv. 5000] [Raid Boss]") then
                        for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
                            if v.Name == "rip_indra True Form [Lv. 5000] [Raid Boss]" and v.Humanoid.Health > 0 then
                                if v.Humanoid:FindFirstChild("Animator") then
                                    v.Humanoid.Animator:Destroy()
                                end
                                repeat wait(_G.Fast_Delay)
                                    EquipWeapon(_G.Setting_table.Weapon)
                                    TP(v.HumanoidRootPart.CFrame*CFrame.new(0,30,0))
                                    AttackNoCD()
                                until not v.Parent or v.Humanoid.Health <= 0 or not Auto_Dark_Dagger
                            end
                        end
                    elseif game.ReplicatedStorage:FindFirstChild("rip_indra True Form [Lv. 5000] [Raid Boss]") then
                        TP(game.ReplicatedStorage:FindFirstChild("rip_indra True Form [Lv. 5000] [Raid Boss]").HumanoidRootPart.CFrame*CFrame.new(0,30,0))
                    end
                else
                    wait(5)
                    if game.Workspace.Enemies:FindFirstChild("rip_indra True Form [Lv. 5000] [Raid Boss]") or game.ReplicatedStorage:FindFirstChild("rip_indra True Form [Lv. 5000] [Raid Boss]") then
                    else
                        HopServer()
                        wait(20)
                    end
                end
			end
		end)
	end
end)
Quest_Tab:Toggle("No Color Haki","9610159123",_G.Setting_table.No_Color_Haki_Dark_Dagger,function(vu)
	_G.Setting_table.No_Color_Haki_Dark_Dagger = vu
	Update_Setting(getgenv()['MyName'])
end)
function activatefly()
	local mouse=game.Players.LocalPlayer:GetMouse''
	localplayer=game.Players.LocalPlayer
	game.Players.LocalPlayer.Character:WaitForChild("HumanoidRootPart")
	local torso = game.Players.LocalPlayer.Character.HumanoidRootPart
	local keys={a=false,d=false,w=false,s=false}
	local e1
	local e2
	local function start()
		local pos = Instance.new("BodyPosition",torso)
		local gyro = Instance.new("BodyGyro",torso)
		pos.Name="EPIXPOS"
		pos.maxForce = Vector3.new(math.huge, math.huge, math.huge)
		pos.position = torso.Position
		gyro.maxTorque = Vector3.new(9e9, 9e9, 9e9)
		gyro.cframe = torso.CFrame
		repeat
			wait()
			localplayer.Character.Humanoid.PlatformStand=true
			local new=gyro.cframe - gyro.cframe.p + pos.position
			if not keys.w and not keys.s and not keys.a and not keys.d then
				speed=1
			end
			if keys.w then
				new = new + workspace.CurrentCamera.CoordinateFrame.lookVector * speed
				speed=speed+speedSET
			end
			if keys.s then
				new = new - workspace.CurrentCamera.CoordinateFrame.lookVector * speed
				speed=speed+speedSET
			end
			if keys.d then
				new = new * CFrame.new(speed,0,0)
				speed=speed+speedSET
			end
			if keys.a then
				new = new * CFrame.new(-speed,0,0)
				speed=speed+speedSET
			end
			if speed>speedSET then
				speed=speedSET
			end
				pos.position=new.p
			if keys.w then
				gyro.cframe = workspace.CurrentCamera.CoordinateFrame*CFrame.Angles(-math.rad(speed*15),0,0)
			elseif keys.s then
				gyro.cframe = workspace.CurrentCamera.CoordinateFrame*CFrame.Angles(math.rad(speed*15),0,0)
			else
				gyro.cframe = workspace.CurrentCamera.CoordinateFrame
			end
		until not Fly
		if gyro then 
			gyro:Destroy() 
		end
		if pos then 
			pos:Destroy() 
		end
		flying=false
		localplayer.Character.Humanoid.PlatformStand=false
		speed=0
	end
	e1=mouse.KeyDown:connect(function(key)
		if not torso or not torso.Parent then 
			flying=false e1:disconnect() e2:disconnect() return 
		end
		if key=="w" then
			keys.w=true
		elseif key=="s" then
			keys.s=true
		elseif key=="a" then
			keys.a=true
		elseif key=="d" then
			keys.d=true
		end
	end)
	e2=mouse.KeyUp:connect(function(key)
		if key=="w" then
			keys.w=false
		elseif key=="s" then
			keys.s=false
		elseif key=="a" then
			keys.a=false
		elseif key=="d" then
			keys.d=false
		end
	end)
	start()
end
PvP_Tab:Label("Main")
PvP_Tab:Toggle("Fly","9606294253",_G.Setting_table.Fly,function(vu)
	Fly = vu
	_G.Setting_table.Fly = vu
	Update_Setting(getgenv()['MyName'])
	if vu then
		activatefly()
	end
end)
_G.Setting_table.Speed = 15
speedSET = 15
PvP_Tab:Slider("Speed",1,50,_G.Setting_table.Speed,function(vu)
	speedSET = vu
	_G.Setting_table.Speed = vu
	Update_Setting(getgenv()['MyName'])
end)

PvP_Tab:Label("Misc")
PvP_Tab:Toggle("Auto PvP Turn On","9606294253",_G.Setting_table.Auto_PvP_Turn_On,function(vu)
	_G.Setting_table.Auto_PvP_Turn_On = vu
	Update_Setting(getgenv()['MyName'])
end)
spawn(function()
	while wait(1) do
		pcall(function()
			if _G.Setting_table.Auto_PvP_Turn_On then
				game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("EnablePvp")
			end
		end)
	end
end)
PvP_Tab:Toggle("Auto Teleport To Position Spawn","9606294253",_G.Setting_table.TP_Position_Spawn,function(vu)
	_G.Setting_table.TP_Position_Spawn = vu
	Update_Setting(getgenv()['MyName'])
end)
spawn(function()
	while wait(1) do
		pcall(function()
			if _G.Setting_table.TP_Position_Spawn then
				if _G.Setting_table.Pos_Spawn ~= nil and game.Players.LocalPlayer.Character.Humanoid.Health > 0 then
					TP(_G.Setting_table.Pos_Spawn)
				end
			end
		end)
	end
end)
PvP_Tab:Button("Set Position Spawn",function()
	_G.Setting_table.Pos_Spawn = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame
	Update_Setting(getgenv()['MyName'])
	Com()
end)

PvP_Tab:Label("No Cooldown & Infinity")
PvP_Tab:Toggle("Soru No Cooldown","9606294253",_G.Setting_table.Sorunocool,function(vu)
	Sorunocool = vu
	_G.Setting_table.Sorunocool = vu
	if vu then
		NoSoruCool()
	end
	Update_Setting(getgenv()['MyName'])
end)
function NoSoruCool()
    for i, v in pairs(getgc()) do
        if type(v) == "function" and getfenv(v).script == game.Players.LocalPlayer.Character:WaitForChild("Soru") then
            for i2,v2 in pairs(debug.getupvalues(v)) do
                if type(v2) == 'table' then
                    if v2.LastUse then
                        repeat wait()
                            setupvalue(v, i2, {LastAfter = 0,LastUse = 0})
                        until not Sorunocool
                    end
                end
            end
        end
    end
end
PvP_Tab:Toggle("Dodge No Cooldown","9606294253",_G.Setting_table.Dodge_No_Cooldown,function(vu)
	nododgecool = vu
	_G.Setting_table.Dodge_No_Cooldown  = vu
	Update_Setting(getgenv()['MyName'])
    if vu then
        NoDodgeCool()
    end
end)
	function NoDodgeCool()
		if nododgecool then
			for i,v in next, getgc() do
				if game.Players.LocalPlayer.Character.Dodge then
					if typeof(v) == "function" and getfenv(v).script == game.Players.LocalPlayer.Character.Dodge then
						for i2,v2 in next, getupvalues(v) do
							if tostring(v2) == "0.4" then
								repeat wait(.1)
									setupvalue(v,i2,0)
								until not nododgecool
							end
						end
					end
				end
			end
		end
	end
PvP_Tab:Toggle("Infinity Geppo","9606294253",_G.Setting_table.Infinity_Geppo,function(vu)
	noGeppocool = vu
	_G.Setting_table.Infinity_Geppo = vu
	Update_Setting(getgenv()['MyName'])
    if vu then
        NoGeppoCool()
    end
end)
function NoGeppoCool()
    if noGeppocool then
        for i,v in next, getgc() do
            if game.Players.LocalPlayer.Character.Geppo then
                if typeof(v) == "function" and getfenv(v).script == game.Players.LocalPlayer.Character.Geppo then
                    for i2,v2 in next, getupvalues(v) do
                        if tostring(v2) == "0" then
                            repeat wait(.1)
                                setupvalue(v,i2,0)
                            until not noGeppocool
                        end
                    end
                end
            end
        end
    end
end
PvP_Tab:Toggle("Infinity Energy","9606294253",_G.Setting_table.InfinitsEnergy,function(vu)
	InfinitsEnergy = vu
	if vu then
		infinitestam()
	end
	_G.Setting_table.InfinitsEnergy = vu
	Update_Setting(getgenv()['MyName'])
end)
	local LocalPlayer = game:GetService'Players'.LocalPlayer
	local originalstam = LocalPlayer.Character.Energy.Value
	function infinitestam()
		game:GetService'Players'.LocalPlayer.Character.Energy.Changed:connect(function()
			if InfinitsEnergy then
				LocalPlayer.Character.Energy.Value = originalstam
			end 
		end)
	end
PvP_Tab:Label("Bounty")
	PvP_Tab:Toggle("Aattack","9606294253",false,function(vu)
		Attack = vu
	end)
	PlayerName = {}
	for i,v in pairs(game.Players:GetChildren()) do  
		table.insert(PlayerName ,v.Name)
	end
	SelectedKillPlayer = "..."
	local Sl_P = PvP_Tab:Dropdown("Select Player","...",PlayerName,function(vu)
		SelectedKillPlayer = vu
	end)
	PvP_Tab:Button("Refresh Select Player",function()
		Sl_P:Clear()
		for i,v in pairs(game.Players:GetChildren()) do  
			Sl_P:Add(v.Name)
		end
	end)
	spawn(function()
		local gg = getrawmetatable(game)
		local old = gg.__namecall
		setreadonly(gg,false)
		gg.__namecall = newcclosure(function(...)
			local method = getnamecallmethod()
			local args = {...}
			if tostring(method) == "FireServer" then
				if tostring(args[1]) == "RemoteEvent" then
					if tostring(args[2]) ~= "true" and tostring(args[2]) ~= "false" then
						if UseSkillMasteryDevilFruit then
							args[2] = PositionSkillMasteryDevilFruit
							return old(unpack(args))
						elseif Skillaimbot then
							args[2] = AimBotSkillPosition
							return old(unpack(args))
						end
					end
				end
			end
			return old(...)
		end)
	end)
	PvP_Tab:Toggle("Aimbot Gun","9606294253",false,function(vu)
		Aimbot = vu
		if vu then
			for i,v in pairs(game.Players.LocalPlayer.Backpack:GetChildren()) do  
				if v:IsA("Tool") then
					if v:FindFirstChild("RemoteFunctionShoot") then 
						SelectToolWeaponGun = v.Name
					end
				end
			end
			for i,v in pairs(game.Players.LocalPlayer.Character:GetChildren()) do  
				if v:IsA("Tool") then
					if v:FindFirstChild("RemoteFunctionShoot") then 
						SelectToolWeaponGun = v.Name
					end
				end
			end
		end
	end)
	PvP_Tab:Toggle("Aimbot Skill","9606294253",false,function(vu)
		Skillaimbot = vu
		if Skillaimbot then
			if game.Players:FindFirstChild(SelectedKillPlayer) and game.Players:FindFirstChild(SelectedKillPlayer).Character:FindFirstChild("HumanoidRootPart") and game.Players:FindFirstChild(SelectedKillPlayer).Character:FindFirstChild("Humanoid") and game.Players:FindFirstChild(SelectedKillPlayer).Character.Humanoid.Health > 0 then
				AimBotSkillPosition = game.Players:FindFirstChild(SelectedKillPlayer).Character:FindFirstChild("HumanoidRootPart").Position
			end
		end
	end)
	local lp = game:GetService('Players').LocalPlayer
	local mouse = lp:GetMouse()
	mouse.Button1Down:Connect(function()
		if Aimbot and game.Players.LocalPlayer.Character:FindFirstChild(SelectToolWeaponGun) and game:GetService("Players"):FindFirstChild(SelectedKillPlayer) then
			tool = game:GetService("Players").LocalPlayer.Character[SelectToolWeaponGun]
			v17 = workspace:FindPartOnRayWithIgnoreList(Ray.new(tool.Handle.CFrame.p, (game:GetService("Players"):FindFirstChild(SelectedKillPlayer).Character.HumanoidRootPart.Position - tool.Handle.CFrame.p).unit * 100), { game.Players.LocalPlayer.Character, workspace._WorldOrigin });
			game:GetService("Players").LocalPlayer.Character[SelectToolWeaponGun].RemoteFunctionShoot:InvokeServer(game:GetService("Players"):FindFirstChild(SelectedKillPlayer).Character.HumanoidRootPart.Position, (require(game.ReplicatedStorage.Util).Other.hrpFromPart(v17)));
		end
	end)
PvP_Tab:Toggle("Auto Farm Bounty","9606294253",_G.Setting_table.Auto_Farm_Bounty,function(vu)
	Auto_Farm_Bounty = vu
	_G.Setting_table.Auto_Farm_Bounty = vu
	Update_Setting(getgenv()['MyName'])
end)
PvP_Tab:Slider("Skip Player",1,30,10,function(vu)
	Skip_S = vu
end)
Skip_S = 10
function Get_Mon(vu)    
	for i,v in pairs(game.Workspace.Characters:GetChildren()) do
		if v.Name ~= game.Players.LocalPlayer.Name and v.Name ~= "Sapab" then
			if (v.HumanoidRootPart.Position-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= tonumber(vu) then
				_G.Players_Mon = v
				return
			end
		end
	end
end
spawn(function()
	while wait(.5) do
		pcall(function()
			if Auto_Farm_Bounty then
				_G.Players_Mon = nil
				for i = 10000,500,-500 do
					Get_Mon(i)
				end
				if _G.Players_Mon ~= nil then
					print("Player : "..tostring(_G.Players_Mon.Name))
					SelectedKillPlayer = _G.Players_Mon.Name
					Start_Kill = true
					repeat wait(.1)
					until Kop
					repeat task.wait()
						EquipWeapon(_G.Setting_table.Weapon)
						if game:GetService("Players")["LocalPlayer"].PlayerGui.Main.InCombat.Visible == true then
							TP(_G.Players_Mon.HumanoidRootPart.CFrame*CFrame.new(0,10,0))
						else
							TP(_G.Players_Mon.HumanoidRootPart.CFrame)
						end
						game:GetService'VirtualUser':Button1Down(Vector2.new(1280,600))
						if Skillaimbot and (_G.Players_Mon.HumanoidRootPart.Position-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 30 then
							game:service('VirtualInputManager'):SendKeyEvent(true, "X", false, game)
							wait(.1)
							game:service('VirtualInputManager'):SendKeyEvent(false, "X", false, game)
						end
					until _G.Players_Mon == nil or not _G.Players_Mon.Parent or _G.Players_Mon.Humanoid.Health <= 0 or not Auto_Farm_Bounty or game.Players.LocalPlayer.Character.Humanoid.Health <= 0
					if _G.Players_Mon ~= nil then
						print("Kill : "..tostring(_G.Players_Mon.Name))
					end
					_G.Players_Mon.Name = "Sapab"
				end
			end
		end)
	end
end)
spawn(function()
	while wait(.5) do
		pcall(function()
			if Start_Kill then
				Kop = true
				Kip = 0
				repeat wait()
					if (_G.Players_Mon.HumanoidRootPart.Position-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 500 then
						if game:GetService("Players")["LocalPlayer"].PlayerGui.Main.InCombat.Visible == true then
						else
							wait(1)
							Kip = Kip + 1
							print("Skip : "..tostring(Kip))
						end
					end
				until Kip >= Skip_S or not _G.Players_Mon.Parent or _G.Players_Mon.Humanoid.Health <= 0 or not Auto_Farm_Bounty
				Start_Kill = false
				Kop = false
				if Kip >= Skip_S then
					_G.Players_Mon.Name = "Sapab"
					_G.Players_Mon = nil
				end
			end
		end)
	end
end)

General_Tab:Toggle("Mob Aura","9606294253",_G.Setting_table.MobAura,function(vu)
	MobAura = vu
	_G.Setting_table.MobAura = vu
	Update_Setting(getgenv()['MyName'])
end)
spawn(function()
	while wait() do
		pcall(function()
			if MobAura then
				if not Mix_Farm then
					if game.Workspace.Enemies:FindFirstChild("Reborn Skeleton [Lv. 1975]") then
						game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("SetSpawnPoint")
						for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
							if v.Name == "Reborn Skeleton [Lv. 1975]" and v.Humanoid.Health > 0 then
								if v.Humanoid:FindFirstChild("Animator") then
									v.Humanoid.Animator:Destroy()
								end
								_G.PosMon = v.HumanoidRootPart.CFrame
								StatrMagnet = true
								repeat wait(_G.Fast_Delay)
									EquipWeapon(_G.Setting_table.Weapon)
									TP(v.HumanoidRootPart.CFrame * CFrame.new(0, 30, 0))
									AttackNoCD()
								until v.Humanoid.Health <= 0 or not v.Parent or Mix_Farm or not MobAura 
								StatrMagnet = false
							end
						end
					elseif game.ReplicatedStorage:FindFirstChild("Reborn Skeleton [Lv. 1975]") then
						TP(game.ReplicatedStorage:FindFirstChild("Reborn Skeleton [Lv. 1975]").HumanoidRootPart.CFrame*CFrame.new(0,30,0))
					else
						for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
							if not string.find(v.Name,"Boss") and v.Humanoid.Health > 0 and (v.HumanoidRootPart.Position-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 1000 then
								if v.Humanoid:FindFirstChild("Animator") then
									v.Humanoid.Animator:Destroy()
								end
								_G.PosMon = v.HumanoidRootPart.CFrame
								StatrMagnet = true
								repeat wait(_G.Fast_Delay)
									EquipWeapon(_G.Setting_table.Weapon)
									TP(v.HumanoidRootPart.CFrame * CFrame.new(0, 30, 0))
									AttackNoCD()
								until v.Humanoid.Health <= 0 or not v.Parent or Mix_Farm or not Auto_Farm_Bone
								StatrMagnet = false
							end
						end
					end
				end
			end
		end)
	end
end)

spawn(function()
	while wait(2) do
		pcall(function()
			if Auto_Raid_Farm then
				if game:GetService("Players")["LocalPlayer"].PlayerGui.Main.Timer.Visible == false then
					_G.Stop_Tween = true
				elseif game:GetService("Players")["LocalPlayer"].PlayerGui.Main.Timer.Visible == true then
					_G.Stop_Tween = false
				end
			end
		end)
	end
end)
spawn(function()
	while wait(.5) do
		pcall(function()
			if Auto_Raid then
				if game:GetService("Players")["LocalPlayer"].PlayerGui.Main.Timer.Visible == false then
					if game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Special Microchip") or game:GetService("Players").LocalPlayer.Character:FindFirstChild("Special Microchip") then
						Auto_Raid_Farm = true
						Mix_Farm = true
						if New_World then
							fireclickdetector(game:GetService("Workspace").Map.CircleIsland.RaidSummon2.Button.Main.ClickDetector)
							repeat wait(1)
							until game:GetService("Players")["LocalPlayer"].PlayerGui.Main.Timer.Visible == true
						elseif Three_World then
							fireclickdetector(game:GetService("Workspace").Map["Boat Castle"].RaidSummon2.Button.Main.ClickDetector)
							repeat wait(1)
							until game:GetService("Players")["LocalPlayer"].PlayerGui.Main.Timer.Visible == true
						end
					else
						if _G.Setting_table.Auto_Raid_Hop or _G.Setting_table.Melee_Hop or Auto_Phoenix_Awaken then
							_G.Have_Fruit = nil
							Raid_FG()
						end
						Buy_Chip()
						wait(1)
						if _G.Setting_table.Auto_Raid_Hop and not game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Special Microchip") and not game:GetService("Players").LocalPlayer.Character:FindFirstChild("Special Microchip") then
							HopServer()
							wait(50)
						elseif Auto_Raid_Farm and not game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Special Microchip") and not game:GetService("Players").LocalPlayer.Character:FindFirstChild("Special Microchip") then
							Mix_Farm = nil
							_G.Stop_Tween = nil
							Auto_Raid_Farm = nil
							Text("ไม่มีผลปีศาจเหลือแล้ว")
						end
					end
				elseif game:GetService("Players")["LocalPlayer"].PlayerGui.Main.Timer.Visible == true then
					repeat wait(1)
					until game:GetService("Players")["LocalPlayer"].PlayerGui.Main.Timer.Visible == false
					if _G.Setting_table.Auto_Awaken then
						wait(2)
						game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Awakener","Check")
						game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Awakener","Awaken")
					end
				end
			end
		end)
	end
end)

Status_Tab:Label("Check Status")
Status_Tab:Button("Open Fruit Inventory",function()
	game:GetService("Players").LocalPlayer.PlayerGui.Main.FruitInventory.Visible = true
end)
Status_Tab:Button("Open Fruit Awaken",function()
	game:GetService("Players").LocalPlayer.PlayerGui.Main.AwakeningToggler.Visible = true
end)
Status_Tab:Button("Open Fruit Store",function()
	game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("GetFruits")
    game.Players.localPlayer.PlayerGui.Main.FruitShop.Visible = true
end)
Status_Tab:Button("Open Inventory",function()
	game:GetService("Players").LocalPlayer.PlayerGui.Main.Inventory.Visible = true 
end)
Status_Tab:Button("Open Color Haki",function()
	game.Players.localPlayer.PlayerGui.Main.Colors.Visible = true
end)
Status_Tab:Button("Open Title Name",function()
	game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("getTitles")
    game.Players.localPlayer.PlayerGui.Main.Titles.Visible = true
end)
function isnil(thing)
	return (thing == nil)
end
local function round(n)
	return math.floor(tonumber(n) + 0.5)
end
Number = math.random(1, 1000000)
function UpdatePlayerChams()
	for i,v in pairs(game:GetService'Players':GetChildren()) do
		pcall(function()
			if not isnil(v.Character) then
				if ESPPlayer then
					if not isnil(v.Character.Head) and not v.Character.Head:FindFirstChild('NameEsp'..Number) then
						local bill = Instance.new('BillboardGui',v.Character.Head)
						bill.Name = 'NameEsp'..Number
						bill.ExtentsOffset = Vector3.new(0, 1, 0)
						bill.Size = UDim2.new(1,200,1,30)
						bill.Adornee = v.Character.Head
						bill.AlwaysOnTop = true
						local name = Instance.new('TextLabel',bill)
						name.Font = Enum.Font.GothamSemibold
						name.FontSize = "Size14"
						name.TextWrapped = true
						name.Text = (v.Name ..' \n'.. round((game:GetService('Players').LocalPlayer.Character.Head.Position - v.Character.Head.Position).Magnitude/3) ..' M')
						name.Size = UDim2.new(1,0,1,0)
						name.TextYAlignment = 'Top'
						name.BackgroundTransparency = 1
						name.TextStrokeTransparency = 0.5
						if v.Team == game.Players.LocalPlayer.Team then
							name.TextColor3 = Color3.new(0,255,0)
						else
							name.TextColor3 = Color3.new(255,0,0)
						end
					else
						v.Character.Head['NameEsp'..Number].TextLabel.Text = (v.Name ..' | '.. round((game:GetService('Players').LocalPlayer.Character.Head.Position - v.Character.Head.Position).Magnitude/3) ..' M\nHealth : ' .. round(v.Character.Humanoid.Health*100/v.Character.Humanoid.MaxHealth) .. '%')
					end
				else
					if v.Character.Head:FindFirstChild('NameEsp'..Number) then
						v.Character.Head:FindFirstChild('NameEsp'..Number):Destroy()
					end
				end
			end
		end)
	end
end
function UpdateChestChams() 
	for i,v in pairs(game.Workspace:GetChildren()) do
		pcall(function()
			if string.find(v.Name,"Chest") then
				if ChestESP then
					if string.find(v.Name,"Chest") then
						if not v:FindFirstChild('NameEsp'..Number) then
							local bill = Instance.new('BillboardGui',v)
							bill.Name = 'NameEsp'..Number
							bill.ExtentsOffset = Vector3.new(0, 1, 0)
							bill.Size = UDim2.new(1,200,1,30)
							bill.Adornee = v
							bill.AlwaysOnTop = true
							local name = Instance.new('TextLabel',bill)
							name.Font = Enum.Font.GothamSemibold
							name.FontSize = "Size14"
							name.TextWrapped = true
							name.Size = UDim2.new(1,0,1,0)
							name.TextYAlignment = 'Top'
							name.BackgroundTransparency = 1
							name.TextStrokeTransparency = 0.5
							if v.Name == "Chest1" then
								name.TextColor3 = Color3.fromRGB(109, 109, 109)
								name.Text = ("Chest 1" ..' \n'.. round((game:GetService('Players').LocalPlayer.Character.Head.Position - v.Position).Magnitude/3) ..' M')
							end
							if v.Name == "Chest2" then
								name.TextColor3 = Color3.fromRGB(173, 158, 21)
								name.Text = ("Chest 2" ..' \n'.. round((game:GetService('Players').LocalPlayer.Character.Head.Position - v.Position).Magnitude/3) ..' M')
							end
							if v.Name == "Chest3" then
								name.TextColor3 = Color3.fromRGB(85, 255, 255)
								name.Text = ("Chest 3" ..' \n'.. round((game:GetService('Players').LocalPlayer.Character.Head.Position - v.Position).Magnitude/3) ..' M')
							end
						else
							v['NameEsp'..Number].TextLabel.Text = (v.Name ..'   \n'.. round((game:GetService('Players').LocalPlayer.Character.Head.Position - v.Position).Magnitude/3) ..' M')
						end
					end
				else
					if v:FindFirstChild('NameEsp'..Number) then
						v:FindFirstChild('NameEsp'..Number):Destroy()
					end
				end
			end
		end)
	end
end
function UpdateDevilChams() 
	for i,v in pairs(game.Workspace:GetChildren()) do
		pcall(function()
			if DevilFruitESP then
				if string.find(v.Name, "Fruit") then   
					if not v.Handle:FindFirstChild('NameEsp'..Number) then
						local bill = Instance.new('BillboardGui',v.Handle)
						bill.Name = 'NameEsp'..Number
						bill.ExtentsOffset = Vector3.new(0, 1, 0)
						bill.Size = UDim2.new(1,200,1,30)
						bill.Adornee = v.Handle
						bill.AlwaysOnTop = true
						local name = Instance.new('TextLabel',bill)
						name.Font = Enum.Font.GothamSemibold
						name.FontSize = "Size14"
						name.TextWrapped = true
						name.Size = UDim2.new(1,0,1,0)
						name.TextYAlignment = 'Top'
						name.BackgroundTransparency = 1
						name.TextStrokeTransparency = 0.5
						name.TextColor3 = Color3.fromRGB(255, 0, 0)
						name.Text = (v.Name ..' \n'.. round((game:GetService('Players').LocalPlayer.Character.Head.Position - v.Handle.Position).Magnitude/3) ..' M')
					else
						v.Handle['NameEsp'..Number].TextLabel.Text = (v.Name ..'   \n'.. round((game:GetService('Players').LocalPlayer.Character.Head.Position - v.Handle.Position).Magnitude/3) ..' M')
					end
				end
			else
				if v.Handle:FindFirstChild('NameEsp'..Number) then
					v.Handle:FindFirstChild('NameEsp'..Number):Destroy()
				end
			end
		end)
	end
end
function UpdateFlowerChams() 
	for i,v in pairs(game.Workspace:GetChildren()) do
		pcall(function()
			if v.Name == "Flower2" or v.Name == "Flower1" then
				if FlowerESP then 
					if not v:FindFirstChild('NameEsp'..Number) then
						local bill = Instance.new('BillboardGui',v)
						bill.Name = 'NameEsp'..Number
						bill.ExtentsOffset = Vector3.new(0, 1, 0)
						bill.Size = UDim2.new(1,200,1,30)
						bill.Adornee = v
						bill.AlwaysOnTop = true
						local name = Instance.new('TextLabel',bill)
						name.Font = Enum.Font.GothamSemibold
						name.FontSize = "Size14"
						name.TextWrapped = true
						name.Size = UDim2.new(1,0,1,0)
						name.TextYAlignment = 'Top'
						name.BackgroundTransparency = 1
						name.TextStrokeTransparency = 0.5
						name.TextColor3 = Color3.fromRGB(255, 0, 0)
						if v.Name == "Flower1" then 
							name.Text = ("Blue Flower" ..' \n'.. round((game:GetService('Players').LocalPlayer.Character.Head.Position - v.Position).Magnitude/3) ..' M')
							name.TextColor3 = Color3.fromRGB(0, 0, 255)
						end
						if v.Name == "Flower2" then
							name.Text = ("Red Flower" ..' \n'.. round((game:GetService('Players').LocalPlayer.Character.Head.Position - v.Position).Magnitude/3) ..' M')
							name.TextColor3 = Color3.fromRGB(255, 0, 0)
						end
					else
						v['NameEsp'..Number].TextLabel.Text = (v.Name ..'   \n'.. round((game:GetService('Players').LocalPlayer.Character.Head.Position - v.Position).Magnitude/3) ..' M')
					end
				else
					if v:FindFirstChild('NameEsp'..Number) then
					v:FindFirstChild('NameEsp'..Number):Destroy()
					end
				end
			end   
		end)
	end
end
function UpdateRealFruitChams() 
	for i,v in pairs(game.Workspace.AppleSpawner:GetChildren()) do
		if v:IsA("Tool") then
			if RealFruitESP then 
				if not v.Handle:FindFirstChild('NameEsp'..Number) then
					local bill = Instance.new('BillboardGui',v.Handle)
					bill.Name = 'NameEsp'..Number
					bill.ExtentsOffset = Vector3.new(0, 1, 0)
					bill.Size = UDim2.new(1,200,1,30)
					bill.Adornee = v.Handle
					bill.AlwaysOnTop = true
					local name = Instance.new('TextLabel',bill)
					name.Font = Enum.Font.GothamSemibold
					name.FontSize = "Size14"
					name.TextWrapped = true
					name.Size = UDim2.new(1,0,1,0)
					name.TextYAlignment = 'Top'
					name.BackgroundTransparency = 1
					name.TextStrokeTransparency = 0.5
					name.TextColor3 = Color3.fromRGB(255, 0, 0)
					name.Text = (v.Name ..' \n'.. round((game:GetService('Players').LocalPlayer.Character.Head.Position - v.Handle.Position).Magnitude/3) ..' M')
				else
					v.Handle['NameEsp'..Number].TextLabel.Text = (v.Name ..' '.. round((game:GetService('Players').LocalPlayer.Character.Head.Position - v.Handle.Position).Magnitude/3) ..' M')
				end
			else
				if v.Handle:FindFirstChild('NameEsp'..Number) then
					v.Handle:FindFirstChild('NameEsp'..Number):Destroy()
				end
			end 
		end
	end
	for i,v in pairs(game.Workspace.PineappleSpawner:GetChildren()) do
		if v:IsA("Tool") then
			if RealFruitESP then 
				if not v.Handle:FindFirstChild('NameEsp'..Number) then
					local bill = Instance.new('BillboardGui',v.Handle)
					bill.Name = 'NameEsp'..Number
					bill.ExtentsOffset = Vector3.new(0, 1, 0)
					bill.Size = UDim2.new(1,200,1,30)
					bill.Adornee = v.Handle
					bill.AlwaysOnTop = true
					local name = Instance.new('TextLabel',bill)
					name.Font = Enum.Font.GothamSemibold
					name.FontSize = "Size14"
					name.TextWrapped = true
					name.Size = UDim2.new(1,0,1,0)
					name.TextYAlignment = 'Top'
					name.BackgroundTransparency = 1
					name.TextStrokeTransparency = 0.5
					name.TextColor3 = Color3.fromRGB(255, 174, 0)
					name.Text = (v.Name ..' \n'.. round((game:GetService('Players').LocalPlayer.Character.Head.Position - v.Handle.Position).Magnitude/3) ..' M')
				else
					v.Handle['NameEsp'..Number].TextLabel.Text = (v.Name ..' '.. round((game:GetService('Players').LocalPlayer.Character.Head.Position - v.Handle.Position).Magnitude/3) ..' M')
				end
			else
				if v.Handle:FindFirstChild('NameEsp'..Number) then
					v.Handle:FindFirstChild('NameEsp'..Number):Destroy()
				end
			end 
		end
	end
	for i,v in pairs(game.Workspace.BananaSpawner:GetChildren()) do
		if v:IsA("Tool") then
			if RealFruitESP then 
				if not v.Handle:FindFirstChild('NameEsp'..Number) then
					local bill = Instance.new('BillboardGui',v.Handle)
					bill.Name = 'NameEsp'..Number
					bill.ExtentsOffset = Vector3.new(0, 1, 0)
					bill.Size = UDim2.new(1,200,1,30)
					bill.Adornee = v.Handle
					bill.AlwaysOnTop = true
					local name = Instance.new('TextLabel',bill)
					name.Font = Enum.Font.GothamSemibold
					name.FontSize = "Size14"
					name.TextWrapped = true
					name.Size = UDim2.new(1,0,1,0)
					name.TextYAlignment = 'Top'
					name.BackgroundTransparency = 1
					name.TextStrokeTransparency = 0.5
					name.TextColor3 = Color3.fromRGB(251, 255, 0)
					name.Text = (v.Name ..' \n'.. round((game:GetService('Players').LocalPlayer.Character.Head.Position - v.Handle.Position).Magnitude/3) ..' M')
				else
					v.Handle['NameEsp'..Number].TextLabel.Text = (v.Name ..' '.. round((game:GetService('Players').LocalPlayer.Character.Head.Position - v.Handle.Position).Magnitude/3) ..' M')
				end
			else
				if v.Handle:FindFirstChild('NameEsp'..Number) then
					v.Handle:FindFirstChild('NameEsp'..Number):Destroy()
				end
			end 
		end
	end
end
Esp_Tab:Toggle("ESP Players","9606294253",false,function(a)
	ESPPlayer = a
	UpdatePlayerChams()
end)
Esp_Tab:Toggle("ESP Chests","9606294253",false,function(a)
	ChestESP = a
	UpdateChestChams() 
end)
Esp_Tab:Toggle("ESP Devil Fruit","9606294253",false,function(a)
	DevilFruitESP = a
	UpdateDevilChams() 
end)
Esp_Tab:Toggle("ESP Fruit Spawn","9606294253",false,function(a)
	RealFruitESP = a
	UpdateRealFruitChams() 
end)
Esp_Tab:Toggle("ESP Flowers","9606294253",false,function(a)
	FlowerESP = a
	UpdateFlowerChams() 
end)
spawn(function()
	while wait(2) do
		if FlowerESP then
			UpdateFlowerChams() 
		end
		if DevilFruitESP then
			UpdateDevilChams() 
		end
		if ChestESP then
			UpdateChestChams() 
		end
		if ESPPlayer then
			UpdatePlayerChams()
		end
		if RealFruitESP then
			UpdateRealFruitChams()
		end
	end
end)


Hop_Tab:Label("Main")
Hop_Tab:Toggle("Bring Fruit Hop","9606294253",_G.Setting_table.BringFruit_Hop,function(vu)
	BringFruit = vu
	_G.Setting_table.BringFruit_Hop = vu
	Update_Setting(getgenv()['MyName'])
	if vu then
		wait(15)
		HopServer()
		wait(50)
	end
end)
if _G.Setting_table.BringFruit then
	BringFruit = true
end
Hop_Tab:Toggle("Auto Farm All Boss Hop","9606294253",_G.Setting_table.Auto_Farm_Boss_All_Hop,function(vu)
	_G.Setting_table.Auto_Farm_Boss_All_Hop = vu
	Update_Setting(getgenv()['MyName'])
end)
Hop_Tab:Toggle("Auto Farm Boss Hop","9606294253",_G.Setting_table.Auto_Farm_Boss_Hop,function(vu)
	_G.Setting_table.Auto_Farm_Boss_Hop = vu
	Update_Setting(getgenv()['MyName'])
end)

if _G.Setting_table.Boss_Select_1 == nil then
	_G.Setting_table.Boss_Select_1 = ""
end
_G.Setting_table.Boss_All_Select = {}
local S_B_1 = Hop_Tab:Dropdown("Select Boss 1",_G.Setting_table.Boss_Select_1,Boss_List,function(vu)
	_G.Setting_table.Boss_Select_1 = vu
	if type(_G.Setting_table.Boss_Select_1) == "string" then
		table.insert(_G.Setting_table.Boss_All_Select,_G.Setting_table.Boss_Select_1)
	end
	Update_Setting(getgenv()['MyName'])
end)
if _G.Setting_table.Boss_Select_2 then
	_G.Setting_table.Boss_Select_2 = ""
end
local S_B_2 = Hop_Tab:Dropdown("Select Boss 2",_G.Setting_table.Boss_Select_2,Boss_List,function(vu)
	_G.Setting_table.Boss_Select_2 = vu
	if type(_G.Setting_table.Boss_Select_2) == "string" then
		table.insert(_G.Setting_table.Boss_All_Select,_G.Setting_table.Boss_Select_2)
	end
	Update_Setting(getgenv()['MyName'])
end)
if _G.Setting_table.Boss_Select_3 then
	_G.Setting_table.Boss_Select_3 = ""
end
local S_B_3 = Hop_Tab:Dropdown("Select Boss 3",_G.Setting_table.Boss_Select_3,Boss_List,function(vu)
	_G.Setting_table.Boss_Select_3 = vu
	if type(_G.Setting_table.Boss_Select_3) == "string" then
		table.insert(_G.Setting_table.Boss_All_Select,_G.Setting_table.Boss_Select_3)
	end
	Update_Setting(getgenv()['MyName'])
end)
if _G.Setting_table.Boss_Select_4 == nil then
	_G.Setting_table.Boss_Select_4 = ""
end
local S_B_4 = Hop_Tab:Dropdown("Select Boss 4",_G.Setting_table.Boss_Select_4,Boss_List,function(vu)
	_G.Setting_table.Boss_Select_4 = vu
	if type(_G.Setting_table.Boss_Select_4) == "string" then
		table.insert(_G.Setting_table.Boss_All_Select,_G.Setting_table.Boss_Select_4)
	end
	Update_Setting(getgenv()['MyName'])
end)
if _G.Setting_table.Boss_Select_5 == nil then
	_G.Setting_table.Boss_Select_5 = ""
end
local S_B_5 = Hop_Tab:Dropdown("Select Boss 5",_G.Setting_table.Boss_Select_5,Boss_List,function(vu)
	_G.Setting_table.Boss_Select_5 = vu
	if type(_G.Setting_table.Boss_Select_5) == "string" then
		table.insert(_G.Setting_table.Boss_All_Select,_G.Setting_table.Boss_Select_5)
	end
	Update_Setting(getgenv()['MyName'])
end)
Hop_Tab:Button("Refresh Select Boss",function()
	S_B_1:Clear()
	S_B_2:Clear()
	S_B_3:Clear()
	S_B_4:Clear()
	S_B_5:Clear()
	for i,v in pairs(Boss_List) do
		S_B_1:Add(v)
		S_B_2:Add(v)
		S_B_3:Add(v)
		S_B_4:Add(v)
		S_B_5:Add(v)
	end
end)
Hop_Tab:Toggle("Auto Farm Observation Haki Hop","9606294253",_G.Setting_table.Farm_Ken_Hop,function(vu)
	_G.Setting_table.Farm_Ken_Hop = vu
	Update_Setting(getgenv()['MyName'])
end)
Hop_Tab:Toggle("Auto Buy Legendary Sword Hop","9606294253",_G.Setting_table.Auto_Buy_Legendary_Sword_Hop,function(vu)
	_G.Setting_table.Auto_Buy_Legendary_Sword = vu
	_G.Setting_table.Auto_Buy_Legendary_Sword_Hop = vu
	Update_Setting(getgenv()['MyName'])
	if vu then
		wait(15)
		HopServer()
		wait(50)
	end
end)
Hop_Tab:Toggle("Auto Buy Color Buso Haki Hop","9606294253",_G.Setting_table.Buso_Haki_Hop,function(vu)
	Buso_Haki_Buy = vu
	_G.Setting_table.Buso_Haki_Hop = vu
	Update_Setting(getgenv()['MyName'])
end)
if _G.Setting_table.Buso_Haki then
	Buso_Haki_Buy = vu
end


Hop_Tab:Label("Quest")
Hop_Tab:Toggle("Auto Open Don Swan Hop","9606294253",_G.Setting_table.Open_Don_Swan_Hop,function(vu)
	Inventory_Fruit = vu
	BringFruit = vu
	Don_Swan_Quest = vu
	_G.Setting_table.Open_Don_Swan_Hop = vu
	Update_Setting(getgenv()['MyName'])
end)
if _G.Setting_table.Open_Don_Swan then
	Inventory_Fruit = true
	BringFruit = true
	Don_Swan_Quest = true
end
spawn(function()
	while wait(2) do
		pcall(function()
			if _G.Setting_table.Open_Don_Swan_Hop then
				if game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("TalkTrevor","1") ~= 0 then
					wait(15)
					HopServer()
					wait(50)
				else
					_G.TP_Ser = true
					wait(2)
					game.Players.LocalPlayer:Kick("\n✅ : Quest Open Don Swan ")
				end
			else
				wait(2)
			end
		end)
	end
end)

Hop_Tab:Toggle("Auto Farm Elite Hunter Hop","9606294253",_G.Setting_table.Auto_Elite_Hunter_Hop,function(vu)
	Auto_Elite_Hunter = vu
	_G.Setting_table.Auto_Elite_Hunter_Hop = vu
	Update_Setting(getgenv()['MyName'])
end)
if _G.Setting_table.Auto_Elite_Hunter then
	Auto_Elite_Hunter = true
end
Hop_Tab:Toggle("Auto Phoenix Awaken Hop","9606294253",false,function(vu)
	_G.Setting_table.Phoenix_Hop = vu
	Update_Setting(getgenv()['MyName'])
end)
Hop_Tab:Toggle("Auto Observation Haki V2 Hop","9606294253",_G.Setting_table.Farm_Ken_V2_Hop,function(vu)
	Farm_Ken = vu
	Farm_Ken_V2 = vu
	_G.Setting_table.Farm_Ken_V2_Hop = vu
	Update_Setting(getgenv()['MyName'])
end)
if _G.Setting_table.Farm_Ken_V2 then
	Farm_Ken = true
	Farm_Ken_V2 = true
end

Hop_Tab:Label("Sword")
Hop_Tab:Toggle("Auto Pole V1 Hop","9606294253",_G.Setting_table.Pole_V1_Hop,function(vu)
	Pole_Farm = vu
	_G.Setting_table.Pole_V1_Hop = vu
	Update_Setting(getgenv()['MyName'])
end)
if _G.Setting_table.Pole_Farm then
	Pole_Farm = true
end
Hop_Tab:Toggle("Auto Saber Hop","9606294253",_G.Setting_table.Saber_Farm_Hop,function(vu)
	Saber_Farm = vu
	_G.Setting_table.Saber_Farm_Hop = vu
	Update_Setting(getgenv()['MyName'])
end)
if _G.Setting_table.Saber_Farm then
	Saber_Farm = true
end
Hop_Tab:Seperator("Second World")
Hop_Tab:Toggle("Auto Rengoku Hop","9606294253",_G.Setting_table.Rengoku_Hop,function(vu)
	Rengoku_A = vu
	_G.Setting_table.Rengoku_Hop = vu
	Update_Setting(getgenv()['MyName'])
end)
if _G.Setting_table.Rengoku_A then
	Rengoku_A = true
end
Hop_Tab:Toggle("Auto Ko Ko Hop","9606294253",false,function(vu)
	
end)
Hop_Tab:Toggle("Auto Dragon Trident Hop","9606294253",_G.Setting_table.Auto_Dragon_Trident_Hop,function(vu)
	Auto_Dragon_Trident = vu
	_G.Setting_table.Auto_Dragon_Trident_Hop = vu
	Update_Setting(getgenv()['MyName'])
end)
if _G.Setting_table.Auto_Dragon_Trident then
	Auto_Dragon_Trident = true
end
Hop_Tab:Toggle("Auto True Triple Katana Hop","9606294253",_G.Setting_table.Triple_Hop,function(vu)
	Triple_A = vu
	Auto_Farm_Sword = vu
	_G.Setting_table.Triple_Hop = vu
end)
if _G.Setting_table.Triple_A then
	Auto_Farm_Sword = true
	Triple_A = true
end
Hop_Tab:Seperator("Thrid World")
Hop_Tab:Toggle("Auto Yama Hop","9606294253",_G.Setting_table.Auto_Yama_Hop,function(vu)
	Auto_Yama = vu
	_G.Setting_table.Auto_Yama_Hop = vu
	Update_Setting(getgenv()['MyName'])
end)
if _G.Setting_table.Auto_Yama then
	Auto_Yama = true
end
Hop_Tab:Toggle("Auto Tushita Hop","9606294253",_G.Setting_table.Auto_Tushita_Hop,function(vu)
	Auto_Tushita = vu
	_G.Setting_table.Auto_Tushita_Hop = vu
	Update_Setting(getgenv()['MyName'])
end)
if _G.Setting_table.Auto_Tushita then
	Auto_Tushita = true
end
Hop_Tab:Toggle("No Color Haki","9606294253",_G.Setting_table.No_Color_Haki_Tushita,function(vu)
	_G.Setting_table.No_Color_Haki_Tushita = vu
	Update_Setting(getgenv()['MyName'])
end)
Hop_Tab:Toggle("Auto Twin Hooks Hop","9606294253",_G.Setting_table.Auto_Twin_Hooks_Hop,function(vu)
	Auto_Twin_Hooks = vu
	_G.Setting_table.Auto_Twin_Hooks_Hop = vu
	Update_Setting(getgenv()['MyName'])
end)
if _G.Setting_table.Auto_Twin_Hooks then
	Auto_Twin_Hooks = true
end
Hop_Tab:Toggle("Auto Canvander Hop","9606294253",_G.Setting_table.Auto_Canvander_Hop,function(vu)
	Auto_Canvander = vu
	_G.Setting_table.Auto_Canvander_Hop = vu
	Update_Setting(getgenv()['MyName'])
end)
if _G.Setting_table.Auto_Canvander then
	Auto_Canvander = true
end
Hop_Tab:Toggle("Auto Buddy Sword Hop","9606294253",_G.Setting_table.Auto_Buddy_Sword_Hop,function(vu)
	Auto_Buddy_Sword = vu
	_G.Setting_table.Auto_Buddy_Sword_Hop = vu
	Update_Setting(getgenv()['MyName'])
end)
if _G.Setting_table.Auto_Buddy_Sword then
	Auto_Buddy_Sword = true
end
Hop_Tab:Toggle("Auto Spikey Trident Hop","9606294253",_G.Setting_table.Spikey_Trident_Hop,function(vu)
	Auto_Spikey_Trident = vu
	_G.Setting_table.Spikey_Trident_Hop = vu
	Update_Setting(getgenv()['MyName'])
end)
if _G.Setting_table.Auto_Spikey_Trident then
	Auto_Spikey_Trident = true
end
Hop_Tab:Toggle("Auto Hallow Scryte Hop","9606294253",_G.Setting_table.Auto_Hallow_Scryte,function(vu)
	Auto_Hallow_Scryte = vu
	_G.Setting_table.Hallow_Scryte_Hop = vu
	Update_Setting(getgenv()['MyName'])
end)
if _G.Setting_table.Auto_Hallow_Scryte then
	Auto_Hallow_Scryte = true
end
Hop_Tab:Toggle("Auto Dark Dagger Hop","9606294253",_G.Setting_table.Auto_Dark_Dagger_Hop,function(vu)
	Auto_Dark_Dagger = vu
	_G.Setting_table.Auto_Dark_Dagger_Hop = vu
	Update_Setting(getgenv()['MyName'])
end)
if _G.Setting_table.Auto_Dark_Dagger then
	Auto_Dark_Dagger = true
end
Hop_Tab:Toggle("No Color Haki","9606294253",_G.Setting_table.No_Color_Haki_Dark_Dagger,function(vu)
	_G.Setting_table.No_Color_Haki_Dark_Dagger = vu
	Update_Setting(getgenv()['MyName'])
end)

Hop_Tab:Label("Gun")
Hop_Tab:Toggle("Auto Acidum Rifle Hop","9606294253",_G.Setting_table.Auto_Acidum_Rifle_Hop,function(vu)
	Auto_Acidum_Rifle = vu
	_G.Setting_table.Auto_Acidum_Rifle_Hop = vu
	Update_Setting(getgenv()['MyName'])
end)
if _G.Setting_table.Auto_Acidum_Rifle then
	Auto_Acidum_Rifle = true
end
Hop_Tab:Toggle("Auto Serpent Bow Hop","9606294253",_G.Setting_table.Auto_Serpent_Bow_Hop,function(vu)
	Auto_Serpent_Bow = vu
	_G.Setting_table.Auto_Serpent_Bow_Hop = vu
	Update_Setting(getgenv()['MyName'])
end)
if _G.Setting_table.Auto_Serpent_Bow then
	Auto_Serpent_Bow = true
end

Hop_Tab:Label("Accessory")
Hop_Tab:Toggle("Auto Dark Coat Hop","9606294253",_G.Setting_table.Auto_Dark_Coat_Hop,function(vu)
	Auto_Dark_Coat = vu
	_G.Setting_table.Auto_Dark_Coat_Hop = vu
	Update_Setting(getgenv()['MyName'])
end)
if _G.Setting_table.Chest_Lock == nil then
	_G.Setting_table.Chest_Lock = 50
end
C_H_H = 0
spawn(function()
	while wait(2) do
		pcall(function()
			if _G.Setting_table.Auto_Dark_Coat_Hop then
				if C_H_H >= _G.Setting_table.Chest_Lock and not H_F_T then
					HopServer()
					wait(50)
				end
			end
		end)
	end
end)
Hop_Tab:Slider("Chest Lock",1,100,_G.Setting_table.Chest_Lock,function(vu)
	_G.Setting_table.Chest_Lock = vu
	Update_Setting(getgenv()['MyName'])
end)

local L_C = Hop_Tab:Label("Chest : "..C_H_H.."/".._G.Setting_table.Chest_Lock)
if _G.Setting_table.Auto_Dark_Coat then
	Auto_Dark_Coat = true
end
spawn(function()
	while wait(.5) do
		pcall(function()
			if Auto_Dark_Coat then
				if game.Workspace.Enemies:FindFirstChild("Darkbeard [Lv. 1000] [Raid Boss]") or game.ReplicatedStorage:FindFirstChild("Darkbeard [Lv. 1000] [Raid Boss]") then
					H_F_T = true
					if game.Workspace.Enemies:FindFirstChild("Darkbeard [Lv. 1000] [Raid Boss]") then
                        for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
                            if v.Name == "Darkbeard [Lv. 1000] [Raid Boss]" and v.Humanoid.Health > 0 then
                                repeat wait(_G.Fast_Delay)
                                    EquipWeapon(_G.Setting_table.Weapon)
                                    TP(v.HumanoidRootPart.CFrame*CFrame.new(0,30,0))
                                    AttackNoCD()
                                until v.Humanoid.Health <= 0 or not v.Parent or not Auto_Dark_Coat
								H_F_T = nil
								if _G.Setting_table.Auto_Dark_Coat_Hop then
									HopServer()
									wait(50)
								end
							end
                        end
                    elseif game.ReplicatedStorage:FindFirstChild("Darkbeard [Lv. 1000] [Raid Boss]") then
                        TP(game.ReplicatedStorage:FindFirstChild("Darkbeard [Lv. 1000] [Raid Boss]").HumanoidRootPart.CFrame*CFrame.new(0,30,0))
                    end
				elseif game.Players.LocalPlayer.Backpack:FindFirstChild("Fist of Darkness") or game.Players.LocalPlayer.Character:FindFirstChild("Fist of Darkness") then
					H_F_T = true
					repeat wait(.5)
                        EquipWeapon("Fist of Darkness")
                        TP(CFrame.new(3778.0603, 15.0511189, -3499.95801, -0.0148028014, 1.28971422e-07, -0.999890447, 3.63752335e-08, 1, 1.28447041e-07, 0.999890447, -3.44698741e-08, -0.0148028014))
                    until game.Workspace.Enemies:FindFirstChild("Darkbeard [Lv. 1000] [Raid Boss]") or game.ReplicatedStorage:FindFirstChild("Darkbeard [Lv. 1000] [Raid Boss]") or not Auto_Dark_Coat
				else
					
					H_F_T = nil
					_G.Chest_100 = nil
						_G.Chest_500 = nil
						_G.Chest_1000 = nil
						_G.Chest_1500 = nil
						_G.Chest_2000 = nil
						_G.Chest_2500 = nil
						_G.Chest_3500 = nil
						_G.Chest_4500 = nil
						_G.Chest_5500 = nil
						_G.Chest_6500 = nil
						_G.Chest_7500 = nil
						_G.Chest_9500 = nil
						_G.Chest_10500 = nil
						_G.Chest_12500 = nil
						_G.Chest_15500 = nil
						_G.Chest_17500 = nil
						Chest_100()
						Chest_500()
						Chest_1000()
						Chest_1500()
						Chest_2000()
						Chest_2500()
						Chest_3500()
						Chest_4500()
						Chest_5500()
						Chest_6500()
						Chest_7500()
						Chest_9500()
						Chest_10500()
						Chest_12500()
						Chest_15500()
						Chest_17500()
						if _G.Chest_100 ~= nil then
							repeat wait(.3)
								TP(_G.Chest_100.CFrame)
							until not _G.Chest_100.Parent or not Auto_Dark_Coat
							if Auto_Dark_Coat then
								C_H_H = C_H_H + 1
								L_C:Set('Chest : '..tostring(C_H_H).."/".._G.Setting_table.Chest_Lock)
							end
						elseif _G.Chest_500 ~= nil then
							repeat wait(.3)
								TP(_G.Chest_500.CFrame)
							until not _G.Chest_500.Parent or not Auto_Dark_Coat
							if Auto_Dark_Coat then
								C_H_H = C_H_H + 1
								L_C:Set('Chest : '..tostring(C_H_H).."/".._G.Setting_table.Chest_Lock)
							end
						elseif _G.Chest_1000 ~= nil then
							repeat wait(.3)
								TP(_G.Chest_1000.CFrame)
							until not _G.Chest_1000.Parent or not Auto_Dark_Coat
							if Auto_Dark_Coat then
								C_H_H = C_H_H + 1
								L_C:Set('Chest : '..tostring(C_H_H).."/".._G.Setting_table.Chest_Lock)
							end
						elseif _G.Chest_1500 ~= nil then
							repeat wait(.3)
								TP(_G.Chest_1500.CFrame)
							until not _G.Chest_1500.Parent or not Auto_Dark_Coat
							if Auto_Dark_Coat then
								C_H_H = C_H_H + 1
								L_C:Set('Chest : '..tostring(C_H_H).."/".._G.Setting_table.Chest_Lock)
							end
						elseif _G.Chest_2000 ~= nil then
							repeat wait(.3)
								TP(_G.Chest_2000.CFrame)
							until not _G.Chest_2000.Parent or not Auto_Dark_Coat
							if Auto_Dark_Coat then
								C_H_H = C_H_H + 1
								L_C:Set('Chest : '..tostring(C_H_H).."/".._G.Setting_table.Chest_Lock)
							end
						elseif _G.Chest_2500 ~= nil then
							repeat wait(.3)
								TP(_G.Chest_2500.CFrame)
							until not _G.Chest_2500.Parent or not Auto_Dark_Coat
							if Auto_Dark_Coat then
								C_H_H = C_H_H + 1
								L_C:Set('Chest : '..tostring(C_H_H).."/".._G.Setting_table.Chest_Lock)
							end
						elseif _G.Chest_3500 ~= nil then
							repeat wait(.3)
								TP(_G.Chest_3500.CFrame)
							until not _G.Chest_3500.Parent or not Auto_Dark_Coat
							if Auto_Dark_Coat then
								C_H_H = C_H_H + 1
								L_C:Set('Chest : '..tostring(C_H_H).."/".._G.Setting_table.Chest_Lock)
							end
						elseif _G.Chest_4500 ~= nil then
							repeat wait(.3)
								TP(_G.Chest_4500.CFrame)
							until not _G.Chest_4500.Parent or not Auto_Dark_Coat
							if Auto_Dark_Coat then
								C_H_H = C_H_H + 1
								L_C:Set('Chest : '..tostring(C_H_H).."/".._G.Setting_table.Chest_Lock)
							end
						elseif _G.Chest_5500 ~= nil then
							repeat wait(.3)
								TP(_G.Chest_5500.CFrame)
							until not _G.Chest_5500.Parent or not Auto_Dark_Coat
							if Auto_Dark_Coat then
								C_H_H = C_H_H + 1
								L_C:Set('Chest : '..tostring(C_H_H).."/".._G.Setting_table.Chest_Lock)
							end
						elseif _G.Chest_6500 ~= nil then
							repeat wait(.3)
								TP(_G.Chest_6500.CFrame)
							until not _G.Chest_6500.Parent or not Auto_Dark_Coat
							if Auto_Dark_Coat then
								C_H_H = C_H_H + 1
								L_C:Set('Chest : '..tostring(C_H_H).."/".._G.Setting_table.Chest_Lock)
							end
						elseif _G.Chest_7500 ~= nil then
							repeat wait(.3)
								TP(_G.Chest_7500.CFrame)
							until not _G.Chest_7500.Parent or not Auto_Dark_Coat
							if Auto_Dark_Coat then
								C_H_H = C_H_H + 1
								L_C:Set('Chest : '..tostring(C_H_H).."/".._G.Setting_table.Chest_Lock)
							end
						elseif _G.Chest_9500 ~= nil then
							repeat wait(.3)
								TP(_G.Chest_9500.CFrame)
							until not _G.Chest_9500.Parent or not Auto_Dark_Coat
							if Auto_Dark_Coat then
								C_H_H = C_H_H + 1
								L_C:Set('Chest : '..tostring(C_H_H).."/".._G.Setting_table.Chest_Lock)
							end
						elseif _G.Chest_10500 ~= nil then
							repeat wait(.3)
								TP(_G.Chest_10500.CFrame)
							until not _G.Chest_10500.Parent or not Auto_Dark_Coat
							if Auto_Dark_Coat then
								C_H_H = C_H_H + 1
								L_C:Set('Chest : '..tostring(C_H_H).."/".._G.Setting_table.Chest_Lock)
							end
						elseif _G.Chest_12500 ~= nil then
							repeat wait(.3)
								TP(_G.Chest_12500.CFrame)
							until not _G.Chest_12500.Parent or not Auto_Dark_Coat
							if Auto_Dark_Coat then
								C_H_H = C_H_H + 1
								L_C:Set('Chest : '..tostring(C_H_H).."/".._G.Setting_table.Chest_Lock)
							end
						elseif _G.Chest_15500 ~= nil then
							repeat wait(.3)
								TP(_G.Chest_15500.CFrame)
							until not _G.Chest_15500.Parent or not Auto_Dark_Coat
							if Auto_Dark_Coat then
								C_H_H = C_H_H + 1
								L_C:Set('Chest : '..tostring(C_H_H).."/".._G.Setting_table.Chest_Lock)
							end
						elseif _G.Chest_17500 ~= nil then
							repeat wait(.3)
								TP(_G.Chest_17500.CFrame)
							until not _G.Chest_17500.Parent or not Auto_Dark_Coat
							if Auto_Dark_Coat then
								C_H_H = C_H_H + 1
								L_C:Set('Chest : '..tostring(C_H_H).."/".._G.Setting_table.Chest_Lock)
							end
						end
				end
			else
				wait(2)
			end
		end)
	end
end)
Hop_Tab:Toggle("Auto Swan Glass Hop","9606294253",_G.Setting_table.Auto_Swan_Glass_Hop,function(vu)
	Auto_Swan_Glass = vu
	_G.Setting_table.Auto_Swan_Glass_Hop = vu
	Update_Setting(getgenv()['MyName'])
end)
if _G.Setting_table.Auto_Swan_Glass then
	Auto_Swan_Glass = true
end
Hop_Tab:Toggle("Auto Pale Scarf Hop","9606294253",false,function(vu)
	Auto_Pale_Scarf = vu
	_G.Setting_table.Auto_Pale_Scarf_Hop = vu
	Update_Setting(getgenv()['MyName'])
end)
if _G.Setting_table.Auto_Pale_Scarf then
	Auto_Pale_Scarf = true
end
Hop_Tab:Toggle("Auto Valkyrie Helmet Hop","9606294253",_G.Setting_table.Auto_Valkyrie_Helmet_Hop,function(vu)
	Auto_Valkyrie_Helmet = vu
	_G.Setting_table.Auto_Valkyrie_Helmet_Hop = vu
	Update_Setting(getgenv()['MyName'])
end)
if _G.Setting_table.Auto_Valkyrie_Helmet then
	Auto_Valkyrie_Helmet = true
end
--end
--end
