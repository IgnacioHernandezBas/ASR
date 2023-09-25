# ASR-02

## 1a Solución: creación de máquina de salto - 4 puntos
+ Montar una máquina de salto para poder acceder a nuestro servidor web. Esta máquina se debería encender y apagar cada vez que se quiera modificar algo del servidor web.
+ Exponer únicamente en ambos servidores lo mínimo indispensable con reglas de firewall (firewall capa 4).

# Creación de las Vm Instances (Máquina de salto y Servidor Web):
+ Servidor Web
![image](https://github.com/IgnacioHernandezBas/ASR/assets/91118338/e2e3a637-970d-4997-852a-9e0b874da864)


+ Jump Server
![image](https://github.com/IgnacioHernandezBas/ASR/assets/91118338/65a1d845-7a4f-48ed-a97b-2840c8ad6adf)


# Creación de las reglas de firewall para ambas instancias
+ Servidor Web
![image](https://github.com/IgnacioHernandezBas/ASR/assets/91118338/f4acc4e4-6dab-4c7c-b891-732eeec0e909)



+ Jump Server
![image](https://github.com/IgnacioHernandezBas/ASR/assets/91118338/1df93d91-4f0f-45b7-9611-6baf5ebd31dd)

# Comprobación de acceso por SSH a las instancias
+Jump Server:
![image](https://github.com/IgnacioHernandezBas/ASR/assets/91118338/dabdd1f5-528c-4f3b-a7bc-82e645f311f0)


+Servidor Web: solamente se puede acceder a este mediante el jump server a pesar de presentar una ip externa. En las siguiente captura se observa el acceso a partir del jump server.
![image](https://github.com/IgnacioHernandezBas/ASR/assets/91118338/df6ddaea-5da7-47a6-b016-58c92eb3ac02)
Por otro lado si se trata de acceder desde el propio equipo del usuario, la conexión no es admitida.
![image](https://github.com/IgnacioHernandezBas/ASR/assets/91118338/504ee781-d6ed-45cb-a289-bffac36f3d87)

## 2da mejora solución: introducción a los WAF - Web Application Firewall (firewall capa 7) - 4 puntos
+ Convertir nuestro servidor web para que no tenga ip pública

  ![image](https://github.com/IgnacioHernandezBas/ASR/assets/91118338/8c3656b5-cbf9-4ddb-863d-0215378a74ef)


+ Montar un balanceador con servicio de WAF haciendo HTTPS offloading.

  ![image](https://github.com/IgnacioHernandezBas/ASR/assets/91118338/062c47b9-0324-4809-873e-e6c16f4d54c6)




+¿Qué ventajas e incovenientes tiene hacer https offloading en el balanceador?

Emplear Https offloading libera la carga y recursos necesarios para el proceso de cifrado y descifrado por parte de las instancias. A costa de esto la red interna es menos segura al no estar cifrada la información al traspasar el load balancer. 





+ ¿Qué pasos adicionales has tenido que hacer para que la máquina pueda salir a internet para poder instalar el servidor nginx?








+ Proteger nuestra máquina de ataques SQL Injection, Cross Syte Scripting y restringir el tráfico sólo a paises de confianza de la UE implantando un WAF a nuestro balanceador.

## 3ra mejora solución: zero trust - 1 punto
- Cifrar el contenido web también dentro del cloud y quitar el HTTPS offloading.

## 4ta mejora solución - 1 punto
¿Qué otras mejoras se te ocurrirían para mejorar la seguridad o disponibilidad del servidor web? (No hace falta implementarlas)










