# ASR-02

# 1a Solución: creación de máquina de salto - 4 puntos

+ Montar una máquina de salto para poder acceder a nuestro servidor web. Esta máquina se debería encender y apagar cada vez que se quiera modificar algo del servidor web.
+ Exponer únicamente en ambos servidores lo mínimo indispensable con reglas de firewall (firewall capa 4).

## Creación de las Vm Instances (Máquina de salto y Servidor Web):

+ Servidor Web

![image](https://github.com/IgnacioHernandezBas/ASR/assets/91118338/e2e3a637-970d-4997-852a-9e0b874da864)


+ Jump Server
  
![image](https://github.com/IgnacioHernandezBas/ASR/assets/91118338/65a1d845-7a4f-48ed-a97b-2840c8ad6adf)


## Creación de las reglas de firewall para ambas instancias

+ Servidor Web
  
![image](https://github.com/IgnacioHernandezBas/ASR/assets/91118338/f4acc4e4-6dab-4c7c-b891-732eeec0e909)



+ Jump Server
  
![image](https://github.com/IgnacioHernandezBas/ASR/assets/91118338/1df93d91-4f0f-45b7-9611-6baf5ebd31dd)

## Comprobación de acceso a las instancias

+Jump Server (SSH):

![image](https://github.com/IgnacioHernandezBas/ASR/assets/91118338/dabdd1f5-528c-4f3b-a7bc-82e645f311f0)


+Servidor Web: 

Se puede acceder a este mediante el jump server (SSH).

![image](https://github.com/IgnacioHernandezBas/ASR/assets/91118338/df6ddaea-5da7-47a6-b016-58c92eb3ac02)

Acceso web a NginX

![image](https://github.com/IgnacioHernandezBas/ASR/assets/91118338/a0fd8a1f-a1af-4040-9afd-624e7f909778)




# 2da mejora solución: introducción a los WAF - Web Application Firewall (firewall capa 7) - 4 puntos

## Convertir nuestro servidor web para que no tenga ip pública

  ![image](https://github.com/IgnacioHernandezBas/ASR/assets/91118338/8c3656b5-cbf9-4ddb-863d-0215378a74ef)


## Montar un balanceador con servicio de WAF haciendo HTTPS offloading.

  ![image](https://github.com/IgnacioHernandezBas/ASR/assets/91118338/062c47b9-0324-4809-873e-e6c16f4d54c6)

  + Creación certificado

    ![image](https://github.com/IgnacioHernandezBas/ASR/assets/91118338/c9426edb-df9a-4eeb-b8a3-85fa2f4b1b07)


  + Healthcheck

    ![image](https://github.com/IgnacioHernandezBas/ASR/assets/91118338/ccac88b0-4561-448d-9fdd-8442da1a7fd4)

  + Backend

    ![image](https://github.com/IgnacioHernandezBas/ASR/assets/91118338/9ae23729-e352-439d-a526-ede8e97d7fd4)



    

  

## ¿Qué ventajas e incovenientes tiene hacer https offloading en el balanceador?

Emplear https offloading libera carga y recursos necesarios en los servidores debido a que el balancer s eencarga del proceso de cifrado y descifrado aliviando esta tarea a las instancias. A costa de esto, la red interna es menos segura al no estar cifrada la información al traspasar el load balancer. 


## ¿Qué pasos adicionales has tenido que hacer para que la máquina pueda salir a internet para poder instalar el servidor nginx?

Es necesario habilitar la **cloud NAT** para poder llevar a cabo la instalación de Nginx en el servidor web.

![image](https://github.com/IgnacioHernandezBas/ASR/assets/91118338/77568845-2d56-4f31-b558-84480c3ef36c)


## Proteger nuestra máquina de ataques SQL Injection, Cross Syte Scripting y restringir el tráfico sólo a paises de confianza de la UE implantando un WAF a nuestro balanceador.

Para llevar a cabo esta tarea se han establecido las siguientes reglas en el apartado de **cloud armor** perteneciente al load balancer.

![image](https://github.com/IgnacioHernandezBas/ASR/assets/91118338/cbbb8552-63b9-4119-afc2-f77dfd8001e0)

## Acceso a Nginx del servidor web a partir del load balancer

Para acceder al servidor web, al no tener IP pública, es necesario acceder a partir de la dirección load balancer desde el navegador.

![image](https://github.com/IgnacioHernandezBas/ASR/assets/91118338/e8c5a2e9-edda-4c65-85cd-50eda3644a97)


## 3ra mejora solución: zero trust - 1 punto
- Cifrar el contenido web también dentro del cloud y quitar el HTTPS offloading.

## 4ta mejora solución - 1 punto
¿Qué otras mejoras se te ocurrirían para mejorar la seguridad o disponibilidad del servidor web? (No hace falta implementarlas)










