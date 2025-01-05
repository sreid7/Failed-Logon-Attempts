# Failed Logon Attempts
Elastic Dashboard Creation

**Dashboard Creation**

**Failed Logon Attempts**

1. Delete existing dashboards
2. Click create dashboard
3. Click create visualization
4. Enter "last 15 years" for time range.
5. Add Filter date for "failed logon attempts" - IDs that match **4625** = Failed logon attempt on a Windows system. Field = event.code, Operator = is, and Value = 4625
6. Specify "Windows" as the Index pattern
7. For the visualization type, use a table.
8. Create a row. select a field = user.name.keyword, number of values = 1000, ranked by = count of records. (Displaay name = Username)
9. Add metrics, function = count, (The count of records will be the data, assuming that data will be preset). (Display name = # of logins)
10. Create another row as "host.hostname.keyword" (which represents the computer reporting the failed logon attempt.) (Display name = Event logged by)
11. Create another row for "logon type". Using the "winlog.logon.type.keyword", (Used to display the type of method used to logon - either network or service. (Display name = Logon Type)
12. Save and return the dashboard. Name "No title" the table and also the dashboard.
13. To reopen dashboard, click the listed dashboard and then click on the gear - select edit lens to be taken to the full saved dashboard. 

    **Usernames can be excluded by specifying additional filters ex. field = user.name.keyword, operator = is not, value = "username to be excluded".**
    **Computer accounts can be excluded by specifying the following KQL query and clicking on the "Update" button.

      **SIEM Visualization Example 1: Failed Logon Attempts (All Users)**
      NOT user.name: *$ AND winlog.channel.keyword: Security
      The AND winlog.channel.keyword: Security part is to ensure that no unrelated logs are accounted for.

**UPDATED** (add multiple users in one script) ---
    NOT (user.name: "john.doe" OR user.name: "admin" OR user.name: "system") AND winlog.channel.keyword: Security

Ex. NOT user.name.keyword: ("WIN-OK9BH1BCKSD" OR "DESKTOP-DPOESND" OR "WIN-RMMGJA7T9TC") AND winlog.channel.keyword: "Security" 


_____________

**Disabled USer**

**New Visualization, Same Dashboard**

1. Click edit on the dashboard (the pencil)
2. Click create visualization
3. Set the index pattern to windows
4. Add filter Field = event.code, Operator = is, and Value = 4625 (event.code: 4625)
5. Add filter Field = winlog.event_data.SubStatus, Operator = is, and Value = 0xc0000072 (winlog.event_data.SubStatus:0xc0000072)
6. Filter by type = user.name.keyword
7. Set visualization to "Table"
8. Add Row, select field = user.name.keyword, number of values = 1000, close row.
9. Add Metrics, select "count" (this will populate the table with data).
10. Add Row, host.hostname.keyword, to show the machine where the failed logon attempt occurred. Number of values = 1000, close row.
11. Click Save and Return, title the new visualization table.

    *to find usernames with a specific name or word within the username, in the kql you can use "user.name:*admin*" as an example. This will list only the usernames with this word in it.

    

    
