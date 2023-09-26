# Power_Query_Financial_Import
## Project Goal
This project aims to show a business use case of Power Automate. By leveraging Power Automate, you can streamline the process of consolidating and transforming your employees' monthly account and balance files into a single Excel file. This consolidated file can be linked to a pivot table, providing an up-to-date data view.  

## Folder Structure
1. The PQ_Financial_Import Project Folder is the main folder for the project.
2. The PQ_Import_Folder is where the raw data is stored (PQ=Power Query).
3. The Power_Automate_Financial_Information Excel file is where you will utilize Power Automate to import the raw data.
4. The Random_Account_Generator is the Excel file that, when refreshed, can create multiple files for testing.


## Random_Account_Generator
### Summary
The Random_Account_Generator allows users to create unlimited accounts to test the Power Automate process. Follow the below steps:
1. Open the Excel File
2. Press the F9 Key
   - This will recalculate all the calculations in the workbook
4. Click Save As and give the file a new name



_In the professional world, place your raw data in the PQ_Import_Folder instead of the sample data._

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

## Power_Automate_Financial_Information
### Power Query
1. Open the Excel file.
2. Select Data from the headers.
3. Select the Get Data dropdown.
4. Hover over From File
5. Select From Folder.
6. Select the PQ_Import_Folder created previously.
7. Select Combine & Transform under the Combine button.
8. Remove the Changed Type on the right of your screen.
9. Right Click Account_Number.
10. Select Split Column by Delimeter.
11. Select Underscore.
12. Select the 123 icon next to Account_Number.2 and change it to Text.
13. Right-click and remove Account_Number.1
14. Right-click the Account_Number.2 column and rename to Account_Number.
15. By mirroring Step 12, correct the rest of the column types to either Date or Currency.
16. Select Add Column from the top headers.
17. Select Add Custom Column
18. Name the Custom Column: TOTAL_PAYED
19. Paste the following into the custom column formula area: =[BALANCE]+[FEES]
20. Select Okay.
21. Change the Type to Currency.
22. Select the Home Tab.
23. Select Close & Load.


The table will be generated in the Excel File and can be refreshed anytime to pull in the new data.
### Pivot Table & Chart
The user can now create Pivot tables based on the table created by Power Query. In the future, when the data is updated/new files are uploaded, the table and the pivot table will refresh.

In this example, a pivot table has a custom column that calculates =CHARGE_OFF_AMT-TOTAL_PAYED. This calculates how much money is owed per year of CHARGE_OFF, allowing the viewer to determine where the most money will be earned and the loan age. Paired with the Pivot Chart, it gives a visual representation of the pivot table.
_This project is designed to teach specifically Power Automate; please refer to other study material for Pivot Tables & Pivot Charts._

# Summary
Power Automate is a business process automation (BPA) tool that can help your organization in several ways. Here are some of the benefits of using Power Automate:

__Improved efficiency and productivity:__ By automating repetitive tasks, Power Automate streamlines your business processes, reduces errors, and accelerates high-level operations1.
__Reduced time and costs:__ Automation helps your business save time and money by eliminating manual paper processes and reallocating resources to more important matters.
__Simple data and document management:__ Power Automate simplifies document management by organizing all your documents and data in a single location.
__Visibility and transparency:__ Automation solutions ensure that best practices are followed, governance is enforced, and provide visibility into your business processes1.
These are just a few of the many benefits that Power Automate offers to businesses. It can enhance operational outcomes, improve overall performance, and enable business transformation.

Please note that this is just a brief summary, and there may be additional advantages specific to your organization’s needs.

_Summary collected from Bing Chat/AI_
