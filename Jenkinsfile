pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/alexmegua/TestJenkins.git'
                // Проверяем структуру репозитория
                bat 'dir game'  // Выводим содержимое папки game
            }
        }

        stage('Install Dependencies') {
            steps {
                bat 'C:\\Users\\User\\AppData\\Local\\Programs\\Python\\Python313\\python.exe -m pip install pytest'
            }
        }

        stage('Run Tests') {
            steps {
                bat 'C:\\Users\\User\\AppData\\Local\\Programs\\Python\\Python313\\Scripts\\pytest.exe --junitxml=reports/unit.xml tests/test_jumps.py'
                bat 'C:\\Users\\User\\AppData\\Local\\Programs\\Python\\Python313\\Scripts\\pytest.exe --junitxml=reports/ui.xml tests/test_ui.py'
                bat 'C:\\Users\\User\\AppData\\Local\\Programs\\Python\\Python313\\Scripts\\pytest.exe --junitxml=reports/scene.xml tests/scenes_check.py'
                bat 'C:\\Users\\User\\AppData\\Local\\Programs\\Python\\Python313\\Scripts\\pytest.exe --junitxml=reports/characters.xml tests/characters_check.py'
            }
        }

stage('Publish Results') {
    steps {
        script {
            // Примусово публікуємо навіть після помилок
            catchError(buildResult: 'UNSTABLE', stageResult: 'UNSTABLE') {
                junit 'reports/*.xml'
            }
        }
    }
}
    }

    post {
        failure {
            echo 'Build failed. Check logs for details.'  // Отключаем email до настройки SMTP
        }
    }
}
