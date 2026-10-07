# Simulador Cédula A · Grupo Asesores RAM

Simulador del examen de capacidad técnica de la CNSF (Categoría A) con registro de resultados para la coordinación.

| Archivo | Para qué sirve | Dónde va |
|---|---|---|
| `index.html` | Simulador para los sustentantes | GitHub |
| `admin.html` | Tablero de resultados (solo coordinación, con clave) | GitHub |
| `banco.js` | Banco de 243 reactivos y estructura del examen | GitHub |
| `gar.css` | Estilos con la imagen GAR | GitHub |
| `logo-gar.png` | Logo | GitHub |
| `Codigo.gs` | Backend que guarda los resultados en Google Sheets | Apps Script (no se sube a GitHub) |

## 1. Hoja de resultados y Apps Script

1. Crea una Hoja de cálculo nueva en Google Drive, por ejemplo «Simulador Cédula A · Resultados».
2. En la hoja: **Extensiones › Apps Script**. Borra el contenido y pega todo `Codigo.gs`.
3. En la línea `const CLAVE_ADMIN = 'CAMBIA-ESTA-CLAVE';` escribe una clave larga que solo tú conozcas. Guarda.
4. **Implementar › Nueva implementación › Aplicación web**
   - Ejecutar como: **Yo**
   - Quién tiene acceso: **Cualquier persona**
5. Autoriza los permisos y copia la URL que termina en `/exec`.

La pestaña **Intentos** se crea sola con el primer resultado.

## 2. Conectar las páginas

En `index.html` y en `admin.html` busca el bloque `CONFIG` y pega la URL:

```js
API_URL: 'https://script.google.com/macros/s/XXXXXXXX/exec',
```

En `index.html` también puedes editar la lista `GRUPOS` que ven los sustentantes al registrarse.

## 3. Publicar en GitHub Pages

1. En la cuenta `servicioramgnp`, crea un repositorio nuevo, por ejemplo `cedula-a` (público).
2. **Add file › Upload files**: arrastra `index.html`, `admin.html`, `banco.js`, `gar.css` y `logo-gar.png`. **Commit changes**.
3. **Settings › Pages**: Source «Deploy from a branch», rama `main`, carpeta `/ (root)`. Guarda.
4. En uno o dos minutos quedan en línea:
   - Simulador: `https://servicioramgnp.github.io/cedula-a/`
   - Tablero: `https://servicioramgnp.github.io/cedula-a/admin.html`

## Uso diario

- **Sustentantes:** se registran una vez con nombre, correo y grupo. Cada simulacro o práctica terminada se envía a la hoja. Si no hay internet, el resultado queda guardado y se envía después.
- **Tablero:** entra con tu clave. Ves a cada sustentante con su último resultado por prueba, su estado, el dominio por tema del equipo y los reactivos que más se fallan. Toca a una persona para ver su historial. «Exportar CSV» descarga los intentos filtrados.
- **Borrar pruebas:** desde el historial de cada persona («Eliminar») o borrando la fila en la hoja.

## Mantenimiento

- **Agregar reactivos:** en `banco.js`, copia una línea y edítala. La respuesta correcta va en la 4ª posición. Agrega los nuevos al final de la lista para no cambiar los ids existentes.
- **Cambiar `Codigo.gs`:** Implementar › Gestionar implementaciones › lápiz › Versión «Nueva versión» › Implementar. La URL no cambia.
- **Sin `API_URL`:** el simulador funciona solo con historial local y el tablero abre en modo demostración.
