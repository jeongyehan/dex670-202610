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
- curl -ik -X PUT -H "Content-Type: application/json" -d "{\"lastName\":\"Mule\",\"numBags\":2}" https://localhost:8081/api/v1/tickets/PNR123/checkin
- cd $PROJECT_HOME
- cp -r $STUDENT_FILE/walkthroughs/devint/module01/wt1-4_starter/paypal-sapi $PROJECT_HOME/.
- cd $PROJECT_HOME/paypal-sapi
- mvn clean verify -U -Dencrypt.key=secure12345 -DskipTests=true
- curl -i -X POST -H "Accept: application/json" -H "Accept-Language:en_US" -u "APP-80ANYAIRLINE8184JT3:1929FHDUAL8392K9ABKSNMM" -d "grant_type=client_credentials" https://training-paypal-fake-api-sandbox-mjf1rw.5sc6y6-1.usa-e2.cloudhub.io/v1/oauth2/token
- export atoken=8s9kaj3.SDkkd4145_ZsrqVh38sjdhNsqrEU9xem4QJ6sQa36VHfyuBes
- curl -i -X POST -H "Content-Type: application/json" -H "Authorization: Bearer $atoken" -d "{\"intent\":\"sale\", \"payer\": {\"payment_method\":\"paypal\"}, \"transactions\":[{\"amount\":{\"total\":\"80.00\", \"currency\":\"USD\"}, \"description\": \"Check-In Baggage.\", \"custom\": \"ANYAIRLINE_90048630024435\",\"invoice_number\": \"48787589673\", \"payment_options\":{\"allowed_payment_method\":\"INSTANT_FUNDING_SOURCE\"},\"soft_descriptor\":\"ANYAIRLINE BAGGAGE\"}], \"note_to_payer\":\"Behappy.\"}" https://training-paypal-fake-api-sandbox-mjf1rw.5sc6y6-1.usa-e2.cloudhub.io/v1/payments/payment
- curl -ik -X POST -H "Content-Type: application/json" -d "{\"amount\":12.34, \"description\": \"something\"}" https://localhost:8081/api/v1/payments
- curl -ik -X PUT -H "Content-Type: application/json" -d "{\"payerID\":\"STJ8222K092ST\"}" https://localhost:8081/api/v1/payments/PAY-1B56960729604235TKQQIYVY/approval
- cd $PROJECT_HOME
- cp -r $STUDENT_FILE/walkthroughs/devint/module01/wt1-5_starter/flights-management-sapi $PROJECT_HOME/.
- cd $PROJECT_HOME/flights-management-sapi
- mvn clean verify -U -Dencrypt.key=secure12345 -DskipTests=true
- curl -ik -X PUT -H "Content-Type: application/json" -d "{\"lastName\":\"Mule\",\"numBags\":2}" https://localhost:8081/api/v1/tickets/PNR123/checkin
- cd $PROJECT_HOME
- mvn install:install-file -Dfile=bom/pom.xml -DpomFile=bom/pom.xml
- mvn install:install-file -Dfile=parent-pom/pom.xml -DpomFile=parent-pom/pom.xml
- cd $PROJECT_HOME/apps-commons
- mvn clean install
- cd $PROJECT_HOME/bom
- mvn deploy -f pom.xml -Pdeploy-to-exchange-v3
- cd $PROJECT_HOME/parent-pom
- mvn deploy -f pom.xml -Pdeploy-to-exchange-v3
- cd $PROJECT_HOME/apps-commons
- mvn deploy -f pom.xml
- curl -ik -H "Content-Type:text/xml" -d "<CancellationNotification><PNR>PNR123</PNR><PassengerLastName>Mule</PassengerLastName></CancellationNotification>" https://localhost:8081/api/cancelFlight
- curl -ik -H "Content-Type:text/plain" -d "invalid content type and content" https://localhost:8081/api/cancelFlight
- curl -ik -H "Content-Type:text/xml" -d "<CancellationNotification><PNR>DEX670-202610</PNR><PassengerLastName>Jeong</PassengerLastName></CancellationNotification>" https://localhost:8081/api/cancelFlight
- cp -r $STUDENT_FILE/walkthroughs/devint/module02/wt2-4_starter/mobile-notifications-eapp $PROJECT_HOME/.
- cd $PROJECT_HOME/mobile-notifications-eapp
- mvn clean verify -U -Dencrypt.key=secure12345 -DskipTests=true

