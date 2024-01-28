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

3. ¿Qué nodos se lanzan? 
   
   Una vez lanzado el Kobuki, si en otra terminal escribimos:
   ```
   ros2 node list
   ```
   nos aparece la lista de los nodos.  
   ![Captura desde 2024-01-28 12-13-38](https://github.com/Docencia-fmrico/2024-p1-kobuki-jmartinm2021/assets/92941332/08c93e72-dc67-4e14-b7ec-b57244925578)


4. ¿Qué topics están disponibles? 
   
   Una vez lanzado el Kobuki, si en otra terminal escribimos:
   ```
   ros2 topic list
   ```
   nos aparece la lista de los topic.  
   ![Captura desde 2024-01-28 12-16-11](https://github.com/Docencia-fmrico/2024-p1-kobuki-jmartinm2021/assets/92941332/820b3aba-f40d-49b1-9de7-ae465d59c012)


5. Analiza los topics (tipo, QoS y explicación de campos) que permiten hacer al robot moverse, detectar obstáculos con el bumper y recibir la información del láser.
   - **Movimiento:**
        - Topic: /cmd_vel
        - Type: geometry_msgs/msg/Twist
   - **Bumper:**
        - Topic: /parameter_events
        - Type: rcl_interfaces/msg/ParameterEvent
   - **Láser:**
        - Topic: /scan
        - Type: sensor_msgs/msg/LaserScan
6. ¿Qué servicios o acciones están disponibles? 
   
   Para ver los servicios usaremos el comando
```
ros2 service list
```
![Captura desde 2024-01-28 16-23-05](https://github.com/Docencia-fmrico/2024-p1-kobuki-jmartinm2021/assets/92941332/97149bab-0538-431f-a99b-a5fc20d2619d)


7. Haz una diagrama del Kobuki con [drawio](https://app.diagrams.net/) similar al del robot Tiago que te muestro, cuyo fuente está en el repositorio. El diagrama debe mostrar los nodos existentes, sus conexiones y su tipo. Sube al repositorio tanto un .png como el fuente .drawio.
![tiago_graph](https://github.com/Docencia-fmrico/2024-P1-Kobuki/assets/3810011/a2161319-f181-4905-8fd2-2b1ed3f2151e)
  Usando [drawio](https://app.diagrams.net/) he creado el diagrama del Kobuki incluyendo nodos, topics, suscriptores y publicadores:  
  ![Captura desde 2024-01-28 15-29-35](https://github.com/Docencia-fmrico/2024-p1-kobuki-jmartinm2021/assets/92941332/b7481011-6146-439a-aac7-b86d9450573e)


8. Trata de que el robot avance medio metro y luego gire PI/2. Indica el proceso.  
    
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

