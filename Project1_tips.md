# **Project1 Tips and Q&A**

**These tips aim to help you through some common mistakes in Project1, and give you some hints on writing code**

## **0.** Reference Starter Code for Project1
- We have released a **starter code for project1 on canvas/Project1 folder**, containing all the codes for following tips. These starter codes are only **for reference**. You aren't forced to use these code.
- Note: The reference starter code is very similar to the original STARTER code, except for some comments instructing you to modify the code.
- Wherever you see `/* Input / modify code here: */`, you should input / modify the code there. You should modify codes in the following files.
  - `Core/Src/main.c`
  - `Core/Inc/main.h`
  - `WHEELTEC/control.c`
  - `BSPcode/usart3.c`
  - `WHEELTEC/show.c`
  - `Core/Src/usart.c`

## **1.** Definition of Global Variables
- Global variables aim to be used in multiple functions / files, and they are defined outside of any function, and are accessible from any function in the program.
- In Project1, you should define the global variables with `extern` in the `main.h` file, and define the global variables `main.c` file. Then you can access the global variables in any other files.
  - Example:
    ```c
    // Core/Inc/main.h, define the global variables with extern

    /* Input / modify code here:
    Input definition of global variables
    This is a definition of global variable: Yaw_Angle.
    */
    extern float Yaw_Angle;
    ```

    ```c
    // Core/Src/main.c, define the global variables

    /* Input / modify code here:
    Input definition of global variables
    This is a definition of global variable: Yaw_Angle.
    */
    float Yaw_Angle=0.0;
    ```

    ```c
    // WHEELTEC/control.c, use the global variable: Yaw_Angle
    void Get_Angle(u8 way)
    {
      ...
      /* Input / modify code here:
      we can calculate the global variable Yaw_Angle here.
      */
	    Yaw_Angle = Yaw_Angle + gyro_z * 0.005;// Input your code
    }
    ```
  - Note: `main.h` and `main.c` aren't the only files you can define global variables, defining them in some of the other files also works. This is just a practice that **definitely works**.

## **2.** Comment out codes for PID debugging and remote control
  - If you need to do PID debugging or remote control using mobile APP, remember to uncomment these codes.
  - If you don't need PID debugging or remote control function for WHEETEC mobile APP, you should comment out the following codes to remove unnecessary bluetooth transmission.
    - `BSPcode/usart3.c`, but be aware, **don't** comment out **``` HAL_UART_Receive_IT(&huart3,Usart3_Receive_buf,sizeof(Usart3_Receive_buf));```**!
      ```c
      //BSPcode/usart3.c
      void HAL_UART_RxCpltCallback(UART_HandleTypeDef *UartHandle)
      {

        if(UartHandle->Instance == USART3)
        {
          ...
          /* Input / modify code here:
            Comment out these codes if you don't need remote control and PID tuning
          */

          if(uart_receive==0x59)  Flag_velocity=2;
          if(uart_receive==0x58)  Flag_velocity=1;
          ...
            {
                j=0;
                Data=0;
                memset(Receive, 0, sizeof(u8)*50);
            }
          HAL_UART_Receive_IT(&huart3,Usart3_Receive_buf,sizeof(Usart3_Receive_buf));
        }
      }
      ```
    - `WHEELTEC/show.c`
      ```c
      //WHEELTEC/show.c
      void APP_Show(void)
      {
        ...

        /* Input / modify code here:
          Comment out these codes if you don't need remote PID tuning
        */
        if(PID_Send==1)
        ...
          else
          printf("{B%d:%d:%d}$",(int)Pitch,(int)Roll,(int)Yaw);

      }
      ```

## **3.** Change baudrate to 921600
  - You can achieve higher throughput of bluetooth transmission by changing the baudrate to 921600.
    - e.g. Say if you want to transmit a 5 byte information like "1234\n". 9600 baudrate will take 5ms, while 921600 baudrate will take only 0.05ms. You can increase the frequency of bluetooth transmission by **100** times.
  - The command for changing baudrate of bluetooth module is entering AT mode and print `AT+UART=921600,0,0`, which sets the baudrate to 921600. Detailed command can be found in the lab3 manual.
  - Remember to change the baudrate in `Core/Src/usart.c` as well. Be aware that it's **`USART3`**, not `USART1`!.
    ```c
    // Core/Src/usart.c
    void MX_USART3_UART_Init(void)
    {

      huart3.Instance = USART3;
      /* Input / modify code here:
      Change the baudrate to the value you set on bluetooth module
      */
      huart3.Init.BaudRate = 9600;
      
      ...
    }
    ```

## **4.** Enable ultra-sonic module in Normal Mode
  - Current ultra-sonic module only works in Ultrasonic_Avoid_Mode or Ultrasonic_Follow_Mode. You need to modify these codes to make it work in Normal Mode. Also there're codes that control to do obstacle follow / avoidance. You can comment out these codes if you don't need them.
  - `Core/Src/main.c`
    ```c
    // Core/Src/main.c
    int main(void)
    {
      ...
      /* Input / modify code here:
        MX_TIM2_Init() is necessary for ultra-sonic module to work.
        Currently, MX_TIM2_Init() isn't called when the mode Normal_Mode is selected.
        How to change the code to make sure that MX_TIM2_Init() is called when the mode Normal_Mode is selected?
      */
      if(Mode==Ultrasonic_Avoid_Mode||Mode==Ultrasonic_Follow_Mode)
        MX_TIM2_Init();
      
      ...
    }
    ```
  - `WHEELTEC/control.c`
    ```c
    // WHEELTEC/control.c
    void HAL_GPIO_EXTI_Callback(uint16_t GPIO_Pin)
    {
      ...
      /* Input / modify code here:
        Read_Distane() is the function that reads the distance from the ultra-sonic module, and stores it to variable: Distance.
        Currently, Read_Distane() isn't called when the mode Normal_Mode is selected.
        How to change the code to make sure that Read_Distane() is called when the mode Normal_Mode is selected?
      */
      if(Mode==Ultrasonic_Avoid_Mode||Mode==Ultrasonic_Follow_Mode)
          Read_Distane();
      
      ...
    }
    ```
  - `WHEELTEC/control.c`
    ```c
    // WHEELTEC/control.c
    int Velocity(int encoder_left,int encoder_right)
    {
      ...
      /* Input / modify code here:
        These codes are used to control the car to follow or avoid obstacles.
        If we don't need these functions, we can comment out these codes.
      */

      // if(Mode==Ultrasonic_Follow_Mode&&(Distance>200&&Distance<500)&&Flag_Left!=1&&Flag_Right!=1) //跟随
      // 	 Movement=Target_Velocity/Flag_velocity;
      // if(Mode==Ultrasonic_Follow_Mode&&Distance<200&&Flag_Left!=1&&Flag_Right!=1)
      // 	 Movement=-Target_Velocity/Flag_velocity;
      // if(Mode==Ultrasonic_Avoid_Mode&&Distance<450&&Flag_Left!=1&&Flag_Right!=1)  //超声波避障
      // 	 Movement=-Target_Velocity/Flag_velocity;
      ...
    }
    ```

## **5.** Calculation of Yaw_Angle
  - In lab2, we using the acceleration of the Z-axis to calculate the yaw angle.
  - Notice that **even when the car is static**, our `gyro_z` is not zero because of hardware imperfections. But through our observation, we can find that the `gyro_z` is relatively stable when the car is static. How can we cancel out the error in `gyro_z`?
  - Hint: We can manually keep the car static for a few seconds and record the average value of `gyro_z`. Then we can subtract this average value from gyro_z to get a more accurate `gyro_z`.
  - Code in `WHEELTEC/control.c`
    ```c
    //WHEELTEC/control.c
    void Get_Angle(u8 way)
    {
      ...
      /* Input / modify code here:
        Using the acceleration of the Z-axis to calculate the yaw angle.
        Notice that even when the car is static, our gyro_z is not zero because of hardware imperfections.
        But through our observation, we can find that the gyro_z is relatively stable when the car is static.
        How can we cancel out the error in gyro_z?
        Hint: We can manually keep the car static for a few seconds and record the average value of gyro_z.
        Then we can subtract this average value from gyro_z to get a more accurate gyro_z.
        
        We can calculate the global variable Yaw_Angle here.
      */
      Yaw_Angle = Yaw_Angle + gyro_z * 0.005;// Input your code
    }
    ```

## **6.** Recommendation for writing out your logic
  - We recommend to write your main logic in `Core/Src/main.c` file. You can control the car by setting the value of `Flag_front`, `Flag_back`, `Flag_Left`, `Flag_Right`.
    - If `Flag_front==1` and `Flag_back==0`, the car will move forward.
    - If `Flag_front==0` and `Flag_back==1`, the car will move backward.
    - If `Flag_Left==1` and `Flag_Right==0`, the car will turn left.
    - If `Flag_Left==0` and `Flag_Right==1`, the car will turn right.
  - Note that the `while(1)` loop in `main.c` has the period of **50ms**, while the code in `control.c` has the period of **5ms**.
  - There's an example code in `Core/Src/main.c` that shows how to control the car to move forward. We also provide a function `move_and_turn()` that shows how to control the car to move forward and turn right when there's an obstacle in front of the car.
    ```c
    // Core/Src/main.c

    /* Input / modify code here:
      move_and_turn is an example function, that's called in main() function's while(1) loop.
      We maintain a static variable called status, which is used to determine the status of the robot.
      It's very important to maintain the status of the robot in a variable, so that the robot can remember its previous state.
    */
    #define MOVE_AND_TURN_STATUS_MOVE 0
    #define MOVE_AND_TURN_STATUS_TURN 1
    #define MOVE_AND_TURN_STATUS_STOP 2
    void move_and_turn(){
      static u8 status = MOVE_AND_TURN_STATUS_MOVE;
      if (status == MOVE_AND_TURN_STATUS_MOVE){
        // Move forward
        Flag_front = 1;
        Flag_back = 0;
        Flag_Left = 0;
        Flag_Right = 0;

        // If obstacle is near, turn right
        if (Distance <= 300){
          status = MOVE_AND_TURN_STATUS_TURN;
        }
      }
      else if (status == MOVE_AND_TURN_STATUS_TURN){
        // Turn right
        Flag_front = 0;
        Flag_back = 0;
        Flag_Left = 0;
        Flag_Right = 1;

        // If we turn for 90 degress, stop
        if (Yaw_Angle < -PI/2){
          status = MOVE_AND_TURN_STATUS_STOP;
        }
      }
      else if (status == MOVE_AND_TURN_STATUS_STOP){
        // Stop
        Flag_front = 0;
        Flag_back = 0;
        Flag_Left = 0;
        Flag_Right = 0;
      }
    }

    int main(void)
    {
      ...
      while (1)
      {
        ...

        /* Input / modify code here:
          We recomment to put your main logic in main.c. Also, you can use functions to make your code more readable.
        */
        move_and_turn();

        ...
      }
    }
    ```

## Hope these tips can help you with Project1! Good luck!

---
# **Q&A**
## Before reaching out to TA, please check the following Q&A first.
## **Q1.** Why my bluetooth module HC-05 doesn't communicate?
  - Please follow these steps to debug
    1. Press the reset button of the car, make sure computer's serial monitor isn't dead and baudrate is correct.
    2. Make sure the indication light is double blink slowly indicating that connection between HC-05.
    3. If step 1 and 2 fail to solve, connect both HC-05 modules to computer and check if they can communicate with each other. (Be aware of baudrate and line connection too)
    4. For both modules, enter AT mode and type `AT`, `AT+ROLE?`, `AT+PSWD?`, `AT+UART?`. In many times, only inquiring these commands can make the bluetooth module work again.
    5. Ask TA for help

## **Q2.** Why the LED screen of my car displays nothing?
  - Very likely, you added a dead loop in your code. The LED screen will not display anything if the while(1) loop in main functionis blocked.
  - Or maybe, you have `printf()` in your `control.c` code. Since `control.c` has a period of 5ms, its update frequency is too high.

## **Q3.** Why the car doesn't move?
  - Check your code first
  - Make sure your battery has voltage higher than 10.0V when running, otherwise charge your car

## **Q4.** Why the car doesn't turn?
  - Turning right will make `gyro_z` has negative value, be aware of the sign!
