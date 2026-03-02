## Test Scenario 3: Validate that the uploaded file is correctly stored in the database
## Objective
Validate that the uploaded file is correctly stored in the database
## Test Steps
1. "Log in to OPTIMUS Commission Reconcilation https://vcr-qa.victra.com/"
2. Verify If Optimus Commission Reconciliation dashboards are visible
3. Verify 'Reporting' tab is visible
4. Click the 'Reporting' tab
5. Verify if the user navigate to 'Reporting' tab
6. Verify if the 'Upload' button is visible
7. Click 'Upload' button
8. Drag or drop the 'SendToVzDiscrepancies1' csv file
9. Click 'Submit' button
10 Verify the status of the upload
11. Click again 'Upload" button
12. Drag or drop the 'SentToVzDiscrepancies2' csv file
13. Click 'Submit' button
14 Verify the status of the upload
15. Open Microsoft SQL server
16. Input a Server name
17. On Authentication drop-down menu select 'Microsoft Entra MFA'
18. Click 'Connect'
19. Expand 'Databases' folder
20. Expand 'vcr' database
21. Verify if 'Optimus.Uploaded Files' is visible
22. Right click the table
23. Click "Select Top 1000 Rows"

## Expected Result
- The Uploaded file should in reflect in "Optimus.Uploaded Files" Table
