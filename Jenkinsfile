pipeline {
   agent {
       docker {
           image 'papitoio/robotwd'
           args '--network=skynet'
       }
   }

   stages {
      stage('Build') {
         steps {
            echo 'Baixando as depedências do projeto'
            sh 'pip install -r requirements.txt'
         }
      }
      stage('Test') {
         steps {
            echo 'Executando testes de regressão'
            input(message: 'Aguarge!!!', ok: 'Proseguir')
            sh 'robot -d ./logs -i login tests/'
         }
         post {
            always {
               robot 'logs'
            }
         }
      }
      stage('UAT') {
         steps {
            echo 'Aprovação dos testes de aceitação' 
         } 
      }
      stage('Production') {
         steps {
            echo 'WebApp Ok em produção!'
         } 
      }
   }
}
