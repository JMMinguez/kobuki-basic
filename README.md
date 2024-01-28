[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-24ddc0f5d75046c5622901739e7c5dd533143b0c8e959d652212380cedb1ea36.svg)](https://classroom.github.com/a/tecaRa11)
# 2024-P1-Kobuki

El objetivo de esta práctica es usar los comandos de ROS 2 en la terminal para examinar el robot Kobuki.

Debes completar el siguiente cuestionario para realizar la práctica. Incluye los comandos que has usado en cada una:


1. ¿Has tenido que hacer algún setup en tu ordenador? Indica los pasos
   
   [Respuesta]

3. ¿Qué comando has usado para lanzar el Kobuki en ROS 2?

   Para lanzar el Kobuki en ROS 2 con el simuladopr Gazebo he usado el siguiente comando:

   ```
   ros2 launch kobuki simulation.launch.py
   ```

5. ¿Qué nodos se lanzan? 
   
   Una vez lanzado el Kobuki, si en otra terminal escribimos:
   ```
   ros2 node list
   ```
   nos aparece la lista de los nodos.  
   ![Captura desde 2024-01-28 12-13-38](https://github.com/Docencia-fmrico/2024-p1-kobuki-jmartinm2021/assets/92941332/08c93e72-dc67-4e14-b7ec-b57244925578)


7. ¿Qué topics están disponibles? 
   
   Una vez lanzado el Kobuki, si en otra terminal escribimos:
   ```
   ros2 topic list
   ```
   nos aparece la lista de los topic.  
   ![Captura desde 2024-01-28 12-16-11](https://github.com/Docencia-fmrico/2024-p1-kobuki-jmartinm2021/assets/92941332/820b3aba-f40d-49b1-9de7-ae465d59c012)


9. Analiza los topics (tipo, QoS y explicación de campos) que permiten hacer al robot moverse, detectar obstáculos con el bumper y recibir la información del láser.
   - **Movimiento:**
        - Topic: /cmd_vel
        - Type: geometry_msgs/msg/Twist
   - **Bumper:**
        - Topic: 
   - **Láser:**
        - Topic: /scan
        - Type: sensor_msgs/msg/LaserScan
10. ¿Qué servicios o acciones están disponibles? 
   
   [Respuesta]

11. Haz una diagrama del Kobuki con [drawio](https://app.diagrams.net/) similar al del robot Tiago que te muestro, cuyo fuente está en el repositorio. El diagrama debe mostrar los nodos existentes, sus conexiones y su tipo. Sube al repositorio tanto un .png como el fuente .drawio.
![tiago_graph](https://github.com/Docencia-fmrico/2024-P1-Kobuki/assets/3810011/a2161319-f181-4905-8fd2-2b1ed3f2151e)

12. Trata de que el robot avance medio metro y luego gire PI/2. Indica el proceso.
