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

## SQL
/*
================================================================================
No Pays Tile
================================================================================
Purpose:
This set of queries supports the No Pays dashboard tile. It provides:

1. Total number of boxes (sales invoices) processed within a date range.
2. Total dollar amount of those boxes (Financed + Commission).
3. Summary metrics for No Pay / Short Pay discrepancies:
   - Total discrepancy count and variance amount
   - Unreviewed discrepancy count and amount
   - Reviewed discrepancy count and amount

Discrepancy Types Included:
- 'NOPAY'
- 'SHORTPAY'
================================================================================
*/


-- ============================================================
-- Total Boxes
-- ============================================================
-- Returns the total number of sales invoices (boxes)
-- processed within the specified date range.
SELECT COUNT(*) AS TotalBoxes
FROM RqSalesInvoiceData
WHERE DateSoldProcessed >= '01/01/2026'
  AND DateSoldProcessed <= '01/31/2026';


-- ============================================================
-- Total Boxes Amount
-- ============================================================
-- Returns the total dollar amount of all boxes processed
-- in the date range.
-- Amount is calculated as:
-- FinancedAmount + CommissionAmount (nulls treated as 0).
SELECT 
    SUM(COALESCE(FinancedAmount, 0) 
      + COALESCE(CommissionAmount, 0)) AS TotalBoxesAmount
FROM RqSalesInvoiceData
WHERE DateSoldProcessed >= '01/01/2026'
  AND DateSoldProcessed <= '01/31/2026';


-- ============================================================
-- No Pay / Short Pay Discrepancy Metrics
-- ============================================================
-- Returns summary metrics for discrepancies within
-- the specified date range and limited to:
--   DiscrepancyType IN ('NOPAY', 'SHORTPAY')
--
-- Metrics include:
--   • Total discrepancies and total variance
--   • Unreviewed discrepancies (Disposition = 'UNREV')
--   • Reviewed discrepancies (Disposition != 'UNREV')

DECLARE @StartDate AS DATETIME = '2026-01-01'
DECLARE @EndDate AS DATETIME = '2026-01-31'

SELECT 
   -- ======================
   -- Total Discrepancies
   -- ======================
   COUNT(1) AS TotalCount,  -- Total number of NoPay/ShortPay records
   SUM(ISNULL([ACTUAL VARIANCE], 0)) AS TotalAmount,  -- Total variance amount

   -- ======================
   -- Unreviewed Discrepancies
   -- ======================
   -- Records still marked as 'UNREV'
   COUNT(CASE WHEN Disposition = 'UNREV' THEN 1 END) AS UnreviewedCount,
   SUM(CASE 
         WHEN Disposition = 'UNREV' 
         THEN ISNULL([ACTUAL VARIANCE], 0) 
         ELSE 0 
       END) AS UnreviewedAmount,

   -- ======================
   -- Reviewed Discrepancies
   -- ======================
   -- Records that have been reviewed (not 'UNREV')
   COUNT(CASE WHEN Disposition != 'UNREV' THEN 1 END) AS ReviewedCount,
   SUM(CASE 
         WHEN Disposition != 'UNREV' 
         THEN ISNULL([ACTUAL VARIANCE], 0) 
         ELSE 0 
       END) AS ReviewedAmount

FROM vw_LineItemDiscrepancy

-- Filter by processing date and discrepancy type
WHERE RqDateSoldProcessed >= @StartDate
  AND RqDateSoldProcessed <= @EndDate
  AND DiscrepancyType IN ('NOPAY', 'SHORTPAY');
