In this project, I have demonstrated the simulation of a Hand Gesture Controlled Drone using Computer Vision. The drone is fully controlled using different hand gestures, with real-time hand tracking powered by OpenCV and Mediapipe. The estimated hand landmarks are processed to generate the control commands which is then sent to the simulated drone. The flight control is handled via DroneKit on a simulated environment using SITL and ArduPilot. The target waypoint of the actual drone is mapped according to the position of the virtual copter which is dragged virtually using the finger tip. Again, the virtual zone is mapped to a physical space of 80mx80m. As a result, the drone will not go beyond this area.

🚁 Features:

1. Hand gesture-based takeoff, altitude control, and RTL (Return to Launch).
2. Dynamic movement of the drone in physical space mapped  based on the position of the virtual copter which is dragged with the finger tip within the virtual zone. 

📌Continuous Navigation Gestures: 
1. Take Off - Left Hand Thumb
2. Climb - Left Hand Victory Sign 
3. Descend - Left Hand Rock On
4. XY Plane -  Dragging Using the Middle Finger of Right Hand
5. RTL - Left Hand 5 Fingers

📌Discrete Navigation Gestures: 

1. Take Off - Right Hand Thumb
2. Climb - Right Hand Victory Sign 
3. Descend - Right Hand Rock On
4. Forward -  Left Hand Victory Sign
5. Right -  Right Hand (Thumb+Index) 
6. Left -  Left Hand (Thumb+Index)
7. RTL -  Right Hand 5 Fingers

Check this video for environment configuration: https://youtu.be/_AkhfvExsOc

DroneKit is a popular python package that allows you to program your drone using a low latency link. Flight controllers are limited to make artificial perception or intelligence based decisions. In this perspective, DroneKit adds intelligence to vehilcle's behaviour and perform tasks that are computationally intensive or time-sensitive (for example, computer vision, path planning, or 3D modelling). It is compatible with vehicles that communicate using the MAVLink protocol (including most vehicles made by 3DR and other members of the DroneCode foundation). It runs on Linux, Mac OS X, or Windows. 

For more information, check the following link:  https://dronekit-python.readthedocs.io/en/latest/about/index.html

My Environment: 

1. Python 3.9
2. DroneKit 2.9.2
3. DroneKit - SITL 3.3.0
4. MAVProxy 1.8.71
5. Pymavlink 2.4.43

Step: 01: Install the required packages: 
pip install dronekit dronekit-sitl mavproxy 

Step: 02: Fix the bug with Pymavlink:
a. Go to your site packages and open pymavlink folder
b. Open pymavutil.py file
c. Find the fucntion set_mode_apm and Comment out the following section: 

        # self.mav.command_long_send(self.target_system,
        #                            self.target_component,
        #                            mavlink.MAV_CMD_DO_SET_MODE,
        #                            0,
        #                            mavlink.MAV_MODE_FLAG_CUSTOM_MODE_ENABLED,
        #                            mode,
        #                            0,
        #                            0,
        #                            0,
        #                            0,
        #                            0)

d. Replace it by the following section and save the file: 

self.mav.set_mode_send(self.target_system, 
                                   mavlink.MAV_MODE_FLAG_CUSTOM_MODE_ENABLED,
                                   mode,
                                   )

Step: 03: Open a new terminal and run:  dronekit-sitl copter --home=23.4613785,91.1767227,10,270

Step: 04: Open another new terminal and run:  python3.9 -m MAVProxy.mavproxy --master tcp:127.0.0.1:5760 --sitl 127.0.0.1:5501 --out 127.0.0.1:14550 --out 127.0.0.1:14551 --out 127.0.0.1:14552

Step: 05: Connect Ardupilot on the UDP link and run the pyscript to check the simulation. 

Quadcopter Specifications:

1. S500 Quadcopter Frame.
2. Radiolink Pixhawk Flight Controller.
3. Radiolink SE100 M10N GPS.
4. FlySky FS-i6S Radio Transmitter with FS-iA10B Receiver.
5. HTIRC Hummingbird Dshot 20A ESC.
6. DJI 2212/920KV BLDC Motors.
7. 3S 60C 3200mAh Lipo Battery.
8. 4S 40C 4000mAh SAMSUNG(Original) 21700 Li-Ion Battery Pack (Custom Made).
9. DJI 1045 10" Self Locking Propeller.
10. Imax B6 AC 80W Charger.
11. ESP8266 Based WiFi Telemetry.
12. Cell Checker.
