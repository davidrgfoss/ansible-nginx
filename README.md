# ansible-nginx
Realiza la configuración básica de nginx que ejecute scripts PHP creando una receta ansible.

##### 1. Instalación de los servicios (cada servicio se instalará y configurará en un rol diferenciado).
##### 2. Además de copiar un index.html en el DocumentRoot, copiará también un fichero info.php que muestre la información de la configuración de PHP.
##### 3. Como hace la receta original, creará virtualhost que tengas definido en una lista. Estos virtual host estarán configurados para ejecutar PHP.
##### 4. La receta debe poder desactivar los virtualhost que tengas definido en otra lista.
##### 5. Configura sobre una máquina virtual, usando la receta de ansible, un servidor nginx + PHP con dos virtualhost:
  * www.pagina1.org, cuyo DocumentRoot estará en /srv/www/pagina1.
  * www.pagina2.org, cuyo DocumentRoot estará en /srv/www/pagina2.

### Funcionamiento de la receta ansible.

Esta receta se compone de diferentes directorios, cada uno para un rol en específico. Lo más importante sería el directorio **"nginx"**, en este caso toda la configuración de los *virtualhost* de **"nginx"** se harán desde el fichero de variables dentro de **"group_vars"**. Actualmente hay definido dos **"virtualhost"**, si añadimos alguno más manteniendo la estructura se creará. En este fichero de variable, deberemos indicar el estado del **"virtualhost"** que vamos a crear o eliminar con las opciones ***"create/delete"***.

En el fichero de la receta perteneciente al rol **"nginx"** tenemos dos tareas principales a ejecutar, una creará los vhost, directorios etc, y otra los eliminará. Ambas son personalizables, basta con deshabilitar el **"notify"** de eliminar directorios si no queremos que se eliminen al borrar el **"virtualhost"** o quitar la copia de un fichero **"index.html"** si no tenemos ninguno dentro del directorio **"file"**.
