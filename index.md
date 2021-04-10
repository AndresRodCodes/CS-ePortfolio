[Weather Station with Python and RaspberryPi.zip](https://github.com/Ar64/CS-ePortfolio/files/6268387/Weather.Station.with.Python.and.RaspberryPi.zip)
## Andres Rodriguez Computer Science ePortfolio

This page is to showcase three of my best CS projects created during my undergraduate studies at Southern New Hampshire University.

# Software Design/Engineering
Picture
Description
Code Example
```markdown
This is a place holder for code
```
# Algorithms and Data Structures
Picture
Description
Code Example
```markdown
This is a place holder for code
```
# Databases

<img src="https://github.com/Ar64/CS-ePortfolio/blob/gh-pages/AndroidInventoryApp%20Screenshots/Grid%20with%20items.png" width="200" height="400"/>

This is an Android inventory app that uses SQLite to authenticate users and track inventory. It can do 
all the basic CRUD operations like adding items, editing items, and deleting items. It also gives the option to 
only show items that have low inventory by quiering the SQLite database.

Code Example: Function to get low inventory items from the SQLite database based on item count.

```markdown
// Get low inventory Items from item table
public ArrayList<Item> getLowInventoryItems(){
    // ArrayList to hold low inventory items
    ArrayList<Item> lowInventoryItems = new ArrayList<>();
    SQLiteDatabase dbItems = getReadableDatabase();

    // Select all items in item database table where item count is less than or equal to 5
    String sql = "Select * from " + ItemDatabase.ItemTable.TABLE
            + " where " + ItemTable.COL_ITEM_COUNT + " <= 5"
            + " order by " + ItemTable.COL_ITEM_COUNT + " ASC";
    Cursor cursor = dbItems.rawQuery(sql, new String[] {});

    // Place items from ItemDatabase table into the loInventoryItems ArrayList
    if (cursor.moveToFirst()){
        do {
            long id = cursor.getLong(0);
            String dbItemName = cursor.getString(1);
            int dbCount = cursor.getInt(2);

            // Add items to ArrayList of Type Item
            Item item = new Item();
            item.itemId = id;
            item.itemName = dbItemName;
            item.itemCount = dbCount;

            lowInventoryItems.add(item);
        } while (cursor.moveToNext());
    }
    cursor.close();
    return lowInventoryItems;
}
```
