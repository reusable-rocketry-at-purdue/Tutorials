# Tutorial One: Blinking LEDs

**The most basic action, yet seemingly complex**

<p align="center"><img src="../Resources/RRaPTransCropped.png" width="300" height="300"></p>

## Setup

Before we can start programming the `STM32`, we must first set up the project and generate code. These steps are similar for all projects.

### Importing a Project

If you are importing a project (that is, you are cloning something from GitHub to work on it), you must generate code first. To start, make sure you have cloned the GitHub repository that you would like to work on and know where it is on your computer. Next, open the `STM32CubeMX` software. This will allow you to graphically configure the project. Next, load the project using `File -> Load Project`. Then, locate the project files and select the `.ioc` file. This will allow you to share configurations with others. Finish the setup by clicking `GENERATE CODE`. Once this is done, you can edit the code in `System Workbench`.

### Creating a New Project

Creating a new project is simple if you know the correct information. To begin, open `STM32CubeMX`. Then follow the steps below:

- Click `File -> New Project`
- When the part search screen shows up, search for the `STM32F407VG`. It should say `STM32F4DISCOVERY` in the `Board` section.
- Click `Project Manager`. Select a project name and location.
- Set the `Toolchain / IDE` to be `SW4STM32` and make sure `Generate Under Root` is selected.
- Click `Pinout & Configuration`. This is where you can set the individual pins to their desired input/output types.
  - Left clicking a pin gives all the possible pin types. Selecting a pin type will automatically set it to that type without any code.
  - Right clicking a pin allows the user to assign the pin a label. A label is the name that the user will use to reference the pin in the code.
    - Because of this, naming pins properly is very important!
- Click `System Core` and select `SYS`.
- Set the `Debug` to `Serial Wire`
  - The `Timebase Source` is set depending on the use of `RTOS`; don't worry about it now.
- Now click pins `PD12 - PD15` and set them to `GPIO_Output`.
  - These pins are assigned to LEDs on the board. To find the color LED that each pin uses, refer to [this](https://www.st.com/content/ccc/resource/technical/document/user_manual/70/fe/4a/3f/e7/e1/4f/7d/DM00039084.pdf/files/DM00039084.pdf/jcr:content/translations/en.DM00039084.pdf) document.
  - Name each pin according to the color that the LED it controls is.
- Now click `System Core -> GPIO`. Click on one of the pins you set. Notice that you can configure each pin depending on the hardware it is used on. Leave them on the defaults for now.
- Click `GENERATE CODE` to finish the `Cube` setup.

### Importing a Project to `System Workbench`

Now that we have the code generated, we can begin programming. **Remember, if you don't generate the code, the project will not work!**

- To begin, open `System Workbench`.
- After choosing a workspace, right click on the left side panel. This panel should be called `Project Explorer`.
  - Select `Import -> General -> Existing Projects Into Workspace`.
  - Find the folder that you created/imported the project to, and open that folder.
    - You should now see the files in the left side of `System Workbench`.
- Open `Src` and find `main.c`. This is where we will be doing the coding for this project.
- Using the example code below, and the full source code on [GitHub](https://github.com/reusable-rocketry-at-purdue/Tutorials/tree/master/TutorialOne), make the LEDs blink one after another. The order doesn't matter, but understand when each turns on and when each turns off, as well as why they do such.

***Required Commands***

```C
//Waits for an arbitrary amount of time
void sleep(int time)
{
    for(size_t i = 0; i <= time, i++)
}

int main()
{
    /* USER CODE BEGIN SysInit */
    HAL_GPIO_Init(LED_Orange_GPIO_Port, LED_Orange_Pin); //Initializes the Orange LED
    /* USER CODE END SysInit */

    while(1)
    {
        HAL_GPIO_TogglePin(LED_Orange_Port, LED_Orange_Pin); //Turns the LED on
        sleep(10000000); //Waits for some time
        HAL_GPIO_TogglePin(LED_Orange_Port, LED_Orange_Pin); //Turns the LED off
    }
}

```

Thigs to note:

- Code that is not inside one of the comments saying `USER CODE BEGIN` and `USER CODE END` will be deleted when `Cube` generates the files. In other words, don't put any code here or else it will be deleted.
- We will use HAL (Hardware Abstraction Layer) a lot. It is recommended that you read [this](https://www.st.com/content/ccc/resource/technical/document/user_manual/2f/71/ba/b8/75/54/47/cf/DM00105879.pdf/files/DM00105879.pdf/jcr:content/translations/en.DM00105879.pdf) document that will show you how to use HAL to its maximum potential. There is a lot to learn, but learning it will be very beneficial in the long run.
  - ***No, you don't have to read the whole thing. But do search for the topic you are working on when programming. This will allow you to learn the commands for a certain task without having to read the whole thing.***
  - With this being said, use this document for troubleshooting before requesting help. This document will answer just about any question with the `hardware abstraction layer`.

## Important Documents

This is a list of documents you will need while programming with the `STM32` microcontrollers:

- [STM32F4 Discovery Board Datasheet](https://www.st.com/content/ccc/resource/technical/document/user_manual/70/fe/4a/3f/e7/e1/4f/7d/DM00039084.pdf/files/DM00039084.pdf/jcr:content/translations/en.DM00039084.pdf) ***Review for troubleshooting***
- [STM32F407VG Datasheet](https://www.st.com/resource/en/datasheet/stm32f407vg.pdf) ***Review for troubleshooting***
- [Hardware Abstraction Layer Manual](https://www.st.com/content/ccc/resource/technical/document/user_manual/2f/71/ba/b8/75/54/47/cf/DM00105879.pdf/files/DM00105879.pdf/jcr:content/translations/en.DM00105879.pdf) ***Recommend at least skimming***
- [STM32F407VG Programming Manual](https://www.st.com/content/ccc/resource/technical/document/programming_manual/6c/3a/cb/e7/e4/ea/44/9b/DM00046982.pdf/files/DM00046982.pdf/jcr:content/translations/en.DM00046982.pdf) ***Recommend at least skimming***

The bottom line is, don't get discouraged. This stuff isn't easy, but we're here to help. Don't think you need to read all of this, or any of it. But, these resources will help a ton when something just won't work right.