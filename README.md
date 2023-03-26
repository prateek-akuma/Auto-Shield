# Auto-Shield
It is an IoT Project, For car Protection and also to enhance user experience using Node-Red, Grafana and Raspberry Pi.


Go through this readme file for implementing and testing the Auto-Shield Prototype.


For Implementing:


Components Needed:
* Raspberry pi (For implementing the prototype)
* Ultrasonic Sensor  (For to know if there is any moment inside the car within a range( 20cm))
* Camera (if there is a person inside the car it will capture his/her image for user Authentication)
* Angle Rotary Sensor (To demonstrate speed of the car, as we don’t have real car)


After acquiring the above components, connect the components to the raspberry pi. (ultrasonic to D5, Angle Rotary to A2)


Turn on the raspberry pi and install node-red, Influx DB, Grafana. And also enable the camera of raspberry pi through configurations.


On the Microsoft Azure we use 2 custom vision services
API key for User Authentication:
* URL:https://userauth-prediction.cognitiveservices.azure.com/customvision/v3.0/Prediction/e4dab08b-bad9-41f0-a7cb-19f172fa8d70/classify/iterations/Iteration3/image
API keys for User Consciousness:
* URL:https://fatigue-prediction.cognitiveservices.azure.com/customvision/v3.0/Prediction/572bd4e3-990e-4b18-a827-69bf54e2302a/classify/iterations/Iteration3/image
API key for Knowing the city:
* URL:http://ip-api.com/json


Captured images will be stored in raspberry pi
* Authentication check image  : /usr/share/grafana/public/images/user.jpg
* Consciousness check image: /home/pi/Desktop/car/user.png


Next open node-red and import the flow, also connect the sensors to the corresponding ports. 
also import grafana flow in grafana


Finally deploy the Flow.


For Testing the Prototype:

Set the prototype in front, besides the steering.


* If the person is inside the car( or say in a range of 30-40 cm), it triggers the camera.
* And camera captures the image of person and sends to Azure Custom Vision model which will return, whether the person is authenticated or not
* If he/she is not Authenticated, the Car Buzzer will go off and also owner of the car will be notified.
*  If he/she is Authenticated, then the engine will turn on and trigger the camera to continuously capture the images of the user to determine whether the person is alert or not while driving. 
* If the person fall asleep while driving, it will alert the person so that the person can come to consciousness
* Also the prototype monitors the speed of the car for every 5 minutes, if the avg if higher than 40 miles, this will be recorded and also the frequency of user falling asleep will be recorded
* These recorded values will be sent to State DMVs which gives a penalty to the users license and with the increase in points the insurance of car will also increases.
* Stop Engine with node-red Dashboard.
