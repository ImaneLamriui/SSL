<!-- Algunos de los usos más comunes de OpenSSL incluyen la creación y gestión de certificados digitales, la generación de claves criptográficas, la firma y verificación de datos, y la realización de pruebas de vulnerabilidad en sistemas y aplicaciones. -->
<h1>Pemitir el protocolo HTTPS utilizando la biblioteca OpenSSL</h1>
<p>Algunos de los usos más comunes de OpenSSL incluyen la creación y gestión de certificados digitales, la generación de claves criptográficas, la firma y verificación de datos, y la realización de pruebas de vulnerabilidad en sistemas y aplicaciones.
   En la carpeta  tenemos nuestro proyecto que contiene nuestra página index.html en este caso es la página wiue viene por defecto con apache2, tambien se puede editarla pero sigue funcionando con el protocolo http</p>
<ul>
   <li>Instalar el paquete openSSL:<br>
      sudo apt update<br>
      sudo apt upgrade<br>
      sudo apt-get install openssl<br></li>
      <img src="images/openSSL.png" alt="openSSL">

   <li>Crear un certificado autofirmado para el servidor web, para ello creamos carpeta donde guardar el certificado:<br>
           #sudo mkdir /etc/apache2/tu-cert<br>
           <img src="images/createSSLdirectory.png" alt="create-your-cert1">
      entramos al directorio:<br>
           #cd /etc/apache2/tu-cert<br>
      activamos ssl:<br>
           #sudo a2enmod ssl<br>
      nos piderá el sistema reiniciar el servidor con:<br>
           #systemstl restart apache2<br>
           <img src="images/privateKey.png" alt="create-your-cert2">
      creamos el nuevo certificado:<br>
           #sudo opessl req -new -nodes -keyout www.empresa-tarea-daw02.local.key -out www.empresa-tarea-daw02.local.csr<br> 
      se genera la clave privada del certificado(private key)<br>
          <img src="images/10y.png" alt="cert-created"><br>
      lo personalizamos y le signamos al certificado 10 años de validez<br>
           #sudo openssl x509 -in www.empresa-tarea-daw02.local.csr -out www.empresa-tarea-daw02.local.crt -req -signkey www.empresa-tarea-daw02.local.key -days 3650<br>

      si a pasado todo bien: en la firma sale el resultado ok(signature ok)<br>
      luego comprobamos los datos del certificado en el navegador<br></li>

   <li>por defecto se nos cargará la página de apache insegura o sin el certificado ssl para ello hay que deshabilitar
      el archivo 000-default para evitar que se cargue la página html de apache2 en nuestro
      sitio, posteriormente crearé una página html para el nuevo sitio, es esta página que se cargará cuando llamamos a la página web:<br>
           <img src="images/test-navegator.png" alt="test-navegator"><br>
           #sudo a2dissite 000-default.conf<br>
           #systemctl reload apache2<br>
           <img src="images/disabled-000-default.png" alt="disabled-000-default"><br>
      configurar el archivo de configuración(imágen): todo-empresa-tarea-daw02-ssl.conf y activarlo:<br>
          # sudo a2ensite todo-empresa-tarea-daw02-ssl.conf<br></li>
          <img src="images/update-ssl-file.png" alt="update-ssl-file"><br>
          <img src="images/activate-ssl-file.png" alt="activate-ssl-file"><br>
   <li>comprobamos accediendo con el protocolo https, el certificado es autofirmado, y no se ha reconocido del navegador porque no lo contiene en su listado de los certofocados reconocidos.Por eso muestra adverencia en la url
      Podemos personalizar la página html para obtenerla por ejemplo así(imagen), el archivo html se encuentra en la
      carpeta /var/www/todo-empresa-tarea-daw02<br>
      <img src="images/createhtml.png" alt="HTML"><br>
      <img src="images/webSSL.png"  alt="webSSL"><br>
      <img src="images/certAdministrator.png" alt="certAdministrator"><br>
      <img src="images/port443Activate.png" alt="port443Activate"><br>
   </li>
</ul>
