# Kubernetes Elasticsearch Backup with Helm 
 
This project demonstrates a setup for automating Elasticsearch backups on Kubernetes using Helm, ConfigMaps, and CronJobs. 
 
## Prerequisites 
 
- [Kubernetes](https://kubernetes.io/) cluster set up. 
- [Helm](https://helm.sh/) installed on your local machine. 
- Access to an Elasticsearch cluster. 
 
## Project Structure 
 
- \`my-elasticsearch/\`: Helm chart for Elasticsearch deployment. 
- \`my-kibana/\`: Helm chart for Kibana deployment. 
- \`elasticsearch-backup-cronjob.yaml\`: CronJob configuration for automated backups. 
- \`elasticsearch-snapshot-config.yaml\`: ConfigMap for Elasticsearch snapshot repository configuration. 
 
## Instructions 
 
### 1. Set up Elasticsearch and Kibana 
 
```bash 
# Install Elasticsearch 
helm install my-elasticsearch ./my-elasticsearch/ 
 
# Install Kibana 
helm install my-kibana ./my-kibana/ 
``` 
 
### 2. Configure Elasticsearch Snapshot Repository 
 
Adjust \`elasticsearch-snapshot-config.yaml\` to specify the backup location. 
 
```bash 
kubectl apply -f elasticsearch-snapshot-config.yaml 
``` 
 
### 3. Schedule Automated Backups 
 
```bash 
kubectl apply -f elasticsearch-backup-cronjob.yaml 
``` 
 
This CronJob runs daily at midnight, creating backups using the specified configuration. 
 
### 4. Check Backup Status 
 
Monitor the CronJob logs for backup status: 
 
```bash 
kubectl logs -f cronjob/elasticsearch-backup 
``` 
 
### 5. Cleanup 
 
```bash 
# Delete CronJob 
kubectl delete cronjob elasticsearch-backup 
 
# Uninstall Elasticsearch and Kibana 
helm uninstall my-elasticsearch 
helm uninstall my-kibana 
``` 
 
## Customization 
 
- Adjust Helm chart values in \`my-elasticsearch/values.yaml\` and \`my-kibana/values.yaml\`. 
- Customize CronJob schedule in \`elasticsearch-backup-cronjob.yaml\`. 
 
## Contributing 
 
Feel free to contribute by opening issues or pull requests. 
 
## License 
 
This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details. 
