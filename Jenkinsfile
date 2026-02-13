pipeline {
    agent any

    environment {
        COMPOSE_PROJECT_NAME = "project"
    }

    stages {

        stage('Create Root Env File') {
            steps {
                sh '''
                cat <<EOF > .env
POSTGRES_USER=kogo
POSTGRES_PASSWORD=math1106
POSTGRES_DB=mydb

DBNAME=mydb
DBUSER=kogo
DBPASSWORD=math1106
DBHOST=db
DBPORT=5432

DJANGO_SECRET_KEY=django-secret
DJANGO_DEBUG=False
DJANGO_ALLOWED_HOSTS=localhost,127.0.0.1,3.35.194.215
CORS_ALLOWED_ORIGINS=http://localhost,http://127.0.0.1,http://3.35.194.215

NEXT_PUBLIC_API_BASE_URL=/api
EOF
                '''
            }
        }

        stage('Build & Deploy') {
            steps {
                sh '''
                set -e
                echo "🚀 Deploy start"

                docker-compose down || true
                docker-compose build --no-cache
                docker-compose up -d

                echo "✅ Deploy finished"
                '''
            }
        }
    }
}
