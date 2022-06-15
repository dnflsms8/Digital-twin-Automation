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


