Hello, this docs its teaching basics of inventory!

# I want to create custom inventory!

- Okey then find the "config_items"
```
  ["inventory_item_name"] = {    -- Our custom inventory
        ["item"] = {
            _id = "inventory_item_name",
            _name = "NotImportant",
            _parent = "",
            _type = "Node",
            _data = {
                Name = "Inventory Name",
                Label = "Inventory Label",
                Description = "",
                Width = 1,
                Height = 1,
                Weight = 1.5,
                ExamineTime = 3.0,
                Backgroundcolor = "black",
                ItemSound = "gear_generic",
                Type = "container",
                MaxStack = 1,
                Grids = {
                    [0] = {
                        _name ="1",
                        _id ="Not_Important",
                        _parent ="inventory_item_name",
                        cellsH = 9, -- Our cells width
                        cellsV = 3, -- Our grids width
                    },
                },
                Itemimage = "",
            }
        }
    },
```
- Add this thing and customize with yourself!
```
exports["ls-inventoryhud"]:OpenCustomInventory(ourinventoryid, inventory_item_name, isTemporary)
```
## What is mean this variables?
- ourinventoryid
Is means Inventory name in database like "motel-george"
- inventory_item_name
It's a created item in config_items
- isTemporary
If is true never will be saved

# I want to make more and more items !

- Okey then find the "config_items"
- And make your custom item like that
```
  ["pasta"] = {    -- Our custom item
        ["item"] = {
            _id = "pasta",
            _name = "Pasta",
            _parent = "",
            _type = "Item",
            _data = {
                Name = "Pasta",
                Label = "Pasta La Wista",
                Description = "Its so delicous!",
                Width = 1,
                Height = 1,
                Weight = 0.5,
                ExamineTime = 1.0,
                Backgroundcolor = "black",
                ItemSound = "gear_generic",
                Type = "Item",
                MaxStack = 1,
                Grids = {},
                Itemimage = "icons/pasta.png",
            }
        }
    },
```


# I have items in my core and i want to convert! (QB-ESX)

- Find resources/server/items-convert.lua
- Find "convertitems" and convert with your items (Edited for QB)
- Start server
- Write "/convertitems" to console!
Done our items is succesfully converted but you need to transfer these items its located in config_converted.lua transfer to config_items.lua!


# I dont know keybindings i need to know keybindings!?
Okey, keybindings so easy

- Dragging items ( Hold left click to item )
- Research items ( Middle mouse button to unsearched item )
- Research containers ( Middle mouse button to UNSEARCHED text or left click to Search )
- Hotbar/Fastuse ( Click 3-9 keys in keyboard 1-2 for first and second weapon never be manually changed! )
- Context Menu/Attachment Menu ( Right click to item )

# I have custom images per item!
Okey, this so easy too!
- Locate html > classes.js
- Find "GetItemImage" and customize with your own
