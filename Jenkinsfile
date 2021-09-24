pipeline {
    
    agent any
    tools {
        maven "MVN_3.8.2"
    }
    parameters{
        string(name:'OPERATION', defaultValue:'package', description: 'Operación maven a realizar')        
    }
    stages{
        stage("Verificación"){
            steps {
                bat "java -version"
                bat "mvn -version"
                echo "Operación a ejecutar por Github: ${params.OPERATION}"
            }
        }

        stage ("Descarga del código y build") {
            steps {
                git "https://github.com/jesuscle/junitmavenexample"
                bat "mvn clean ${params.OPERATION}"
            }
        }
    }
    
    post{
        success{
            junit 'target/surefire-reports/TEST-*.xml'
        }
    }
}

