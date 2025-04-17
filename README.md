# 1. Configuring the VESC

**Important Safety Tips**

- Put your car on an elevated stand so that its wheels can turn without it going anywhere. If you don’t have an RC car stand, you can use the box that came with your Jetson.
- Make sure you hold on to the car while testing the motor to prevent it from flying off the stand.
- Make sure there are no objects (or people) in the vicinity of the wheels while testing.
- Use a fully-charged LiPO battery instead of a power supply to ensure the motor has enough current to spin up.

**Equipment Required:**

- Fully built RoboRacer vehicle.
- Box or Car [stand](https://www.amazon.com/Duratrax-Tech-Deluxe-Truck-Stand/dp/B0014T74MS/ref=sr_1_6?keywords=rc%2Bcar%2Bjack&link_code=qs&qid=1584393402&sr=8-6&th=1) to put vehicle on.
- Laptop/computer (does not need to be running Linux).

**Approximate Time Investment:** 1 hour

**Note**

If using the VESC mkIV, e.g., hardware based on VESC 4.12, see [here](https://github.com/Mohamed-Elgouhary/vesc_firmware) for more details on how you can build your firmware for corresponding VESCs, and prebuilt firmware for different VESC hardware versions.

**1. Installing the VESC Tool**

We need to configure the VESC so that it works with our motor and vehicle transmission. Before you start, you’ll need to install the [VESC Tool](https://vesc-project.com/vesc_tool). You’ll have to register for an account to download. Add the free tier tool to the cart (you don’t have to fill in any information other than your email). After checkout, a download link will be sent to your email address. There should be versions of the software for Linux, Windows, and macOS.

**2. Powering the VESC**

First, we need to power the VESC. Plug the battery in, and make sure the polarity is correct. Note that you don’t need to turn on the Powerboard for configuring the VESC.

![vesc01](https://github.com/user-attachments/assets/eb1be3ec-2ea5-4ef6-9da7-385947f84a4c)

Next, unplug the USB cable of the VESC from the Jetson NX and plug the USB into your laptop that’s running the VESC Tool. You may want to use a longer cable.

![vesc02](https://github.com/user-attachments/assets/5f1f364e-56fc-48e4-af8c-f72023edb0f5)

**3. Connecting the VESC to Your Laptop**

Launch the VESC Tool. On the Welcome page, press the AutoConnect button on bottom left of the page. After the VESC is connected, you should see an updated status on the bottom right of the screen.

![image](https://github.com/user-attachments/assets/9b9594ba-0687-40cf-8b30-bb04d367fd49)

**4. Updating the Firmware on the VESC**

The first thing you’ll need to do is update the firmware onboard the VESC. Depending on the version of the VESC tool you’re using, you’ll need to go through different steps to enable servo out from the PPM port on the VESC.

With VESC Tool versions released after Mar. 31, 2021, you can use the latest default firmware. And to enable servo out, go to App Settings > General > Enable Servo Output in the VESC Tool to enable servo out.

![image](https://github.com/user-attachments/assets/8277efbe-efba-43c5-8e68-cc1d3471e924)

Before VESC Tool version 2.05, you could enable servo out by using a non-default firmware. On the left side of the screen, click on the Firmware tab. On the bottom left of the page, check the Show non-default firmwares check box. On the right, you should see extra firmware options show up. Select the VESC_servoout.bin option. Afterwards, on the bottom right of the page, press the button with the down arrow to update the firmware on the connected VESC. A status bar at the bottom of the page will show firmware update status. After it’s finished, follow the prompt on screen.

![image](https://github.com/user-attachments/assets/fce508b7-6d8d-485c-9482-1b1b0e0ff884)

**5. Uploading the Motor Configuration XML**

After firmware update, Select Load Motor Configuration XML from the drop-down menu and select the provided XML file from [here](https://drive.google.com/file/d/1-KiAh3hCROPZAPeOJtXWvfxKY35lhhTO/view). After the XML is uploaded, click on the Write Motor Configuration button (the button with a down arrow and the letter M) on the right side of the screen to apply the motor configuration. Note that in the future, you’ll have to press this button whenever you make a change in motor configuration.

![image](https://github.com/user-attachments/assets/257564be-b1d6-4a89-b5cb-70d6713c29af)

**6. Detecting and Calculating Motor Parameters**

To detect and calculate the FOC motor parameters, navigate to the FOC tab under Motor Settings on the left. At the bottom of the screen, follow the direction of the arrows and click on the four buttons one by one, and follow the on-screen prompt. Note that during the measuring process, the motor will make noise and spin; make sure the wheels of your vehicle are clear.

![image](https://github.com/user-attachments/assets/e2c376fa-e948-4a3e-bdec-63aeefa4500b)

After the motor parameters are measured, the fields at the bottom of the screen should turn green. Click on the Apply button, and click the Write Motor Configuration button.

![image](https://github.com/user-attachments/assets/2e4db734-e7d7-4cc7-a636-c8a19243b967)

**7. Changing the Openloop Hysteresis and Openloop Time**

Navigate to the Sensorless tab at the top of the screen. Change the Openloop Hysteresis and Openloop Time to 0.01, and click the Write Motor Configuration button.

![image](https://github.com/user-attachments/assets/8c8cb4a8-b005-406c-953f-5392b42cd634)

**8. Tuning the PID controller**

Now you can start tuning the speed PID controller. To see the RPM response from the motor, navigate to the Realtime Data tab under Data Analysis on the left. Click the Stream Realtime Data button on the right (the button with letters RT), and navigate to the RPM tab on the top of the screen. You should see RPM data streaming now.

![image](https://github.com/user-attachments/assets/0d833a8d-5395-4cad-9cdd-56a836277fd6)

To create a step response for the motor, you can set a target RPM at the bottom of the screen (values between 2000 - 10000 RPM). Click the play button next to the text box to start the motor. Note that the motor will spin, so make sure the wheels of your vehicle are clear from objects. Click the Anchor or STOP button to stop the motor.

![image](https://github.com/user-attachments/assets/2532c0f5-3bcf-4b1f-a7d1-5dcd35bbfc3d)

You want to look for a clean step response that has a quick rise time and zero to very little steady-state error. Adjust the gains accordingly by navigating to the PID Controllers tab under Motor Settings on the left, and changing the Speed Controller gains. General rules of tuning PID gains apply. If you’re seeing a lot of oscillations, try changing the Speed PID Kd Filter.

![image](https://github.com/user-attachments/assets/f0b9de3b-1c0a-4f05-9a93-32461bee08ed)

**9. Changing the hardware speed limit**

By default, the motor configuration sets a safe top motor RPM. If you wish to change the hard limit set by the VESC firmware, you can go to Motor Settings > General and change the max ERPM for forward and backwards rotations. You’ll also have to change the configuration file mentioned in the Odometry Tuning section in the software stack setup to change the software limit for your motor ERPM.

![image](https://github.com/user-attachments/assets/aadc9ec2-66c4-42a6-a253-1abec0a36e1a)

# 2. Hokuyo 10LX Ethernet Connection Setup¶

**Note**

If you have a 30LX or a LIDAR that connects via USB, you can skip this section.

**Equipment Required:**

- Fully built RoboRacer vehicle with a Hokuyo 10LX lidar.
- Pit/Host Laptop OR.
- External monitor/display, HDMI cable, keyboard, mouse.

**Approximate Time Investment:** 30 minutes

Connect to the Jetson NX either via SSH or a wired connection (monitor, keyboard, mouse).

In order to utilize the 10LX, you must first configure the eth0 network. From the factory, the 10LX is assigned the following IP: `192.168.0.10`. Note that the lidar is on subnet 0.

Open Network Configuration in the Linux GUI on the Jetson NX. In the IPv4 tab, add a route such that the eth0 port is assigned

- IP address `192.168.0.15`
- Subnet mask is `255.255.255.0`
- Gateway is `192.168.0.10`

Call the connection Hokuyo. Save the connection and close the network configuration GUI.

When you plug in the 10LX, make sure that the Hokuyo connection is selected. If everything is configured properly, you should now be able to ping `192.168.0.10`.


# References:
[Roboracer Official Website](https://roboracer.ai/)
