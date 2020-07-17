# Messaging-System-Using-MQTT-

# SUBSCRIBE MODULE :-
import paho.mqtt.client as mqttClient
import time
broker_address= "15.206.119.242"  
port = 1883                       
topic1 = "set"
instance = "sub 2"	
print( "topic :",topic1)
print( "IP:",broker_address)
print( "Instance:",instance)

def on_connect(client, userdata, flags, rc):
    if rc == 0:
        print("Connected to broker")
        global Connected               
        Connected = True              
    else:
        print("Connection failed")

def on_message(client, userdata, message):
    print ("Received Message: "  + message.payload)
Connected = False  
client = mqttClient.Client(instance)              
client.on_connect= on_connect                   
client.on_message= on_message                     
client.connect(broker_address, port=port)         

client.loop_start()        
while Connected != True:   
    time.sleep(0.1)

client.subscribe(topic1)
try:
    while True:
       	 time.sleep(1)
except KeyboardInterrupt:
   	 print( "exiting")
  	  client.disconnect()
   	 client.loop_stop()



# PUBLISH MODULE :
import paho.mqtt.client as mqtt #import the client1
import time
broker_address= "15.206.119.242"  #Broker addre$
port = 1883
instance = "Pub 2"
topic = "set"
client = mqtt.Client(instance) 
client.connect(broker_address, port=port) 
time.sleep(1)
msg="a"
while msg !="end":
        msg=raw_input("Type something : ")
        client.publish(topic,msg) 
time.sleep(1)
