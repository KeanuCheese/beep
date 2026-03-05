# AstroWizard — Estructura inicial de producto (Web-first)

## 1) Visión del producto
AstroWizard será una **aplicación web** con experiencia tipo **mini-sistema operativo** (ventanas + “apps” internas), inspirada en estética **macOS 09 minimalista**, mezclando **fantasía medieval** con **futurismo**.

Estrategia de plataforma:
- **Web-first para todo WizardOS**.
- Diseñada desde el inicio para funcionar como **PWA**.
- Preparada para convertirse en app móvil con **encapsulado** (por ejemplo, Capacitor) cuando sea necesario.

Público objetivo inicial:
- Usuarios en **Chile**.
- Comunidad **skater** (principiante a pro).

Propuesta de valor:
- Gaceta zodiacal personalizada.
- Señales diarias útiles (amor, salud, dinero, skate).
- Comunidad viva con mensajes efímeros e interacción social.
- Interfaz altamente personalizable (tema, iconos emoji, tipografías, colores, estilo de ventanas).

---

## 2) Principios de UX para el MVP
1. **Ergonómica**: una acción importante a 1–2 toques/clicks máximo.
2. **Simple e intuitiva**: evitar pantallas largas y configuraciones escondidas.
3. **Alta personalización sin fricción**: cambios visuales en tiempo real.
4. **Identidad local**: lenguaje, horarios, referencias y eventos orientados a Chile.
5. **Modularidad**: cada funcionalidad vive como un módulo (app interna) para crecer después.
6. **Responsive por defecto**: misma base para desktop, tablet y móvil.

---

## 3) Arquitectura funcional por módulos (“apps” internas)

### Módulo A — Onboarding (Inicio)
Objetivo: capturar contexto base y activar personalización desde el primer uso.

Pantallas:
1. **Splash/Intro** con identidad AstroWizard.
2. **Lore** (historia del “mago medieval viajero del futuro”).
3. **Registro rápido**:
   - Signo zodiacal.
   - Preferencias (horario, interés en skate, idioma/región Chile).
4. **Primer setup visual**:
   - Tema base.
   - Iconos emoji por defecto.

Salidas de datos:
- Perfil inicial.
- Preferencias de contenido.
- Configuración visual inicial.

### Módulo B — Gaceta Zodiacal (Core)
Objetivo: entregar valor diario en formato claro.

Secciones diarias:
- Amor.
- Salud.
- Dinero.
- Skate.

Funcionalidades MVP:
- Mensaje diario por categoría.
- Historial de últimos N días.
- Botón “guardar favorito”.

### Módulo C — ILY Bubble Stream (mensajes efímeros)
Objetivo: crear ambiente social-inspiracional siempre vivo.

Comportamiento:
- Burbujas con mensajes cortos de usuarios y bots.
- Aparición semi-aleatoria en pantalla.
- Desaparición automática (TTL).

Reglas MVP:
- Longitud corta por mensaje.
- Filtro mínimo de contenido.
- Frecuencia configurable para no saturar la UI.

### Módulo D — Feed Social Skate
Objetivo: comunidad y coordinación de actividad real.

Publicaciones permitidas:
- Foto.
- Video corto.
- Ubicación.
- Convocatoria de sesh skate.

Funcionalidades MVP:
- Crear post.
- Ver feed cronológico simple.
- Reacciones rápidas.
- Comentario corto.

### Módulo E — Personalización total (Shell del sistema)
Objetivo: que la app se “sienta propia”.

Opciones iniciales:
- Tema (claro/oscuro + paletas).
- Iconos internos con emojis editables.
- Tipografía.
- Color de ventanas y fondos.
- Tamaño/estilo de widgets del “escritorio”.

---

## 4) Flujo principal recomendado (MVP)
1. Usuario abre WizardOS en web (navegador o instalada como PWA).
2. Completa onboarding (lore + registro + preferencias + tema base).
3. Entra al “escritorio” con iconos tipo OS.
4. Abre Gaceta Zodiacal diaria.
5. Explora burbujas ILY.
6. Publica o consume en Feed Skate.
7. Ajusta personalización en cualquier momento.

---

## 5) Estructura de navegación (simple)
- **Desktop/Home (OS Shell)**
  - Icono: Gaceta
  - Icono: ILY Bubbles
  - Icono: Feed Skate
  - Icono: Perfil
  - Icono: Personalización

Patrón sugerido:
- Dock inferior/floating adaptable según tamaño de pantalla.
- Ventanas modales ligeras para sensación “sistema operativo”.
- En móvil, priorizar navegación por pestañas + hojas deslizables sin perder la metáfora OS.

---

## 6) Modelo de datos mínimo (alto nivel)

Entidades clave:
- `UserProfile`
  - id, signo, país/ciudad, intereses, fecha_registro.
- `UserPreferences`
  - temas, emojis_iconos, fuente, colores, ajustes_UI.
- `DailyMessage`
  - fecha, categoria (amor/salud/dinero/skate), contenido.
- `BubbleMessage`
  - autor_tipo (user/bot), texto, created_at, expires_at.
- `FeedPost`
  - autor, tipo (foto/video/ubicación/sesh), contenido, metadata_geo, created_at.

---

## 7) Funcionalidades principales para empezar (prioridad)

### Prioridad 1 — Base de producto
1. Onboarding con registro por signo + preferencias.
2. Home tipo “OS” con módulos como iconos.
3. Gaceta diaria en 4 categorías.

### Prioridad 2 — Comunidad ligera
4. ILY Bubble Stream con mensajes efímeros.
5. Feed Skate con foto y texto (video/ubicación en iteración siguiente).

### Prioridad 3 — Diferenciación
6. Personalización visual avanzada (emoji icons + temas + fuentes).
7. Sistema de eventos locales (sesh por zona en Chile).

---

## 8) Roadmap sugerido (3 fases)

### Fase 1 (4–6 semanas)
- Onboarding.
- Gaceta diaria.
- Home tipo OS básico.
- Personalización mínima (tema + emojis).
- Base PWA (manifest + service worker + instalación).

### Fase 2 (4–6 semanas)
- ILY Bubble Stream.
- Feed social básico (foto + texto).
- Moderación inicial.
- Optimización responsive avanzada.

### Fase 3 (6+ semanas)
- Video + ubicación.
- Sesh skate colaborativo.
- Mayor personalización de ventanas y layout.
- Empaquetado móvil (Android/iOS) con la misma base web.

---

## 9) Recomendaciones técnicas rápidas (Web)
- Framework sugerido: **Next.js (React + TypeScript)** o **Nuxt/Vue** si el equipo lo prefiere.
- Arquitectura: **modular por feature** (onboarding, zodiac, feed, bubbles, settings).
- UI: sistema de diseño con tokens (temas, tipografías, espaciado) para personalización en tiempo real.
- Estado: store central (Zustand/Redux/Pinia) + cache de servidor (React Query o equivalente).
- Datos locales: IndexedDB/localStorage para preferencias + caché offline.
- Backend inicial: API simple + autenticación social o email.
- Móvil desde web: **PWA** primero y **Capacitor** como puente para stores móviles.

---

## 10) Definición de éxito inicial (KPIs)
- Activación onboarding completado.
- Retención D1/D7.
- % usuarios que leen gaceta diaria.
- % usuarios que personalizan su interfaz.
- Posts y sesiones de uso en Feed Skate.
- % instalaciones PWA sobre usuarios activos.

---

## 11) Sistema de insignias y niveles (estilo Gunbound)

Objetivo:
- Recompensar participación real dentro de la app.
- Mezclar progreso digital con cultura skate en terreno (IRL).

### 11.1 Progresión base
El usuario sube de nivel por dos vías:
1. **XP por interacción en la app** (acciones diarias).
2. **Códigos de autorización** obtenidos en juntas, meets, seshs y eventos oficiales.

Regla general MVP:
- `XP Total = XP Básica + XP por Código`.
- Los códigos tienen validación única (1 uso por cuenta y por código).

### 11.2 Rangos propuestos (inspiración “pollito”)
Ejemplo inicial de escalera de rangos:
1. **Pollito Cósmico** (Nivel 1)
2. **Aprendiz de Tabla** (Nivel 2)
3. **Rider Astral** (Nivel 3)
4. **Mensajero Zodiacal** (Nivel 4)
5. **Nómada del Bowl** (Nivel 5)
6. **Mago del Spot** (Nivel 6)
7. **Leyenda de la Sesh** (Nivel 7)
