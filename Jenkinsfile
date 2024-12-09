pipeline {
    agent any
    environment {
        PATH = "/Library/Frameworks/Python.framework/Versions/3.13/bin:${env.PATH}"
        ANSIBLE_BECOME_PASS = "student" // Замените на ваш пароль
    }
    stages {
        stage('Установка переменной PATH') {
            steps {
                script {
                    env.PATH = "/usr/local/bin:${env.PATH}"
                }
            }
        }
        stage('Проверка Ansible') {
            steps {
                script {
                    sh 'ansible --version'
                }
            }
        }
        stage('Выполнение плейбука Ansible') {
            steps {
                script {
                    // Замените 'your_playbook.yml' на имя вашего плейбука
                    sh 'ansible-playbook -i DevOps/inventory.ini DevOps/prepare-environment.yml --become'
                }
            }
        }
        stage('Запуск приложений') {
            steps {
                script {
                    // Замените 'your_playbook.yml' на имя вашего плейбука
                    sh 'ansible-playbook -i DevOps/inventory.ini DevOps/start_application.yml --become'
                }
            }
        }
    }
    post {
        always {
            echo 'Pipeline завершен.'
        }
        success {
            echo 'Pipeline выполнен успешно.'
        }
        failure {
            echo 'Pipeline завершился с ошибкой.'
        }
    }
}
