---
layout: post
title: What is CANalyse and how do I control(hack) cars through telegram? (Part — 1)
date: 2021-02-12 00:00:00
categories: [tool]
tags: [tool, CANalyse]
last_modified_at: 2021-02-12
---

#### CANalyse

<figure>
  <img src="assets/img/blogs/2021-02-12/CANalyse_cover.webp" alt="CANalyse — A vehicle network analysis tool!">
  <figcaption>CANalyse — A vehicle network analysis tool!</figcaption>
</figure>


CANalyse is a tool built to analyze the log files to find out unique datasets automatically and able to connect to simple user interfaces such as Telegram. Basically, while using this tool you can provide your bot-ID and be able to use the tool over the internet through telegram.

CANalyse is made to be placed inside a raspberry-PI and able to exploit the vehicle through a telegram bot by recording and analysing the data logs, like a hardware implant planted inside a car which can communicate with the Network bus.

Let’s install the tool, clone the repository from [KartheekLade/CANalyse](https://github.com/KartheekLade/CANalyse), and open your terminal in the CANalyse folder. if you are using it for the first time install the requirements by using the command:

> pip3 install -r requirements.txt

requirements.txt is already provided in the repository and by running the above command it will automatically install all the required libraries used in this tool. Now, you need to run the canalyse_tool.py command:

> python3 canalyse_tool.py

Once you install the requirements and run the tool it should open a menu like this

<figure>
  <img src="\assets\img\blogs\2021-02-12\starting the tool.gif">
</figure>

You have four options,

* CANalyse
* Connect to Telegram
* settings
* Manual - "it’s a manual where it describes the functionality of each option in the


“ CANalyse menu ”

<figure>
  <img src="\assets\img\blogs\2021-02-12\CANalyse options.webp">
</figure>

in the CANalyse menu, you can manually record the source and attack files and analyse them. once you navigate to the “ Play payload “ option you can see all the IDs present in the payload.log on the screen. at this point, you can also play the specific ID from the payload log file also.


<figure>
  <img src="\assets\img\blogs\2021-02-12\payload play options.webp">
</figure>

All that we have done manually can also be done over the internet(telegram). Yep, that's the cool part of the tool. Let’s get started with that, to do that navigate back to the “ Main menu ”.

#### Connect to Telegram:

once you go to the second option you will be asked to give an “ API token ”. you can create your own Telegram bot and get the “ HTTP API token” enter the token into the tool and it will automatically connect with the tool.


<figure>
  <img src="\assets\img\blogs\2021-02-12\Telegram API token.webp">
</figure>

Once you enter your bot “ HTTP API ” ID and it is connected it will show something like this on your terminal.

<figure>
  <img src="\assets\img\blogs\2021-02-12\bot connection with tool.webp">
</figure>

at this point, the tool has successfully connected with your telegram bot and you can go to your bot on telegram and start to see the menu. the menu displays all the functions which can be used through the telegram bot and the data input format.

<figure>
  <img src="\assets\img\blogs\2021-02-12\response on telegram.webp">
</figure>

if you can see the menu it confirms that your bot can communicate with the tool, now lets hover to the seetings menu


<figure>
  <img src="\assets\img\blogs\2021-02-12\CANalyse settings.webp">
</figure>

Comm_channel: you can change the communication protocol.
Interface: you can change the interface here, the library python-can supports various interfaces such as:



- [SocketCAN](https://python-can.readthedocs.io/en/stable/interfaces.html#socketcan): Linux native CAN implementation.
- [Kvaser’s CANLIB](https://python-can.readthedocs.io/en/stable/interfaces.html#kvaser): Kvaser’s CANLIB SDK.
- [CAN over Serial](https://python-can.readthedocs.io/en/stable/interfaces.html#can-serial): CAN interface over serial connection.
- [CAN over Serial / SLCAN](https://python-can.readthedocs.io/en/stable/interfaces.html#slcan): Serial line CAN interface.
- [IXXAT Virtual CAN Interface](https://python-can.readthedocs.io/en/stable/interfaces.html#ixxat): IXXAT Virtual CAN Interface.
- [PCAN Basic API](https://python-can.readthedocs.io/en/stable/interfaces.html#pcan-basic-api): PEAK-System Technik PCAN Basic API.
- [USB2CAN Interface](https://python-can.readthedocs.io/en/stable/interfaces.html#usb2can): USB to CAN interface.
- [NI-CAN](https://python-can.readthedocs.io/en/stable/interfaces.html#ni-can): National Instruments CAN interface.
- [isCAN](https://python-can.readthedocs.io/en/stable/interfaces.html#iscan): isCAN USB to CAN interface.
- [NEOVI Interface](https://python-can.readthedocs.io/en/stable/interfaces.html#neovi): NEOVI USB to CAN interface.
- [Vector](https://python-can.readthedocs.io/en/stable/interfaces.html#vector): Vector CAN interface.
- [Virtual](https://python-can.readthedocs.io/en/stable/interfaces.html#virtual): Virtual CAN interface.
- [CANalyst-II](https://python-can.readthedocs.io/en/stable/interfaces.html#canalyst-ii): CANalyst-II USB to CAN interface.
- [SYSTEC interface](https://python-can.readthedocs.io/en/stable/interfaces.html#systec): SYSTEC CAN interface.
