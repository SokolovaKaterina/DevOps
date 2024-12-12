pipeline {
    agent any
    environment {
        PATH = "/Library/Frameworks/Python.framework/Versions/3.13/bin:${env.PATH}"
        ANSIBLE_BECOME_PASS = "182713"  // Замените на ваш пароль sudo
    }
    stages {
        stage('Установка переменной PATH') {
            steps {
                script {
                    // Добавляем путь к Ansible в переменную PATH
                    env.PATH = "/usr/local/bin:${env.PATH}"
                }
            }
        }
        stage('Проверка Ansible') {
            steps {
                script {
                    // Проверяем, доступен ли Ansible
                    sh 'ansible --version'  // Теперь просто используем ansible, так как мы добавили путь в PATH
                }
            }
        }
        stage('Выполнение плейбука для подготовки окружения') {
            steps {
                script {
                    // Запускаем плейбук setup-env.yml для подготовки окружения
                    sh 'ansible-playbook -i /home/ekaterina/Lab_3/DevOps/inventory.ini /home/ekaterina/Lab_3/DevOps/prepare_environment.yml --become'
                }
            }
        }
        stage('Запуск приложений') {
            steps {
                script {
                    // Запускаем плейбук deploy-apps.yml для запуска приложений
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
