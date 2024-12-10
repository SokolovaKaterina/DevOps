pipeline {
    agent any
    environment {
        PATH = "/Library/Frameworks/Python.framework/Versions/3.13/bin:${env.PATH}"
        ANSIBLE_BECOME_PASS = "182713" // Замените на ваш пароль
    }
    stages {
        stage('Установка переменной PATH') {
            steps {
                script {
                    env.PATH = "/usr/bin:${env.PATH}"
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
                    sh 'ansible-playbook -i /home/ekaterina/Lab_3/DevOps/inventory.ini /home/ekaterina/Lab_3/DevOps/prepare_environment.yml --become'
                }
            }
        }
        stage('Запуск приложений') {
            steps {
                script {
                    // Замените 'your_playbook.yml' на имя вашего плейбука
                    sh 'ansible-playbook -i /home/ekaterina/Lab_3/DevOps/inventory.yml /home/ekaterina/Lab_3/DevOps/start_application.yml --become'
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
