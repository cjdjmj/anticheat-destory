local MT = getrawmetatable(game)
	local NC = MT.__namecall
	setreadonly(MT, false)

	MT.__namecall = newcclosure(function(self, ...)
		local A = {...}
		local GNCM = getnamecallmethod() or get_namecall_method()
		if GNCM == "FireServer" and self.Name == "MainEvent" then
			return wait(9e9)
		end
		return NC(self, unpack(A))
	end)
	setreadonly(MT, true)

	for i,v in pairs(game:GetService("Players").LocalPlayer.Character:GetDescendants()) do
		if v:IsA("Script") and v.Name == "LocalScript" and v.Disabled == false then
			v.Disabled = true
		end
	end
	if game:GetService("Players").LocalPlayer.Character:FindFirstChild("") then
		game:GetService("Players").LocalPlayer.Character:FindFirstChild(""):Destroy()
	else
		if game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("") then
			game:GetService("Players").LocalPlayer.Backpack:FindFirstChild(""):Destroy()
		end
	end

	local mt = getrawmetatable(game)
	local old = mt.__newindex
	local Plr = game.Players.LocalPlayer
	local bad, otherbad = {"BodyPosition", "BodyVelocity", "BodyGyro"}, {"HumanoidRootPart", "UpperTorso"}
	setreadonly(mt, false)
	local oldie
	oldie = hookfunc(Instance.new, newcclosure(function(e, i, ...) 
		if i and table.find(bad, e) and table.find(otherbad, tostring(i)) and i.Parent == Plr.Character then
			print("reparented")
			return oldie(e, Plr.Character.LowerTorso, ...)
		end
		return oldie(e, i, ...)
	end))
	mt.__newindex = newcclosure(function(t, i, v)
		if Plr.Character and table.find(bad, t.ClassName) and i == "Parent" and (table.find(otherbad, tostring(v)) and v.Parent == Plr.Character) then
			print("reparented")
			return old(t, i, Plr.Character.LowerTorso)
		end
		return old(t, i, v)
	end)
	setreadonly(mt, true)

	local sowd = getrawmetatable(game)
	local sucks = sowd.__namecall
	local player = game.Players.LocalPlayer
	setreadonly(sowd, false)
	sowd.__namecall = newcclosure(function(name, ...)
		local tabs = {...}
		if getnamecallmethod() == "FireServer"  and tostring(name) == "MainEvent" then
			if tabs[1] == "CHECKER_1" or tabs[1] == "TeleportDetect" or tabs[1] == "OneMoreTime" then
				return wait(9e9)
			end
		end
		return sucks(name, unpack(tabs))
	end)
	setreadonly(sowd, true)
	local a={163721789,15427717,201454243,822999,63794379,17260230,28357488,93101606,8195210,89473551,16917269,85989579,1553950697,476537893,155627580,31163456,7200829,25717070,201454243,15427717,63794379,16138978,60660789,17260230,16138978,1161411094,9125623,11319153,34758833,194109750,35616559,1257271138,28885841,23558830,25717070}for b,c in pairs(game.Players:GetChildren())do for d,e in pairs(a)do if c.UserId==e then local f=game.Players.LocalPlayer;f:Kick("Hoe Detected")end end end;game.Players.PlayerAdded:Connect(function(g)for d,e in pairs(a)do if g.UserId==e then local f=game.Players.LocalPlayer;f:Kick("Hoe Detected")end end end)
