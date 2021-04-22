# aws-cloud-engineer-sprint-1
Primer sprint del bootcamp Cloud Engineer


# CloudSprint 1: Sitio estático

En este CloudSprint pondrás en práctica las distintas metodologías para el despliegue de sitios  web estáticos con un caso de negocio




## Problemática

Pizza as a Service es una compañía emergente que está buscando migrar sus aplicaciones a la nube, no tienen ninguna experiencia y se muestran temerosos respecto a la utilización de la misma. Tu deber como Cloud Engineer es realizar un trabajo que los pueda convencer completamente.

En este primer sprint, deberás lanzar su sitio web estático en la nube con las siguientes características.



*   Redireccionamiento de un dominio paas-{tu-nombre}.tk  (o cualquier otro dominio que incluya el texto paas)
*   Escalabilidad del servicio
*   Modelo de Costos

¿Imágenes de arquitectura e historia?


# Paso 1: Registrar un dominio DNS

Utilizaremos registros de dominios gratuitos para integrar con Route53, te recomendamos [freenom](http://freenom.org/)



1. Busca y selecciona un dominio gratuito en freenom
2. Click en el dominio (**Get it now!)**
3. Click en **Checkout**
4. Ingresa tu información de contacto, recibirás un correo electrónico de confirmación
5. Inicia sesión con la cuenta creada en freenom



<p id="gdcalert4" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image1.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert5">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image1.png "image_tooltip")




6. Click en la pestaña de **Services**
7. Selecciona **My Domains**
8. Observarás que el dominio solicitado se muestra en el tablero



<p id="gdcalert5" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image2.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert6">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image2.png "image_tooltip")



# Paso 2: Desplegar el aplicativo en EC2



1. Lanza una instancia de EC2 con las siguientes características
    1.  AMI: **Amazon Linux 2**
    2. Type: **t2.micro**
    3. Key: **Name **Value: **ec2-paas**
    4. Security Group: **SSH 0.0.0.0/0 y HTTP 0.0.0.0/0**
    5. Resguarda las 
2. En el paso **3.** **Configure Instance **ingresa el siguiente código para lanzar un servidor web


```#!/bin/bash
yum -y install httpd
systemctl enable httpd
systemctl start httpd
```



3. Inicializa un ambiente de **Cloud9** y conéctate a la instancia lanzada
4. Clona el repositorio del Sprint

```
git clone https://github.com/lemmhub/aws-cloud-engineer-sprint-1 
```




5. Descomprime la carpeta del repositorio

```
unzip aws-cloud-engineer-sprint-1/CloudSprint_1.zip 
```



6. Copia la carpeta descomprimida en la ruta de apache para ejecutar el aplicativo

<table>
  <tr>
   <td>


<p id="gdcalert9" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image6.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert10">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


<img src="images/image6.png" width="" alt="alt_text" title="image_tooltip">

   </td>
   <td>#Asegúrate de estar en la carpeta de git
<p>
cd CloudSprint_1/
<p>
 sudo mv index.html /var/www/html/
<p>
sudo mv images/ /var/www/html/
<p>
#revisa la carpeta de apache
<p>
cd /var/www/html/
<p>
ls  -a
   </td>
  </tr>
</table>




7. Revisa el aplicativo desplegado


   <td><strong>Challenge :</strong> Recrea el aplicativo como un sitio estático en S3
   </td>



# Paso 3: Integrar con Route53



1.  Crea una nueva **Hosted Zone** en Route53 
    1. En el menú lateral selecciona **Hosted Zone**
    2. Click en **Create hosted zone**
    3. Ingresa los nombres del dominio
    4. Click en **Create  hosted zone**



<p id="gdcalert11" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image8.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert12">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image8.png "image_tooltip")




2. Deberás configurar freenom para poder vincular con Route53
    1. Ingresa en **My domains**
    2. Selecciona **Manage Domain **en el dominio creado



<p id="gdcalert12" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image9.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert13">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image9.png "image_tooltip")




    3. 
3.  Selecciona **Create record**
    4. Selecciona la pestaña **Management Tools, Name Servers**
    5. Elige la opción** Custom Name Servers**
    6. Deberás ingresar a Route 53 y buscar en tu Hosted Zone los NS



<p id="gdcalert13" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image10.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert14">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image10.png "image_tooltip")




    7. Copia y pega dichos valores en freenom
4. Selecciona **Create record **en **Route53**
    8. Elige **Simple routing**



<p id="gdcalert14" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image11.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert15">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image11.png "image_tooltip")




    9. Click en **Next**
    10. Selecciona **Define simple record**
    11. Elige: **A – Routes traffic to an IPv4 address and some AWS resources**
    12. Value/Route traffic to: **IP address or another, depending on the record type**
    13. Ingresa la **IP de la instancia**
    14. Click en **Define simple record**
    15. Prueba  la liga del dominio de freenom
5. Elimina el record creado y genera uno para el sitio web estático en S3
6. Selecciona **Create record **en **Route53**
    16. Elige **Simple routing**
    17. Click en **Next**
    18. Selecciona **Define simple record**
    19. Elige: **A – Routes traffic to an IPv4 address and some AWS resources**
    20. Value/Route traffic to: **Alias to S3 website endpoint**
    21. Ingresa la **url del sitio estático**
    22. Click en **Define simple record**
    23. Prueba  la liga del dominio de freenom


# Paso 4: Revisar los costos de la implementación



1. Ingresa la [calculadora de costos de AWS](https://calculator.aws/#/)
2. Click en **Create estimate**
3. Busca el servicio EC2
4. Click en **Configure**
5. Prueba las distintas configuraciones de costos



<p id="gdcalert15" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image12.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert16">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image12.png "image_tooltip")




6. Selecciona **Add to my estimate**
7. Click en **Add service**
8. Busca** Route 53, **click en **Configure**
9. Solo deberás ingresar el número de **Hosted Zones = 1**


   <td><strong>Challenge :</strong> Realiza un reporte similar basado en S3
   </td>



```
¡Felicidades, has terminado el laboratorio! 👏 
Ayúdanos a mejorar y califica tu experiencia
⭐
⭐⭐
⭐⭐⭐
⭐⭐⭐⭐
⭐⭐⭐⭐⭐
¿Comentarios? Escríbenos a labs@bootcamp.institute
