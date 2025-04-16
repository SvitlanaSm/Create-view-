# Create-view
## Description
This project creates a BigQuery view to analyze how actively users (accounts) send emails within each month. It tracks the proportion of emails sent by each account compared to the total number of emails sent in the same month, as well as the date range of their activity.

The workflow consists of two parts:

1. **View Creation** — defines and stores reusable monthly statistics for each account.

2. **Query** — calculates the percentage contribution of each account to the total monthly email volume.

## View
The view aggregates and partitions data from email sending activity and sessions to compute:

`sent_month`: the month when emails were sent

`id_account`: account identifier

`msg_cnt_account`: number of emails sent by the account in the month

`msg_cnt_month`: total number of emails sent by all users in that month

`first_sent_date`: first email sent by the account in that month

`last_sent_date`: last email sent by the account in that month

This is achieved using **DATE_ADD**, **DATE_TRUNC**, and **window functions** for accurate per-account and per-month aggregations.

## Query: Email Contribution per Account
The query selects from the view and computes:

* `sent_msg_percent_from_this_month`: percentage of all emails in a given month that were sent by a specific account

* `first_sent_date`, `last_sent_date`: to understand the span of activity for each account in the month

