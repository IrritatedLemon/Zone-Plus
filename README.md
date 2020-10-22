# Zone+
 Open source version of Zone+  
 All source code is in the Source Code folder.  

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

# Zone
## Constructors
### new
`local zone = Zone.new(group, additionalHeight)`
Constructs a new zone where `group` is an instance (such as a Model or Folder) containing parts to represent the zone, and `additionalHeight`, a number defining how many studs to extend the zone upwards, defaulting to `0`.

## Methods
### update  
`zone:update()`  
Reconstructs the region and clusters forming the zone. Zones are dynamic (they listen for changes in children, such as the adding or removing of a part, and the resizing and positioning of these children), therefore will update automatically for you.  

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
### getPlayersInRegion  
`local players = zone:getPlayersInRegion()`  
Returns an array of players within the zone's region.  

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
### getPlayer  
`local hitpart, intersection = zone:getPlayer(player)`  
If within the zone, returns the group part the player is standing on or within (a `BasePart`) and the intersection point (a `Vector3`), otherwise `false`.  

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
### getPlayers  
`local players = zone:getPlayers()`  
Returns an array of players within the zone.  

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
### initLoop  
`zone:initLoop(interval)`  
Initiates a loop which calls `getPlayers()` every x second, defaults to `0.5`.  

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
### initClientLoop()  
`zone:initClientLoop(interval)`  
Initiates a loop which calls `zone:getPlayer(localPlayer)` every x second, defaults to `0.5`.  

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
### endLoop  
`zone:endLoop()`  
Cancels any loop created with `zone:initLoop()`.  

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
### getRandomPoint  
`local randomCFrame, hitPart, hitIntersection = zone:getRandomPoint()`  
Returns a random point (a `CFrame`), within the zone, along with the group part (a `BasePart`) directly below, and its intersection vector relative to the point (a `Vector3`).  

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
### destroy  
`zone:destroy()`  
Destroys all instances, connections and signals associcated with the zone, and ends any loop running.  

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## Events  
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
### playerAdded  
`zone.playerAdded`  
Fired when a player enters the zone.  
```
zone.playerAdded:Connect(function()
	{Insert Code Here}
end)
```
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
### playerRemoving  
`zone.playerRemoving`  
Fired when a player leaves the zone.  
```
zone.playerRemoving:Connect(function()

end)
```
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
### updated
`zone.updated`
Fired when the zone updates (i.e. a group part is changed, such as its position or size, or a part is added or removed from the group).
```
zone.updated:Connect(function()

end)
```
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## Properties
### autoUpdate
`zone.autoUpdate`  
A boolean deciding whether the zone should automatically update when its group parts change.  

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
### respectUpdateQueue
`zone.respectUpdateQueue`  
A boolean that when set to `true` delays the automatic updating of the zone, preventing multiple calls within a short time period.  

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
### group
{read-only}  
`zone.GroupParts`  
An array of all BaseParts within `group`.  

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
### clusters
{read-only}  
`zone.clusters`  
An array of clusters.  

***Cluster***  
A dictionary describing a collection of touching parts within the zone.  

Key | Value | Desc  
parts | Array | A collection of touching parts that form the cluster  
region | Region3 | A region formed from the cluster's parts.  
volume | Int | The volume calculated from `region.Size`  

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
### additionalHeight  
{read-only}  
`zone.additionalHeight`  
The number originally passed when constructing the zone, or 0. Describes how far to extend the zone in the global Y direction.  

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
### region  
{read-only}  
A Region3 formed from `groupParts`.  

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
### boundMin  
{read-only}  
`zone.boundMin`  
A Vector3 used to form `region`, describing the zone's minimum point.  

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
### boundMax  
{read-only}  
`zone.boundMax`  
A Vector3 used to form `region`, describing the zone's maximum point.  

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
### regionHeight  
{read-only}  
`zone.regionHeight`  
A number describing the Y value difference between `boundMin` and `boundMax`.

# Credits

___Zone+ by ForeverHD___  
___Maid and Signal by Quenty___  
___Promise by evaera___  
___Repository by Irritatedlemon___  

You may find me at IrritatedLemon#0015.  
