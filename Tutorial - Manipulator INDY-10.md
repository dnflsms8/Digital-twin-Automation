## Tutorial - Manipulator INDY-10

##### 로봇 연결

1. 컨트롤박스를 콘센트에 연결한뒤, 전원 버튼을 누릅니다. 2~5분이면 로봇이 완전히 작동하게 됩니다.
2. 컨트롤 박스 뒷면에 **랜선을 공유기에 연결**합니다. (**컴퓨터와 같은 wifi로 연결**되어야지만 ROS 코드를 사용한 제어가 가능합니다.)
3. 태블릿을 컨트롤 박스 뒷면 USB포트로 연결합니다.
4. 태블릿의 **Conty 앱**에 들어가 **USB연결**을 눌러 로봇이 잘 연결되는지 확인합니다.

4-1. 만약 연결이 되지 않을 경우 **Emergency 버튼**을 확인해보세요. 눌러져 Lock되어 있을 경우, **돌려서 빼면 됩니다. **

4-2. 우측 상단에 붉은 메세지가 떠있을 경우, 우측 상단에 있는 **리셋을 눌러 초기화**하면 됩니다.

[![img](https://github.com/chaochao77/ROS_neuromeka_tutorial/raw/main/image/11.jpg)](https://github.com/chaochao77/ROS_neuromeka_tutorial/blob/main/image/11.jpg)

1. 로봇의 IP를 확인하기 위해 환경설정, **애플리케이션 정보**를 들어가 **IP**를 확인합니다. (**ROS로 로봇과 연결 시 **IP를 알아야합니다.)

   [![img](https://github.com/chaochao77/ROS_neuromeka_tutorial/raw/main/image/12.jpg)](https://github.com/chaochao77/ROS_neuromeka_tutorial/blob/main/image/12.jpg)[![img](https://github.com/chaochao77/ROS_neuromeka_tutorial/raw/main/image/13.jpg)](https://github.com/chaochao77/ROS_neuromeka_tutorial/blob/main/image/13.jpg)

2. 이제 USB 연결을 해제하고 **확인한 IP로 WIFI모드로 연결**합니다. (*이때 태블릿 또한 같은 공유기 WIFI로 연결되어 있어야합니다)

3. 로봇이 작동이 잘되는지 간단히 테스트 하고싶으시다면 아래와 같이 **프로그램 > 새로만들기 > 시간기준 > 조인트이동 편집 > 직접 교시**로 들어가 직접 손으로 로봇 조인트들을 움직일 수 있습니다.

   [![img](https://github.com/chaochao77/ROS_neuromeka_tutorial/raw/main/image/17.jpg)](https://github.com/chaochao77/ROS_neuromeka_tutorial/blob/main/image/17.jpg)[![img](https://github.com/chaochao77/ROS_neuromeka_tutorial/raw/main/image/14.jpg)](https://github.com/chaochao77/ROS_neuromeka_tutorial/blob/main/image/14.jpg)

   [![img](https://github.com/chaochao77/ROS_neuromeka_tutorial/raw/main/image/15.jpg)](https://github.com/chaochao77/ROS_neuromeka_tutorial/blob/main/image/15.jpg)[![img](https://github.com/chaochao77/ROS_neuromeka_tutorial/raw/main/image/19.jpg)](https://github.com/chaochao77/ROS_neuromeka_tutorial/blob/main/image/19.jpg)

   [![img](https://github.com/chaochao77/ROS_neuromeka_tutorial/raw/main/image/16.jpg)](https://github.com/chaochao77/ROS_neuromeka_tutorial/raw/main/image/16.jpg)

   또한 이동 > 홈 위치 or 영위치를 누르는 것으로 조인트 별로 이상이 없는지 간단히 체크 할 수 있습니다.

실험 도중 로봇이 멈추거나, 오류가 생길 경우 **태블릿의 Reset 버튼**을 누르면 로봇 상태가 초기화 되며 오류가 고쳐집니다.



##### 실제 로봇 연결

1. INDY-10을 작동시키고, **컨트롤박스에 연결된 공유기와 동일한 WIFI로 컴퓨터와 연결**합니다.

2. 태블릿으로 확인한 로봇의 IP로 터미널 창에서 아래의 명령어의 xxx부분에 **IP주소를 추가하여 실행**합니다.

   `roslaunch indy10_moveit_config moveit_planning_execution.launch robot_ip:=xxx.xxx.xxx.xxx`

3. 태블릿으로 로봇을 조작하여 움직이면 Rviz에서도 실시간으로 로봇이 움직이는 것을 확인 할 수 있습니다.

4. 종료하시고 싶으시다면 명령을 실행한 터미널로 가서 `ctrl+c` 를 눌러 실행한 `roslaunch`가 종료되면서 Rviz가 꺼지고 로봇과의 연결이 끊깁니다.



## Hardware - Gripper

##### VGC10(Vacuum Gripper)

![image](https://user-images.githubusercontent.com/84519300/174002441-122a5212-4a7f-4212-b197-89e084c95485.png)

###### Specification

- **정격전압: 24[V]**, (최소 20.4[V], 최대 28.8[V])
- 최대 15kg까지 들어올릴 수 있음 (단, Vacuum cup 사이즈와 개수에 따라 달라짐)
- **Open, close 두개의 입력선**으로 그리퍼 **흡입, 열기 제어**

###### Vacuum cup 종류
![image](https://user-images.githubusercontent.com/84519300/174008469-91b4f07d-c9dd-488d-840e-5396cdafa0d6.png)
* 들어올리려는 물체의 종류에 따라 적절한 Vacuum cup을 골라야 한다

###### 무게-압력에 따른 필요한 Vaccum cup의 개수 (공극이 없는 물체에 대해)
![image](https://user-images.githubusercontent.com/84519300/174006996-e7b22f54-c3af-4073-a402-abb98f4ef78f.png)
* 15[mm]짜리를 7개 이상 혹은 30[mm]짜리를 4개 이상 혹은 40[mm]짜리를 3개 이상 달기 위해선, 커스터마이즈된 Adaptor plate가 필요함 

###### Adaptor plate
![image](https://user-images.githubusercontent.com/84519300/174009286-800c5017-5b4b-4d7d-8219-55b40b0d66b8.png)
![image](https://user-images.githubusercontent.com/84519300/174009791-7168c35e-52e5-44cd-ac07-6cb35b8eb3a1.png)

- 4개의 나사를 4Nm 토크로 조여서 설치할 수 있음
- 설치 방향에 따라, Vaccum 채널(1,2)을 효율적으로 사용할 수 있음


###### 연결 - 컨트롤 박스

1. 컨트롤 박스 후면을 보면 아래의 이미지와 같이 Digital I/O, Analog I/O가 있습니다.

   [![img](https://github.com/chaochao77/ROS_neuromeka_tutorial/raw/main/image/112.jpg)](https://github.com/chaochao77/ROS_neuromeka_tutorial/blob/main/image/112.jpg)[![img](https://github.com/chaochao77/ROS_neuromeka_tutorial/raw/main/image/111.jpg)](https://github.com/chaochao77/ROS_neuromeka_tutorial/blob/main/image/111.jpg)

   [![img](https://github.com/chaochao77/ROS_neuromeka_tutorial/raw/main/image/114.jpg)](https://github.com/chaochao77/ROS_neuromeka_tutorial/raw/main/image/114.jpg)

   전선을 포트에 넣어 연결하려면은 **일자 드라이버 작은게 **필요합니다. 각 번호의 포트 **구멍 옆의 주황색 부분**을 일자 드라이버로 꾸욱 누르면 포트 구멍이 열려 쉽게 넣고 뺄 수 있습니다. **하지만 너무 깊게 넣을 시 빼기 힘들 수 있으니 잘 잡힐 정도로만 넣으면 됩니다.**

2. 컨트롤 박스의 I/O보드들에 전력을 공급하기 위해 위의 오른쪽 이미지 처럼 **1-10포트의 9,10번째를 서로 연결**하고, **11-20포트의 9,10번째를 서로 연결**합니다

   - 1-10 의 9,10번째 포트는 **GND**, 1-20의 9,10번째 포트는 **24[V] VCC**로 **컨트롤 박스 내부에서 자체적으로 I/O보드에 24[V]전력이 공급**되게 해줍니다.

3. 이제 그리퍼 EGP-C-64에 전력 공급을 위해 **41-50의 10번 포트에 Vcc(빨강, 파랑 패턴선), 9번에 GND(회색 갈색 패턴선)을 연결**합니다.

4. 그리퍼의 **Close(파랑선)을 41-50의 2번 포트에, Open(빨강)을 1번에 연결**합니다. 아래의 이미지처럼 연결되었다면 그리퍼를 사용할 준비가 완료 된겁니다.

   [![img](https://github.com/chaochao77/ROS_neuromeka_tutorial/raw/main/image/113.jpg)](https://github.com/chaochao77/ROS_neuromeka_tutorial/raw/main/image/113.jpg)

###### 제어 - 태블릿

1. Conty 앱을 실행하여 로봇과 연결합니다.

2. 로봇 설정에 들어가면 아래의 이미지 처럼 화면에 바로 6개의 조인트 및 **Smart DI/O** 들이 보입니다.

   [![img](https://github.com/chaochao77/ROS_neuromeka_tutorial/raw/main/image/141.jpg)](https://github.com/chaochao77/ROS_neuromeka_tutorial/raw/main/image/141.jpg)

3. Smart D I/O에서 **10 번과 11번**의 출력에 따라 그리퍼와 연결된 **Close(blue), Open(red) 선에 0,1의 디지털 값**이 입력됩니다.

4. 태블릿에서 **10번을 눌러 On (초록색) , 11번을 off(회색)**을 하면 그리퍼 **흡입**, 반대로 **10번을 다시 눌러 off, 11번을 눌러 on**하면 그리퍼 **배출** 작용을 하게 됩니다.

5. VGC10의 경우 **Open과 Close가 { 1 ,0 } 또는 {0 , 1} 으로 입력**이 되어야 지만 열고 닫는 작용을 하게 됩니다.

###### 제어 - ROS(INDY-10)

qr_classify_robot.py에는 **ROS에서 연결된 로봇의 컨트롤 박스로 명령어를 주거나, 데이터를 받게 해주는 py 코드파일** 입니다. 이 곳에서 컨트롤 박스 후면 디지털 포트들(Smart DI/O)에 **입력을 받거나, 출력을 주는 명령어를 보내 그리퍼를 작동** 하는 코드가 포함되어 있습니다.


위의 링크로 해당 코드파일을 보면, 태블릿에서 작동한 것과 같이 10번과 11번포트로 디지털 값 입출력을 **코드 명령어를 통해 직접 전달** 해 VGC10의 흡입/배출을 조절하는 코드가 있습니다.

- VGC10 흡입

  ```
   # 1단계: 우편이 놓여진 고정된 위치로 간다.
        t_pos = [0.43406, -0.44675, 0.48322, -176.72, 35.65, 137.13]             # 고정된 위치
        indy.task_move_to(t_pos) # move to 절대좌표, move by 상대좌표

        while True:
            status = indy.get_robot_status()
            sleep(0.2)
            if status[key[5]]==1 :
                break
        print('done : move1 process')
        
        prog = JsonProgramComponent(policy=0, resume_time=2)  # Make Json program
        
        
      
        indy.set_do(10, 0)
        indy.set_do(11, 1) # 흡입
       
        print("gripper")
  ```



- VGC10 배출

  ```
  # 3단계: location에 해당되는 위치로 간다.
        t_pos = locate_pos
        indy.task_move_to(t_pos)

        while True:
            status = indy.get_robot_status()
            sleep(0.2)
            if status[key[5]]==1 :
                break
        print('done : move2 process')        

    
        print("gripper")   
      
        
        indy.set_do(11, 0)
        indy.set_do(10, 1) # 배출
  ```

  - Open과 반대로 11번 인덱스에 0 값을, 10번 인덱스에 1값을 넣으면 작동 됩니다.

위와 같이 작성 완료 후, ROS에서 실제 로봇을 작동하는 파일을 roslaunch로 실행하게 되면 해당 명령을 처리 할때 그리퍼가 작동하게 됩니다.

