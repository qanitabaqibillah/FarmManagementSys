# My Farm Management System

This README file is for a significant school project that I have worked on. While the project's full codebase isn't included here due to specific requirements, this README serves as an essential guide to understanding the project's objectives, methodology, and outcomes.

## Description:
  - This program is a Crop Farm Management System designed to assist farmers in managing their crops and tracking important information such as crop types, instances, planting days, and profits. It includes functionalities to add crop types, add instances of crops, display crop details, harvest crops, and calculate the total count and expected profits for the crops.

  - The system is implemented using C++ programming language and utilizes classes to represent crop types and instances. The main components of this program include the Farm, CropType, and CropInstance classes. The Farm class acts as the central management system, while CropType represents a specific crop type with its name, harvest duration, and profit per crop. The CropInstance class represents an instance of a crop, including the crop type it is an instance of, the day it was planted, and count of how many instances it includes.

## Requirements:
Develop a simple Farm Management System in C++. This system should:
- Add new crops to the farm.
- Register instances of each crop type.
- Get the total count of each crop type.
- Display details of the crops.
  - How long it has been planted
  - How many days until harvest
  - Expected profit
- Keep track of the day in the farm, and increment the days.
- When the crop has been made, automatically harvest the crop after the duration for harvest.
- Put the crop profit sum into the farm budget.

## Challenges Faced:
  - During the development of this program, the following challenges were encountered:
    - Proper memory management: Ensuring proper memory allocation and deallocation was crucial to prevent memory leaks and undefined behavior. The program uses dynamic memory allocation and deallocation for crop instances, requiring careful management to avoid memory issues.

    - Data management: Maintaining accurate and updating information about crop counts and total counts were a big challenge. It was necessary to ensure that the counts were correctly updated when crops were added or harvested.
    - Persistent Bugs: Unable to resolve several bugs listed below after through and time consuming debugging sessions.

    - Error handling: Some error handling was implemented to handle cases such as adding invalid crop types or accessing non-existent crops. Error messages were displayed to provide feedback to the user.

## How to Run the Program
  To run the Crop Farm Management System, follow these steps:

  1) Ensure you have a C++ compiler installed on your system.

  2) Download the makefile source code files (CropType.h, CropType.cpp, Farm.h, Farm.cpp, main.cpp) and place them in the same directory.

  3) Compile the program using the makefile:
    ```make```

  4) Run the compiled executable:
    ```./farm```

  5) The program will execute various tests to verify its functionality. The test results will be displayed in the console, indicating whether each test passed or failed.


## Known Bugs/ Potential Issues/ Potential Fixes
  - Currently, the program does not handle the scenario of adding additional instances to the same crop type well and will often produce an incorrect count of instances within a crop
    - Potential Fix: Currently brainstorming
  - The displayCropDetails() function within the Farm class does not output as expected.
    - Potential Fix: Unavailible - may be due to processing speed of computer
  - Failing test: The edge case for Farm::harvestCrops() within the Tester::testHarvestCrops() unit test is failing due to the totalCount of instances being incorrect.
    - Originally, const int Farm::getTotalCount(const string &name) was not made to return a const, however, it was changed to return a const dues to concern that it may have been unexpectedly manipulated at some point in the program.
    - Another related fix added was initializing the totalCount variable to 0 in the CropType class. Due to it being uninitialized in the begininng, it was causing issues with unpredictable numbers. 
  - Although the program was intended to run as such, this may be considered a bug. Once a crop is harvested, all of its instances are removed, but the crop type will remain in the cropTypes vector for future use.

## Possible Future Improvements
  - Error handling: Strengthen error handling mechanisms and input validation to handle various edge cases and ensure the program can gracefully handle unexpected inputs.
  - Better Formatting: Clean up output to console for better readability for user.
  - Better coding practices: Create a seperate test file for unit testing instead of including them in main. Will require adjusting the makefile as well.
  - Bug Fixes: Find and release fixes for known bugs listed above.
 
## High-Level Overview of the Code and its Functionality:
- The Farm class represents a farm that grows different crop types. It has member variables for the current day (m_day) and the budget (m_budget).
  - The Farm class constructor initializes the Farm object with day 0 and budget 0.0.
  - The Farm class destructor deletes all the CropType objects stored in the cropTypes vector to prevent memory leaks.
  - The addCropType() function adds a new crop type to the farm. It checks if the crop type already exists and returns false if it does. If the crop type doesn't exist, it creates a new CropType object and adds it to the cropTypes vector. Every three insertion into cropTypes, it calls the incrementDay() function to increment the day.
  - The addInstance() function adds a new instance of a crop to the farm. It searches for the crop type with the specified name in the cropTypes vector. If found, it creates a new CropInstance object, links it to the crop type, sets the planting day to the current day, and updates the total count of the crop type.
  - The incrementDay() function increments the current day by 1 and calls the harvestCrops() function to harvest mature crops.
  - The getTotalCount() function returns the total count of a specific crop type in the farm. It searches for the crop type with the specified name in the cropTypes vector and returns the total count if found.
  - The harvestCrops() function iterates through the cropTypes vector and harvests crops that have reached their harvest duration. It updates the budget, deletes mature crop instances, and updates the total count for each crop type.
  - The displayCropDetails() function displays the details of the crops in the farm. It loops through each crop type in the cropTypes vector and prints the crop type name, instance count, days planted, and expected profit for each crop instance.
  - The getCrop() function retrieves a crop type from the farm based on the specified index. It checks if the index is within the valid range of the cropTypes vector and returns the crop type at the specified index.
  
- The CropType class represents a type of crop that can be grown on a farm. It has the following private members:
  - name: A string that holds the name of the crop type.
  - instances: A vector of pointers to CropInstance objects, representing the instances of this crop type.
  - totalCount: An integer that represents the total count of instances of this crop type.
  - harvestDuration: An integer that represents the number of days it takes to harvest this crop type.
  - profitPerCrop: A double that represents the profit per crop unit for this crop type.
  - The CropType class also has a constructor that takes the name, harvest duration, and profit per crop as parameters and initializes them
 
- The CropInstance class represents an instance of a crop planted on a farm. It has the following private members:
  - type: A reference to a CropType object that represents the crop type of this instance.
  - plantingDay: An integer that represents the day when this crop instance was planted.
  - count: An integer that represents the count of crops planted for this instance.
  - The CropInstance class has a constructor that takes a reference to a CropType object and the count of crops planted as parameters. It also has the Farm class declared as a friend, allowing the Farm class to access its private members.

- The Tester class performs the following tasks:
  - It is responsible for testing the functionality of the Farm class.
  - The Tester class defines test functions to test individual features of the Farm class.
  - Each test function within the Tester class focuses on testing a specific aspect of the Farm class, such as adding crop types, adding instances, incrementing days, harvesting crops, and displaying crop details.
  - The mainTestFunc() function within the Tester class is the main testing function that executes all the test functions.
    - The mainTestFunc() displays the evaluation results of different tests, including the test name, description, output, and pass/fail status.
    - The mainTestFunc() also calculates and displays the total number of passed and failed tests, as well as the pass/fail rate of the program.
    - The mainTestFunc() counts the number of passed and failed tests and provides an overall evaluation of the program's testing results.
  - The test functions include error cases, normal cases, and edge cases to cover different scenarios and ensure the correct behavior of the Farm class.
  - If a test function encounters any issue or fails the checks, it returns false, indicating that the test has failed.
  - After demonstrating the functionality of the farm management system, the main() function instantiates the Tester class and calls mainTestFunc() to execute the unit tests.

Additionally, the code includes the necessary header files vector and string and uses the std namespace for ease of coding.

