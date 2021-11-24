Backup Documentation for RLT

  Backup coverage
- MySQL - must be covered MySQL dump of application data (Agama DB);
- InfluxDB - must be covered all collecting logs of monitoring vms;
- Ansible repository - must be covered all repository code.

  RPO
Backup must be created on time 1:25.
Full backup is created on Monday
Incremental backups is created on Thursday and Sunday
RPO is 72 hours.

  Versioning and retention
Must be save a 10 versions of backup.
Every version of backup is saved for 30 days.

  Usability checks
Every sunday 3 engineers, who is in charge for IT Workflow reporting, restoring and using backed up system for testing workflow and writing their reports.

  Restoration criteria
Backup should be restorer if: 
 - Ansible repository code was changed and system is crashed after running it;
 - InfluxDB or MySQL database is crashed and current version of data is lost.

  RTO
Objective recovery time is 70 min:
 - 30 min is for downloading backup information;
 - 40 min is for re-setup from ansible repository and restarting services.

