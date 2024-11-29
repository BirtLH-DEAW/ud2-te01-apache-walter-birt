# Ejemplo de fichero Dockerfile
# Crea una nueva imagen a partir de httpd, verisón 2.4

FROM ubuntu:latest

# Da información sobre la imagen que estamos creando
# Podemos usar la \ para encadenar todos los valores
LABEL \
	authors="DEAW" \
	version="2.0" \
	description="DEAW02. Tarea evaluativa 1" \
	creationDate="99-99-9999"

# Ejecutamos diferentes comandos
# Debemos encadenarlos en un mismo RUN mediante la \
RUN \
	apt-get update \ 
	&& apt-get -y install nano apache2 openssl

# Crear las carpetas necesarias en el contenedor
RUN mkdir -p /var/www/html/wabanchero/privado

# Se copian las plantillas web 
COPY ./html/index.html /var/www/html
COPY ./html/css_index /var/www/html/css_index
COPY ./html/virtualhost.html /var/www/html/wabanchero
COPY ./html/css_virtualhost /var/www/html/wabanchero/css_virtualhost
COPY ./html/privado.html /var/www/html/wabanchero/privado
COPY ./html/css_privado /var/www/html/wabanchero/privado/css_privado

# Se copian los archivos de configuaración, clave y certificados
COPY ./conf/virtualhost.conf /etc/apache2/sites-available/
COPY ./conf/htpasswd /etc/apache2/htpasswd
COPY ./conf/certs/virtualhost.pem /etc/ssl/certs/virtualhost.pem
COPY ./conf/certs/virtualhost.key /etc/ssl/private/virtualhost.key

# Habilitar configuraciones y módulos necesarios
RUN a2enmod ssl\
&& a2ensite virtualhost.conf

# Indica el puerto que utiliza la imagen
# para que lo mapeemos al crear el contenedor
EXPOSE 80 443

