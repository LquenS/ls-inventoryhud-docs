How can i implement my framework?

# QB

- Locate qb-core > server > player.lua
- Find "AddItem" and replace with that
```
function self.Functions.AddItem(item, amount, slot, info)
	exports["ls-inventoryhud"]:AddItem(self.PlayerData.source, item, amount, info)
end
```

- After doing this find "RemoveItem" and replace with that
```
function self.Functions.RemoveItem(item, amount, id)
	return exports["ls-inventoryhud"]:RemoveItem(self.PlayerData.source, id, amount)
end
```

## ! IF YOUR VERSION NEWEST OF QB-CORE !

- You cannot find any "AddItem" & "RemoveItem"
- Find "QBCore.Player.CreatePlayer"
- Find "self.Functions = {}" and add this functions (!!YOU NEED TO ADD BOTTOM OF self.Functions IF YOU DONT YOU GET ERRORS!!),
```
function self.Functions.AddItem(item, amount, slot, info)
	exports["ls-inventoryhud"]:AddItem(self.PlayerData.source, item, amount, info)
end

function self.Functions.RemoveItem(item, amount, id)
	return exports["ls-inventoryhud"]:RemoveItem(self.PlayerData.source, id, amount)
end
```

# ESX

- Locate es_extended > server > classes > player.lua
- Find "addInventoryItem" and replace with that
```
function self.addInventoryItem(name, count, metadata, slot)
	exports["ls-inventoryhud"]:AddItem(self.source, name, count, metadata)
end
```
- After doing this find "removeInventoryItem" and replace with that
```
function self.removeInventoryItem(name, count, metadata, slot)
	exports["ls-inventoryhud"]:RemoveItem(self.source, name, count)
end
```

# If you finished this thing, last thing left clothing!

## QB

- Find your clothing script (probably qb-clothing)
- After that find you skin saving function add this
```
TriggerEvent("ls-inventoryhud:c:giveClothesAsItem", skinData, previousSkinData, false) (skinData is currently skin, previousSkinData oldest skin)
```

### If you have qb-clothing

- Find "SaveSkin" and replace with that
```
function SaveSkin()
    local model = GetEntityModel(PlayerPedId())
    local clothing = json.encode(skinData)
    TriggerServerEvent("qb-clothing:saveSkin", model, clothing)
    TriggerEvent("ls-inventoryhud:c:refreshClothes")

    TriggerEvent("ls-inventoryhud:c:giveClothesAsItem", skinData, previousSkinData, false)
end
```

## ESX

- Find your clothing script (probably esx-skin)
- After that find you skin saving function add this
```
TriggerEvent("ls-inventoryhud:c:giveClothesAsItem", skin, lastSkin, false) (skinData is currently skin, previousSkinData oldest skin)
```

### If you have esx-skin

- Find "OpenSaveableMenu" and replace with that
```
function OpenSaveableMenu(submitCb, cancelCb, restrict)
    TriggerEvent('skinchanger:getSkin', function(skin) lastSkin = skin end)

    OpenMenu(function(data, menu)
        menu.close()
        DeleteSkinCam()

        TriggerEvent('skinchanger:getSkin', function(skin)
            TriggerServerEvent('esx_skin:save', skin)

            if submitCb ~= nil then
                submitCb(data, menu)
            end
			
			TriggerEvent("ls-inventoryhud:c:giveClothesAsItem", skin, lastSkin, false)
        end)

    end, cancelCb, restrict)
end
```
