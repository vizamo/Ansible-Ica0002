Install and configure infrastructure with Ansible:

    ansible-playbook infra.yaml

Restore MySQL data from the backup:

{mysql-master-vm-port} must be found in host file

	ssh -p{mysql-master-vm-port} ubuntu@193.40.156.86
	sudo -u backup duplicity --no-encryption restore rsync://vizamo@backup.rlt.vizamo//home/vizamo/mysql /home/backup/restore/
	
	sudo su -
	mysql agama < /home/backup/restore/agama.sql

If restore is correct - see on agama application restored data

Restore InfluxDB data from the backup:

{influxdb-vm-port} must be found in host file

	ssh -p{influxdb-vm-port} ubuntu@193.40.156.86
	sudo -u backup duplicity --no-encryption restore rsync://vizamo@backup.rlt.vizamo//home/vizamo/influxdb /home/backup/restore/
	
	sudo service telegraf stop
	sudo influx -execute 'DROP DATABASE telegraf'
	sudo influxd restore -portable -database telegraf /home/backup/restore
		
	Again configure the infrastructure with:
	ansible-playbook infra.yaml 

If restore is correct - see old InfluxDB logs in Grafana

