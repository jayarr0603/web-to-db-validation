# Test Scenario 2: Verify that the "Not in RQ" report shows consistent data between the UI and the database, including row counts and record details.
## Objective 
Validate if Not In RQ records count matches with database's count
## Preconditions
- Web application is accessible
- User has permission to create data
- Database access available
## Test Steps
	1. "Login to Vision Application via ADFS https://vision-qa-web.azurewebsites.net/Default.aspx"
	2. Impersonate a user with an vcr user role
	3. Click "Everything" Mega Menu
	4. Verify if the Optimus Tool link is visible
	5. Verify if the Optimus Tool link is enabled
	6. Click on  "Optimus Tool" link.
	7. Verify if the link redirects to the OPTIMUS - Commission Reconciliation dashboard in a new tab.
	8. Verify if "OPTIMUS - Commission Reconciliation" dashboard is visible.
	9. Verify default active tab
	10. Click the 'Research Now' button on the No Pays tile.
	11. Verify the 'Report' button is visible
	12. Click the 'Report' button
	13. Click 'Report Type' drop-down menu
	14. Select 'Not in RQ' report type
	15. Click textbox on Date
	16. Select Range on Date Picker
	17. Click 'Download' button
	18. "Open the downloaded excel file on downloads folder on local machine Eg:Not in RQ_Report_12-01-2025_12-10-2025.csv"
	19. Verify details recorded in the database: Server Name: common-qa-dbserver.database.windows.net"
	20. Verify the "Not in RQ" Report row count in Excel matches the row count in the database
  
## Expected Result
- Not in RQ' report row count in Excel should match the row count in the database

