# freelancers-data-cleaning
# Global Freelancers Data Cleaning & Analysis (PostgreSQL)

## Problem
A raw dataset of 1,000 fictional global freelancer profiles had inconsistent gender labels, mixed currency formatting, inconsistent true/false values, percentage values stored as text, missing data across several numeric fields, and names with inconsistent titles/suffixes mixed in.

## What I fixed
- Standardized `gender` (9+ inconsistent spellings like "f", "FEMALE", "male", "M" -> clean "Male"/"Female")
- Cleaned `hourly_rate_usd` (mixed formats like "USD 100", "$40" -> converted to NUMERIC)
- Standardized `is_active` (mixed 0/1, True/False, T/F, Y/N, yes/no -> converted to a single BOOLEAN column)
- Cleaned `client_satisfaction` (percentage text like "84%" -> converted to NUMERIC)
- Filled 101 missing `rating` values using the average rating for the same primary_skill
- Filled 51 missing `years_of_experience` values using the average for the same primary_skill
- Left 30 missing `age` values as NULL -- no reliable column to estimate age from, so it was not guessed
- Cleaned `name` by stripping inconsistent titles and suffixes (e.g. "Ms.", "Dr.", "DDS")

## Analysis
Using SQL filtering and aggregation (`GROUP BY`, `AVG`, `COUNT`, `ORDER BY`, `LIMIT`):

- **Average hourly rate by skill:** Cybersecurity pays the most ($54.26/hr), followed by DevOps ($54.14) and Web Development ($54.01); Blockchain Development pays the least of the top 10 ($50.00/hr)
- **Active vs inactive freelancers:** 465 inactive, 361 active, 174 with no recorded status
- **Top 5 countries by average rating:** United States (2.89), Russia (2.82), Canada (2.69), Italy (2.67), China (2.66)
- **Average client satisfaction by gender:** Male freelancers average 79.55%, Female freelancers average 78.97%, a small gap
- **Top 5 countries by number of freelancers:** South Korea (68), Canada (65), Germany (52), Australia (51), Netherlands (51)

## Key finding
A meaningful share of freelancers (174 out of 1,000) have no recorded active status at all, worth flagging for anyone using this data to measure platform engagement, since excluding or assuming a value for these would change the active/inactive split significantly.

## Before / After

**gender -- before:**
<img width="124" height="232" alt="Screenshot 2026-10-05 125043" src="https://github.com/user-attachments/assets/072f1d58-ddb1-4dfc-993b-a1fde9444e51" />


**gender -- after:**
<img width="200" height="269" alt="Screenshot 2026-10-05 125009" src="https://github.com/user-attachments/assets/1232b190-ef96-4742-9fff-14888b9b39f9" />

**hourly_rate_usd -- before:**
<img width="233" height="295" alt="Screenshot 2026-10-05 125214" src="https://github.com/user-attachments/assets/54ff4f46-61e3-4f5b-bd71-72445f8963cf" />

**hourly_rate_usd -- after:**
<img width="246" height="307" alt="Screenshot 2026-10-05 125241" src="https://github.com/user-attachments/assets/ac246dce-7482-47e4-8532-7a857cc15b18" />

**is_active -- before:**
<img width="281" height="341" alt="Screenshot 2026-10-05 125315" src="https://github.com/user-attachments/assets/cf4d3061-56c9-41b8-9e5c-a25c20ea3c1b" />

**is_active -- after:**
<img width="227" height="255" alt="Screenshot 2026-10-05 130018" src="https://github.com/user-attachments/assets/f64a33b3-a123-4bf9-9cc8-7972f0948862" />

## Query results
<img width="230" height="147" alt="Screenshot 2026-10-05 123212" src="https://github.com/user-attachments/assets/04db0c1f-e481-40f1-a871-4c20db1758cd" />
<img width="251" height="182" alt="Screenshot 2026-10-05 123155" src="https://github.com/user-attachments/assets/2c0aa42a-718c-49bc-b91a-defbf6e0954f" />
<img width="179" height="120" alt="Screenshot 2026-10-05 123138" src="https://github.com/user-attachments/assets/5a135c46-d317-42af-bf7f-80456afbf358" />
<img width="199" height="227" alt="Screenshot 2026-10-05 123124" src="https://github.com/user-attachments/assets/ce059008-244f-494c-9f8c-03a6a1351df1" />
<img width="193" height="128" alt="Screenshot 2026-10-05 123019" src="https://github.com/user-attachments/assets/dd86ef1b-2138-40be-b9cd-04bf32afc8a2" />

## Dashboard
_(describe the dashboard here once built, e.g. what it visualizes)_
_(screenshot: finished dashboard)_

## Tools
PostgreSQL, pgAdmin

## Files
[freelancers_clean_csv.sql](https://github.com/user-attachments/files/33047632/freelancers_clean_csv.sql)
## Before table 
<img width="670" height="321" alt="Screenshot 2026-10-05 131422" src="https://github.com/user-attachments/assets/5fa6922e-4b43-41d6-9fc4-4edc283dfdc9" />
## After table
<img width="725" height="362" alt="Screenshot 2026-10-05 131443" src="https://github.com/user-attachments/assets/4941a9e0-f294-41e4-8e0c-984ad2a6a2e0" />

