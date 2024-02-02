[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-24ddc0f5d75046c5622901739e7c5dd533143b0c8e959d652212380cedb1ea36.svg)](https://classroom.github.com/a/tecaRa11)
# 2024-P1-Kobuki

El objetivo de esta práctica es usar los comandos de ROS 2 en la terminal para examinar el robot Kobuki.

Debes completar el siguiente cuestionario para realizar la práctica. Incluye los comandos que has usado en cada una:


1. ¿Has tenido que hacer algún setup en tu ordenador? Indica los pasos
   
   He tenido que incorporar 3 setup en mi bshrc, uno para ros, otro para el simulador Gazebo y un ultimo para el workspace
   ```
   source /opt/ros/humble/setup.bash
   source /usr/share/gazebo/setup.bash
   source wks/install/setup.bash
   ```

2. ¿Qué comando has usado para lanzar el Kobuki en ROS 2?

   Para lanzar el Kobuki en ROS 2 con el simuladopr Gazebo he usado el siguiente comando:

   ```
   ros2 launch kobuki simulation.launch.py
   ```
   Para lanzarlo en un Kobuki físico:
   ```
   ros2 launch kobuki kobuki.launch.py
   ```
4. ¿Qué nodos se lanzan? 
   
   Una vez lanzado el Kobuki, si en otra terminal escribimos:
   ```
   ros2 node list
   ```
   nos aparece la lista de los nodos.  
   ![Captura desde 2024-01-30 14-16-11](https://github.com/Docencia-fmrico/2024-p1-kobuki-jmartinm2021/assets/92941332/9105fc2f-3daa-4df8-a404-9bc959147e7b)

   Sin embargo si al lanzar el kobuki añadimos lidar:=True y esta conectado el laser, apareceran 2 nodo mas: /scan_to_scan_filter_chain y /rplidar_node


6. ¿Qué topics están disponibles? 
   
   Una vez lanzado el Kobuki, si en otra terminal escribimos:
   ```
   ros2 topic list
   ```
   nos aparece la lista de los topic.  
   ![Captura desde 2024-01-30 14-14-51](https://github.com/Docencia-fmrico/2024-p1-kobuki-jmartinm2021/assets/92941332/e9ab1634-d488-4deb-9029-2fae1b519fc2)

   Sin embargo si la lanzar el kobuki añadimos lidar:=True, aparecen 2 topic mas: /scan y scan_filtered

8. Analiza los topics (tipo, QoS y explicación de campos) que permiten hacer al robot moverse, detectar obstáculos con el bumper y recibir la información del láser.
   Para analizar los topic usaremos el comando
   ```
   ros2 topic info --verbose [topic]
   ```
   
   - **Movimiento:**
        - Topic: /cmd_vel  
          ![Captura desde 2024-01-29 12-35-53](https://github.com/Docencia-fmrico/2024-p1-kobuki-jmartinm2021/assets/92941332/6b6b9a9c-2ef8-447c-b043-fe9c7ce9ef59)

   - **Bumper:**
        - Topic: /events/bumper  
        ![Captura desde 2024-01-29 12-39-42](https://github.com/Docencia-fmrico/2024-p1-kobuki-jmartinm2021/assets/92941332/c007555e-1b03-4275-883b-3bcbed3f16d0)

   - **Láser:**
        - Topic: /scan  
        ![Captura desde 2024-01-29 12-37-13](https://github.com/Docencia-fmrico/2024-p1-kobuki-jmartinm2021/assets/92941332/e31ca47f-89fc-4471-8a91-ad2abdc489cf)

9. ¿Qué servicios o acciones están disponibles?
   Para ver los servicios usaremos el comando
   ```
   ros2 service list
   ```
![Captura desde 2024-01-30 14-17-07](https://github.com/Docencia-fmrico/2024-p1-kobuki-jmartinm2021/assets/92941332/c653ef3a-fd8a-4488-8708-851c3d6a5755)


   Para ver las acciones usaremos el comando
   ```
   ros2 action list
   ```
![Captura desde 2024-01-29 12-33-33](https://github.com/Docencia-fmrico/2024-p1-kobuki-jmartinm2021/assets/92941332/617fe6bf-6a2b-4f53-a7f2-bff7fbd785f9)


7. Haz una diagrama del Kobuki con [drawio](https://app.diagrams.net/) similar al del robot Tiago que te muestro, cuyo fuente está en el repositorio. El diagrama debe mostrar los nodos existentes, sus conexiones y su tipo. Sube al repositorio tanto un .png como el fuente .drawio.
![tiago_graph](https://github.com/Docencia-fmrico/2024-P1-Kobuki/assets/3810011/a2161319-f181-4905-8fd2-2b1ed3f2151e)
  
  Usando [drawio](https://app.diagrams.net/) he creado el diagrama del Kobuki SIMULADO EN GAZEBO (ros2 launch kobuki simulation.launch.py) incluyendo nodos, topics, suscriptores y publicadores:  
    
  ![Captura desde 2024-01-28 15-29-35](https://github.com/Docencia-fmrico/2024-p1-kobuki-jmartinm2021/assets/92941332/b7481011-6146-439a-aac7-b86d9450573e)  

  Usando [drawio](https://app.diagrams.net/) he creado el diagrama del Kobuki (ros2 launch kobuki kobuki.launch.py) incluyendo nodos, topics, suscriptores y publicadores:
![kobuki_graph](https://github.com/Docencia-fmrico/2024-p1-kobuki-jmartinm2021/assets/92941332/53719ff4-98b8-483f-b18b-71edf3a31ddc)


9. Trata de que el robot avance medio metro y luego gire PI/2. Indica el proceso.  
   **EN EL SIMULADOR:**  
   Para hacer que avance 0.5 metros en linea recta hacia delante:
```
ros2 topic pub --once /cmd_vel geometry_msgs/msg/Twist "{linear: {x: 0.1, y: 0.0, z: 0.0}, angular: {x: 0.0, y: 0.0, z: 0.0}}" && sleep 5
```
   Para hacer que gire pi/2:
```
ros2 topic pub --once /cmd_vel geometry_msgs/msg/Twist "{linear: {x: 0.0, y: 0.0, z: 0.0}, angular: {x: 0.0, y: 0.0, z: 0.5}}" && sleep 3
```
   Para que se detenga:
```
ros2 topic pub --once /cmd_vel geometry_msgs/msg/Twist "{linear: {x: 0.0, y: 0.0, z: 0.0}, angular: {x: 0.0, y: 0.0, z: 0.0}}"
```
   Todo junto:
```
ros2 topic pub --once /cmd_vel geometry_msgs/msg/Twist "{linear: {x: 0.1, y: 0.0, z: 0.0}, angular: {x: 0.0, y: 0.0, z: 0.0}}" && sleep 5 && ros2 topic pub --once /cmd_vel geometry_msgs/msg/Twist "{linear: {x: 0.0, y: 0.0, z: 0.0}, angular: {x: 0.0, y: 0.0, z: 0.5}}" && sleep 3 && ros2 topic pub --once /cmd_vel geometry_msgs/msg/Twist "{linear: {x: 0.0, y: 0.0, z: 0.0}, angular: {x: 0.0, y: 0.0, z: 0.0}}"
```
   Video demostracion en Gazebo:
   

https://github.com/Docencia-fmrico/2024-p1-kobuki-jmartinm2021/assets/92941332/50af8638-4dc1-4c5c-9340-63ff7c853dd1

   **EN EL KOBUKI FISICO:**  
      Para hacer que avance 0.5 metros en linea recta hacia delante:
```
ros2 topic pub --times 3 /cmd_vel geometry_msgs/msg/Twist "{linear: {x: 0.3, y: 0.0, z: 0.0}, angular: {x: 0.0, y: 0.0, z: 0.0}}" && sleep 1
```
   Para hacer que gire pi/2:
```
ros2 topic pub --once /cmd_vel geometry_msgs/msg/Twist "{linear: {x: 0.0, y: 0.0, z: 0.0}, angular: {x: 0.0, y: 0.0, z: 2}}" && sleep 1
```
   Para que se detenga:
```
ros2 topic pub --once /cmd_vel geometry_msgs/msg/Twist "{linear: {x: 0.0, y: 0.0, z: 0.0}, angular: {x: 0.0, y: 0.0, z: 0.0}}"
```
   Todo junto:
```
ros2 topic pub --times 3 /cmd_vel geometry_msgs/msg/Twist "{linear: {x: 0.3, y: 0.0, z: 0.0}, angular: {x: 0.0, y: 0.0, z: 0.0}}" && sleep 1 && rros2 topic pub --once /cmd_vel geometry_msgs/msg/Twist "{linear: {x: 0.0, y: 0.0, z: 0.0}, angular: {x: 0.0, y: 0.0, z: 2}}" && sleep 1 && ros2 topic pub --once /cmd_vel geometry_msgs/msg/Twist "{linear: {x: 0.0, y: 0.0, z: 0.0}, angular: {x: 0.0, y: 0.0, z: 0.0}}"
```
