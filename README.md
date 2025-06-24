# cost-optimization
A simple automation script to read today’s Jenkins build logs and upload them to an S3 bucket using the AWS CLI. Ideal for backup, audit, or log retention purposes.
This project provides a lightweight Shell script to automatically collect daily Jenkins build logs and upload them to an Amazon S3 bucket. Designed for DevOps teams looking to maintain offsite backups of CI/CD pipeline logs with minimal setup. Uses AWS CLI for seamless integration with S3.

Project Title:
Jenkins CI/CD Logs — Automate Cost‑Efficient Log Archiving

Short Description:
A DevOps-friendly script to streamline daily Jenkins (or other CI/CD) build logs, filter relevant data, and upload them to AWS S3—minimizing cloud storage costs through FinOps best practices.

What This Project Solves:

🎯 Cost Optimization: Reduce the size and retention span of CI logs to lower S3 storage expenses 


⚙️ Automation: Fully script-driven—no manual handling—using shell or Python and AWS CLI.

🗓️ Daily Archival: Automatically harvest today’s build logs, compress or filter them, and push to S3.

Tools used for this Project:

Jenkins build logs

AWS S3 archival

CI/CD cost control

Shell scripting + AWS CL
