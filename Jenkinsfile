pipeline {
    agent any

    environment {
        AWS_REGION = 'us-west-1' // AWS 지역 설정
        S3_MAIN = 'jenkins-nps'
        S3_BUCKET_DATA = 'Data'
        S3_BUCKET_DATA_Eval = 'Eval'
        S3_BUCKET_DATA_Train = 'Train'
        
        S3_BUCKET_MODEL = 'Model'
        S3_BUCKET_MODEL_CLASS2 = 'Class_2'
        S3_BUCKET_MODEL_CLASS3 = 'Class_3'
        
        S3_BUCKET_MONITOR = 'Monitor'
        S3_BUCKET_MONITOR_MLFLOW = 'Mlflow'
        S3_BUCKET_MONITOR_READERBOARD = 'ReaderBoard'
        S3_BUCKET_MONITOR_TMP = 'tmp'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/kanghee931210/aws_mlops.git'
            }
        }
        stage('Create S3 Buckets') {
            steps {
                script {
                    def buckets = [
                        "${S3_MAIN}/${S3_BUCKET_DATA}",
                        "${S3_MAIN}/${S3_BUCKET_DATA}/${S3_BUCKET_DATA_EVAL}",
                        "${S3_MAIN}/${S3_BUCKET_DATA}/${S3_BUCKET_DATA_TRAIN}",
                        "${S3_MAIN}/${S3_BUCKET_MODEL}",
                        "${S3_MAIN}/${S3_BUCKET_MODEL}/${S3_BUCKET_MODEL_CLASS2}",
                        "${S3_MAIN}/${S3_BUCKET_MODEL}/${S3_BUCKET_MODEL_CLASS3}",
                        "${S3_MAIN}/${S3_BUCKET_MONITOR}",
                        "${S3_MAIN}/${S3_BUCKET_MONITOR}/${S3_BUCKET_MONITOR_MLFLOW}",
                        "${S3_MAIN}/${S3_BUCKET_MONITOR}/${S3_BUCKET_MONITOR_READERBOARD}",
                        "${S3_MAIN}/${S3_BUCKET_MONITOR}/${S3_BUCKET_MONITOR_TMP}"
                    ]
                    
                    buckets.each { bucket ->
                        sh """
                        aws s3api create-bucket --bucket ${bucket} --region ${AWS_REGION} --create-bucket-configuration LocationConstraint=${AWS_REGION} || true
                        """
                    }
                }
            }
        }
    }
}

