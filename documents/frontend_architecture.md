# Arquitectura Frontend (Mobile)

Este documento detalla la arquitectura técnica implementada en `apps/mobile`.

## Stack Tecnológico

- **Framework Core**: [Expo (SDK 52)](https://expo.dev) - React Native gestionado.
- **Lenguaje**: TypeScript.
- **Navegación**: [Expo Router](https://docs.expo.dev/router/introduction/) (Navegación basada en archivos).
- **Estilos**: [NativeWind](https://www.nativewind.dev/) (TailwindCSS para React Native).

## Estructura de Directorios

### `apps/mobile`

Directorio raíz de la aplicación móvil.

- `app/`: **Corazón de la navegación**. Cada archivo aquí es una pantalla.
  - `_layout.tsx`: Layout raíz. Configura proveedores globales (Fuentes, Temas) e importa los estilos globales (`global.css`).
  - `(tabs)/`: Grupo de rutas "Tabs".
    - `_layout.tsx`: Configura la barra de navegación inferior (Iconos, Títulos: Inicio, Buscar, Perfil).
    - `index.tsx`: Pantalla "Inicio".
    - `search.tsx`: Pantalla "Buscar".
    - `profile.tsx`: Pantalla "Perfil".
- `components/`: Componentes UI reutilizables (Botones, Tarjetas, Inputs).
- `assets/`: Imágenes y Fuentes estáticas.

## Archivos de Configuración Clave

### 1. Estilos (NativeWind + Tailwind)

La magia de usar clases de Tailwind en RN ocurre gracias a:

- **`tailwind.config.js`**: Define qué archivos escanear en busca de clases (`content: ["./app/**/*", "./components/**/*"]`).
- **`babel.config.js`**: Incluye el plugin `nativewind/babel` para compilar las clases a estilos nativos en tiempo de build.
- **`global.css`**: Archivo de entrada de CSS estándar (`@tailwind base; ...`).
- **`app/_layout.tsx`**: Importa `../global.css` para que los estilos estén disponibles en toda la app.
- **`nativewind-env.d.ts`**: Corrige errores de TypeScript permitiendo la propiedad `className` en componentes nativos.

## Flujos de Trabajo

- **Crear nueva pantalla**: Crear un archivo `.tsx` en `app/`. (ej: `app/producto/[id].tsx` para detalle de producto).
- **Estilar**: Usar `className` en componentes `<View>`, `<Text>`.
  - _Ejemplo_: `<Text className="text-red-500 font-bold">Error</Text>`
