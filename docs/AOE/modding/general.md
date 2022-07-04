# General

* When you restart the content editor you might notice that the `attribute` tab isn't really showing all the attributes like `map_gen`, etc. To get those back in the list you need to just kind of refresh the asset explorer.
 	- Go to `Views -> Asset Explorer` or press `ctrl+atl+L` and then go in `Mod -> attrib -> instances` and there should be a file name after the name of your mod. But the extension should be `.xml`. Just double click on that XML file and it will show a sort of loading pop-up. Once that is done you'll see all the attributes back in the menu.


* Below code will place a ring of trees around the map, exactly how it's done in the King of the hill map.

```lua
for row = 1, gridSize do
	for col = 1, gridSize do
		
		if(row == 1 or row == gridSize or col == 1 or col == gridSize) then
			terrainLayoutResult[row][col].terrainType = tt_impasse_trees_plains_forest
		end
	end
end

```
 
* All the rrtex files which are basically icons for the maps are present in the `UIArt.sga` file.
	- UIArt.sga - `data\images\ui\map_gen_layout`
    - You can save them and maybe edit them to suit your map if you like
    
* In order to add images to your mod. Make a directory named `ui` under `attrib` and then make another directory inside `ui` directory called `images`. Add your icon there. Then go in `attributes > map_gen > map_gen_layout > ui > icon` and just write the icon name there.