# car-loan-gateway-service
Car loan management

Requirement – Design and implement a Loan Approval Platform (Car Loan)

a.            It should implement KYC
b.            As an end user, I should be able to apply for loan(online)
c.             As a front officer, I should be able to validate the loan request and ask for approval from the car loan department and risk department
d.            As an approving officer, I should be able to approve or reject the loan request
e.            As a risk officer, I should be able to approve or reject a loan application and a risk officers’ decision is final and overrides any other approvers
f.             Based on the final decision, a request should be send to disbursal department to disburse the money


Services – 

1.	KYC service - https://github.com/suniltamoli/kyc-service
2.	Front office service - https://github.com/suniltamoli/front-office-service
3.	Loan officer service -  https://github.com/suniltamoli/loan-service/settings
4.	Risk officer service-  https://github.com/suniltamoli/risk-officer-service
5.	Disbursement service- https://github.com/suniltamoli/disbursement-service

Architecture diagram – 

 


Tech stack – Java, Spring boot, spring framework, Hibernate/JPA, MySQL, Tomcat 
APIs –
KYC : -
1.	Create KYC  - 
URL - http://localhost:8080/kyc-service/v1/carloan/customer/kyc
Method - POST
Header - Content-Type: application/json
Request: - {
  "pan_number": "AEJHG1962J",  
  "personal_details": {
    "first_name":"Sumit",
    "middle_name":"kumar",
    "last_name":"Tamoli",
    "father_name": "B.N. Chaurasia",
    "mother_name": "Krishna",
    "dob" :"10-10-1980",
    "phone":"9899087012",
    "gender": "Male",
    "marital_status": "Married",
    "nationality": "Indian",
    "occupation": "Salaried",
    "sector" : "Private"
  },
  "identity_details": {
    "identity_type" : "PAN",
    "identity_number" : "SEJSsF7293221N"
    
  },
  
  "address_details" : {
    "proof_of_address":"AADHAR",
    "address_proof_id": "320084755213910",
    "address_type": "Permanent",
    "address": {
      "address_line1" : "i 707",
      "address_line2" : " ajnara",
      "address_line3" : "sector-74",
      "city": "noida",
      "postal":"201301",
      "district":"GB Nagar",
      "state" :"up",
      "country":"india"
    }
    
  }
  
}
Response : - {
    "kyc_number": "KYC044687fbb0dd4e8b847ebee54f15e0a5",
    "pan_number": "AEJHG1962J",
    "personal_details": {
        "phone": "9899087012",
        "first_name": "Sumit",
        "middle_name": "kumar",
        "last_name": "Tamoli",
        "father_name": "B.N. Chaurasia",
        "mother_name": "Krishna",
        "dob": "10-10-1980",
        "gender": "Male",
        "marital_status": "Married",
        "nationality": "Indian",
        "occupation": "Salaried",
        "sector": "Private"
    },
    "identity_details": {
        "identity_type": "PAN",
        "identity_number": "SEJSsF7293221N"
    },
    "address_details": {
        "proof_of_address": "AADHAR",
        "address_proof_id": "320084755213910",
        "address_type": "Permanent",
        "address": {
            "address_line1": "i 707",
            "address_line2": " ajnara",
            "address_line3": "sector-74",
            "city": "noida",
            "postal": "201301",
            "district": "GB Nagar",
            "state": "up",
            "country": "india"
        }
    }
}
2.	Get KYC detail by KYC number
1.	URL - http://localhost:8080/kyc-service/v1/carloan/customer/kyc/{kycNumber}
2.	Method – GET
3.	Content-type : application/json


3.	Update KYC by identity Id
a.	URL - http://localhost:8080/kyc-service/v1/carloan/customer/kyc/{identityId}
b.	Method – PUT
c.	Content-type : application/json



Front office Service – 
1.	Loan Approval request – 
•	URL : - http://localhost:8080/front-office-service/v1/carloan/approval
a.	Method – POST
b.	Content-type : application/json

Request – 
	{
  "pan_number": "AMJPT7905N",  
  "vehicle_company" :"Maruti",
  "vehicle_name" : "Swift",
  "vehicle_type" : "4 wheeler",
  "total_price": 19000000,
  "loan_amount": 13000000,
  "down_payment": 1100000,
  "roi": 9.8,
  "financed_by": "hdfc bank",
  "financer_address" : "sec-18, noida",
  "tenure": 10,
  "emi": 10000,
  "kyc_number" : "KYC044687fbb0dd4e8b847ebee54f15e0a5" ,
  "loan_status" : "pending",
  "annual_salary" : 40000000,
  "form_16_received" : true,
  "bank_statement_received": true
  
}

Response – 
	{
    "loan_ref_number": "REF70a474d83b16488db628b0c82f091493",
    "pan_number": "AMJPT7905N",
    "vehicle_company": "Maruti",
    "vehicle_name": "Swift",
    "vehicle_type": "4 wheeler",
    "total_price": 19000000,
    "loan_amount": 13000000,
    "down_payment": 1100000,
    "roi": 9.8,
    "financed_by": "hdfc bank",
    "financer_address": "sec-18, noida",
    "tenure": 10,
    "emi": 10000,
    "kyc_number": "KYC044687fbb0dd4e8b847ebee54f15e0a5",
    "loan_status": "pending",
    "annual_salary": 40000000,
    "form_16_received": true,
    "bank_statement_received": true,
    "approved_by_front_officer": "su007ta",
    "approved_On_by_front_officer": "2020-10-25 19:43:35.496"
}

2.	Check loan status – 
a.	URL -  http://localhost:8080/front-office-service/v1/carloan/details/{loanRefNum}
b.	Method – GET
c.	Content-type : application/json
d.	Response - {
    "loan_ref_number": "REF70a474d83b16488db628b0c82f091493",
    "pan_number": "AMJPT7905N",
    "vehicle_company": "Maruti",
    "vehicle_name": "Swift",
    "vehicle_type": "4 wheeler",
    "total_price": 19000000,
    "loan_amount": 13000000,
    "down_payment": 1100000,
    "roi": 9.8,
    "financed_by": "hdfc bank",
    "financer_address": "sec-18, noida",
    "tenure": 10,
    "emi": 10000,
    "kyc_number": "KYC044687fbb0dd4e8b847ebee54f15e0a5",
    "loan_status": "Approved",
    "annual_salary": 40000000,
    "form_16_received": true,
    "bank_statement_received": true,
    "approved_by_risk_officer": "risk-officer",
    "approved_by_front_officer": "su007ta",
    "approved_On_by_front_officer": "2020-10-25 19:43:35.000",
    "approved_On_by_risk_officer": "2020-10-25 19:43:36.000"
}


Gateway Service – This is the gateway service which route all the request as per path.

Implementation approach: - Considering high volume I tried to build it on microservice based architecture so that individual microservice easily build deploy and scale without any dependency of other micro-service. I build a gateway service which will route all request as per path basis. First, user need to create a KYC by KYC service and the he will be eligible to apply the loan. Once KYC done request come to front officer service which will check and validate loan request by KYC number if we found information by KYC number then will proceed the further processing else decline with error code. If request is valid then push this request in KAFKA topic where this will be listened by risk officer and loan department service and these will process it and push response back to own response KAFKA topic where front office service and disbursement service listen these topic and process their response. After processing disbursement service put response back to disbursement response topic which is listened by front office service and update in DB. 

Steps to run code – 
1.	Download and install KAFKA
2.	Start KAFKA Zookeeper 
a.	./bin/zookeeper-server-start.sh config/zookeeper.properties

3.	Start KAFKA server
a.	./bin/kafka-server-start.sh config/server.properties

4.	Create topics –
a.	DisbursementResponseTopic
b.	DisbursementTopic
c.	LoanOfficerResponseTopic
d.	LoanOfficerTopic
e.	RiskOfficerResponseTopic
f.	RiskOfficerTopic
5.	Setup code in IntelliJ /eclipse and start each microservice.
6.	Then start using via APIs.
