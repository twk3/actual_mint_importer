# ACTUAL_MINT_IMPORTER

This importer will import CSV exports from Mint.com into Actual Budget.

Mint doesn't export any budget data so you will need to setup the budgets yourself.

# Run

To run the script I had the following setup:

1. Setup Actual how you like. You need an instance of actual-server running for the importer to access.
2. Create a new budget file and leave it empty.  Don't encrypt the file yet, the script isn't setup to open those.
2. Clone this repo, and cd into it
3. Store csv file in this directory that you exported from Mint.com
4. run `npm install`.  (I tested with node18)
5. Edit all the variables at the top of the file to match your setup.  You will need to use the sync_id from your budget file.  That can be found in settings->Advanced Settings->IDs
6. run `node mint.js`

The importer does the following:
* All categories listed in the CSV export will be created under a category group "Mint Import"

# Budget Options

## Report Budget

One option is to use the Report Budget in Actual.  That is a more traditional budget style and more in line with Mint. The data will look much more clean in the budget, but I recommend the other budget style as I find it more useful.  To use the Report Budget you need to enable it under Settings->Advanced Settings->Experimental Features->Budget Mode Toggle

## Rollover Budget (recommended)

If you elect to use the default Rollover Budget (my recommended one) your imported data will cause really messy balances for prior months.  As I see it your options to use this style are to (sorted by expected difficulty)

1. Use a report budget to store the old data and start fresh in a new file moving forward. I would do this because most people seldom look at their old data, and I find zero-based budgeting much more useful.  You can always open the file of the old data and run reports on that if you want.
2. [Do your best to start from the current month and ignore old ones](#ignoring-budgets-for-previous-months).  It may take some transaction trickery to do this.
3. Do what it takes to clean up the old months.  May be hard if you have have years of data

### Ignoring budgets for previous months

This method of using the rollover budget allows you to keep all your mint previous months mint transactions in your accounts, while only worrying about budget data from the current month forward.

You can follow these steps once your import is complete.

1. In the Budgets screen, navigate to the very first month that you have transactions for.
2. Set each category to rollover overspending.
   * For each category. Click the "Balance" value field (even if it's 0.00). A dropdown will open.
   * Select "Rollover Overspending"
3. Navigate to most recent *full* month you have mint transactions for.
4. Cover your spending from previous month to reset your budget fresh next month
   * For each category with a negative (red) balance. Click the "Balance" value field. A dropdown will open.
   * Choose "Cover Overspending" from the dropdown and select "To Be Budgeted" to rebalance the category.
   * You can can also choose to "Remove Overspending Rollover" at this pint from the Balance dropdown if you don't want it for this category going forward.
5. Navigate to the current month, and now you can set up your new budget accurately going forward.
