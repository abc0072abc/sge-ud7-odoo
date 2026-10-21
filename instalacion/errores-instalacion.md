
# Errores durante la instalación

## Error al ejecutar Docker Desktop

Cuando instalé Docker Desktop y fui a ejecutarlo por primera vez, me encontré con un error que indicaba que la virtualización no estaba activada o no estaba disponible en mi dispositivo. Por este motivo, Docker Desktop no podía iniciarse correctamente, ya que necesita la virtualización para funcionar.

### Solución

Para intentar solucionar el problema, abrí la terminal de Windows como administrador y ejecuté el siguiente comando:

```powershell
wsl --install
```

Este comando sirve para instalar el Subsistema de Windows para Linux (WSL), que permite ejecutar un entorno Linux en Windows y que se utiliza habitualmente para trabajar con Docker Desktop.

Después de ejecutar el comando, tuve que reiniciar el ordenador para que los cambios se aplicaran correctamente. Una vez reiniciado, volví a abrir Docker Desktop y comprobé que ya funcionaba correctamente.

### Resultado

El problema se solucionó después de aplicar los cambios y reiniciar el ordenador. Con esto, pude ejecutar Docker Desktop y continuar con la instalación y configuración del entorno de trabajo.
