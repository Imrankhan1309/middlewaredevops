pipeline { agent any

stages {
    stage('Checkout') {
        steps {
            echo 'Checking out middlewaredevops repository...'

            git branch: 'main',
                url: 'https://github.com/Imrankhan1309/middlewaredevops.git'
        }
    }

    stage('Find WAR Files') {
        steps {
            sh '''
                echo "Checking WAR files..."
                find . -maxdepth 1 -name "*.war" -ls
            '''
        }
    }

    stage('Deploy to Tomcat') {
        steps {
            sh '''
                TOMCAT_WEBAPPS="/opt/tomcat/webapps"

                if [ ! -d "$TOMCAT_WEBAPPS" ]; then
                    echo "Tomcat webapps directory not found!"
                    exit 1
                fi

                for WAR_FILE in benefits.war contacts.war messaging.war testds.war timeoff.war
                do
                    if [ -f "$WAR_FILE" ]; then
                        echo "Deploying $WAR_FILE"
                        cp "$WAR_FILE" "$TOMCAT_WEBAPPS/"
                    else
                        echo "ERROR: $WAR_FILE not found"
                        exit 1
                    fi
                done

                echo "All five WAR files copied successfully!"
            '''
        }
    }
}


}
