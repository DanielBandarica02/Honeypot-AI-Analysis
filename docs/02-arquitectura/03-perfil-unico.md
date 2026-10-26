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

Toda la identidad se genera desde un único fichero, `infra/persona.yml`: sector, dominio propio,
personas, versiones de cada servicio y contenido. Ansible deriva de él banners, mensajes de
bienvenida, contenido web y ficheros cebo. Las pruebas de realismo validan contra ese mismo
fichero.

## Cómo se verifica que los datos son ficticios

- El nombre de la empresa se comprueba contra registros mercantiles, de marcas y buscadores.
- El dominio se registra a nombre propio; nunca se usa un dominio ajeno o inventado.
- Las personas se generan sintéticamente, sin corresponder a individuos identificables.
- No se emplean documentos de identidad ni números de cuenta, ni siquiera con formato válido.
- Las credenciales sembradas solo funcionan dentro del propio conjunto de señuelos.

## Qué se descartó

**Varios perfiles en una sola dirección.** Incoherente y fácilmente identificable.

**Perfil industrial.** Más llamativo, pero incompatible con el resto de servicios en la misma
dirección. Queda como segundo perfil en otra dirección, si hay presupuesto.

## Qué implica

A favor: entorno creíble, superficie coherente y cebos que conectan servicios entre sí.

En contra: no se observa tráfico contra protocolos industriales ni de directorio. Se asume: están
fuera de los requisitos actuales.
