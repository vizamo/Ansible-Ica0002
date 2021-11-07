Install and configure infrastructure with Ansible:

    ansible-playbook infra.yaml

Restore MySQL data from the backup:

	duplicity --no-encryption restore rsync://vizamo@backup.rlt.vizamo//home/vizamo/ /home/backup/restore/
	
	mysqldump agama > /home/backup/mysql/agama.sql

If restore is correct - see on web application url restored table

Restore MySQL data from the backup:

	service telegraf stop
	influx -execute 'DROP DATABASE telegraf'
	influxd restore -portable -database telegraf /home/backup/influxdb

If restore is correct - see InfluxDB logs in Grafana

