# Player Spawn

No matter what type of map you create you'll obviously have to add the places where the players will be spawned. Now there are various ways to actually do it.


## Basic method

If you are just getting started I'd say you try to use the below method to actually see how the players get spawned.

```lua
terrainLayoutResult[gridSize-5][gridSize].terrainType = tt_player_start_classic_plains
terrainLayoutResult[gridSize-5][gridSize].playerIndex = 0

terrainLayoutResult[2][3].terrainType = tt_player_start_classic_plains
terrainLayoutResult[2][3].playerIndex = 1
```

__NOTE__: The above code is only for player spawn and just these 4 lines won't work. In this `SetupGrid` code also needs to be added.

In order to see a very basic tutorial that uses the above code you can watch [this video](https://www.youtube.com/watch?v=LXh4Hpgo050)


## Using PlacePlayerStart* functions


The above example is just for two-player and if you try to expand the map for 4 players or more it will give an error because we are only placing 2 players. So the better way to do is to use either of the following functions:

- `PlacePlayerStartsDivided` - This can be used when you are trying to make sure all the teams spawn on the same side or are together.
- `PlacePlayerStartsRing` - These are for more `randomPosition` generation. 

Ex: The following code is taken from the `nagari` map:

```lua
-- check randomPositions is false i.e teams should be together
if (#teamMappingTable == 2) and (randomPositions == false) and (worldPlayerCount >= 2) then
	minTeamDistance = 7
	minPlayerDistance = 8
	if (rangeType == 1) then --vertical orientation
		terrainLayoutResult = PlacePlayerStartsDivided(teamMappingTable, minTeamDistance, minPlayerDistance, edgeBuffer, .48, cornerThreshold, false, spawnBlockers, 1, 0.05, playerStartTerrain, tt_plains, 1, false, terrainLayoutResult)
	else --horizontal orientation
		terrainLayoutResult = PlacePlayerStartsDivided(teamMappingTable, minTeamDistance, minPlayerDistance, edgeBuffer, .48, cornerThreshold, true, spawnBlockers, 1, 0.05, playerStartTerrain, tt_plains, 1, false,terrainLayoutResult)
	end
else
    -- if teams are not meant to be together just place them somewhere on the map
	terrainLayoutResult = PlacePlayerStartsRing(teamMappingTable, minTeamDistance, minPlayerDistance, edgeBuffer, .4, cornerThreshold, spawnBlockers, 1, 0.05, playerStartTerrain, tt_plains, 1, false, terrainLayoutResult)
end

```

Below is an example showing you how to use these functions along with the variables being used in them. 

```lua
teamMappingTable = CreateTeamMappingTable()
minTeamDistance = Round((#terrainLayoutResult * 0.85))
minPlayerDistance = Round((#terrainLayoutResult * 0.9))
edgeBuffer = 3
innerExclusion = 0.45
topSelectionThreshold = 0.1
impasseTypes = {tt_mountains_small}
impasseDistance = 1.5
cornerThreshold = 0
spawnBlockDistance = 1.5
spawnBlockers = {tt_mountains, tt_plateau_low}
playerStartTerrain = tt_player_start_classic_plains_naval

terrainLayoutResult = PlacePlayerStartsRing(teamMappingTable, minTeamDistance, minPlayerDistance, edgeBuffer, innerExclusion, cornerThreshold, spawnBlockers, spawnBlockDistance, 0.02, playerStartTerrain, tt_plains_smooth, 2, true, terrainLayoutResult)


terrainLayoutResult = PlacePlayerStartsDivided(teamMappingTable, minTeamDistance, minPlayerDistance, edgeBuffer, .48, cornerThreshold, true, spawnBlockers, 1, 0.05, playerStartTerrain, tt_plains, 1, false,terrainLayoutResult)

--make sure to use them either in an "if" condition or comment out one of them.
```

Below are the comments which are taken from one of the game files called `map_setup.lua`. It explains all the variables used above:

```lua
--This function(PlacePlayerStartsDivided) places two teams of players in two horizontal or vertical bands
--The teamMappingTable holds player IDs and team compositions, gotten from the CreateTeamMappingTable function.
--minTeamDistance is how far apart the "team locations" must be. A "team location" is a central spot around which players from that team will be placed. This is a distant relative to the course grid squares.
--minPlayerDistance determines how far each player must be from another player. When using "Teams Apart", this determines how far opposite teams can be from one another also.
--edgeuffer determines how many squares around a grid's perimeter players cannot spawn
--innerExclusion is a value between 0 and 1 that determines the percentage of the interior of the grid to block from player spawning. eg on a 20x20 grid, a 0.5 innerExclusion would black out the center 10x10
--impasseTypes are the terrain types that are avoided
--impasseDistance is how far away all potential player spawns must be from any squares that have an impasseTypes grid type.
--topSelectionThreshold is how variable the selection of starts around the selected team location can be, on a scale from 0 to 1. 0.05 will give only the top 5% of spaces, resulting in a tightly grouped team.
--playerStartTerrain is the terrain that gets put down at a chosen player spawning position
--startBufferTerrain is the terrain that gets put down around player starts
--terrainGrid is the terrainLayoutResult from the map layout
```

* In the example code shown above the `tt_plains_smooth` is `startBufferTerrain`, 2 is `startBufferRadius` and true is `placeBufferTerrain`
    - The startBufferTerrain is the terainType that will surround each player start that gets placed.
    - The startBufferRadius is a float that is how many squares in each direction the buffer terrain will be placed 
    - PlaceBufferTerrain is a bool that tells the function to place the buffer or not


## Using CreateIslandsTeams* functions

Then there are also other functions such as :

* `CreateIslandsTeamsTogether`
* `CreateIslandsTeamsTogetherEven`
* `CreateIslandsTeamsApart`

The functions does exactly what the name says. These functions are mostly used in maps which had the `tt_ocean` as the base. So maps like `archipelago`, `warring island`.

These functions sort of helps in generating islands for player placements and can then also be combined with other functions like `FillWithIslands` to generate some more random islands.

Take example of `archipelago` where players start on their own island and then there are random number of few more island on which no player is placed. But there are resources on those islands. That map uses `CreateIslandsTeamsApartEven` to place players and then uses `FillWithIslands` to place those random island which contains stone/gold resources.

Below is the code taken from game file `archipelago.lua`

```lua
CreateIslandsTeamsApartEven(islandSize, editedPlayerCount, totalIslandNum, distanceBetweenIslands, edgeGap, innerExclusion, inlandRadius, islandGap, teamMappingTable, playerStartTerrain, startBufferRadius, cliffChance, forestChance, inlandTerrainChance, inlandTerrain, minTeamDistance, minPlayerDistance, impasseTypes, impasseDistance, topSelectionThreshold, playerEdgeGap, terrainLayoutResult)


specialTerrain = {}
specialTerrain = {tt_bounty_gold_plains, tt_bounty_stone_plains}

extraIslands = {}

equalIslands = false
extraIslands = FillWithIslands(extraIslandSize, equalIslands, totalIslandNum, distanceBetweenIslandsExtra, startingEdgeGap, edgeGap, 0, islandGap, cliffChance, forestChance, inlandTerrainChance, inlandTerrain, impasseTypes, impasseDistance, specialTerrain, playerStartTerrain, terrainLayoutResult)
```

Again below are the comments take from `map_setup.lua` to example __some__ of the variables being used in these functions

```lua
--this function(CreateIslandsTeamsTogether) sets up a water map with teams of players placed on their own islands
--weightTable is a table of values that hold the islands that will be created and their weight values. A higher weighted island will have a larger chance of being expanded in size as the map is built
--land coverage is a value from 0 to 1 and specifies the percentage of the map to be covered in land. eg a map with 0.75 landCoverage will have 75% of the grid squares consist of land terrain types
--distanceBetweenIslands is how far apart initial island seeding points are
--edgeGap is the number of squares around the edge of the map that island land squares cannot occupy
--islandGap is the number of spaces between island shores
--the teamMappingTable (created with the CreateTeamMappingTable function) holds which players are on which teams and sets up islands appropriately
--playerStartTerrain is whatever type of terrain you are using to spawn your starting resources
--cliffChance denotes the likelihood of a cliff spawning on the shore of an island (gives a non-landable beach)
--inlandTerrainChance is a number from 0 to 1 denoting the chance to change a square of island land terrain into one of the other types passed in
--inlandTerrain is a table of terrain types that can be chosen to replace basic plains on islands (based on the inlandTerrainChance parameter)
```

## Tips about player spawning on water base


It's possible that you are trying to set the base of the map to `tt_ocean` and when using any player spawn function you might see that the TC is being generated under water. There are ways to fix it. One way would be to use the `PlacePlayerStartsDivided` or `PlacePlayerStartsRing` function and for the value of `PlayerStartTerrain` choose any `Plain` terrain like `tt_player_start_classic_plains` and for the value of bufferTerrain use something with hill like `tt_hills_high_flattop`. 

What I just said above in english is shown below in the lua code:

```lua
playerStartTerrain = tt_player_start_classic_plains

terrainLayoutResult = PlacePlayerStartsDivided(teamMappingTable, minTeamDistance, minPlayerDistance, edgeBuffer, innerExclusion, cornerThreshold, true, spawnBlockers, spawnBlockDistance, 0.05, playerStartTerrain, tt_hills_high_flattop, 5, true, terrainLayoutResult)
```

Another hacky method is to just place them with whatever plain you wanna use and if during the spawn the TC/vills are under water then you can record their starting position and place some different type of terrain around the starting position.

Ex:

```lua
for row = 1, gridSize do
	for col = 1, gridSize do
		
		if(terrainLayoutResult[row][col].terrainType == playerStartTerrain) then
            terrainLayoutResult[row][col].terrainType = tt_player_start_classic_plain_naval
		end
		
	end
end
```