# Daily Personal Finance Tracker

Welcome to the Daily Personal Finance Tracker project! This tool is designed to help you effortlessly record and track your expenses, income, investments, and more. This repository contains the code for a comprehensive personal finance tracking system that seamlessly integrates Google Forms with Google Sheets & Google Apps Script.

## Overview of Unique Features

- **Daily Email Summary Reports**: Receive a daily email summarizing your financial activities, including visualizations of categorized expenses, income summaries, investment aggregates, and more.
- **Shared Expense Tracking**: Record shared expenses in a transaction and automatically derive your share as the actual expense.
- **Non-Expense Credit Card & BNPL Bills**: Easily track Credit Card and Buy Now Pay Later (BNPL) bill payments as non-expenses.
- **Flexible Income Handling**: Record cashbacks, refunds, and shared expense settlements as non-income, providing a more accurate financial snapshot.
- **Adjustable Variable Expenses**: Calculate actual adjustable variable expenses, excluding fixed and unavoidable costs such as rent, utilities, and more.

## Project Components

### [Google Sheet](https://docs.google.com/spreadsheets/d/1TSlU4nUgUqOpIddVJRPErqxDdDFrdUw3TyUvrhYP818/edit?usp=sharing)

- The backend of this project, the Google Sheet, automatically receives responses from the Google Form and contains essential column derivations, aggregations, and visualizations.
- Customize the sheet according to your preferences using the editable_cells sheet.
- Visualizations and aggregate tables in the category_wise_aggregates sheet serve as a source for the scheduled email App Script.

### [Google Form](https://docs.google.com/forms/d/1lFl5eX9yBX_l8sIc0pF3KDcKBPI4QuWZbrhYDlPrAms/edit)

- The Google Form allows you to input data for each cashflow, whether it's an expense, income, investment, or Credit Card/BNPL bill payment.
- Customize expense, income, and investment categories, as well as payment modes to suit your financial situation.
- Note: Changing the sequence or number of questions in the form requires caution, as it may affect data filtering.

### Google Apps Script

- This script facilitates the creation and scheduling of a daily email containing a budget report. The report includes visualizations of categorized expenses, summaries of income, expenses, and investments, aggregates of variable expenses, and more.
- Setting up this daily email provides a convenient way to review your finances and serves as a reminder to track daily expenses.

## Setting Up the Project

1. Ensure you're logged into your Google Drive.
2. **Set up the Google Sheet & Form.**
   1. Make a copy of this [Google Sheet](https://docs.google.com/spreadsheets/d/1TSlU4nUgUqOpIddVJRPErqxDdDFrdUw3TyUvrhYP818/edit?usp=sharing) (the associated Google Apps Script should also be copied).
   2. Click on this [Google Form link](https://docs.google.com/forms/d/1lFl5eX9yBX_l8sIc0pF3KDcKBPI4QuWZbrhYDlPrAms/copy) - it should directly suggest creating a copy once logged in.
   3. Link your form to the spreadsheet: Open your copy of the Form, head to the Responses tab, click on the green Create Spreadsheet button, and choose your copy of the Google spreadsheet in the Drive.
   4. You should see a new sheet auto-created in your copy of the Google Sheet. Rename the Form Responses sheet to something like `cashflow_form_responses` (you can delete the existing `google_form_responses_sheet`).
   5. Set the new sheet's name at the `editable_cells` sheet for key `Google Form Name` - cell `B2`.
   6. Set the daily personal finance summary email's recipient at `editable_cells` sheet for key `Daily Summary Email Recipient` - cell `B3`.
3. **Fill out your form.**
   1. In the Google Form, click on the "Send" button.
   2. Switch to the link tab, copy & paste it into a new browser tab.
   3. Since it's a Google Form, you can comfortably use it in your mobile browser too!
   4. Open your form and fill out your first expense.
   5. You can verify the corresponding data population at `cashflow_form_responses` & other sheets.
4. **Configure the Google Apps Script.**
   1. In the Google Sheet, open the Google Apps Script Editor.
      1. Go to Extensions and click on Apps Script.
      2. In the Apps Script console, you should see the editable code at `Editor` -> `Files` -> `Code.gs`.
   3. To verify the Apps Script integration, you can run it by clicking on the `Run` button (it will autosave the script) to try it out.
      1. The first time you run the script, you will get a pop-up asking to Review Permissions. Click on the blue Review button.
      2. Select your Google Account.
      3. You will get a warning as the script is trying to send an email on your behalf. *This is perfectly safe to execute* & you will need to proceed by allowing it (click `Advanced` and then click on `Go to <the daily mailer's name> (unsafe)`)
      4. Review the permissions & allow them.
      5. You might need to click on `Run` again after granting the required permissions the first time.
   4. Check your email once executed & Et Voila! You should have received a report summarizing the expenses you've added so far.
   5. Note: The script is configured to send a report of expenses added since the last salary date - this salary date formula can be modified to get the required value in the Google Sheet at `editable_cells!B5` (key `Last Salary Day`, default formula is set to extract last Friday of the previous month).
5. **Set the schedule of the Apps Script email.**
   1. Go to `Triggers`.
   2. Add a trigger as per your preference (currently set to a time-based trigger scheduled between 7am-8am daily).
      1. Click on the blue Add Trigger button.
      2. Select the event source as Time-driven.
      3. Select the type of time-based trigger as Day timer.
      4. Select the time of day as "7am to 8am".
      5. You can expect to receive the summary email between 7 am to 8 am as scheduled.
6. **View Personal Finance Summaries & Aggregates**
   1. Add more expenses, incomes & investments using the Google Form.
   2. Note: In case of errors, you can edit the form output in the `cashflow_form_responses` sheet.
   3. Go to your Google Sheet `category_wise_aggregates` & modify the date range params (as instructed in `editable_cells!A11`) & visualize the corresponding financial summaries.
   4. Overall monthly aggregates can be found in the `monthly_aggregates` sheet.
   5. You can also continue to `Run` the script to get an ad-hoc summary over email.
      1. You can customize the date range in the email summary by modifying line `6` in the Apps Script (`sheet.getRange('B2').setValue('Current Salary Month'); // change as required`) to the required dropdown value. If needed, you can set the value to `Custom`, in which case it will pick the custom dates set in the cells `category_wise_aggregates!B3` & `category_wise_aggregates!B4`.
7. **Modify the Google Sheet & Form according to personal preferences**
   1. Feel free to edit the sheet & form according to personal preferences.
      1. Edit the `editable_cells` sheet values as suitable for your financial spend & income categories, your monthly budget, and your salary cycle.
      2. In the Google Form, you can modify expense, income, investment categories, payment modes, etc as needed.
         - NOTE 1: Do remember that changing the sequence / number of questions in the form will affect everything! If doing this, be careful, and always make sure to check that the filters are using the correct column sequences.
         - NOTE 2: Modifying the above also might affect aggregations, especially if you modify the category names specified in the `editable_cells` sheet.
8. Happy tracking!

## Additional Features in Progress

- **Budgeting for Each Expense Category**
- **Investments/Wealth Tracker**
  - Granular investment tracking (e.g., MF name, FD bank name & a/c number)
  - Monthly visualization of Net Worth
- **Aggregate Credit Card & BNPL Bills Monthly**
- **Monthly Opening Bank Balance Comparison**
- **Expense Tracking at Account Level**
- **Merchant-wise Aggregates**
- **EMI & Loan Tracking**
- **Record Shared Expense Settlements**

## Contribution

Feel free to contribute to this project by submitting issues or pull requests. Your feedback and enhancements are warmly welcomed!

## License

This project is licensed under the [MIT License](LICENSE).
