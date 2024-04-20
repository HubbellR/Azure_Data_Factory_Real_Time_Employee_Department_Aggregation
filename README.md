# Azure_Data_Factory_Real_Time_Employee_Department_Aggregation
The purpose of this project is to take two .json sources of employee.json and department.json, and ultimately convert these sources into a joined .csv file incorporating both employee and deprtment data. Products are stored by saving employee data into employe container, department data into a dapartment container, and the joined information in a separate container. The general process entials first converting the .json files into .csv files, storing these into containers, then joining them, and aggregating what we want as a final product and storing this into its own employee-department container. This is done using Azure Data Factory, using the studio UI. 

Below are the following steps performed to get this done:

1. The first activity we create is the Get Metadata activity. We use this to import the .json files from their raw container, and make them available as child items for the next activity. After creating this, remember to always debug the activity to check for errors.

2.  Next, our objective is to differentiate between different vriables specified within the item catagory of these .json files, and for this we use the ForEach activity. We pass the output of the Get Metadata activity child items into the For Each activity. We use an if confition activity within the ForEach Activity. We use the If condition to check if the inputed item name category is equal to 'employee.json' or not. We do this using the "@contains(item().name, 'employee.json'" expression within the if condition expression. remember to run the debug functionality to make sure it runs without errors.

3.  Now we need to assign different actions depending on result of the previously specified if condition. So we want to save the .json file as a .csv file within the employee container if the condition is true, and the inputed item name catagory is equal to 'employee.json', else we want the item to instead be saved within the 'department' container . So we comply with this by creating a copy activty following the true condition which will move all items with names of 'employee.json' to the employee container as delimited text files (csv files). We do the same for the false statement, saving those items into the department container. Remember to look for errors using the debug functionality. 

4. Our next task is to join the two compiled employee and department .csv files, and the best way of doing this to my knowlage is using a new data flow. So we create a new data flow. In the data flows we set up both .csv files as sources. Don't forget to define all integer and string variable types within the projection tab of the data flow source.

5. Next, within the data flow specified in step 4, we join the two sources together. In this step we simply want to perform an inner join where the employee.csv department_id is equal to the department.csv department_id.
We are also performing a group by the employee ID. 

6. Next we create an aggregation after this joining process. We are summing the salary column for the employee-deprtment information, grouped by the department name. Pretty simple and self explanitory. This is just a simple example of what you could aggregate from these tables, providing the total department salaries. 

7.  Finally we create a sink activity within the data flow to out put the aggregated, joined employee and deprtment lcsv files into the employee-dept container as a .csv file. We also add another sink before the aggregation to save this joined, non aggregated table in a separate container.

8.  Now we are done! We have sucessfully created what could easily be a real time solution to compiling, joining and aggregating data as necessary within an Azure data factory process, which in practice is incredibly useful, and can be used for a large variety of needs through out a projects data process and data life cyle. It is just really useful to be able to do this as a quick solution when dealing with real time data.

The json templates of the two pipelines built are attached.

If you all have any questions, please let me know. Thank you!


