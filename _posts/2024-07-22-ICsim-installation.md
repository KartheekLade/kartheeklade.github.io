---
layout: post
title: How to install ICSim in ubuntu / kali 
date: 2024-07-12 00:00:00
categories: [tool]
tags: [tool, ICSim]
last_modified_at: 2024-07-22
---

```
  Note : All the required information to install ICSim is availiable on official github repository by Craigsmith and contributors of ICSim, Incase if you're looking for a step by step guidance please follow below. 
```
### ICSim

[ICsim](https://github.com/zombieCraig/ICSim) (Instrument Cluster Simulator) is a tool used for simulating a CAN bus environment, particularly the interaction between different Electronic Control Units (ECUs) in a vehicle. It provides a graphical interface to simulate an instrument cluster, allowing users to visualize and interact with CAN messages in real-time.

### Key Features of ICsim:
1. **Simulation Environment**: ICsim connects to a virtual CAN bus environment where users can simulate various vehicle functions by sending and receiving CAN messages.
2. **Instrument Cluster Display**: It includes a graphical instrument cluster display that reacts to CAN messages, showing changes in speed, Incators and Doors according to their respective signals.
3. **Real-Time Interaction**: Users can send CAN messages to the simulated environment and observe real-time responses on the instrument cluster.
4. **CAN Message Injection**: ICsim can be used in combination with tools like `python-can` to inject custom CAN messages for testing and development purposes.

### Typical Use Cases:
- **Educational Purposes**: It serves as a learning tool for those studying automotive systems and CAN bus communication.
- **Cybersecurity Testing**: It allows cybersecurity professionals to test various attack vectors on a simulated vehicle network.

### Setup:
To use ICsim, you typically need to set up a virtual CAN interface using tools like `vcan0` and then run the ICsim application to visualize the instrument cluster.ICsim can be integrated with Python scripts using the `python-can` library to automate CAN message sending and receiving. 

we will also be installing [can-utils](https://github.com/linux-can/can-utils) along with the libsdl2-dev, libsdl2-image-dev these package contains the development files for the Simple DirectMedia Layer (SDL) version 2, which is a cross-platform library used for handling graphics, sound, and input, the development files for SDL_image, an image file loading library that loads images as SDL surfaces.

Along with the above dependenceis we will be using `Meson` an open-source build system for building the projec.

### Steps to Install ICSim:

1. Install the dependencies
  ```
    sudo apt-get install libsdl2-dev libsdl2-image-dev can-utils
  ```
  <figure>
    <img src="\assets\img\blogs\2024-07-22\depedecies" alt="Install the dependencies">
    <figcaption>Install the dependencies</figcaption>
  </figure>

2. Install 'Meson'
  ```
    sudo apt install meson
  ```
  <figure>
    <img src="\assets/img/blogs/2024-07-22/meson" alt="Install Meson">
    <figcaption>meson isntallation</figcaption>
  </figure>

3 Clone the repository
  ```
    git clone https://github.com/zombieCraig/ICSim
  ```
  <figure>
    <img src="\assets/img/blogs/2024-07-22/repo" 
      alt="Clone the repositore">
    <figcaption>clone the repository from github</figcaption>
  </figure>

4. Build the project
  ```
    cd ICSim 
    meson setup builddir && cd builddir
    meson compile
    mv controls icsim ..
  ```

5. to start ICsim, hop over to the main folder

  ```
    cd ..
    ./setup_vcan.sh
    ./icsim vcan0
    ./controls vcan0
  ```
  <figure>
    <img src="\assets/img/blogs/2024-07-22/setup" 
      alt="build the tool">
    <figcaption>Build the project</figcaption>
  </figure>

### Conclusion:
ICsim is a powerful tool for simulating and testing CAN bus interactions, making it invaluable for automotive software development, testing, and cybersecurity research. By providing a virtual environment, it eliminates the need for physical hardware during the initial stages of development and testing.

I hope this blog post gave you a good overview on how to install ICSim in 2024. If you are reading up to this point, you are very much interested in Automotive security. Going forward, i'll be writing more such blogs. I hope you enjoyed reading this as much as I enjoyed writing it :)