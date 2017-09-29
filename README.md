
## Automatización de Flujos de Documentos y Firma Electrónica. 

La Ley de Firma Electronica de El Salvador instruye a las instituciones públicas a implementar sistemas de gestión de documentos que utilicen firma electrónica para eliminar las copias físicas:

Art. 29.- Las autoridades, funcionarios y empleados del Estado que presten servicios públicos dentro de su ámbito de competencia podrán suscribirlos por medio de firma electrónica simple.

Esta guía muestra como instalar el gestor documental libre Alfresco para implementar flujos de trabajo y firmar documentos electronicamente. Esta guía utiliza Alfresco 5.1 y Ubuntu 16.04 LTS y debería funcionar en otros sistemas Linux. 

## Instalación
El módulo requerido para firmar PDF no esta disponible para Alfresco 5.2,  [descargue la versión 5.1 aquí](
https://download.alfresco.com/release/community/201605-build-00010/alfresco-community-installer-201605-linux-x64.bin), el proceso de instalación esta [descrito en esta página.](http://docs.alfresco.com/5.1/tasks/simpleinstall-enterprise-lin.html). 

Antes de instalar Alfresco, cree la carpeta de destino de la instalación y luego ejecute el instalador:

```
 mkdir /opt/alfresco 
  ./alfresco-community-installer-201605-linux-x64.bin
```

Seleccione la carpeta '/opt/alfresco' al instalar la aplicación. Puede ingresar a la aplicación desde http://[DIRECCION IP]:8080/share con el usuario 'admin' y la contraseña que eligió durante la instalación.

## Flujos de Trabajo 

Alfresco tiene ya instalados varios flujos de trabajo (dentro del menú Tareas) que pueden ser usados para automatizar tareas administrativas y la revision de documentos:

* Nueva tarea - Asignar una tarea nueva a usted o a un colega
* Revisar y aprobar (revisión de grupo) - Asignar una tarea de revisión a un grupo de personas
* Revisar y aprobar (uno o más revisores) - Asignar una tarea de revisión a varias personas
* Revisar y aprobar (revisión agrupada) - Asignar una tarea de revisión a varias personas, que pueden hacerse cargo de la tarea
* Revisar y aprobar (solo un revisor) - Asignar una tarea de revisión a un único revisor
 
Es posible diseñar y agregar flujos personalizados diseñados usando BPMN 2.0, las instrucciones están [disponibles en esta página](http://docs.alfresco.com/community/topics/wf-howto.html).
 

## Firma Electrónica de Documentos
 
Es posible que dentro del flujo de trabajo sea necesario firmar documentos. Para incorporar la función de firma electrónica al sistema es necesario instalar el [módulo de firma digital](https://github.com/rouxemmanuel/DigitalSigning/wiki). Este módulo permite firmar archivos PDF, es posible firmar archivos DOC pero estos son convertidos automáticamente a formato PDF. Para usar este módulo cada usuario del sistema debe contar con un certificado de firma electrónica en formato p12. Para instalarlo siga los siguientes pasos:

```
cp digitalSigningAlfresco.amp /opt/alfresco/amps/
cp digitalSigningShare.amp /opt/alfresco/amps_share/

cd /opt/alfresco/
./afresco.sh stop
rm -rf tomcat/webapps/alfresco tomcat/webapps/share

cd /opt/alfresco/bin
./apply_amps 

cd /opt/alfresco
./afresco.sh start
```

Una vez instalado el módulo, ingrese al sistema y configure el panel de inicio. Seleccione la opción 'añadir dashlets' y arrastre 'Signature' a un panel de la página de inicio, luego presione aceptar.  De regreso en la página de inicio, ubíquese sobre el panel de Firma Digital y presione el icono del lápiz para abrir del diálogo de configuración de su firma. Es posible ademas incluir una imagen de su firma manual si lo desea.


## Licencia

Este trabajo esta cubierto dentro de la estrategia de desarrollo de servicios de Gobierno Electrónico del Gobierno de El Salvador y como tal es una obra de valor público sujeto a los lineamientos de la Política de Datos Abiertos y la licencia [CC-BY-SA](https://creativecommons.org/licenses/by-sa/3.0/deed.es).  



