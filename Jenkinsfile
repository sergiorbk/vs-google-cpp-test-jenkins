pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git(
                    branch: 'main',
                    url: 'https://github.com/sergiorbk/vs-google-cpp-test-jenkins.git',
                    credentialsId: 'gh-repo-http-access-token-vs-google-cpp-test-jenkins'
                )
            }
        }
        
        stage('Build') {
            steps {
                // Збірка проекту з Visual Studio
                // template: bat '"path to MSBuild" test_repos.sln /t:Build /p:Configuration=Release'
                bat '"E:\\Programs\\VS\\Community\\MSBuild\\Current\\Bin\\MSBuild.exe" 
                    test_repos.sln /t:Build /p:Configuration=Release'
            }
        }

        stage('Test') {
            steps {
                // Команди для запуску тестів
                bat "x64\\Debug\\test_repos.exe --gtest_output=xml:test_report.xml"
            }
        }
    }

    post {
    always {
        // Publish test results using the junit step
        // Specify the path to the XML test result files
        junit 'test_report.xml'
    }
}
}