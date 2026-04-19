# SonarQube-Run-on-EC2-Manually
steps:
1️⃣ Clone the below reository:
    https://github.com/harshshahu/SonarQube-And-SonarScanner-Installation-on-EC2.git
  
2️⃣ Follow all steps to install SonarQube and SonarScanner on EC2.

3️⃣ URL: http://<EC2-PUBLIC-IP>:9000
    Default credentials: admin/admin
    Change password on first login


4️⃣ Generate Authentication Token
    Login to SonarQube
    Go to: User → My Account → Security → Generate Token
    Save the token securely


5️⃣ Configure Environment Variables
    copy and export on your EC2:
    export SONAR_HOST_URL=http://<EC2-PUBLIC-IP>:9000
    export SONAR_TOKEN=<your-sonarQube-generated-token>

  Example:
    export SONAR_HOST_URL=http://52.66.253.129:9000
    export SONAR_TOKEN=sqa_f37afc92c642b3cdff0e6d54942a2a5d469e08fe


6️⃣ Git Clone Repository on EC2:  
    git clone 
Step 4: Run Applications
Python Application
cd python-app
pip install -r requirements.txt
python hello.py
pytest test_hello.py
Java Application
cd java-app
mvn clean compile
mvn exec:java -Dexec.mainClass="com.example.HelloWorld"
mvn test
Node.js Application
cd nodejs-app
npm install
node index.js
npm test
Step 5: Analyze Code with SonarQube
Option 1: Analyze All Applications at Once
chmod +x analyze-all.sh
./analyze-all.sh
Option 2: Analyze Individual Applications
Python:

cd python-app
pytest --cov=. --cov-report=xml:coverage.xml
cd ..
sonar-scanner \
    -Dsonar.projectKey=helloworld-python \
    -Dsonar.sources=python-app \
    -Dsonar.host.url=$SONAR_HOST_URL \
    -Dsonar.login=$SONAR_TOKEN
Java:

cd java-app
mvn clean verify sonar:sonar \
    -Dsonar.projectKey=helloworld-java \
    -Dsonar.host.url=$SONAR_HOST_URL \
    -Dsonar.login=$SONAR_TOKEN
Node.js:

cd nodejs-app
npm run test:coverage
cd ..
sonar-scanner \
    -Dsonar.projectKey=helloworld-nodejs \
    -Dsonar.sources=nodejs-app \
    -Dsonar.host.url=$SONAR_HOST_URL \
    -Dsonar.login=$SONAR_TOKEN

