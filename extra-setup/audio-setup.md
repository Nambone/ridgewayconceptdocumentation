# Audio Setup

### What you'll need: <a href="#what-youll-need" id="what-youll-need"></a>

\- [Sounds File](https://mega.nz/file/5Vp0FJQA#71abNbKtGRFA6gn9NXOpYShyNYpTUnA6-CSSKq5CyHs)

### Audio Files <a href="#fixing-animations-1" id="fixing-animations-1"></a>

#### Step 1:

Download the **sounds file (ridgeway sounds export)** attached below

#### Step 2:

Replace every **IDGOESHERE** in the script below with the ID of **your re-uploaded audio**

```lua
//local audioTable = {
	["DaySound-Fix2"] = "rbxassetid://IDGOESHERE",
	["rw-nightsound"] = "rbxassetid://IDGOESHERE",
	["Snow Winds Ambiance (2 mins)"] = "rbxassetid://IDGOESHERE",
	["LETC"] = "rbxassetid://IDGOESHERE",
	["Engine Sound (Dart)"] = "rbxassetid://IDGOESHERE",
	["new-airhorn-cut"] = "rbxassetid://IDGOESHERE",
	["(Manual)"] = "rbxassetid://IDGOESHERE",
	["Priority2"] = "rbxassetid://IDGOESHERE",
	["Yelp1"] = "rbxassetid://IDGOESHERE",
	["OldWail"] = "rbxassetid://IDGOESHERE",
	["OldBlip"] = "rbxassetid://IDGOESHERE",
	["OldYelp"] = "rbxassetid://IDGOESHERE",
	["quint-pump"] = "rbxassetid://IDGOESHERE",
	["TRAIN-ON-TRACKS"] = "rbxassetid://IDGOESHERE",
	["Waterfall"] = "rbxassetid://IDGOESHERE",
	["GARAGEDoor"] = "rbxassetid://IDGOESHERE",
}
 
game.Workspace.AmbientSounds.DaySound.SoundId = audioTable["DaySound-Fix2"]
game.Workspace.AmbientSounds.NightSound.SoundId = audioTable["rw-nightsound"]
game.Workspace.AmbientSounds.Wind.SoundId = audioTable["Snow Winds Ambiance (2 mins)"]
game.Workspace.GraduationSound.SoundId = audioTable["LETC"]
 
for i,v in pairs(game.ServerStorage.Cars:GetDescendants()) do
	if v:IsA("Sound") and v.Parent.Parent.Parent then
		if not v.Parent.Parent.Parent.Parent.Name:find("RCFD") then
			if v.Name == "RealEngineSound" then
				v.SoundId = audioTable["Engine Sound (Dart)"]
			elseif v.Name == "Airhorn" then
				v.SoundId = audioTable["new-airhorn-cut"]
			elseif (v.Name == "Manual" or v.Name == "Wail") and not v.Parent.Parent.Parent.Parent.Name:find("Visco") then
				v.SoundId = audioTable["(Manual)"]
			elseif (v.Name == "Manual" or v.Name == "Wail") and v.Parent.Parent.Parent.Parent.Name:find("Visco") then
				v.SoundId = audioTable["OldWail"]
			elseif v.Name == "Priority" and v.Parent.Parent.Parent.Parent.Name:find("Visco") then
				v.SoundId = audioTable["OldBlip"]
			elseif v.Name == "Yelp" and v.Parent.Parent.Parent.Parent.Name:find("Visco") then
				v.SoundId = audioTable["OldYelp"]
			elseif v.Name == "Priority" and not v.Parent.Parent.Parent.Parent.Name:find("Visco") then
				v.SoundId = audioTable["Priority2"]
			elseif v.Name == "Yelp" and not v.Parent.Parent.Parent.Parent.Name:find("Visco") then
				v.SoundId = audioTable["Yelp1"]
			end
		end
	end
end
 
game.ServerStorage.Cars["RCFD Quint"].Cosmetics.Body.Extra.QuintInteracts.Pump.PumpSound.SoundId = audioTable["quint-pump"]
 
for i,v in pairs(game.Workspace:GetDescendants()) do
	if v:IsA("Sound") and v.Name == "OnTrackSound" then
		v.SoundId = audioTable["TRAIN-ON-TRACKS"]
	elseif v:IsA("Sound") and v.Name == "Waterfall" then
		v.SoundId = audioTable["Waterfall"]
	elseif (v:IsA("Sound") and v.Name == "OpenSound" and v.Parent.Parent.Name:find("GarageDoor")) then
		v.SoundId = audioTable["GARAGEDoor"]
	end
end
```

#### Step 3:

Once you replace all desired IDs, paste the script into the roblox studio **command line** and execute

#### Step 4:

Lastly, grab your **Universe ID (Not the same as Place/Experience ID!)**, go onto the roblox website and into the audios management thingy under the **Create** tab ([https://www.roblox.com/develop?View=3](https://www.roblox.com/develop?View=3)) and grant sound permissions using the **Universe ID** of your game.



### Instruction Clarification

### **Experience IDs**

#### **Step 1:**

If using the Google Chrome web browser, click the three dots in the top right. Ensure you are on your games Roblox page (Similar to [this](https://www.roblox.com/games/13702845118/Parliament))

#### Step 2:

After doing so look down until you find 'More Tools', click it.

#### Step 3:

Then hit Ctrl+Shift+I or find 'Developer Tools'

#### Step 4:

On the top bar make sure you are on elements. Then Ctrl+F and type in "Universe" you should see this line of code highlighted.

```lua
<div id="game-detail-meta-data" data-universe-id="YOUR UNIVERSE ID" data-place-id="13702845118" data-place-name="Parliament" data-page-id="3de54041-f922-4048-92dc-45976236dc6a" data-root-place-id="13702845118" data-show-shut-down-all-button="True" data-user-can-manage-place="True" data-private-server-price="0" data-can-create-server="False" data-private-server-limit="0" data-seller-name="" data-seller-id="0" data-private-server-product-id="0" data-private-server-link-code="" data-preopen-create-private-server-modal="False" data-experience-invite-link-id="" data-experience-invite-status="" data-can-copy-place="False" class="hidden"></div>ua
```

#### Step 5:

Focus on `data-universe-id="UNIVERSE ID"`At that point what ever is in the quotes is it!



DIRECT ALL INQUIRIES AND QUESTIONS TO **RaspberryStruggle#1205** DMS!
