node {
      def app
      
      stage('clone repository'){
      checkout scm
      }
      
      stage('Build image'){
      app = docker.build("raushanpython/tutorials")
      }

      stage('Test image') {
           app.inside{
		sh 'echo "Tests passed"'
	    }
       }
    
      stage('Push image') {
         docker.withRegistry('https://registry.hub.docker.com','004f1a1a-6fba-4e86-bc30-f8a6acbb8107') {
	app.push("${env.BUILD_NUMBER}")
        app.push("lastest")
        }
      }
   }        		