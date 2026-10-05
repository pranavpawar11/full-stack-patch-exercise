# Patch Notes

## Summary of Changes

1. The first bug I found was a filtering issue. When I used the DONE filter, I was receiving tasks with different statuses. I tested this using Postman, which confirmed that the issue was in the backend API. I fixed the SQL filtering condition and also updated the Oracle reference query.

2. The second bug was related to pagination. I used ChatGPT to review what I was doing and suggested a few test cases. While testing, I found that applying a search or status filter while being on a later page could return no results even when matching tasks existed. I fixed this by resetting the page to 1 whenever the search or filter changes.

3. The third bug was found while checking the backend connection/error behavior. When the backend was unavailable, the UI remained stuck on "Loading tasks". I found that `setLoading(false)` was missing from the error handling and fixed it.

## What I Chose Not to Change

I kept the existing artificial query delay because it was not creating a specific bug or user-facing problem.

## Biggest Remaining Risk

In-memory pagination should be replaced with database-side pagination. Currently, all matching tasks are loaded before selecting the requested page. This works well for the current dataset but could use unnecessary memory and processing when there are thousands of tasks.

## Tools / AI Used

I used ChatGPT to review the code, help identify possible issues, suggest test cases, and understand the SQL and frontend behavior. I verified the identified issues and fixes by running and testing the application locally.