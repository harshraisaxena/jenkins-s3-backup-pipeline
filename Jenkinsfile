pipeline {
    agent any
    stages {
        stage('Backup Jenkins to S3') {
            steps {
                sh '''
                    # === Jenkins Backup Script ===
                    
                    # --- IMPORTANT: EDIT THIS LINE ---
                    # Replace "your-s3-bucket-name-goes-here" with your actual S3 bucket name.
                    S3_BUCKET="your-s3-bucket-name-goes-here"
                    
                    # --- Do not edit below this line ---
                    JENKINS_HOME="/var/lib/jenkins"
                    TIMESTAMP=$(date +%F_%H-%M-%S)
                    BACKUP_FILE="/tmp/jenkins_backup_${TIMESTAMP}.tar.gz"
                    
                    echo "Starting Jenkins backup..."
                    
                    # Create a compressed archive of the Jenkins home directory
                    tar -czf ${BACKUP_FILE} ${JENKINS_HOME}
                    
                    echo "Backup file created at ${BACKUP_FILE}"
                    
                    # Upload the backup file to the specified S3 bucket
                    aws s3 cp ${BACKUP_FILE} s3://${S3_BUCKET}/
                    
                    echo "Backup successfully uploaded to s3://${S3_BUCKET}/"
                    
                    # Remove the local backup file to save space
                    rm -f ${BACKUP_FILE}
                    
                    echo "Local backup file removed. Process complete."
                '''
            }
        }
    }
}
