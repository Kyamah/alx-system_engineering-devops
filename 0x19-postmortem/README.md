Issue Summary

Duration: 
March 1, 2025, 14:00 UTC - March 1, 2025, 16:30 UTC (2 hours 30 minutes)
Impact: 
During the outage, users were unable to search for available listings or book reservations. Approximately 70% of users experienced slow response times or complete failures when attempting to access the platform. Host dashboards were also affected, preventing them from managing bookings.

Root Cause: 
A database migration introduced a schema change that was incompatible with an existing query in the reservation system, leading to increased database load and query failures.
Timeline
14:00 UTC - Monitoring alerts triggered due to increased response times and failed database queries.
14:05 UTC - Engineers began investigating logs and noticed a surge in database query failures.
14:20 UTC - Initial assumption was a high-traffic spike causing database overload, and the team attempted to scale database resources.
14:40 UTC - A deeper review of recent deployments identified a database migration as a potential cause.
15:00 UTC - The database team was brought in to analyze the migration logs.
15:15 UTC - Rollback of the migration was attempted but failed due to foreign key constraints.
15:45 UTC - A hotfix was deployed to update the faulty query, resolving the issue.
16:30 UTC - Services fully recovered, and normal operations resumed.


Root Cause and Resolution

 Root Cause: The outage was caused by a database migration that altered the structure of the reservations table, inadvertently modifying an index used by a frequently executed query. This resulted in slower query execution, causing a bottleneck that degraded the system’s performance.
Resolution: Engineers identified the problematic query and deployed a hotfix that optimized the query to align with the new schema. A subsequent migration was planned to restore indexing while ensuring compatibility with the modified structure.

Corrective and Preventative Measures
Improvements:
Implement stricter database schema validation before migrations.
Enhance rollback procedures to prevent failures due to foreign key constraints.
Improve monitoring alerts to detect query slowdowns earlier.
To-Do:
Implement pre-migration query performance tests.
Establish an automated rollback mechanism for database changes.
Enhance logging to capture query execution times more effectively.
Conduct training sessions on schema migration best practices for engineers.
By implementing these measures, we aim to reduce the likelihood of similar outages in the future.


Representative Diagram

Representative Diagram
[ 🚨 Issue Summary 🚨 ]
       |
       v
[ 🕒 Timeline ]  
       |
       v
[ 🛠 Root Cause & Resolution ]  
       |
       v
[ 🚀 Corrective & Preventative Measures ]  
       |
       v
[ 📌 Moral of the Story: Test, Validate, Monitor! ] 

