pipeline {
    agent any

    environment {
        REPO_URL = 'https://github.com/Allen0602/BW6.git'
        PROJECT_PATH = '/home/allen_1/BW6'
        OUTPUT_DIR = '/home/allen_1/BW6'
        EAR_FILE = 'ems_project.application_2.0.0.ear'
        DOMAIN = 'DefaultDomain'
        APP_SPACE = 'DefaultAppSpace'
    }

    stages {
        stage('Checkout from GitHub') {
            steps {
                git branch: 'main', url: "${REPO_URL}"
            }
        }

        stage('Build EAR File') {
            steps {
                script {
                    sh "bwdesign -b -p ${PROJECT_PATH} -o ${OUTPUT_DIR}/${EAR_FILE}"
                }
            }
        }

        stage('Deploy to TIBCO Admin') {
            steps {
                script {
                    sh "bwadmin deploy -d ${DOMAIN} -a ${APP_SPACE} ${OUTPUT_DIR}/${EAR_FILE}"
                }
            }
        }
    }
}
