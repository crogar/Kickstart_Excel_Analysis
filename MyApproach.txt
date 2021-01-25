# Excel Homework: Kickstart My Chart
# this is a version of README.md that shows the approach I took to solve the steps in
# that file.

## Background

Over $2 billion has been raised using the massively successful crowdfunding service, Kickstarter, but not every project has found success. Of the more than 300,000 projects launched on Kickstarter, only a third have made it through the funding process with a positive outcome.

Getting funded on Kickstarter requires meeting or exceeding the project's initial goal, so many organizations spend months looking through past projects in an attempt to discover some trick for finding success. For this week's homework, you will organize and analyze a database of 4,000 past projects in order to uncover any hidden trends.

### Before You Begin

1. Create a new space for this project called `excel-challenge` in either DropBox or Google Drive. **Do not add this homework to an existing space**.


        My Approach: I created a local folder on my pc, and I also created a new repository with the name "excel-challenge' on github that will contain the final version of this work
              - Also, the folder was uploaded to google drive and the link was set a public


2. Store your excel workbooks in here and create a sharable link for submission.

## Instructions

![Kickstarter Table](Images/FullTable.png)

Using the Excel table provided, modify and analyze the data of 4,000 past Kickstarter projects as you attempt to uncover some market trends.

* Use conditional formatting to fill each cell in the `state` column with a different color, depending on whether the associated campaign was successful, failed, or canceled, or is currently live.

  * Create a new column O called `Percent Funded` that uses a formula to uncover how much money a campaign made to reach its initial goal.


  	My Approach: I decided to just divide "pledge" by "goal", leave the result of the division as a number and format the cells to represent that value as percentage and rounding the result(only formatting, the whole decimal  number is still there)
		    Formula: "=(E2/D2))" this gives us the percent funded value needed

* Use conditional formatting to fill each cell in the `Percent Funded` column using a three-color scale. The scale should start at 0 and be a dark shade of red, transitioning to green at 100, and blue at 200.
 

    My Approach: for this step I decided to format all cells on their values : Minimum: 0, Midpoint: 1, Maximum: 2,
    		    This because I left the cell value as a float number and not an actual percentage

  * Create a new column P called `Average Donation` that uses a formula to uncover how much each backer for the project paid on average.
  

    My Approach: I decided to use the next formula: "=IF(L2=0,0,ROUND((E2/L2),2))" this because I wanted to be able to avoid the error resulted from trying to divide 0/0 when we know that if "backers_count" = 0 pledge value will be 0
  			- I also applied round function to the result when L'n' is not 0 and this will only show 2 decimal places

  * Create two new columns, one called `Category` at Q and another called `Sub-Category` at R, which use formulas to split the `Category and Sub-Category` column into two parts.
  -->  `MY APPROACH`
   
    My approach: To make this work I decided to make use of the Left() which allows to split text based on index input parameter, Formula: "=LEFT(N2,SEARCH("/",N2,1)-1)"
  			- The Left() function takes 2 arguments as parameters first one is the string and second is a integer that represents up to what index we will take the text, example: "film & video/television" to obtain the category(left of the '/') we need to take the first 12 characters
  			- to be able to find that integer number I have made use of the function SEARCH(), which returns an integer higher than 0 if it finds a specific string in the given sample, it receives 3 parameters: SEARCH(Arg1,Arg2,Arg3(optional))
  					Name	Required/Optional	Data type	Description
  					Arg1	Required	String	Find_text - the text that we want to find.
  					Arg2	Required	String	Within_text - the text in which you want to search for find_text.
  					Arg3	Optional	Variant	Start_num - the character number in within_text at which you want to start searching.
  			- for our example: SEARCH("/",N'n',1) -1, we need to substract 1 this because we need to get the index where / is found and not the index after '/'
  		    The same logic applies to obtain the sub-categories but with a slightly modified formula: "=RIGHT(N2,LEN(N2)-SEARCH("/",N2))"
  			- RIGHT()'s structure is similar to LEFT(), but this method returns the string from right to left, based on our example: "film & video/television"
  			- I'm using the operation [len(N'n') - SEARCH("/",N'n') this will return an integer which will be utilized to get the index that will tell our RIGHT() method up to what point return our string,
  			So using "=RIGHT(film & video/television,LEN(film & video/television)-SEARCH("/",film & video/television))" we will obtain the sub-category: "television"
  			- because Len() returns 23, Search() returns 13, so, =RIGHT("film & video/television",10) will return 10 characters from right to left, "television".
  		* this logic applies to the rest of the cells under Category and sub-Category.

		--> sources I obtained information from: https://docs.microsoft.com/en-us/office/vba/api/excel.worksheetfunction.search

  ![Category Stats](Images/CategoryStats.png)

  * Create a new sheet with a pivot table that will analyze your initial worksheet to count how many campaigns were successful, failed, canceled, or are currently live per **category**.

  * Create a stacked column pivot chart that can be filtered by country based on the table you have created.

  ![Subcategory Stats](Images/SubcategoryStats.png)

  * Create a new sheet with a pivot table that will analyze your initial sheet to count how many campaigns were successful, failed, or canceled, or are currently live per **sub-category**.

  * Create a stacked column pivot chart that can be filtered by country and parent-category based on the table you have created.
 

    My approach: Since there's no such Column or field called 'Parent Category', assuming the Column named 
    'Category' is actually the parent-category, I renamed the field under PivotTable Tools > Analyze> Active Field group, clicked the Active Field text box and renamed to 'Parent Category' which would conclude with this step

    --> sources I obtained information from: https://support.microsoft.com/en-gb/office/rename-a-field-or-item-in-a-pivottable-or-pivotchart-a2393a71-faab-4314-be4a-0aca76804dc9

* The dates stored within the `deadline` and `launched_at` columns use Unix timestamps. Fortunately for us, [there is a formula](https://www.extendoffice.com/documents/excel/2473-excel-timestamp-to-date.html) that can be used to convert these timestamps to a normal date.

  * Create a new column named `Date Created Conversion` that will use [this formula](https://www.extendoffice.com/documents/excel/2473-excel-timestamp-to-date.html) to convert the data contained within `launched_at` into Excel's date format.

  * Create a new column named `Date Ended Conversion` that will use [this formula](https://www.extendoffice.com/documents/excel/2473-excel-timestamp-to-date.html) to convert the data contained within `deadline` into Excel's date format.

  ![Outcomes Based on Launch Date](Images/LaunchDateOutcomes.png)

  * Create a new sheet with a pivot table with a column of `state`, rows of `Date Created Conversion`, values based on the count of `state`, and filters based on `parent category` and `Years`.

  * Now create a pivot chart line graph that visualizes this new table.

* Create a report in Microsoft Word and answer the following questions.

1. Given the provided data, what are three conclusions we can draw about Kickstarter campaigns?
2. What are some limitations of this dataset?
3. What are some other possible tables and/or graphs that we could create?

## Bonus

* Create a new sheet with 8 columns:

  * `Goal`
  * `Number Successful`
  * `Number Failed`
  * `Number Canceled`
  * `Total Projects`
  * `Percentage Successful`
  * `Percentage Failed`
  * `Percentage Canceled`

* In the `Goal` column, create 12 rows with the following headers:

  * Less than 1000
  * 1000 to 4999
  * 5000 to 9999
  * 10000 to 14999
  * 15000 to 19999
  * 20000 to 24999
  * 25000 to 29999
  * 30000 to 34999
  * 35000 to 39999
  * 40000 to 44999
  * 45000 to 49999
  * Greater than or equal to 50000

  ![Goal Outcomes](Images/GoalOutcomes.png)

* Using the `COUNTIFS()` formula, count how many successful, failed, and canceled projects were created with goals within the ranges listed above. Populate the `Number Successful`, `Number Failed`, and `Number Canceled` columns with this data.

* Add up each of the values in the `Number Successful`, `Number Failed`, and `Number Canceled` columns to populate the `Total Projects` column. Then, using a mathematical formula, find the percentage of projects that were successful, failed, or canceled per goal range.

* Create a line chart that graphs the relationship between a goal's amount and its chances at success, failure, or cancellation.

## Bonus Statistical Analysis

If one were to describe a successful crowdfunding campaign, most people would use the number of campaign backers as a metric of success. One of the most efficient ways that data scientists characterize a quantitative metric, such as the number of campaign backers, is by creating a summary statistics table.

For those looking for an additional challenge, you will evaluate the number of backers of successful and unsuccessful campaigns by creating **your own** summary statistics table.

* Create a new worksheet in your workbook, and create a column each for the number of backers of successful campaigns and unsuccessful campaigns.

  ![Images/backers01.png](Images/backers01.png)

* Use Excel to evaluate the following for successful campaigns, and then for unsuccessful campaigns:

  * The mean number of backers.

  * The median number of backers.

  * The minimum number of backers.

  * The maximum number of backers.

  * The variance of the number of backers.

  * The standard deviation of the number of backers.

* Use your data to determine whether the mean or the median summarizes the data more meaningfully.

* Use your data to determine if there is more variability with successful or unsuccessful campaigns. Does this make sense? Why or why not?

## Submission

* To submit your homework, upload the solution and files to a GitHub repo, Dropbox, or Google Drive and submit the link to <https://bootcampspot.com/>.

## Employer-Ready Criteria

Students who are marked as employer-ready gain access to our employer referral program, additional workshops, and other resources. Work with your Career Director to become employer-ready. At a minimum, you must have:

- A clear, concise, and compelling resume. Submit via your learning platform for review.
- A polished GitHub profile:
  - 3 - 6 pinned repositories ([instructions here](https://docs.github.com/en/enterprise/2.13/user/articles/pinning-items-to-your-profile))
  - at least 5 commits per repository
  - professional titles, i.e. not "Homework #1"
  - thorough README.md files for each repository
  - clean code

- - -

© 2019 Trilogy Education Services
