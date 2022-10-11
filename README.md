# ESE5190 LAB2A Set-Up Guide

How to set up the environment to communicate serially with the RP2040 QT PY Board.

## System Specifications

- OS:  Windows 11
- CPU: AMD Ryzen 5000 
- RAM: 16 GB
- SSD: 1 TB

- LOG software used: Notepad
- Code Editor      : VS Code

## Links to relevant software:

- [PuTTy Serial Terminal](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html)
- [ARM GNU Toolchain](https://developer.arm.com/tools-and-software/open-source-software/developer-tools/gnu-toolchain/downloads)
- [Cmake](https://cmake.org/download/)
- [Build Tools for Visual Studio](https://visualstudio.microsoft.com/downloads/#build-tools-for-visual-studio-2022)
- [Git](https://git-scm.com/download/win)
- [C/C++ MinGW Compiler](https://www.mingw-w64.org/downloads/)
- [Pico SDK](https://github.com/raspberrypi/pico-sdk)
- [Pico Examples Repo](https://github.com/raspberrypi/pico-examples)

## Steps:

Note: I used VS Code simply to view and edit code. I compiled the executable and generated the .uf2 examples manually via command line. I chose this route so as to not be totally dependent on one tool (i.e. VS Code) for all my embedded programming and debugging needs. 

1. Clone the Pico SDK and Pico Examples repository (Preferably in the same parent directory to make things easier). Install Git if not previously installed.

2. Use the official guide as a reference: [Raspberry Pi Pico Getting Started Guide](https://datasheets.raspberrypi.com/pico/getting-started-with-pico.pdf)
Following the steps to the tee will not work as I am in a Windows environment and the instructions to program this specific board (Adafruit QT PY) differs slightly from the generic instructions for the RP2040. 

3. Install the GCC/G++ compiler from the MinGW link above. Install CMAKE and the ARM GNU Toolchain from the above links. 

4. Remember to pull in the latest changes from both pico sdk and pico examples repo using git pull. 

5. Add PICO_SDK_PATH to Windows path. Do not do it through commandline through "set" as I found that it does not stick when you open a new terminal. Do it through the GUI. Press the Windows button, search for environment variables. Click "Edit the System Environment Variables". In the advanced tab of the dialog box that opens, click "Environment Variables". Under User Variables, Add a new variable named PICO_SDK_PATH with the path to where you cloned the repo as shown:

![image](https://user-images.githubusercontent.com/40466274/194987178-b4027193-08cc-4d06-bb23-421857463a10.png)

6. Within your pico examples parent directory, create a folder called "build"

7. Open a terminal inside build

8. Generate a cmake build system using the cmake command. Remember that CMAKE must be installed and make sure that it is added to the environment variables. 
   In the terminal, type the following: 
   
   ```
   cmake .. -G "MinGW Makefiles"
   ```
  You should see the build directory populated with many folders. 
  
9. In the same terminal, change directories to the hello_world/usb directory: 

```
cd hello_world/usb 
``` 

10. Build the code by typing 

```
mingw32-make -j6
```

-j6 is to paralellize the tasks to make compilation faster. 

11. You will find a .elf and .uf2 file created. 

12. Mount your RP2040 board by pressing the BOOT button while connecting to the PC. 

13. You will see a drive created named "RP1-RP2" with a .txt and .htm file. 

14. Copy paste the .uf2 file generated in step 11 into the drive. It will disconnect. That is okay. Do not freak out. 

15. Open device manager. Naviagate to COMs and Ports. Find the COM for the board as follows (USB Serial device). Record the COM number.

![image](https://user-images.githubusercontent.com/40466274/194988869-6d82eacf-687a-4e5e-833a-73d342ee3096.png)


16. Open PuTTy. Configure as follows. Write the correct COM number from step 15. Click OK.

![image](https://user-images.githubusercontent.com/40466274/194989013-a69b9cd0-1b9a-48d3-9b77-e075b6ea3891.png)


17. You will see a terminal window with Hello World dispayed every second as follows:

![image](https://user-images.githubusercontent.com/40466274/194989126-53e113b9-de42-45d0-ad4f-ac4907d6510c.png)



