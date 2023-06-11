# Audio Setup

### What you'll need: <a href="#what-youll-need" id="what-youll-need"></a>

\- [Sounds File](https://mega.nz/file/5Vp0FJQA#71abNbKtGRFA6gn9NXOpYShyNYpTUnA6-CSSKq5CyHs)

### Audio Files <a href="#fixing-animations-1" id="fixing-animations-1"></a>

#### Step 1:

Download the **sounds file (ridgeway sounds export)** attached below

#### Step 2:

Replace every **IDGOESHERE** in the script below with the ID of **your re-uploaded audio**

\`local audioTable = { \["DaySound-Fix2"] = "rbxassetid://IDGOESHERE", \["rw-nightsound"] = "rbxassetid://IDGOESHERE", \["Snow Winds Ambiance (2 mins)"] = "rbxassetid://IDGOESHERE", \["LETC"] = "rbxassetid://IDGOESHERE", \["Engine Sound (Dart)"] = "rbxassetid://IDGOESHERE", \["new-airhorn-cut"] = "rbxassetid://IDGOESHERE", \["(Manual)"] = "rbxassetid://IDGOESHERE", \["Priority2"] = "rbxassetid://IDGOESHERE", \["Yelp1"] = "rbxassetid://IDGOESHERE", \["OldWail"] = "rbxassetid://IDGOESHERE", \["OldBlip"] = "rbxassetid://IDGOESHERE", \["OldYelp"] = "rbxassetid://IDGOESHERE", \["quint-pump"] = "rbxassetid://IDGOESHERE", \["TRAIN-ON-TRACKS"] = "rbxassetid://IDGOESHERE", \["Waterfall"] = "rbxassetid://IDGOESHERE", \["GARAGEDoor"] = "rbxassetid://IDGOESHERE", }

game.Workspace.AmbientSounds.DaySound.SoundId = audioTable\["DaySound-Fix2"] game.Workspace.AmbientSounds.NightSound.SoundId = audioTable\["rw-nightsound"] game.Workspace.AmbientSounds.Wind.SoundId = audioTable\["Snow Winds Ambiance (2 mins)"] game.Workspace.GraduationSound.SoundId = audioTable\["LETC"]

for i,v in pairs(game.ServerStorage.Cars:GetDescendants()) do if v:IsA("Sound") and v.Parent.Parent.Parent then if not v.Parent.Parent.Parent.Parent.Name:find("RCFD") then if v.Name == "RealEngineSound" then v.SoundId = audioTable\["Engine Sound (Dart)"] elseif v.Name == "Airhorn" then v.SoundId = audioTable\["new-airhorn-cut"] elseif (v.Name == "Manual" or v.Name == "Wail") and not v.Parent.Parent.Parent.Parent.Name:find("Visco") then v.SoundId = audioTable\["(Manual)"] elseif (v.Name == "Manual" or v.Name == "Wail") and v.Parent.Parent.Parent.Parent.Name:find("Visco") then v.SoundId = audioTable\["OldWail"] elseif v.Name == "Priority" and v.Parent.Parent.Parent.Parent.Name:find("Visco") then v.SoundId = audioTable\["OldBlip"] elseif v.Name == "Yelp" and v.Parent.Parent.Parent.Parent.Name:find("Visco") then v.SoundId = audioTable\["OldYelp"] elseif v.Name == "Priority" and not v.Parent.Parent.Parent.Parent.Name:find("Visco") then v.SoundId = audioTable\["Priority2"] elseif v.Name == "Yelp" and not v.Parent.Parent.Parent.Parent.Name:find("Visco") then v.SoundId = audioTable\["Yelp1"] end end end end

game.ServerStorage.Cars\["RCFD Quint"].Cosmetics.Body.Extra.QuintInteracts.Pump.PumpSound.SoundId = audioTable\["quint-pump"]

for i,v in pairs(game.Workspace:GetDescendants()) do if v:IsA("Sound") and v.Name == "OnTrackSound" then v.SoundId = audioTable\["TRAIN-ON-TRACKS"] elseif v:IsA("Sound") and v.Name == "Waterfall" then v.SoundId = audioTable\["Waterfall"] elseif (v:IsA("Sound") and v.Name == "OpenSound" and v.Parent.Parent.Name:find("GarageDoor")) then v.SoundId = audioTable\["GARAGEDoor"] end end\`
