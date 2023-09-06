<!-- Algunos de los usos más comunes de OpenSSL incluyen la creación y gestión de certificados digitales, la generación de claves criptográficas, la firma y verificación de datos, y la realización de pruebas de vulnerabilidad en sistemas y aplicaciones. -->
<!-- En resumen, los dominios ".local" son una forma conveniente de identificar dispositivos y servicios en una red local sin necesidad de configurar un servidor DNS externo. Sin embargo, es importante recordar que estos nombres solo son válidos y significativos dentro de la red local en la que se utilizan. -->
# Allow HTTPS protocol using OpenSSL library and Apache web server.
# Prerequisites:
* A web server (for example Apache) installed on your host.
* A domain name for your website: in this example i have used the domain: www.empresa-tarea-daw02.local
# Some of the most common uses for OpenSSL include creating and managing digital certificates, generating cryptographic keys, signing and verifying data, and performing vulnerability testing on systems and applications..
# In the folder we have our project that contains our index.html page, in this case it is the page that comes by default with apache2.
* Commands to install the openSSL package:<br>
**sudo apt update**<br>
**sudo apt upgrade**<br>
**sudo apt-get install openssl**<br>
<img src="images/openSSL.png" alt="openSSL"><br>
* Crear un certificado autofirmado para el servidor web, para ello creamos carpeta donde guardar el certificado:<br>
**sudo mkdir /etc/apache2/tu-cert**<br>
<img src="images/createSSLdirectory.png" alt="create-your-cert1"><br><br>
## entramos al directorio:<br>
**cd /etc/apache2/tu-cert**<br>
## Enable the SSL Module:<br>
**sudo a2enmod ssl**<br>
## Test Configuration:
* Before restarting Apache, it's a good practice to test the configuration for syntax errors:
**sudo apachectl configtest**
## nos piderá el sistema reiniciar el servidor:<br>
**systemstl restart apache2**<br>
<img src="images/privateKey.png" alt="create-your-cert2"><br><br>
## Update DNS Records:
* Ensure your domain's DNS records (CNAME or other) point to the correct IP address of your host.
## creamos el nuevo certificado:<br>
**sudo opessl req -new -nodes -keyout www.empresa-tarea-daw02.local.key -out www.empresa-tarea-daw02.local.csr**<br> 
## se genera la clave privada del certificado(private key)<br>
<img src="images/10y.png" alt="cert-created"><br><br>
## lo personalizamos y le signamos al certificado 10 años de validez<br>
**sudo openssl x509 -in www.empresa-tarea-daw02.local.csr -out www.empresa-tarea-daw02.local.crt -req -signkey www.empresa-tarea-daw02.local.key -days 3650**<br>
## si a pasado todo bien: en la firma sale el resultado ok(signature ok)<br>
## Update Server Configuration (Apache): todo-empresa-tarea-daw02-ssl.conf y activarlo:<br>
**sudo a2ensite todo-empresa-tarea-daw02-ssl.conf**<br></li>
<img src="images/update-ssl-file.png" alt="update-ssl-file"><br><br>
<img src="images/activate-ssl-file.png" alt="activate-ssl-file"><br><br>
**Comprobamos los datos del certificado en el navegador**<br>
<img src="images/test-navegator.png" alt="test-navegator"><br><br>
* por defecto se nos cargará la página de apache insegura o sin el certificado ssl para ello hay que deshabilitar
el archivo 000-default para evitar que se cargue la página html de apache2 en nuestro
sitio, posteriormente crearé una página html para el nuevo sitio, es esta página que se cargará cuando llamamos a la página web:<br>
**sudo a2dissite 000-default.conf**<br>
**systemctl reload apache2**<br>
<img src="images/disabled-000-default.png" alt="disabled-000-default"><br><br>
## comprobamos accediendo con el protocolo https, el certificado es autofirmado, y no se ha reconocido del navegador porque no lo contiene en su listado de los certofocados reconocidos.Por eso muestra adverencia en la url<br>
<img src="images/webSSL.png"  alt="webSSL"><br><br>
## Podemos personalizar la página html para obtenerla por ejemplo así(imagen), el archivo html se encuentra en la carpeta #/var/www/todo-empresa-tarea-daw02<br>
<img src="images/createhtml.png" alt="HTML"><br><br>
## comprobamos administrador de certificados:<br>
<img src="images/certAdministrator.png" alt="certAdministrator"><br><br>
## comprobamos puerto activado:<br>
**sudo netstat -tuln**<br>
<img src="images/port443Activate.png" alt="port443Activate"><br><br>
   

