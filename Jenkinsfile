pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Git Information') {
            steps {
                sh '''
                    echo "=== Git version ==="
                    git --version

                    echo "=== Branch ==="
                    git branch

                    echo "=== Last commit ==="
                    git log -1 --oneline
                '''
            }
        }

        stage('Ansible Syntax Check') {
            steps {
                sh '''
                    /usr/bin/ansible-playbook \
                      -i inventory/hosts.ini \
                      site.yml \
                      --syntax-check
                '''
            }
        }

        stage('Ansible Lint') {
            steps {
                sh '''
                    /opt/ansible-lint-venv/bin/ansible-lint .
                '''
            }
        }
    }
}
