# Team Config

### Group-locking Teams:[​](https://ags816710.github.io/rcd/docs/teamConfig#group-locking-teams) <a href="#group-locking-teams" id="group-locking-teams"></a>

#### Step 1:[​](https://ags816710.github.io/rcd/docs/teamConfig#step-1) <a href="#step-1" id="step-1"></a>

Navigate to ServerScriptService>Services>RemoteService:3225

#### Step 2:[​](https://ags816710.github.io/rcd/docs/teamConfig#step-2) <a href="#step-2" id="step-2"></a>

Replace whole line with:

```lua

  if Player:IsInGroup(TeamsDatabase[Value].GroupId) or Developers[Player.UserId] ~= nil then
     PlayerListService:ChangeTeam(Player, Value)
     Events.Alerts:FireClient(Player, "Change Team", "You have been switched to "..tostring(Value), "Blue")
  end

```

### Trello-locking Teams:[​](https://ags816710.github.io/rcd/docs/teamConfig#trello-locking-teams) <a href="#trello-locking-teams" id="trello-locking-teams"></a>

#### Step 1: Open Script[​](https://ags816710.github.io/rcd/docs/teamConfig#step-1-open-script) <a href="#step-1-open-script" id="step-1-open-script"></a>

Navigate to ServerScriptService>Services>TrelloService

#### Step 2: Paste Code[​](https://ags816710.github.io/rcd/docs/teamConfig#step-2-paste-code) <a href="#step-2-paste-code" id="step-2-paste-code"></a>

Paste the following before the `return TrelloService` line.

```lua

function TrelloService:GetTeamWhitelist(Player, Team)
    if cooldown[Player] then return nil end
    cooldown[Player] = true
    task.delay(3, function() cooldown[Player] = nil end)
    
    if not Lists[Team.."_TW"] then return true end
    
    local GET = HttpService:GetAsync(temp)
    local Results = HttpService:JSONDecode(GET)
    if Results then
        for i, v in Results do
            if Lists[Team.."_TW"] == v.idList then
                if Player.UserId == tonumber(v.name) then
                    return true
                elseif Player.Name == v.name then
                    return true
                elseif v.name:sub(1,6):lower() == "group:" then
                    local str = v.name:sub(7)

                    if str then
                        local tbl = str:split(":")

                        if tbl[1] then
                            if tbl[2] then
                                if Player:GetRankInGroup(tbl[1]) >= tbl[2] then
                                    return true
                                end
                            else
                                if Player:IsInGroup(tbl[1]) then
                                    return true
                                end
                            end
                        end
                    end
                end
            end
        end
        return false
    end
end

```

#### Step 3: Open Trello[​](https://ags816710.github.io/rcd/docs/teamConfig#step-3-open-trello) <a href="#step-3-open-trello" id="step-3-open-trello"></a>

Go to [trello](https://trello.com/)

#### Step 4: Create Board[​](https://ags816710.github.io/rcd/docs/teamConfig#step-4-create-board) <a href="#step-4-create-board" id="step-4-create-board"></a>

Create a board by clicking "Create new Board"

#### Step 5: Copy BoardId[​](https://ags816710.github.io/rcd/docs/teamConfig#step-5-copy-boardid) <a href="#step-5-copy-boardid" id="step-5-copy-boardid"></a>

Copy the boardId from the address bar (eg: the "boardId" in [https://trello.com/b/boardId/boardName](https://trello.com/b/boardId/boardName))

#### Step 6: Put boardId into script[​](https://ags816710.github.io/rcd/docs/teamConfig#step-6-put-boardid-into-script) <a href="#step-6-put-boardid-into-script" id="step-6-put-boardid-into-script"></a>

Go to the TrelloService module script and add your boardId into the "board" variable.\
Format:

```lua
local board = "https://api.trello.com/1/boards/boardId
```

#### Step 7: Copy personal app key[​](https://ags816710.github.io/rcd/docs/teamConfig#step-7-copy-personal-app-key) <a href="#step-7-copy-personal-app-key" id="step-7-copy-personal-app-key"></a>

Go [here](https://trello.com/app-key) and copy your personal key

#### Step 8: Generate token[​](https://ags816710.github.io/rcd/docs/teamConfig#step-8-generate-token) <a href="#step-8-generate-token" id="step-8-generate-token"></a>

Look below the personal app key and click generate token.\
You can go up to the address bar and change the text between "name=" and "\&key=" to whatever you wish, or you can keep it the same.\
\


Click "Allow" and copy your token.

#### Step 9: Input token & key into script[​](https://ags816710.github.io/rcd/docs/teamConfig#step-9-input-token--key-into-script) <a href="#step-9-input-token--key-into-script" id="step-9-input-token--key-into-script"></a>

Place your key in both the "getCards" and "getLists" variables.\
Like:

```lua
local getCards = board.."cards?key=KEYHERE&token=TOKENHERE"
local getLists = board.."lists?key=KEYHERE&token=TOKENHERE"
```

#### Step 10: Create Lists[​](https://ags816710.github.io/rcd/docs/teamConfig#step-10-create-lists) <a href="#step-10-create-lists" id="step-10-create-lists"></a>

On your trello board, create lists for each of the teams you would like whitelisted.

#### Step 11: Get ListIds[​](https://ags816710.github.io/rcd/docs/teamConfig#step-11-get-listids) <a href="#step-11-get-listids" id="step-11-get-listids"></a>

Go up to the address bar and add .json to the end of the URL, hit enter.\


This may look crazy at first, but all you need to do is search for the name of the list and copy the id of the board. Like this: ![image](https://ags816710.github.io/rcd/assets/images/screenshotOfHowGetTrelloListId-909fdd728cae8aef99e3fa93fce5d59d.png)

\
\
Repeat for all of the teams/lists you need.

#### Step 12: Add ids to table[​](https://ags816710.github.io/rcd/docs/teamConfig#step-12-add-ids-to-table) <a href="#step-12-add-ids-to-table" id="step-12-add-ids-to-table"></a>

For each of the teams, add them as entries into the "Lists" table. Format:\


```lua
  ["TeamNameHere_TW"] = "ListIdHere",
```

#### Step 13: Paste another bit[​](https://ags816710.github.io/rcd/docs/teamConfig#step-13-paste-another-bit) <a href="#step-13-paste-another-bit" id="step-13-paste-another-bit"></a>

Replace ServerScriptService>Services>RemoteService line 3229 & line 3230 to:

```lua
if TrelloService:GetTeamWhitelist(Player, Value) then
    PlayerListService:ChangeTeam(Player, Value)
    Events.Alerts:FireClient(Player, "Change Team", "You have been switched to "..tostring(Value), "Blue")
else
    Events.Alerts:FireClient(Player, "Team Change", "You do not have permission to join this team!", "Red")
end
```

#### Step 14: Paste again[​](https://ags816710.github.io/rcd/docs/teamConfig#step-14-paste-again) <a href="#step-14-paste-again" id="step-14-paste-again"></a>

Replace ServerScriptService>Services>RemoteService line 709 until 714 with:

```lua
if TrelloService:GetTeamWhitelist(Player, Team) then
    PlayerListService:ChangeTeam(Player, Team)
    MDTService.UpdateCallsign(Player, nil)
    wait(0.25)
    Player:LoadCharacter()
    TeamChangeDebounce[Player] = nil
    API.unlockMovement(Player)
else
    Events.Alerts:FireClient(Player, "Change Team", "You do not have permission to join this team!", "Red")
end
```

### Removing Team Killing Notifications:[​](https://ags816710.github.io/rcd/docs/teamConfig#removing-team-killing-notifications) <a href="#removing-team-killing-notifications" id="removing-team-killing-notifications"></a>

#### Step 1:[​](https://ags816710.github.io/rcd/docs/teamConfig#step-1-1) <a href="#step-1-1" id="step-1-1"></a>

Navigate to ServerScriptService>Services>RemoteService:5027

#### Step 2:[​](https://ags816710.github.io/rcd/docs/teamConfig#step-2-1) <a href="#step-2-1" id="step-2-1"></a>

Remove ( or comment out ) the following:

```lua

if TeamsDatabase[killer.Team.Name].IsLEO == true and TeamsDatabase[Player.Team.Name].IsLEO == true and game.PrivateServerId == "" then
    Events.Alerts:FireClient(killer, "Team Killing", "Killing other LEOs is against game rules. Continuing this behaviour will result in moderation!", "Red", true)
    for i,v in pairs(game.Players:GetPlayers()) do
        if require(game:GetService("ServerScriptService").Services.DataService):GetData(v).Moderator or require(game:GetService("ServerScriptService").Services.DataService):GetData(v).Developer then
            Events.Alerts:FireClient(v, "Team Killing", Player.Name.." has just been team killed by "..killer.Name, "Red", true)
        end
    end
end

```

### Adding team-changer UI:[​](https://ags816710.github.io/rcd/docs/teamConfig#adding-team-changer-ui) <a href="#adding-team-changer-ui" id="adding-team-changer-ui"></a>

#### Step 1:[​](https://ags816710.github.io/rcd/docs/teamConfig#step-1-2) <a href="#step-1-2" id="step-1-2"></a>

Open the 'Find all / Replace All' menu by going to View>Find All / Replace All

#### Step 2:[​](https://ags816710.github.io/rcd/docs/teamConfig#step-2-2) <a href="#step-2-2" id="step-2-2"></a>

Search for 7262405121 and replace with your place's ID#
