ESX & QBCORE is stable, if you have any error check your framework or setup!

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

- After doing this find "GetItemByName" and replace with that
```
function self.Functions.GetItemByName(item)
	item = tostring(item):lower()
		
	for k ,v in pairs ( exports["ls-inventoryhud"]:GetItems(self.PlayerData.source) ) do
		if v._tpl == item then
			return v
		end
	end
end
```

- After doing this find "GetItemsByName" and replace with that
```
function self.Functions.GetItemsByName(item)
	item = tostring(item):lower()
	local items = {}
	for k ,v in pairs ( exports["ls-inventoryhud"]:GetItems(self.PlayerData.source) ) do
		if v._tpl == item then
			items[#items+1] = v
		end
	end
        return items
end
```

## ! IF YOUR VERSION NEWEST OF QB-CORE !

- You cannot find any "AddItem" & "RemoveItem" & "GetItemByName" & "GetItemsByName"
- Find "QBCore.Player.CreatePlayer"
- Find "self.Functions = {}" and add this functions (!!YOU NEED TO ADD BOTTOM OF self.Functions IF YOU DONT YOU GET ERRORS!!),
```
function self.Functions.AddItem(item, amount, slot, info)
	exports["ls-inventoryhud"]:AddItem(self.PlayerData.source, item, amount, info)
end

function self.Functions.RemoveItem(item, amount, id)
	return exports["ls-inventoryhud"]:RemoveItem(self.PlayerData.source, id, amount)
end

function self.Functions.GetItemByName(item)
	item = tostring(item):lower()
		
	for k ,v in pairs ( exports["ls-inventoryhud"]:GetItems(self.PlayerData.source) ) do
		if v._tpl == item then
			return v
		end
	end
end

function self.Functions.GetItemsByName(item)
	item = tostring(item):lower()
	local items = {}
	for k ,v in pairs ( exports["ls-inventoryhud"]:GetItems(self.PlayerData.source) ) do
		if v._tpl == item then
			items[#items+1] = v
		end
	end
        return items
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
	local foundItem = exports["ls-inventoryhud"]:GetItem(self.source, name)
	if foundItem ~= nil then
		exports["ls-inventoryhud"]:RemoveItem(self.source, name, count)
	else
		exports["ls-inventoryhud"]:RemoveItem(self.source, self.getInventoryItem(name)._id, count)
	end
end
```

- After doing this find "getInventoryItem" and replace with that
```
function self.getInventoryItem(name, metadata)
	for k,v in ipairs( exports["ls-inventoryhud"]:GetItems(self.source) ) do
		if v._tpl == name then
			return v
		end
	end
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

- Find "OpenMenu" and replace with that
```
function OpenMenu(submitCb, cancelCb, restrict)
    local playerPed = PlayerPedId()

    TriggerEvent('skinchanger:getSkin', function(skin) lastSkin = skin end)
    TriggerEvent('skinchanger:getData', function(components, maxVals)
        local elements = {}
        local _components = {}

        -- Restrict menu
        if restrict == nil then
            for i=1, #components, 1 do
                _components[i] = components[i]
            end
        else
            for i=1, #components, 1 do
                local found = false

                for j=1, #restrict, 1 do
                    if components[i].name == restrict[j] then
                        found = true
                    end
                end

                if found then
                    table.insert(_components, components[i])
                end
            end
        end
        -- Insert elements
        for i=1, #_components, 1 do
            local value = _components[i].value
            local componentId = _components[i].componentId

            if componentId == 0 then
                value = GetPedPropIndex(playerPed, _components[i].componentId)
            end

            local data = {
                label = _components[i].label,
                name = _components[i].name,
                value = value,
                min = _components[i].min,
                textureof = _components[i].textureof,
                zoomOffset= _components[i].zoomOffset,
                camOffset = _components[i].camOffset,
                type = 'slider'
            }

            for k,v in pairs(maxVals) do
                if k == _components[i].name then
                    data.max = v
                    break
                end
            end

            table.insert(elements, data)
        end

        CreateSkinCam()
        zoomOffset = _components[1].zoomOffset
        camOffset = _components[1].camOffset

        ESX.UI.Menu.Open('default', GetCurrentResourceName(), 'skin', {
            title = _U('skin_menu'),
            align = 'bottom-left',
            elements = elements
        }, function(data, menu)
			TriggerEvent('skinchanger:getSkin', function(skin) 
				TriggerEvent("ls-inventoryhud:c:giveClothesAsItem", skin, lastSkin, false) 
			end)
            TriggerEvent('skinchanger:getSkin', function(skin) lastSkin = skin end)

            submitCb(data, menu)
            DeleteSkinCam()
        end, function(data, menu)
            menu.close()
            DeleteSkinCam()
            TriggerEvent('skinchanger:loadSkin', lastSkin)

            if cancelCb ~= nil then
                cancelCb(data, menu)
            end
        end, function(data, menu)
            local skin, components, maxVals

            TriggerEvent('skinchanger:getSkin', function(getSkin) skin = getSkin end)

            zoomOffset = data.current.zoomOffset
            camOffset = data.current.camOffset

            if skin[data.current.name] ~= data.current.value then
                -- Change skin element
                TriggerEvent('skinchanger:change', data.current.name, data.current.value)

                -- Update max values
                TriggerEvent('skinchanger:getData', function(comp, max)
                    components, maxVals = comp, max
                end)

                local newData = {}

                for i=1, #elements, 1 do
                    newData = {}
                    newData.max = maxVals[elements[i].name]

                    if elements[i].textureof ~= nil and data.current.name == elements[i].textureof then
                        newData.value = 0
                    end

                    menu.update({name = elements[i].name}, newData)
                end

                menu.refresh()
            end
        end, function(data, menu)
            DeleteSkinCam()
        end)
    end)
end
```

# Ayo, clothing not works fine in esx!
I know if you want to works fully
- Locate skinchanger > client > main.lua
- Find "arms" and replace with that
`{label = _U('arms'),                  name = 'arms_1',          value = 0,  min = 0,  zoomOffset = 0.75,  camOffset = 0.15},`

- Replace all "arms" with "arms_1"
