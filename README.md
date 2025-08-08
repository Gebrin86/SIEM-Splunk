# Linux Authentication Log Analysis using Splunk (SIEM Project)

This beginner-friendly SIEM project demonstrates how to use Splunk to detect failed SSH login attempts from a Linux system authentication log. It's an example of how a Security Operations Center (SOC) analyst might perform log analysis and visualize suspicious IP activity.

---

## Objective

- Import and analyze a Linux `auth.log` file in Splunk.
- Search for "Failed password" login attempts.
- Extract source IP addresses using SPL (Search Processing Language).
- Visualize the number of failed attempts per IP using a bar chart.

---

## Tools Used

- **Splunk Enterprise (Free Trial)** — as the SIEM platform
- **auth.log** — Linux authentication log
- **SPL (Search Processing Language)** — for log parsing
- **Screenshots** — for demonstration

---

## Folder Structure

```
splunk-linux-auth-log-analysis/
│
├── README.md
├── auth.log                  # (Optional: include a sample or redacted log)
└── images/
    ├── upload_auth_log.png
    ├── spl_query_result.png
    └── bar_chart.png
```

📁 Place your screenshots inside the `images/` folder before uploading to GitHub. You can upload via GitHub web or Git CLI.

---

## 🧪 Project Steps
### 1. Upload `auth.log` to Splunk 

1. Open Splunk and go to:  
   ![Step 1 - Open Splunk](https://github.com/YOUR-USERNAME/YOUR-REPO/blob/main/images/step1_open_splunk.png?raw=true)

2. Choose your `auth.log` file.  
   ![Step 2 - Choose File](https://github.com/YOUR-USERNAME/YOUR-REPO/blob/main/images/step2_choose_file.png?raw=true)

3. Set the index to:  
   ```
   index = main
   ```
   ![Step 3 - Set Index](https://github.com/YOUR-USERNAME/YOUR-REPO/blob/main/images/step3_set_index.png?raw=true)

4. Set the sourcetype to:  
   ```
   sourcetype = linux_secure
   ```
   ![Step 4 - Set Sourcetype](https://github.com/YOUR-USERNAME/YOUR-REPO/blob/main/images/step4_set_sourcetype.png?raw=true)

5. Finish setup.  
   ![Step 5 - Finish](https://github.com/YOUR-USERNAME/YOUR-REPO/blob/main/images/step5_finish.png?raw=true)

6. Start searching.  
   ![Step 6 - Search](https://github.com/YOUR-USERNAME/YOUR-REPO/blob/main/images/step6_search.png?raw=true)

📸 **Screenshot of Full Upload Process:**  
![Upload auth.log](https://github.com/YOUR-USERNAME/YOUR-REPO/blob/main/images/upload_auth_log.png?raw=true)

---

### 2. Run This SPL Query in Search

```spl
index=main "Failed password"
| rex field=_raw "from (?<src_ip>\d+\.\d+\.\d+\.\d+)"
| stats count by src_ip
```

This query:
- Filters logs with "Failed password"
- Extracts source IPs from each log line
- Counts how many times each IP failed

📸 **Screenshot:**  
![SPL Query Result](https://github.com/YOUR-USERNAME/YOUR-REPO/blob/main/images/spl_query_result.png?raw=true)

---

### 3. Visualize the Data

1. Click the **Visualization** tab.
2. Choose **Bar Chart**.
3. Click **Save As → Report**
4. Use the title:
   ```
   Failed SSH Logins by IP
   ```
5. Save the report.

📸 **Screenshot:**  
![Bar Chart](https://git)


---

## Result

You now have a chart showing which IPs attempted to log in and how many times they failed.

This can help detect:
- Brute-force attacks
- Unauthorized access attempts
- Compromised systems

---

## Why This Matters for SIEM

Security Information and Event Management (SIEM) platforms like Splunk are essential for real-time security monitoring. In real SOC roles, analysts often:
- Ingest logs from systems
- Detect login anomalies
- Create visualizations and alerts
- Investigate IPs or threat actors

This project simulates one of the most common SOC workflows — analyzing Linux auth logs to catch failed logins from unknown IPs.

---

## 📷 Screenshots (Included)

- `images/upload_auth_log.png` – Importing log file into Splunk
- `images/spl_query_result.png` – Output of SPL query showing failed logins
- `images/bar_chart.png` – Final visualization showing IPs and login attempt counts

To show these in GitHub:
```markdown
![Upload Log](images/upload_auth_log.png)  
![Query Result](images/spl_query_result.png)  
![Bar Chart](images/bar_chart.png)
```

---

## What's Next?

- Set alert thresholds (e.g., alert if an IP has more than 5 failed attempts)
- Use external IP reputation feeds to classify known bad actors
- Extend with GeoIP lookups or enrich data with usernames

---

## Author

**Gebrin Alvarez**  
📧 gebrinalvarez@gmail.com  
🔐 Focused on SIEM, cybersecurity, and practical hands-on defense projects.
