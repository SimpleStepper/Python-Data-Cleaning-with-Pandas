# Python Data Cleaning with Pandas
This project focuses on cleaning and standardizing a customer call list dataset using Python and the Pandas library. The goal was to prepare the raw Excel data for use in customer outreach systems by fixing formatting issues, removing incomplete data, and ensuring standardized fields. The final project filters data down to useable client information for a customer outreach agent. 

<img width="1301" height="458" alt="image" src="https://github.com/user-attachments/assets/64465cc6-568d-4bf7-98b0-8efad5ad366f" />

The code for this project with notes can be found here: 

---
# task performed
1) Imported and inspected raw Excel data
2) Removed duplicate records and unnecessary columns
3) Cleaned up name fields (e.g., stripping symbols from Last_Name)
4) Reformatted phone numbers to a consistent XXX-XXX-XXXX structure using regex
5) Split a single address column into Street_Address, State, and Zip_Code
6) Standardized categorical fields like Paying Customer and Do_Not_Contact to consistent Yes/No values
7) Filtered dataset and exported to Excel for Customer Service 
--- 
# Key Data Cleaning Highlights
## Phone Number Reformatting
<img width="450" height="613" alt="image" src="https://github.com/user-attachments/assets/22d1e0d4-f399-4fd0-a18d-85dac9fc6b2c" />

This task was the trickiest part in this project and was more challenging than initially planned - however using Regex made the process more simple and a great skill to pick up. I approached the problem as follows. 

```python
# Clean phone numbers to match 111-111-1111 formatting
df_cleaned["Phone_Number"] = df_cleaned["Phone_Number"].astype(str) #Changes data type to "string" to avoid errors with regex
df_cleaned['Phone_Number'] = df_cleaned['Phone_Number'].str.replace('[^0-9]','', regex=True) #Regex regular expression to strip all values that are not numbers
df_cleaned['Phone_Number'] = df_cleaned['Phone_Number'].fillna('') # Fills Null values as blanks
df_cleaned["Phone_Number"] = df_cleaned['Phone_Number'].apply(lambda x: x[0:3] + '-' + x[3:6] + '-' + x[6:10]) #.apply(lambda) method to format numbers with - seperating numbers
df_cleaned["Phone_Number"] = df_cleaned['Phone_Number'].replace("--","") # Replaces -- that show in our blank values that appear after the .apply(lambda) method
df_cleaned
```
For a non-technical description of the process: 
1) Removed any non-numeric characters (like dashes, spaces, or brackets) so we were left with just digits.
2) Handled any missing numbers by treating them as blanks.
3) Reformatted the numbers to a clean, consistent layout: 123-456-7890.
4) 
This process makes the phone numbers reliable and ready for use in things like customer calls, mail merges, or importing into CRM tools.
