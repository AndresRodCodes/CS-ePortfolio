
[Weather Station with Python and RaspberryPi.zip](https://github.com/Ar64/CS-ePortfolio/files/6268387/Weather.Station.with.Python.and.RaspberryPi.zip)

[AndroidInventoryApp.zip](https://github.com/Ar64/CS-ePortfolio/files/6332211/AndresRodriguezInventoryApp.zip)

[Professional Self-Assessment.docx](https://github.com/Ar64/CS-ePortfolio/files/6332244/Professional.Self-Assessment.docx)

## Andres Rodriguez Computer Science ePortfolio

This page is to showcase three of my best CS projects created during my undergraduate studies at Southern New Hampshire University.

# Software Design/Engineering

<img src="./WeatherStationScreenshots/Weather%20Station%20RPi.jpg" width="200" height="400"/>

This is a weather station project written in python running on a Raspberry Pi with multiple sensors attached. It reads sensor data, saves it to JSON file, and 
gives the option to sort that data with a seprate tool I created. I refactored the code from a one file program, to multi page program to increase maintainability and modularity.

List of sensors:
1. Temperature and humidity
2. LCD display
3. Light
4. Red, blue, green LEDs

**Code Example**: This is the entry point to the weather station and the code that brings the different components of the project together.
```markdown
# Entry point to the weather station program (Main)
while True:
    try:
        # Check if it is daytime hours and daytime conditions
        isDaytimeHour = WeatherConditions.isDaytimeHours()
        isDaytimeCondition = WeatherConditions.isDaytimeConditions()
        
        isDaytimeHour = True
        isDaytimeCondition = True

        # If it is daytime hours and daytime conditions get and save sensor data
        if((isDaytimeHour == True) and (isDaytimeCondition == True)):
            print("It is daytime hours and daytime conditions")
            print("isDaytimeHours: " + str(isDaytimeHour))
            print("isDaytimeConditions: " + str(isDaytimeCondition))

            # Get temp and humidity data
            [tempC, humidity] = getTempAndHumidity()
            # Convert temp to F
            tempF = convertTempCToF(tempC)
            tempF = round(tempF, 3)
            currentDate = getCurrentDate()
            weatherData = WeatherData(currentDate, tempF, humidity)

            # Turn on LED indicators with temp and humidity
            turnOnLightIndicator(weatherData.tempF, weatherData.humidity)

            # Update LED Screen with temp and humidity
            # Display temperature and humidity on LED Screen
            setRGB(0, 255, 255)
            setText("Temp:" + str(weatherData.tempF) + "F\n" + "Humidity: " + str(weatherData.humidity) + "%")

            # Check for JSON file existence
            JSONFunctionsObject = JSONFunctions(fileName)
            JSONFileExists = JSONFunctionsObject.fileExists()
            print("JSON file exists: " + str(JSONFileExists))

            # Create JSON file if it does not exist
            if (JSONFileExists == False):
                print("Creating JSON file...")
                JSONFunctionsObject.createJSONFile()

            # Open JSON file and append data [date, tempF, humidity]
            print("Appending weather data...")
            JSONFunctionsObject.appendJSONFile(weatherData)
```
# Algorithms and Data Structures

<img src="./WeatherStationScreenshots/Weather%20Station%20RPi.jpg" width="200" height="400"/>

This is a weather station project written in python running on a Raspberry Pi with multiple sensors attached. The data is saved into a JSON file which is then read by a seperate tool I created in python to show the data sorted by temperature and humidity. The time taken for the sorting algorithm to sort and display that data is then displayed with the output of the sortted data.

**Code Example**:
```markdown
# Sort by hottest tempurature
def sortByHottestTempF():
    startTime = time.time()

    weatherJSONData.sort(reverse=True, key=tempFFunction)
    totalTime = time.time() - startTime

    weatherJSONDataFormatted = JSONFunctions.formatJSONData(weatherJSONData)
    print(weatherJSONDataFormatted)
    print("Time to sort by hottest tempF: %.10f seconds" % totalTime)

# Sort by coldest tempurature
def sortByColdestTempF():
    startTime = time.time()

    weatherJSONData.sort(key=tempFFunction)
    totalTime = time.time() - startTime

    weatherJSONDataFormatted = JSONFunctions.formatJSONData(weatherJSONData)
    print(weatherJSONDataFormatted)
    print("Time to sort by coldest tempF: %.10f seconds" % totalTime)
```
# Databases

<img src="./AndroidInventoryApp%20Screenshots/Grid%20with%20items.png" width="200" height="400"/>

This is an Android inventory app that uses SQLite to authenticate users and track inventory. It can do 
all the basic CRUD operations like adding items, editing items, and deleting items. It also gives the option to 
only show items that have low inventory by quiering the SQLite database.

**Code Example**: Function to get low inventory items from the SQLite database based on item count.

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
