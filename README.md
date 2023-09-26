# PA_Financial_Import
## Project Goal
This project aims to show a business use case of Power Automate. By leveraging Power Automate, you can streamline the process of consolidating and transforming your employees' monthly account and balance files into a single Excel file. This consolidated file can be linked to a pivot table, providing an up-to-date data view.  

## Folder Structure
1. The PA_Financial_Import Project Folder is the main folder for the project.
2. The PA_Import_Folder is where the raw data is stored (PA=Power Automate).
3. The Power_Automate_Financial_Information Excel file is where you will utilize Power Automate to import the raw data.
4. The Random_Account_Generator is the Excel file that, when refreshed, can create multiple files for testing.


## Random_Account_Generator
### Summary
The Random_Account_Generator allows users to create unlimited accounts to test the Power Automate process. Follow the below steps:
1. Open the Excel File
2. Press the F9 Key
   - This will recalculate all the calculations in the workbook
4. Click Save As and give the file a new name



_In the professional world, place your raw data in the PA_Import_Folder instead of the sample data._

### Creation
ACCOUNT_NUMBER: |=CONCATENATE("_",RANDBETWEEN(1000000000,9999999999))|  
   - CONCATENATE combines the presented variables
   - The underscore is used so Excel sees the data as text, not a number. (This can be helpful professionally when storing account numbers; if you add an underscore to the front, excel will not reformat the number.)
   - RANDBETWEEN generates a random number between the two variables. I chose 1000000000 and 9999999999 to restrict the account number to ten characters.
