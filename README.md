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
__Formulas Used:__
 - CONCATENATE    = CONCATENATE combines the presented variables.
 - RANDBETWEEN    = RANDBETWEEN generates a random number between the two variables.
 - DATE           = Specifys to Excel the string is date, DATE(YEAR,MONTH,DAY).
 - EDATE          = EDATE generates a date based on the first variable + the second variable.
 - IF             = An if statement is a programming conditional statement that, if proved true, performs a function or displays information

__Columns:__
- ACCOUNT_NUMBER: =CONCATENATE("_",RANDBETWEEN(1000000000,9999999999))
   - The underscore is used so Excel sees the data as text, not a number. (This can be helpful professionally when storing account numbers; if you add an underscore to the front, excel will not reformat the number.)
   - 1000000000 and 9999999999 were specified to restrict the account number to ten characters.
- DOB: =RANDBETWEEN(DATE(1975,1,1),DATE(2001,12,31))
   - This formula generates a date between 01/01/1975 and 12/31/2001.
   - This DOB was chosen so that all the accounts will be at least 21 years old as of 09/25/2023.
- CHARGE_OFF_AMT: =RANDBETWEEN(567,2467)
   - These numbers were randomly selected.
- CHARGE_OFF_DATE: =RANDBETWEEN((EDATE([@DOB],12*21)),DATE(2023,9,24))
  - [@DOB] references the DOB field, ensuring the account was 21 years old.
- BALANCE: =RANDBETWEEN(0,[@[CHARGE_OFF_AMT]])
  - [@[CHARGE_OFF_AMT]] references the CHARGE_OFF_AMT field, ensuring the BALANCE was <= CHARGE_OFF_AMT.
- BALANCE_DATE: =RANDBETWEEN([@[CHARGE_OFF_DATE]],DATE(2023,9,24))
  - [@[CHARGE_OFF_DATE]] references the CHARGE_OFF_DATE field, ensuring the BALANCE_DATE was >= CHARGE_OFF_DATE.
  - 2023,9,24 could be substituted with Today() as well.
- FEES: =IF(([@[BALANCE_DATE]]-[@[CHARGE_OFF_DATE]])>1,RANDBETWEEN(1,50)+RANDBETWEEN(1,99)/100,0)
  - If the CHARGE_OFF_DATE is greater than a year, the BALANCE_DATE generates the fee.

