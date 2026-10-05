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
_(screenshot: inconsistent values like f, FEMALE, male, M)_

**gender -- after:**
_(screenshot: only Male and Female)_

**hourly_rate_usd -- before:**
_(screenshot: mixed formats like "USD 100", "$40")_

**hourly_rate_usd -- after:**
_(screenshot: clean numeric values)_

**is_active -- before:**
_(screenshot: mixed 0/1, True/False, Y/N values)_

**is_active -- after:**
_(screenshot: clean TRUE/FALSE boolean values)_

## Query results
_(screenshots of the 5 analysis query results)_

## Tools
PostgreSQL, pgAdmin

## Files
- `freelancers_cleaning_analysis.sql` -- full script: cleaning and analysis queries, one section per task
- Screenshots -- before/after proof and query results
