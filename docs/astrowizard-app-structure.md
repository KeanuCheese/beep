# AstroWizard — Estructura inicial de producto (Android)

## 1) Visión del producto
AstroWizard será una **app Android** con experiencia tipo **mini-sistema operativo** (ventanas + “apps” internas), inspirada en estética **macOS 09 minimalista**, mezclando **fantasía medieval** con **futurismo**.

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
1. **Ergonómica**: una acción importante a 1–2 toques máximo.
2. **Simple e intuitiva**: evitar pantallas largas y configuraciones escondidas.
3. **Alta personalización sin fricción**: cambios visuales en tiempo real.
4. **Identidad local**: lenguaje, horarios, referencias y eventos orientados a Chile.
5. **Modularidad**: cada funcionalidad vive como un módulo (app interna) para crecer después.

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
1. Usuario instala app.
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
- Barra inferior mínima o dock flotante.
- Ventanas modales ligeras para sensación “sistema operativo”.

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

### Fase 2 (4–6 semanas)
- ILY Bubble Stream.
- Feed social básico (foto + texto).
- Moderación inicial.

### Fase 3 (6+ semanas)
- Video + ubicación.
- Sesh skate colaborativo.
- Mayor personalización de ventanas y layout.

---

## 9) Recomendaciones técnicas rápidas (Android)
- Framework sugerido: **Kotlin + Jetpack Compose** (ideal para UI personalizable).
- Arquitectura: **modular por feature** (onboarding, zodiac, feed, bubbles, settings).
- Estado: ViewModel + StateFlow.
- Datos locales: Room/DataStore.
- Backend inicial: API simple + autenticación social o email.

---

## 10) Definición de éxito inicial (KPIs)
- Activación onboarding completado.
- Retención D1/D7.
- % usuarios que leen gaceta diaria.
- % usuarios que personalizan su interfaz.
- Posts y sesiones de uso en Feed Skate.

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

Notas:
- Los nombres se pueden ajustar con feedback de comunidad chilena.
- Cada rango desbloquea cosméticos (marco de perfil, color de ventana, emoji-icon pack).

### 11.3 XP básica por interacción (MVP)
Acciones sugeridas:
- Check-in diario: +5 XP
- Leer gaceta completa del día: +10 XP
- Publicar en feed: +15 XP
- Comentar post: +5 XP
- Reacción a contenido: +2 XP (con límite diario)
- Enviar mensaje ILY: +4 XP (con límite diario)

Controles anti-abuso:
- Tope de XP por día para acciones repetibles.
- Detección de spam (texto duplicado / ráfagas).
- Cooldown por tipo de interacción.

### 11.4 Códigos de autorización (IRL)
Origen:
- Entregados por embajadores/moderadores en eventos reales.
- Activables desde módulo “Perfil > Canjear código”.

Reglas MVP:
- Código único, con expiración opcional.
- Asigna XP alto (ej: +80 a +200 según tipo de evento).
- Puede otorgar insignia especial de evento (ej. “Sesh Plaza Ñuñoa 2026”).

Modelo de seguridad inicial:
- Formato firmado en backend.
- Estado del código: `activo`, `canjeado`, `expirado`, `bloqueado`.
- Auditoría de canjes con timestamp y evento.

### 11.5 Recompensas por nivel
Tipos de desbloqueo:
- Cosméticos del “OS shell” (themes, marcos, fondos).
- Packs de iconos emoji exclusivos.
- Stickers/chat flair para ILY y Feed.
- Acceso temprano a módulos futuros.

### 11.6 Datos mínimos para implementar niveles
Nuevas entidades sugeridas:
- `UserProgress`
  - user_id, nivel_actual, xp_total, xp_semana, rango_nombre.
- `XpLedger`
  - id, user_id, fuente (daily_checkin/post/comentario/codigo), xp, created_at.
- `AuthCode`
  - code, evento_id, xp_otorgada, estado, expires_at.
- `UserBadge`
  - user_id, badge_id, unlocked_at, source.

### 11.7 KPIs del sistema de insignias
- % usuarios que suben al menos 1 nivel en 7 días.
- Promedio de XP semanal por usuario activo.
- Tasa de canje de códigos IRL.
- Retención comparada entre usuarios con y sin canje IRL.
