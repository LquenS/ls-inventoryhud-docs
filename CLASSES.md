Inventory have a classes and works like half framework.

If you have any bugs about item delete, item adding, item checking, inventory getting this doc for that.

# Adding Item

Item adding for inventory so easy like,
```
exports["ls-inventoryhud"]:AddItem(source ItemID, ItemAmount, ItemData)
```
Okey we need to know variable names
### ItemID
Item id equals with name when you try to give any item you need to enter a item id all id located in config_items.lua
### ItemAmount
ItemAmount like variable name, its define item amount
### ItemData
ItemData is mean item.info

# Remove Item

Item removing for inventory so easy like,
```
exports["ls-inventoryhud"]:RemoveItem(source ItemID, ItemAmount)
```
Okey we need to know variable names
### ItemID
ItemID is item identifier and this value is unique cannot be changed
### ItemAmount
ItemAmount like variable name, its define item amount

# Get Item

Item getting for inventory so easy like,
```
exports["ls-inventoryhud"]:GetItem(source ItemID)
```
Okey we need to know variable names
### ItemID
ItemID is item identifier and this value is unique cannot be changed

# Get All Items

All item getting for inventory so easy like,
```
exports["ls-inventoryhud"]:GetItems(source)
```

And done! This docs will be updated in future!
