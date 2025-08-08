2025-08-07 06:23
Status: #baby
Tags: [[computer science]] [[java]]
## Main
### What? 
**Job scheduling** in an application refers to running certain code or tasks at:
- Specific times (e.g., every day at 2 AM)
- Fixed intervals (e.g., every 5 minutes)
- Certain triggers/events (e.g., after user signup)
### Use cases?
- Email reminders
    
- Data cleanup
    
- Report generation
    
- Sync with external services
    
- Invoice batching
    
- Cache refresh

|Approach|Example|Pros|Cons|
|---|---|---|---|
|In-app scheduler|Spring `@Scheduled`, APScheduler|Easy to set up|Tied to app lifecycle|
|External worker|Celery, Sidekiq, Bull|Scalable, async|Needs infra setup|
|OS-level cron|`cron`, `systemd timers`|Reliable, outside app|Harder to test/manage|
|Orchestration|Airflow, Argo Workflows|Complex workflows|Overhead for small apps|

## 🔒 Best Practices

- ✅ **Avoid scheduling inside web servers** like Gunicorn or Tomcat if the job is critical.
    
- ✅ Use **idempotent jobs** to avoid duplicate side effects.
    A **job is idempotent** if **running it multiple times has the same effect as running it once**.
	    ```
	    def send_invoice(invoice_id):
    if invoice_already_sent(invoice_id):
        return
    send_email(invoice_id)
    mark_as_sent(invoice_id) ```

|Practice|Use When|
|---|---|
|Check if result already exists|Report generation, file exports|
|Use `upsert`|DB inserts, data syncing|
|Track job completion by key|Task queues, external API calls|
|Use API idempotency keys|Payments, emails, SMS, remote services|
|Avoid side effects in logic|Only commit changes if required|

- ✅ Store job metadata (last run, status) for visibility/debugging.
    
- ✅ Monitor job failures and alert.
    
- ✅ For long jobs: use async workers or queues.

### Run job in a multi-node env
## 🔑 Solution Options

### ✅ 1. **Distributed Locking**

Use a **distributed lock** to ensure only one instance of your application runs the job.

#### Using hazelcast
##### ✅ How It Works

- Hazelcast is an **in-memory data grid**.
    
- It supports **distributed locks** using the `ILock` interface.
    
- Before executing a job, your node tries to acquire the lock.
    
- Only the node that **successfully acquires the lock** runs the job.


### ✅ 2. **Dedicated Worker Node**

Move job execution to a **single worker node or pod**, decoupled from the rest of your app.

A **Dedicated Worker Node** is a **single instance (pod, container, process)** responsible for running **all scheduled jobs**, separated from your main application replicas.
                    +------------------------+
                    |     Client Requests    |
                    +------------------------+
                           ↓        ↓        ↓
                   +--------+  +--------+  +--------+
                   | App #1 |  | App #2 |  | App #3 |   <-- No scheduled jobs here!
                   +--------+  +--------+  +--------+

                           ↓
                    +-----------------+
                    | Dedicated Worker|
                    | (Job Scheduler) |
                    +-----------------+
                           ↓
                 Executes scheduled jobs


|Benefit|Why it Matters|
|---|---|
|❌ No duplication|Only one instance runs scheduled jobs|
|✅ Isolation of concerns|Keeps web apps fast; jobs don’t block HTTP threads|
|✅ Scales independently|Worker can be scaled separately|
|✅ Easier monitoring|Job logs are isolated|
|✅ Simpler to manage|No need for distributed locks or clustered schedulers|



## References