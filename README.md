## Kuka-G40-proxy-v2

This project implements a custom message on the KR60 at G40 to allow user sending robot motion command to the robot controller from Grasshopper. The communication between the robot and PC are built on top of KukavarProxy - [link](https://github.com/lionpeloux/KukavarProxy/tree/dev).

### Installation 
1. Install KukavarProxy - [link](https://github.com/lionpeloux/KukavarProxy/tree/dev) to the robot controller
2. Copy `./robot/var_proxy_v2.dat` and `./robot/var_proxy_v2.src` into the robot controller
3. Download `kvp_control_v2.gh` to the device which your Rhino and Grasshopper is running


### Usage
1. Turn on `KukavarProxy.exe` on the robot controller
2. Select and run `var_proxy_v2.src` on the teach pendnat until you see the message "waiting next cmd" on the screen
3. You are now ready to send the motion command from Grasshopper. There are 2 example block in `kvp_control_v2.gh` for sending PTP joint movement command and LIN linear movement command respectively
4. Afer sending the command from Grashopper, press and hold the deadman switch and run key on the teach pendant to execute the motion

Note: This project is only tested on the KR60 at G40 with T1 mode. This project is mainly focus on implemntating the protocol, there are no checking on the robot reachability, collision or data validation. User must validate their own data before sending to the robot.


### Data definition

```
//ADDRESS: ghCommand

struct MotionCommand {  
  int motionType; //Required; 0 = No movement OR the motion is done ; 1 = Joint Motion; 2 = Linear Motion           
  E6AXIS jntPos; //Optional; Required when motionType == 1
  E6POS targetPos; //Optional; Required when motionType ==2       
};

```

