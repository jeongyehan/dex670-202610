# Anypoint Platform Development: Production-Ready Integrations - DEX670

## Local Path
- PROJECT_HOME=/Users/yehan.jeong/Desktop/dex670-202610
- STUDENT_FILE=/Users/yehan.jeong/Desktop/CDEV-DEX670-EN-28apr2026-Student-Files

## Anypoint Platform Information
- Mule Account: yehan202610

### Business Group
- Business Group ID: b4840237-a86b-4fa4-b4ce-bebf5b0daf00

### Connected App
- Exchange Viewer ID: 2f8f6f9f3e9445ff8b224abefc26dbc8
- Exchange Viewer Secret: 83CcCFA3402e451D969A915Ef43ca567
- Exchange Contributor ID: 36e277ead54e4abeb7ce07f0eaeef6fb
- Exchange Contributor Secret: fA57Ab77103c4023babF5b37337be688

## Commands
- export PROJECT_HOME=/Users/yehan.jeong/Desktop/dex670-202610
- export STUDENT_FILE=/Users/yehan.jeong/Desktop/CDEV-DEX670-EN-28apr2026-Student-Files
- echo $PROJECT_HOME
- echo $STUDENT_FILE
- cp $STUDENT_FILE/etc/settings.xml ~/.m2/
- cd $PROJECT_HOME
- mkdir bom
- mkdir parent-pom
- cp $STUDENT_FILE/walkthroughs/devint/module01/wt1-1_starter/bom/pom.xml ./bom/pom.xml
- cp $STUDENT_FILE/walkthroughs/devint/module01/wt1-1_starter/parent-pom/pom.xml ./parent-pom/pom.xml
- cd $PROJECT_HOME
- mvn install:install-file -Dfile=bom/pom.xml -DpomFile=bom/pom.xml
- mvn install:install-file -Dfile=parent-pom/pom.xml -DpomFile=parent-pom/pom.xml
- cd $PROJECT_HOME
- cp -r $STUDENT_FILE/walkthroughs/devint/module01/wt1-1_starter/apps-commons ./
- cd $PROJECT_HOME/apps-commons
- mvn clean install
- cd $PROJECT_HOME
- cp -r $STUDENT_FILE/walkthroughs/devint/module01/wt1-1_starter/check-in-papi ./
- cd $PROJECT_HOME/check-in-papi
- mvn clean verify -U -Dencrypt.key=secure12345 -DskipTests=true
- curl -ik -X PUT -H "Content-Type: application/json" -d "{\"lastName\" :\"Smith\",\"numBags\":2}" https://localhost:8081/api/v1/tickets/PNR123/checkin
- curl -ik -X PUT -H "Content-Type: application/json" -d "{\"payerID\": \"STJ8222K092ST\", \"paymentID\": \"PAY-1AKD7482FAB9STATKO\"}" https://localhost:8081/api/v1/tickets/N123/paymentApproval
- curl -ik https://localhost:8081/alive
- curl -ik https://localhost:8081/ready
