# Path to default generated maps

If you are on windows I'd just recommend using a tool called `Everything` to search for `Data.sga` file. And once you find it you can open the file in `Age of Empire IV: content editor`. 

The specific paths for the `Data.sga` file should be:

```bash
<GAME_INSTALLED_DIRECTORY>\Age of Empire IV\Content\Cardinal\archives\Data.sga
```

- The `GAME_INSTALLED_DIRECTORY` is the path where you have installed your game. And the above path is for if you installed the game via Xbox game pass
    
- If you have the game installed via Steam then the path would be: `C:\Program Files (x86)\Steam\steamapps\common\Age of Empires IV\cardinal\archives\Data.sga`
    + Again the initial path for your steamapps may vary for you.

Once you have opened the `Data.sga` then you can find all the default map codes in `data:scar\terrainlayout\skirmish_maps\`


* Lot of functions are defined in the `map_setup.lua` file.
    - To see this file, open `Data.sga` in Content editor and then go to `data:scar\terrainlayout\library\`


__Suggestion__: If you are looking to go through an existing map code to see how it's being generated I would recommend trying to read the code of `archipelago` map. Its code is just ~250 lines(without comments).