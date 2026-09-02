# Convención de pantallas cencoPrime

Usa esta referencia únicamente para cencoPrime o cencoPrime black.

## Estructura

`proyecto/dispositivo/flujo/pantalla_o_estado/foco_ajuste`

- `proyecto`: marca o iniciativa, por ejemplo `cencoprimeblack`.
- `dispositivo`: formato, por ejemplo `desktop` o `mobile`.
- `flujo`: flujo principal, por ejemplo `gestion_cuenta`.
- `pantalla_o_estado`: pantalla, paso o estado real, por ejemplo `detalle`, `skeleton` o `error`.
- `foco_ajuste`: contexto específico cuando aporta información, por ejemplo `carga_inicial` o `usuario_inactivo`.

## Escritura

- Minúsculas.
- Sin tildes.
- `snake_case` dentro de cada nivel.
- `/` para separar niveles.
- Español como idioma predeterminado, salvo términos oficiales del producto.
- Sin nombres temporales de trabajo ni identificadores de Figma.

Ejemplo:

`cencoprimeblack/mobile/gestion_cuenta/skeleton/carga_inicial`

Accessibility Label separado:

`Cargando gestión de cuenta`

## Consistencia

Las pantallas del mismo flujo deben conservar el mismo proyecto, dispositivo, idioma, estructura y nivel de detalle. Omite `foco_ajuste` cuando no agregue información real; no agregues un segmento genérico para rellenar la estructura.
