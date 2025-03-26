# Consolidación

La tecnica utilizada en la bomba (El manejo de eventos) es util porque permite evaluar como la aplicación maneja multiples eventos al mismo tiempo lo que da como resultado ventajas tales como:

1.Mayor eficiencia en el manejo de varias solicitudes lo que permite evitar redundancias y optmizar el programa
2. Ayuda a prevenir bloqueos y fallas del programa, permitiendo identificar problemas con antelacion 
3. Optimización a la hora de la solucion de errores y reutilizacion de los eventos dentro del programa 
4. Evita fugas de memoria o uso excesivo de la CPU 

## Ventajas y desventajas 
Detección temprana de errores: Se pueden identificar fallos en la lógica de la aplicacion 
Mejor rendimiento: Si las pruebas incluyen mediciones de tiempo de respuesta, ayudan a optimizar el codigo
Mayor estabilidad: Las pruebas de carga, estrés o funcionalidad aseguran que la aplicacion puede manejar diferentes escenarios 
Automatización: En muchos casos, se pueden automatizar para ejecutarlas regularmente y detectar problemas antes de un despliegue

Desventajas de estas pruebas
Tiempo de ejecución: Dependiendo de la complejidad de la prueba, pueden tardar en ejecutarse
Falsos resultados: En pruebas automatizadas factores externos pueden afectar los resultados
Dificultad de configuración: Para simular adecuadamente entornos de concurrencia a veces es necesario configurar multiples hilos o instancias lo que puede ser complejo




















