# SonarQube-Run-on-EC2-Manually
1️⃣ Clone the below reository and install SonarQube and SonarScanner on your EC2:
    https://github.com/harshshahu/SonarQube-And-SonarScanner-Installation-on-EC2.git
  
2️⃣ Follow all steps to install SonarQube and SonarScanner on EC2:
    After installation Login to EC2 and install python, pip, flask, nodejs, java, maven, pip install pytest-cov (if not installed).

3️⃣ URL: http://<EC2-PUBLIC-IP>:9000 (Default sonarQube link):
    Default credentials: admin/admin
    Change password on first login


4️⃣ Generate Authentication Token:
    Login to SonarQube
    Go to: User → My Account → Security → Generate Token
    Save the token securely


5️⃣ Configure Environment Variables:
    copy and export on your EC2:
    Login to your EC2 and type below:
    
    export SONAR_HOST_URL=http://<EC2-PUBLIC-IP>:9000
    export SONAR_TOKEN=<your-sonarQube-generated-token>

  Example:
    export SONAR_HOST_URL=http://52.66.253.129:9000
    export SONAR_TOKEN=sqa_f37afc92c642b3cdff0e6d54942a2a5d469e08fe


6️⃣ Git Clone Repository on EC2:  
    git clone https://github.com/harshshahu/SonarQube-Run-on-EC2-Manually.git


7️⃣ First we will run Java, Python, NodeJS code manually:
    cd SonarQube-Run-on-EC2-Manually
    Java:
    cd java-app/
    now to run java application type:
        javac HelloWorkld.java
        java HelloWorkld.java
        or
        mvn clean compile
        mvn exec:java -Dexec.mainClass="com.example.HelloWorld"
        mvn test
        you will see Output in console.
    Python:
    cd python-app/
    now to run python application type:
        pip install -r requirements.txt
        python hello.py
        pytest test_hello.py
        you will see Output in console.
    NodeJs:
    cd nodejs-app/
    now to run NodeJs application type:
        node index.js
        npm test
        you will see Output in console.


8️⃣ Now we will analyze code with SonarQube:  
    Option 1: Analyze All Applications at Once
        chmod +x analyze-all.sh
        ./analyze-all.sh
    Option 2: Analyze Individual Applications
        *Python:
        cd python-app
        pytest --cov=. --cov-report=xml:coverage.xml
        cd ..
        sonar-scanner \
            -Dsonar.projectKey=helloworld-python \
            -Dsonar.sources=python-app \
            -Dsonar.host.url=$SONAR_HOST_URL \
            -Dsonar.login=$SONAR_TOKEN
            
        *Java:        
        cd java-app
        mvn clean verify sonar:sonar \
            -Dsonar.projectKey=helloworld-java \
            -Dsonar.host.url=$SONAR_HOST_URL \
            -Dsonar.login=$SONAR_TOKEN
            
        *Node.js:        
        cd nodejs-app
        npm run test:coverage
        cd ..
        sonar-scanner \
            -Dsonar.projectKey=helloworld-nodejs \
            -Dsonar.sources=nodejs-app \
            -Dsonar.host.url=$SONAR_HOST_URL \
            -Dsonar.login=$SONAR_TOKEN

