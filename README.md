# AWS Lambda
## **AWS Lambda Trigger**


**AWS Lambda** is a serverless computing service offered by Amazon Web Services.  
It allows you to run your code automatically whenever a specific event occurs — for example, when data is uploaded to an S3 bucket, when an IoT device sends data, or when a request is made through an API.  
You don’t have to manage servers or handle scaling; AWS takes care of everything automatically.  

---

### **Key Concepts**

- **Serverless:** No need to create or maintain servers.  
- **Event Driven:** Executes automatically when triggered by events (IoT data, S3 upload, API call, etc.).  
- **Automatic Scaling:** Handles any number of events instantly.  
- **Pay per Use:** You are charged only when your function runs.  
- **Multi-language Support:** Works with Python, Node.js, Java, and more.  

---

### **How Lambda Works**

1. An event (for example, IoT device data) triggers the Lambda function.  
2. AWS runs the function automatically in a fully managed environment.  
3. Your function processes the input, performs a task, and returns the output.  
4. If multiple events occur, Lambda automatically scales up to handle all of them at once.  

---

### **Example: IoT Data Alert System**

In this project, AWS Lambda is used to process IoT sensor data.  
When a device sends temperature readings to **AWS IoT Core**, Lambda checks the value.  
If the temperature is higher than a set limit, the function publishes an alert message to a topic named **`alerts/temperature`**.  

---

### **Python Example Code**

```
import json
import boto3

iot_client = boto3.client('iot-data', region_name='ap-south-1')

def lambda_handler(event, context):
    temp = event.get("temperature", 0)
    if temp > 35:
        alert_msg = {
            "alert": "High temperature detected!",
            "value": temp,
            "deviceId": event["deviceId"]
        }
        iot_client.publish(
            topic="alerts/temperature",
            qos=1,
            payload=json.dumps(alert_msg)
        )
    return {"status": "processed"}
```
 ## **Ouput**


<img width="1890" height="469" alt="image" src="https://github.com/user-attachments/assets/cba3b136-2200-40b6-b42a-e5effeb74fdb" />

<img width="1852" height="858" alt="image" src="https://github.com/user-attachments/assets/be4e17d9-d0ba-4a94-932a-01674ccdcd68" />
<img width="1919" height="844" alt="image" src="https://github.com/user-attachments/assets/b4431aaa-69ea-400d-8324-2f9f9f9ff2e0" />
<img width="1921" height="813" alt="image" src="https://github.com/user-attachments/assets/1c80aaee-272f-4f8e-bd18-be583ab90732" />



## **Common Use Cases**

Processing IoT or sensor data in real time

Running background automation tasks

Handling image or file uploads from S3

Building APIs using Lambda with API Gateway

Performing scheduled jobs via CloudWatch Events
