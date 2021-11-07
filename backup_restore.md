Install and configure infrastructure with Ansible:

    ansible-playbook infra.yaml

Restore MySQL data from the backup:

	ssh -p{database-vm-port} ubuntu@193.40.156.86
	sudo -u backup duplicity --no-encryption restore rsync://vizamo@backup.rlt.vizamo//home/vizamo/ /home/backup/restore/
	
	mysql agama < /home/backup/restore/agama.sql

If restore is correct - see on agama application restored data

Restore InfluxDB data from the backup:

	ssh -p{influxdb-vm-port} ubuntu@193.40.156.86
	sudo -u backup duplicity --no-encryption restore rsync://vizamo@backup.rlt.vizamo//home/vizamo/ /home/backup/restore/
	
	service telegraf stop
	influx -execute 'DROP DATABASE telegraf'
	influxd restore -portable -database telegraf /home/backup/restore
	
	
	Again configure the infrastructure with:
	ansible-playbook infra.yaml

If restore is correct - see old InfluxDB logs in Grafana

