# Neurodinamia – Vigilancia epidemiológica

Formularios digitales para el personal asistencial (FR-VE-02 NAV, FR-VE-03 ITS-AC, FR-VE-04 ISTU-AC, FR-VE-05 ISQ).

## Estructura
- `index.html` + `config.js` + `logo.jpg`: versión web para **GitHub Pages**, guarda en **Supabase**.
- `supabase/schema.sql`: tablas y reglas de seguridad (RLS).
- `artifact/index.html`: versión anterior, publicada como Artifact en claude.ai (no usa Supabase).

## Puesta en marcha
1. **Supabase**: crea un proyecto, abre *SQL Editor*, pega `supabase/schema.sql` y ejecútalo.
2. **Código de acceso**: ejecuta el `insert into public.config_acceso …` del paso 4 del SQL con el código que quieras. Se lo das al personal; lo escriben una vez y el navegador lo recuerda. Puedes cambiarlo cuando quieras.
3. **Administrador**: en *Authentication → Users* crea tu usuario (*Add user*, con contraseña) y ejecuta el `insert into public.admins …` del paso 5 con tu correo. En *Authentication → Providers → Email* desactiva *Allow new users to sign up*.
4. **config.js**: pega la *Project URL* y la clave *anon* (*Project Settings → API*). La clave anon es pública por diseño; los datos los protege RLS.
5. **GitHub Pages**: en el repositorio, *Settings → Pages → Deploy from a branch → main / (root)*. En repositorios privados Pages exige un plan de pago de GitHub; con plan gratuito el repositorio debe ser público (no contiene datos de pacientes ni secretos).

## Uso
- **Personal asistencial**: abre el enlace, elige el formato, escribe el código de acceso y llena el formulario. No necesita cuenta.
- **Administrador**: enlace "Acceso de administración" al pie → correo y contraseña → pestaña *Registros* (buscar, descargar Excel/CSV, eliminar).

## Seguridad
- Los registros contienen nombre e historia clínica de pacientes: están solo en Supabase, nunca en el repositorio.
- Quien tenga el código puede **insertar** pero no leer registros; la lectura y eliminación están limitadas a `admins` por RLS. El código se valida en la base de datos y no se guarda con el registro.
- Quien conozca el código puede enviar registros: cámbialo si se filtra o cuando alguien deje el servicio.
- Nunca pongas la clave `service_role` en este proyecto.
