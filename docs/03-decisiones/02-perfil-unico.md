# Un solo perfil de empresa

## El problema

Exponer servicios dispares en una misma dirección —SSH, un autómata industrial, carpetas
compartidas de Windows y un directorio corporativo— es una combinación que ninguna empresa real
presenta, y que los buscadores de servicios expuestos identifican como señuelo.

Además, la credibilidad de un entorno no depende de sus recursos sino de su coherencia: versiones
que encajan entre sí, contenido que corresponde al sector y ficheros con historia.

## Qué se decidió

Un único perfil: **agencia de marketing y desarrollo web**. Justifica de forma natural el conjunto
de servicios desplegado, porque una agencia que mantiene sitios de clientes administra su propio
servidor: web con gestor de contenidos, base de datos, caché, FTP para intercambio con clientes y
acceso de administración.

El servidor refleja además lo que ocurre en una agencia real: el gestor de contenidos
razonablemente al día, porque avisa de sus actualizaciones, y plugins antiguos que nadie ha vuelto
a tocar desde que se instalaron. De ahí sale la mayoría de los compromisos reales.

## Cómo se gestiona el perfil

Toda la identidad vive en un único fichero, `infra/persona.yml`, del que Ansible deriva banners,
mensajes de bienvenida, contenido web, ficheros cebo y credenciales válidas. Las pruebas de
realismo validan contra ese mismo fichero.

| Bloque | Qué define |
|---|---|
| Empresa | Nombre, sector, ciudad, dominio, tamaño y año de fundación |
| Sistema | Distribución, versión, kernel, nombre de host y zona horaria |
| Servicios | Puerto y versión de cada uno, incluidos los plugins del gestor de contenidos |
| Personas y cuentas de servicio | Usuarios del sistema, con su rol y su correo |
| Clientes | Negocios ficticios que dan contenido a la web y al FTP |
| Credenciales válidas | Las que conceden acceso, según la política de acceso |
| Cebos | Identificador, ubicación y servicio donde cada uno es válido |

### No se versiona

Ni el fichero real ni un ejemplo con su estructura rellena. Publicarlo revelaría qué
vulnerabilidad se emula, dónde están los cebos y qué usuarios existen, lo que permitiría confirmar
el servidor como señuelo sin necesidad de atacarlo.

El fichero vive en el equipo de administración y en el servidor, y está excluido en `.gitignore`
para evitar subirlo por descuido.

## Cómo se verifica que los datos son ficticios

- El nombre de la empresa se comprueba contra registros mercantiles, de marcas y buscadores.
- El dominio se registra a nombre propio, con privacidad de WHOIS; nunca se usa un dominio ajeno
  o inventado.
- Las personas y los clientes se generan sintéticamente, sin corresponder a entidades reales.
- No se emplean documentos de identidad ni números de cuenta, ni siquiera con formato válido.
- Las credenciales sembradas solo funcionan dentro del propio conjunto de señuelos.

## Qué se descartó

**Varios perfiles en una sola dirección.** Incoherente y fácilmente identificable.

**Perfil industrial.** Más llamativo, pero incompatible con el resto de servicios en la misma
dirección. Queda como segundo perfil en otra dirección, si hay presupuesto.

**Publicar el perfil como ejemplo.** Habría facilitado reproducir el laboratorio, pero entrega la
huella completa del señuelo a cualquiera que encuentre el repositorio.

## Qué implica

A favor: entorno creíble, superficie coherente y cebos que conectan servicios entre sí.

En contra: no se observa tráfico contra protocolos industriales ni de directorio. Y el laboratorio
no es reproducible tal cual por un tercero, que tendría que construir su propio perfil.
