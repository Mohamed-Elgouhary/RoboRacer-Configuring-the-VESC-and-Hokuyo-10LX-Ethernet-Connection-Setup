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

If using the VESC mkIV, e.g. hardware based on VESC 4.12, see [here](https://github.com/Mohamed-Elgouhary/vesc_firmware) for more details on how you can build your firmware for corresponding VESCs, and prebuilt firmware for different VESC hardware versions.

**1. Installing the VESC Tool**

We need to configure the VESC so that it works with our motor and vehicle transmission. Before you start, you’ll need to install the [VESC Tool](https://vesc-project.com/vesc_tool). You’ll have to register for an account to download. Add the free tier tool to cart (you don’t have to fill in any information other than your email.) After checkout, a download link will be sent to your email address. There should be versions of the software for Linux, Windows and macOS.

**2. Powering the VESC**

First we need to power the VESC. Plug the battery in, and make sure the polarity is correct. Note that you don’t need to turn on the Powerboard for configuring the VESC.
