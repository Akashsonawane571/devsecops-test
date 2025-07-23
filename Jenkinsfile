pipeline {
    agent any

    environment {
        DEPENDENCY_CHECK = '/opt/dependency-check/dependency-check/bin/dependency-check.sh'
    }

    stages {

        stage('Clone Repository') {
            steps {
                echo 'Cloning the GitHub Repository...'
                sh '''
                    rm -rf temp_repo
                    git clone --depth=1 https://github.com/Akashsonawane571/devsecops-test.git temp_repo
                '''
            }
        }

        // Commented out TruffleHog & Dependency check for now
        /*
        stage('Secret Scan (TruffleHog)') {
            steps {
                echo 'Running TruffleHog on latest commit...'
                sh '''
                    cd temp_repo
                    trufflehog --regex --entropy=True --max_depth=10 . > ../trufflehog_report.txt || true
                '''
                archiveArtifacts artifacts: 'trufflehog_report.txt', onlyIfSuccessful: false
            }
        }

        stage('Dependency Check (OWASP)') {
            steps {
                echo 'Running OWASP Dependency-Check...'
                sh '''
                    mkdir -p dependency-check-report
                    cd temp_repo
                    $DEPENDENCY_CHECK --project "Universal-SCA-Scan" --scan . --format ALL --out ../dependency-check-report || true
                    cd ..
                '''
                archiveArtifacts artifacts: 'dependency-check-report/*', onlyIfSuccessful: false
            }
        }
        */

        stage('SonarQube Scan') {
            steps {
                echo 'Starting SonarQube SAST Scan...'
                withSonarQubeEnv('sonar') {
                    sh '''
                        cd temp_repo
                        ${SONARQUBE_SCANNER_HOME}/bin/sonar-scanner \
                            -Dsonar.projectKey=juice-shop \
                            -Dsonar.sources=. \
                            -Dsonar.host.url=http://192.168.81.128:9000 \
                            -Dsonar.token=YOUR_TOKEN_HERE || true
                    '''
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                echo 'Building Docker Image...'
                // Uncomment below line if Dockerfile exists
                // sh 'docker build -t juice-shop .'
            }
        }
    }

    post {
        always {
            echo 'Cleaning up temporary files...'
            sh 'rm -rf temp_repo dependency-check-report trufflehog_report.txt || true'
        }
    }
}
