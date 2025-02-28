# Explotación del kernel de PS4 9.00
---
## Resumen
En este proyecto encontrará una implementación que intenta aprovechar un error del sistema de archivos para Playstation 4 en el firmware 9.00.
El error se encontró al diferenciar los kernels 9.00 y 9.03. Requerirá una unidad con un sistema de archivos exfat modificado. Activarlo con éxito le permitirá ejecutar código arbitrario como kernel, para permitir jailbreak y modificaciones a nivel de kernel en el sistema. lanzará el lanzador de carga útil habitual (en el puerto 9020).

## Parches incluidos
Los siguientes parches se aplican al kernel:
1) Permitir mapeo de memoria RWX (lectura-escritura-ejecución) (mmap/mprotect)
2) Instrucción Syscall permitida en cualquier lugar
3) Resolución dinámica (`sys_dynlib_dlsym`) permitida desde cualquier proceso
4) Llamada personalizada al sistema #11 (`kexec()`) para ejecutar código arbitrario en modo kernel
5) Permitir que los usuarios sin privilegios llamen a `setuid(0)` con éxito. Funciona como una verificación de estado y también como una escalada de privilegios.
6) parche (`sys_dynlib_load_prx`)
7) Desactiva sysVeri

## Breve instructivo
Este exploit es diferente a los anteriores en los que se basaban exclusivamente en software. Para activar la vulnerabilidad es necesario conectar un dispositivo USB especialmente formateado en el momento adecuado. En el repositorio encontrarás un archivo .img. Puedes escribir este .img en un USB usando algo como Win32DiskImager.

**Nota: Esto borrará la unidad USB, asegúrese de seleccionar la unidad correcta y de que está de acuerdo con ella antes de hacer esto**

![](https://i.imgur.com/qpiVQGo.png)

Cuando ejecute el exploit en la PS4, espere hasta que aparezca una alerta con "Inserte USB ahora. No cierre el cuadro de diálogo hasta que aparezca la notificación, elimine el USB después de cerrarlo". Como indica el cuadro de diálogo, inserte el USB y espere hasta que aparezca la notificación "formato de disco no compatible", luego cierre la alerta con "Aceptar".

Es posible que el exploit tarde un minuto en ejecutarse y que la animación giratoria en la página se congele; esto está bien, déjelo continuar hasta que aparezca un error o se ejecute correctamente y muestre "En espera de carga útil".

## Notas adicionales
- Desenchufe el USB antes de un ciclo de (re)arranque o correrá el riesgo de dañar el montón del kernel durante el arranque.
- El navegador puede tentarte a cerrar la página prematuramente, no lo hagas.
- El círculo de carga puede congelarse mientras se activa el exploit webkit, esto aún no significa que el exploit haya fallado.
- El error es anterior al firmware 1.00, por lo que 1.00-9.00 debería poder explotarse usando la misma estrategia (necesitará un exploit y dispositivos de usuario diferentes).
- Puedes reemplazar el cargador con una carga útil específica para cargar cosas directamente en lugar de hacerlo a través de sockets.
- Este error funciona en ciertos firmwares de PS5, sin embargo, no se conoce ninguna estrategia para explotarlo por el momento. No sería recomendable utilizar este error contra los ciegos de PS5.
- Por favor, no abras ediciones para decirme que no las hay... ni intentes obligarme a hacer la tarea por ti.
- Este repositorio no proporciona nada más allá de los parches iniciales del kernel que le permiten ejecutar cargas útiles.
Si encuentra problemas con ciertas cargas útiles, debe informar sus problemas a los desarrolladores de esas cargas a través de cualquier medio que pongan a su disposición.
- El nombre del repositorio es una fusión de las palabras 'ps4' y '[OOB](https://cwe.mitre.org/data/definitions/787.html)', siendo esta última el tipo de vulnerabilidad de esta implementación. intentos de explotar, cualquier otra interpretación es pura coincidencia y no intencionada.
- Como se indicó anteriormente, este error se encontró al diferenciar los kernels 9.00 y 9.03, esto implica que el error se solucionó en 9.03.
## Colaboradores

- nanospeedgameryt (por hacer su host público)
- laureeeeeee
- [Espectro](https://twitter.com/SpecterDev)
- [Znullptr](https://twitter.com/Znullptr)

## Gracias especiales
- [Andy Nguyen] (https://twitter.com/theflow0)
- [sleirsgoevy](https://twitter.com/sleirsgoevy) - [Explotación de Webkit 9.00](https://github.com/sleirsgoevy/bad_hoist/tree/9.00)
