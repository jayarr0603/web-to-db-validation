# Test Scenario: Optimus Web to DB Validation
    ## Objective
Verify Submission Count increments for different filename uploads in VCR Database

## Preconditions
- Web application is accessible
- User has permission to create data
- Database access available

## Test Steps
1. "Log in to OPTIMUS Commission Reconcilation
https://vcr-qa.victra.com/"
2. Verify If Optimus Commission Reconciliation dashboards are visible
3. Verify 'Reporting' tab is visible
4. Click the 'Reporting' tab
5. Verify if the user navigate to 'Reporting' tab
6. Verify if the 'Upload' button is visible
7. Click 'Upload' button
8. Drag or drop the 'SendToVzDiscrepancies1' csv file
9. Click 'Submit' button
10. Verify the status of the upload
11. Click again 'Upload" button
12. Drag or drop the 'SentToVzDiscrepancies2' csv file
13. Click 'Submit' button
14. Verify the status of the upload
15. Open Microsoft SQL server
16. Input a Server name
17. On Authentication drop-down menu select 'Microsoft Entra MFA'
18. Click 'Connect'
19. Expand 'Databases' folder
20. Expand 'vcr' database
21. Verify if the '[optimus].[SentToVzDiscrepancies]' table is visible
22. Right click the '[optimus].[SentToVzDiscrepancies]' table
23. Select top 1000 rows
24.Verify the 'Discepancyid' column if visible
25. Verify if the 'Submission Count' column increments

## Expected Result
- Record exists in database
- Submission count should increase

# SQL Query

