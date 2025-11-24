# Frontend Spec — The Algorithm's Muse (T.A.M.)

Dominio: https://thealgorithmsmuse.com  
Stack objetivo final: Next.js + Tailwind + Vercel + Supabase (REST/JS SDK).

## 1. Páginas principales

1. `/` — Home / Landing
   - Hero con título T.A.M. + A.N.O.N.
   - Explicación corta del experimento (30 días, Solana, IA gobierna).
   - CTA principal: "Ver el experimento" (lleva a /game).
   - CTA secundaria: "Leer manifiesto" (lleva a /manifesto).

2. `/game` — Juego / PEACE_SCORE / Leaderboard
   - Explicación simple de cómo funciona el juego:
     - PEACE_SCORE
     - Jackpot
     - Notarios
   - Leaderboard (TABLA):
     - columnas: NFT id, PEACE_SCORE, nº de wallets únicas, volumen, ranking.
   - Estado del experimento:
     - Cuenta atrás (tiempo restante de los 30 días).
     - Fase actual (pre-lanzamiento / activo / cerrado).
   - Placeholder para integrar datos on-chain más adelante.

3. `/notaries` — Los 20 Notarios
   - Explicación del rol del Primer Notario.
   - Listado de 1 a 20:
     - Notario #1 (gmoney como target ideal).
     - Notarios 2–20 (slots vacíos inicialmente).
   - Para cada notario:
     - alias / handle (p. ej. @gmoneyNFT).
     - estado: pending / invited / accepted.
     - recompensa (1% primarias + royalties, etc.).
   - Esta página leerá más adelante de una tabla `notaries` en Supabase.

4. `/manifesto` — Manifiesto
   - Versión legible del manifiesto de T.A.M. y A.N.O.N.
   - Secciones:
     - Propósito del experimento.
     - Reglas de juego.
     - Impacto social (ONG, 10%).
     - Intervención mínima humana.
   - Inicialmente texto estático; luego se podría editar desde backend.

5. `/faq` — Preguntas frecuentes
   - ¿Qué es T.A.M.?
   - ¿Cómo funciona el PEACE_SCORE?
   - ¿Qué recibe el Primer Notario?
   - ¿Qué porcentaje de royalties y donación social hay?
   - ¿Qué riesgo tengo al comprar un NFT?

6. `/ngo` — Causa / ONG
   - Explicación del 10% de ventas primarias para ONG.
   - Sección para la ONG elegida (ej. ACNUR / otra).
   - Explicación del tracking transparente on-chain.

7. `/tech` — Detalles técnicos
   - Blockchain: Solana.
   - Colección: 10k–15k NFT.
   - Royalties: 8% total; reparto por rol.
   - Estructura de smart contract (PEACE_SCORE, jackpot, notarios).

## 2. Componentes básicos

- Layout general:
  - Header con logo/wordmark T.A.M. / A.N.O.N.
  - Nav con enlaces: Home, Juego, Notarios, Manifiesto, FAQ, ONG.
  - Footer con:
    - © año dinámico
    - Email de contacto: ANONTAM@proton.me
    - Enlace a X/Twitter (cuando exista).

- Componentes:
  - `Countdown` — cuenta atrás a fecha de fin de experimento.
  - `NotaryCard` — tarjeta para cada notario.
  - `LeaderboardTable` — tabla PEACE_SCORE para /game.
  - `PhaseBadge` — etiqueta con fase actual (0–4).

## 3. Integraciones previstas

- Supabase:
  - Tabla `visitors` (ya creada) para analítica simple.
  - Futuras tablas:
    - `notaries` (id, handle, status, reward_shares, created_at).
    - `experiment_state` (start_at, end_at, phase, notes).

- Integración futura:
  - Al cargar la Home, enviar un POST / upsert a `visitors`.
  - En /notaries, leer de `notaries`.
  - En /game, leer de una fuente on-chain + caché en Supabase.

## 4. Requisitos para la IA (futuro prompt de Next.js)

- Generar app Next.js 14 con:
  - `/app` router.
  - Tailwind CSS ya configurado.
  - Páginas descritas en este documento.
  - Cliente Supabase en el servidor para lectura/escritura.
- No usar librerías pesadas innecesarias.
- Mantener diseño minimalista, oscuro, futurista.
