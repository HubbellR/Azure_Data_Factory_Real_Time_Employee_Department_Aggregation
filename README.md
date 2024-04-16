# Azure_Data_Factory_Real_Time_Employee_Department_Aggregation
The purpose of this project is to take a agorage account with a raw container, with employee and department information. We need to convert these into employee and department .json files, then convert these into .csv files, import the tables, join them, 
store them into the employee-department container, and also store multiple aggregations. This is done using Azure Data Factory.

So first, we need to find the data within the raw container. In darta factory, we first get the metadata using a Get activity, then use a foreach activity to check the metadata using an internal if activity, and it if is a json file, we forward it to the copy ac
activity. If it is a department of csv file, we store it into the department container. After this we, aggregate the data in these two containers to [   ] .

