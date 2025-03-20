# Cato Networks Event Feed Integration for USM Anywhere

This repository contains a **modified version** of the `eventsFeed.py` script provided by **Cato Networks** for integration with **USM Anywhere**.

## Modifications vs. Original Cato Script  

- **Removed duplicate/repeating fields** to optimize log data.  
- **Added a data source field** to ensure logs are recognized as coming from **Cato Networks**, enabling automatic discovery of the appropriate **parser/plugin/app**.  
- **Modified log streaming to a single syslog line** to improve compatibility with SIEMs that cannot process multi-line logs.  

## Important Notes  

- **Webhooks could be used**, but Cato imposes a **rate limit** of **100 webhook forwards per hour**, which may not be sufficient for high-volume environments.  
- **Cato Networks API limitations:**  
  - The API **does not support time-based searches** ([Reference](https://support.catonetworks.com/hc/en-us/articles/360019839477/comments/10070256338461)).  
  - As a result, the script collects **historical event data**, which **may exceed your license tier**.  
  - To start collecting real-time data, you can **reset the event queue** by toggling the event integration **off and on** in the **Cato Console** ([Instructions](https://support.catonetworks.com/hc/en-us/articles/360019839477/comments/9560345196957)).  

## How to Use  

1. In **Cato Networks**, go to the **Event Integration settings** and toggle the integration **off and on**.  
   - This resets the event queue, allowing you to start from **near real-time** data.  

2. Run the script using the following command:  

   ```bash
   eventsFeed.py -K XXXXX -I 7471 -Pp -n 192.168.0.220:601```
  `-K XXXXX` → API key for the Cato account.
  
  `-I 1771` → Account ID.
  
  `-Pp` → Prints the output in the console.
  
  `-n` 192.168.0.220:601 → Sensor IP and UDP Syslog port (Note: The original Cato script only supports TCP).
