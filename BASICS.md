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
exports["ls-inventoryhud"]:CustomInventory(ourinventoryid, inventory_item_name, isTemporary)
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
## What is mean all variables?
- \_id
Is mean item name for given (/giveitem 1 pasta) its needs to same with key \["pasta"\]
- \_parent
Not important make empty
- \_type
If not inventory or like that just make Item
- Grids
Only for stashes or like that

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
- Item Split ( Start dragging a item and hold shift, finally drop the grid, Split thing will be appear on screen. )

# I have custom images per item!
Okey, this so easy too!
- Locate html > classes.js
- Find "GetItemImage" and customize with your own

# I made custom clothing but its buggy!?
- Make sure you created item
- Find html/clothing.css
```
.container-grid-youritemname {
    position: absolute;
    width: 250px;
    height: 325px;

    right: 10px;
    top: 390px;
}

.grid-parent-youritemname-yourgridname {
    position: absolute;
    left: 0px;
    top: 57px;
}
```
## If you didn't understand here a little example

- Find config_items.lua,
- After that we need to create a clothing!
```
    ["myawesomebag"] = {
        ["item"] = {
            _id = "myawesomebag",
            _name = "sport_backpack",
            _parent = "c6jgbwjs9tc2vb8gtpwe7rywe",
            _type = "Item",
            _data = {
                Name = "Backpack",
                AttachableSlot = "backpack",
                Label = "Its my bag so awesome",
                Description = "",
                Width = 4,
                Height = 3,
                Weight = 1.5,
                ExamineTime = 3.0,
                Backgroundcolor = "black",
                ItemSound = "gear_backpack",
                Type = "container",
                MaxStack = 1,
                Grids = {
                    [0] = {
                        _name ="mybestgrid",
                        _id ="isntimportant",
                        _parent ="myawesomebag",
                        cellsH = 8,
                        cellsV = 4,
                    },
                },
                Itemimage = "icons/bag.png",
            }
        }
    },
```
- Okey we created item we need to implement to our UI!
- Find html/clothing.css
```
.container-grid-myawesomebag {
    position: absolute;
    width: 250px;
    height: 325px;

    right: 10px;
    top: 390px;
}

.grid-parent-myawesomebag-mybestgrid {
    position: absolute;
    left: 0px;
    top: 0px;
}
```
- And done we made custom clothing! If you want use this clothing some clothes here,
- Find resources/client/NUI.lua
- Search "if givinItem == "backpack" then"
- Edit freely!

### If you didn't understand here a little example
- We already created a bag if not make one,
- I want to customize bag 85!
```
                if givinItem == "backpack" then
                    if (itemData == 40 or itemData == 41 or itemData == 44 or itemData == 45 or itemData == 81 or itemData == 82 or itemData == 86) then
                        givinItem = "bag1"
                    elseif (itemData == 85)
                        givinItem = "myawesomebag"
                    end
```
- And done! 
- If you using QB 
```
                if givinItem == "backpack" then
                    if (itemData.item == 40 or itemData.item == 41 or itemData.item == 44 or itemData.item == 45 or itemData.item == 81 or itemData.item == 82 or itemData.item == 86) then
                        givinItem = "bag1"
                    elseif (itemData == 85)
                        givinItem = "myawesomebag"
                    end
```
- Done for QB too!

# I WANT TO SHOP

```
    local ShopItems = {
        ["kurkakola"] = {
            amount = 50,
            price = 12500,
        },
        ["sandwich"] = {
            amount = 5000,
            price = 50,
        }
    }
    exports["ls-inventoryhud"]:ShopInventory("SHOP-XXXXX", "shop1", temporary, ShopItems)
```
## What this mean this variables!
### SHOP-XXXXXX 
- Doesnt important thing you can rename noting will be change 
- ( ! IMPORTANT ! DO NOT DELETE SHOP- )
### Shop1
- Is Inventory name in config_items.lua you can customize inventory from location.
- Its not important and big thing!
### Temporary 
- Is equals temporary, make "true"!
### ShopItems 
- ShopItems is shop items you can edit freely. 
- You can add or you can remove items, items created with info 
- (DO NOT MORE INFO ITEMS AMOUNT MORE THAN 1 LIKE WEAPONS)
