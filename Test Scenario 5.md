## Test Scenario 5: Validate No Pays Tile Summary Metrics Match Database Values
## Objective
-To verify that the No Pays Tile summary metrics displayed in the application accurately 
     match the values calculated directly from the database for the selected date range.
# Test Steps
	1. Click "Everything" Mega Menu
	2. Verify if the Optimus Tool link is visible
	3. Verify if the Optimus Tool link is enabled
	4. Click on  "Optimus Tool" link.
	5. Verify if the link redirects to the OPTIMUS - Commission Reconciliation dashboard in a new tab.
	6. Verify if "OPTIMUS - Commission Reconciliation" dashboard is visible.
	7. Verify if the ' Dashboard' tab is visible
	8. Verify the label 'Revenue Assurance Recovery Summary' is visible
	9. Verify the label 'Discrepancies To Research' is visible
	10. Verify if the 'No Pays' tile is visible
	11. Verify if the 'No Pays' amount is visible
	12. Verify if the 'No Pays Quantity' value is visible
	13. Verify if the 'Total Box Quantity' value is visible
	14. Verify if the 'Total Box Amount' value is visible
	15. Verify if the 'Unreviewed Quantity' value is visible
	16. Verify if the 'Unreviewed Amount' value is visible
	17. Verify if the 'Reviewed Quantity' value is visible
	18. Verify if the 'Reviewed Amount' value is visible
	19. Verify the $ prefix for 'Reviewed Amount'
  20. Open Microsoft SQL server
  21. Input a Server name
  22. On Authentication drop-down menu select 'Microsoft Entra MFA'
  23. Click 'Connect'
  24. Click 'New Query' button
  25. Paste the SQL Query on 
  26. Click 'Execute' button

## Expected Result
- All No Pays Tile metrics displayed in the application should exactly match the results returned by the database queries for the same date range and filters.

