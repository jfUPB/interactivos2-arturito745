

# ** PASOS PARA EJECUTAR UNA APLICACIÓN LOCAL CON ** 

## **1️⃣ Instalación de Node.js en Windows**  
Antes de comenzar, necesitamos instalar **Node.js**, ya que nos permitirá ejecutar JavaScript fuera del navegador y gestionar paquetes con `npm`.  

🔹 **Pasos:**  
1. Vamos a la página oficial de **Node.js**:  
    [https://nodejs.org/](https://nodejs.org/)  
2. Descargamos la versión **LTS (Long Term Support)** recomendada.  
3. Instalamos el archivo `.msi` siguiendo el asistente.  
4. Abrimos la terminal (**CMD o PowerShell**) y verificamos la instalación con:  
   ```sh
   node -v
   npm -v
   ```  
   Si nos muestra versiones (ejemplo: `v18.x.x` y `9.x.x`), **Node.js y npm están instalados correctamente**.  

---

## **2️⃣ Clonar el repositorio desde GitHub Desktop**  
Usaremos **GitHub Desktop** para clonar nuestro proyecto desde un repositorio en GitHub.  

🔹 **Pasos:**  
1. Abrimos **GitHub Desktop**.  
2. Vamos a **File > Clone repository...**.  
3. Seleccionamos la opción **"URL"** e ingresamos la dirección del repositorio.  
4. Elegimos una carpeta en nuestro PC donde guardaremos el proyecto.  
5. Hacemos clic en **"Clone"** y esperamos a que termine la descarga.  

---

## **3️⃣ Abrir el proyecto en la terminal**  
Necesitamos acceder al directorio del proyecto para trabajar con él.  

🔹 **Pasos:**  
1. En **GitHub Desktop**, vamos a **Repository > Open in Command Prompt**.  
2. Navegamos hasta la carpeta del servidor con:  
   ```sh
   cd server
   ```

---

## **4️⃣ Instalar dependencias del proyecto**  
Nuestro proyecto usa bibliotecas de Node.js, que debemos instalar antes de ejecutarlo.  

🔹 **Pasos:**  
1. Dentro de la carpeta `server`, ejecutamos:  
   ```sh
   npm install
   ```  
   Esto instalará todas las dependencias necesarias, como **Express** y **Socket.IO**.  

---

## **5️⃣ Ejecutar el servidor**  
Para iniciar el servidor, usaremos **npm start** en lugar de `node server.js`.  

🔹 **Pasos:**  
1. Ejecutamos:  
   ```sh
   npm start
   ```  
2. La terminal debería mostrar un mensaje indicando que el servidor está corriendo en:  
   ```
   Server is listening on http://localhost:3000
   ```
3. **¡El servidor ya está funcionando!**  

---

## **6️⃣ Modificar `sketch.js` para la URL correcta**  
El archivo `sketch.js` es la parte del cliente que se conecta al servidor. Necesitamos cambiar la URL del socket para que funcione correctamente.  

🔹 **Pasos:**  
1. Abrimos el archivo `sketch.js` en un editor de texto.  
2. Modificamos la URL del socket para que apunte a la ruta correcta:  
   ```
   http://localhost:3000/desktop/index.html
   ```
3. Guardamos los cambios.  

---

## **7️⃣ Guardar los cambios en Git y subirlos a GitHub**  
Una vez que hemos modificado el archivo, debemos guardar estos cambios en nuestro repositorio.  

🔹 **Pasos:**  
1. Vamos a **GitHub Desktop** y verificamos los archivos modificados.  
2. Escribimos un mensaje de commit, por ejemplo:  
   ```
   Modifiqué sketch.js con la nueva URL
   ```
3. Hacemos clic en **"Commit to main"**.  
4. Hacemos clic en **"Push origin"** para subir los cambios a GitHub.  

---

## **8️⃣ Probar la aplicación en el navegador**  
Finalmente, verificamos que todo esté funcionando correctamente.  

🔹 **Pasos:**  
1. Abrimos el navegador y vamos a:  
   ```
   http://localhost:3000/desktop/index.html
   ```
2. Revisamos la consola del navegador (**F12 > Console**) para ver si hay errores.  
3. Si todo funciona bien, veremos nuestra aplicación en ejecución y conectada al servidor.  



