# Zone+
 Open source version of Zone+  
 All source code is in the Source Code folder.  
 Repository by IrritatedLemon.  

 ## Installation

 _Installing Zone+ incorrectly may cause many errors_  
 ___Open a Roblox Studio project.___  
 __Create a new folder.__  
 __Name the folder "Zone+"__  
 __Place the folder in ReplicatedStorage__


  ### Zone

  _Create a new ModuleScript_  
  _Name the script "Zone"_  
  _Open Zone.lua_  
  _Copy all the text in the file_  
  _Paste the text into the script editor_  

  ### Zone Service

  _Create a new ModuleScript_  
  _Name the script "ZoneService"_  
  _Open Zone Service.lua_  
  _Copy all the text in the file_  
  _Paste the text into the script editor_  

  ### Maid

  _Create a new ModuleScript_  
  _Name the script "Maid"_  
  _Open Maid.lua_  
  _Copy all the text in the file_  
  _Paste the text into the script editor_  

  ### Promise

  _Create a new ModuleScript_  
  _Name the script "Promise"_  
  _Open Promise.lua_  
  _Copy all the text in the file_  
  _Paste the text into the script editor_  

  ### Signal

  _Create a new ModuleScript_  
  _Name the script "Signal"_  
  _Open Signal.lua_  
  _Copy all the text in the file_  
  _Paste the text into the script editor_  

 ## Documentation

  ### Server Example

  ```
  local ZoneService = require(ZonePlus.ZoneService) -- Retrieve and require ZoneService
  local group = workspace.YourGroupHere -- A container (i.e. Model or Folder) of parts that represent the zone
  local zone = ZoneService:createZone("ZoneName", group, 15) -- Construct a zone called 'ZoneName' using 'group' and with an extended height of 15 

  local playersInZone = zone:getPlayers() -- Retrieves an array of players within the zone

  zone.playerAdded:Connect(function(player) -- Fires when a player enters the zone
      print(player.Name.." entered!")
  end)
  zone.playerRemoving:Connect(function(player)  -- Fires when a player exits the zone
      print(player.Name.." left!")
  end)
  zone:initLoop() -- Initiates loop (default 0.5) which enables the events to work
  ```

  ### Client example

  ```
  local ZonePlus = game:GetService("ReplicatedStorage"):WaitForChild("Zone+")
  local ZoneService = require(ZonePlus.ZoneService)
  local group = workspace.YourGroupHere --A model or folder
  local zone = ZoneService:createZone("ZoneName", group, 15)
  local localPlayer = game:GetService("Players").LocalPlayer

  local isClientInZone = zone:getPlayer(localPlayer) -- Checks whether the local player is within the zone

  zone.playerAdded:Connect(function() -- Fires when the localPlayer enters the zone
      print(localPlayer.Name.." entered!")
  end)
  zone.playerRemoving:Connect(function()  -- Fires when the localPlayer exits the zone
      print(localPlayer.Name.." left!")
  end)
  zone:initClientLoop()
  ```

 ## Media Examples
 
 ### Safe Zone (1)
 Setup a zone with an arbitrary space (using the `additionalHeight` parameter), retrieve all players within the zone at frequent intervals, and apply or remove a forcefield accordingly. This example also generates 2000 random parts as a visual representation of `additionalHeight`.  
 ![](https://github.com/IrritatedLemon/Zone-Plus/blob/main/Media/Safe%20Zones%201.gif)  
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

### Safe Zone (2)
Detect and apply a forcefield to players within an uncancollided red zone using the `playerAdded` and `playerRemoving` events.  
![](https://github.com/IrritatedLemon/Zone-Plus/blob/main/Media/Safe%20Zones%202.gif)  
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

### Coin Spawner
Randomly generate coins a few studs above any surface within the zone.  
![](https://github.com/IrritatedLemon/Zone-Plus/blob/main/Media/Coins.gif)  
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

### Voting Pads
Utilise zones to determine the amount of players on a particular pad.  
![](https://github.com/IrritatedLemon/Zone-Plus/blob/main/Media/Vote.gif)
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
