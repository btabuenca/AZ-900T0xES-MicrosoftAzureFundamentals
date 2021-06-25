---
wts:
    title: '04 - Crear una red virtual (20 minutos)'
    module: 'Módulo 2 - Servicios principales de Azure (Cargas de trabajo)'
---
# 04 - Crear una red virtual

En este tutorial crearemos una red virtual, implementaremos dos máquinas virtuales en esa red virtual y luego permitiremos que una máquina virtual haga ping a la otra dentro de esa red.

# Tarea 1: Crear una red virtual (20 minutos)

En esta tarea, crearemos una red virtual. 

1. Inicie sesión en Azure Portal en <a href="https://portal.azure.com" target="_blank"><span style="color: #0066cc;" color="#0066cc">https://portal.azure.com</span></a>

2. Desde la hoja **Todos los servicios**, busque y seleccione **Redes virtuales** y haga clic en **+ Agregar, + Crear, o + Nuevo** 

3. En la hoja **Crear red virtual** complete lo siguiente (deje los valores predeterminados para todo lo demás):

    | Configuración | Valor | 
    | --- | --- |
    | Suscripción | **Seleccione su suscripción** |
    | Grupo de recursos | **myRGVNet** (crear nuevo) |
    | Nombre | **vnet1** |
    | Ubicación | **(EE. UU.) Este de EE. UU.** |
    | Espacio de direcciones |**10.1.0.0/16** |
    | Subred - Nombre | **predeterminado** |
    | Rango de dirección de subred | **10.1.0.0/24** |

    ![Captura de pantalla del paso "Básico" de la hoja Crear red virtual con los campos predeterminados.](../images/0301a.png)
    ![Captura de pantalla del paso "Dirección IP" de la hoja Crear red virtual con los campos predeterminados.](../images/0301b.png)

5. Haga clic en el botón **Revisar y crear**. Asegúrese de que la validación sea exitosa.

6. Haga clic en el botón **Crear** para implementar la red virtual. 

    **Nota**: En su organización, ¿cómo sabrá qué redes virtuales y direccionamiento IP necesitará?

# Tarea 2: Crear dos máquinas virtuales

En esta tarea crearemos dos máquinas virtuales en la red virtual. 

1. Desde la hoja **Todos los servicios** busque **Máquinas virtuales** y luego haga clic en **+ Agregar** y seleccione **+ Maquinas virtuales**. 

2. En la pestaña **Datos básicos**, complete la siguiente información (deje los valores predeterminados para todo lo demás):

   | Configuración | Valor | 
   | --- | --- |
   | Suscripción | **Elija su suscripción**  |
   | Grupo de recursos |  **myRGVNet** |
   | Nombre de la máquina virtual | **vm1**|
   | Región | **(EE. UU.) Este de EE. UU.** |
   | Imagen | **Centro de datos de Windows Server 2019** |
   | Nombre de usuario| **azureuser** |
   | Contraseña| **Pa$$w0rd1234** |
   | Puertos de entrada públicos| Seleccione **Permitir puertos seleccionados**  |
   | Puertos de entrada seleccionados| **RDP (3389):** |
   |||

3. Seleccione la pestaña **Redes**. Asegúrese de que la máquina virtual esté ubicada en la red virtual vnet1. Revise la configuración predeterminada, pero no realice ningún otro cambio. 

   | Configuración | Valor | 
   | --- | --- |
   | Red virtual | **vnet1** |
   |||

4. Haga clic en **Revisar y crear**. Después de que la validación sea exitosa, haga clic en **Crear**. Los tiempos de implementación pueden variar, pero generalmente la implementación demora entre tres y seis minutos.

5. Supervise su implementación, pero continúe con el siguiente paso. 

6. Cree una segunda máquina virtual repitiendo los pasos anteriores del **2 al 4**. Asegúrese de usar un nombre de máquina virtual diferente, que la máquina virtual esté dentro de la misma red virtual y que esté usando una nueva dirección IP pública:

    | Configuración | Valor |
    | --- | --- |
    | Grupo de recursos | **myRGVNet** |
    | Nombre de la máquina virtual |  **vm2** |
    | Red virtual | **vnet1** |
    | IP pública | (nuevo) **vm2-ip** |
    |||

7. Espere a que se implementen ambas máquinas virtuales. 

# Tarea 3: Probar la conexión 

En esta tarea, permitiremos iniciar sesión en una de las máquinas virtuales y hacer ping a la otra. 

1. Desde la hoja **Todos los recursos**, busque **vm1**, abra la pestaña **Vista general** y asegúrese de que su **Estado** sea **En ejecución**. Es posible que necesite **Actualizar** la página.

2. En la hoja **Información general**, haga clic en el botón **Conectar**.

    **Nota**: Las siguientes instrucciones le indican cómo conectarse a su VM desde un equipo con Windows. 

3. En la hoja **Conectar a la máquina virtual**, mantenga las opciones predeterminadas en conectarse por dirección IP a través del puerto 3389 y haga clic en **Descargar archivo RDP**.

4. Abra el archivo RDP descargado y haga clic en **Conectar** cuando se le solicite. 

5. En la ventana **Seguridad de Windows**, escriba el nombre de usuario **azureuser** y la contraseña **Pa$$w0rd1234** y luego haga clic en **Aceptar**.

6. Es posible que reciba una advertencia de certificado durante el proceso de inicio de sesión. Haga clic en **Sí** o cree la conexión y conéctese a su VM implementada. Debería conectarse correctamente.

7. Abra un símbolo del sistema de PowerShell en la máquina virtual haciendo clic en el botón **Inicio**, escribiendo **PowerShell**, haciendo clic con el botón derecho en **Windows PowerShell** en el menú del botón derecho y seleccionando **Ejecutar como administrador**.

8. En Powershell, teclee el siguiente comando para establecer comunicación con la vm2, podrá ver si ha tenido éxito.

   ```PowerShell
   ping vm2
   ```

¡Enhorabuena! Ha configurado dos máquinas virtuales y las ha implementado en una red virtual. Y ha comprobado que puede comunicarse entre las dos máquinas virtuales. 

**Nota**: Para evitar costes adicionales, puede quitar este grupo de recursos. Busque grupos de recursos, haga clic en su grupo de recursos y, a continuación, haga clic en **Eliminar grupo de recursos**. Compruebe el nombre del grupo de recursos y luego haga clic en **Eliminar**. Supervise las **Notificaciones** para ver cómo se realiza la eliminación.
