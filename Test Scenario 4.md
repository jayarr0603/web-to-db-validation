## Test Scenario 4: Verify that changing the disposition to "File" is correctly reflected in the dbo.FiledDiscrepancyDetails table in the vcr database.
## Objective
Verify that changing the disposition to "File" is correctly reflected in the dbo.FiledDiscrepancyDetails table in the vcr database.. 
## Test Steps
1. "Log in to OPTIMUS Commission Reconcilation https://vcr-qa.victra.com/"
2. Verify If Optimus Commission Reconciliation dashboards are visible
3. Click the 'Research Now' button on the No Pays tile.
4. Select any Line Items on the table
5. Verify if the 'Audit Details' section is visible
6. Click the 'Add a Note' button
7. Verify whether a validation message is displayed for  'Disposition'
8. Verify whether a validation message is displayed for  'Exception'
9. Verify the 'Disposition' place holder
11. Click the 'Disposition' drop-down menu
12. Verify the 'Disposition' drop-down menu
13. Select the 'File' on the Disposition drop-down menu
14. Verify the 'Exception' place holder
15. Click the 'Exception' drop-down menu
16. Verify the 'Exception' drop-down menu
16. Open Microsoft SQL server
17. Input a Server name
18. On Authentication drop-down menu select 'Microsoft Entra MFA'
19. Click 'Connect'
20. Expand 'Databases' folder
21. Expand 'vcr' database
22. Verify if 'dbo.FiledDiscrepancyDetails' is visible
23. Right click the table
24. Click "Select Top 1000 Rows"

## Expected Result
- The Uploaded file should in reflect in 'dbo.FiledDiscrepancyDetails' Table

## SQL Query
SELECT TOP (1000) [FiledDiscrepancyId]
      ,[NoteId]
      ,[CustomerName]
      ,[Esn]
      ,[Mtn]
      ,[DeviceDescription]
      ,[POSCode]
      ,[PricePlan]
      ,[CommissionedAmt]
      ,[FinancedAmt]
      ,[ContractTerm]
      ,[CustomerTypeCode]
      ,[CustomerAccountNumber]
      ,[DPANumber]
      ,[COEDescription]
      ,[AlternateMobileId]
      ,[OutletId]
      ,[SoldOnDate]
      ,[DateCreated]
  FROM [dbo].[FiledDiscrepancyDetails]
  order by 1 desc
