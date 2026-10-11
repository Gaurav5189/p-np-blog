---
Task ID: 1
Agent: Z.ai Code (main)
Task: Design P vs NP research blog site and deliver an interactive demo HTML (3D hero, simulations, full article) for user approval before the full Next.js build.

Work Log:
- Read user's uploaded research article (upload/p-vs-np-article.md, 201 lines, 41KB) covering: barriers (relativization, natural proofs, algebrization), fine-grained complexity (SETH/OV/3SUM/APSP), cryptography & one-way functions, Impagliazzo's five worlds, collapse cascade, defense stack.
- Downloaded Three.js r128 locally to public/vendor/three.min.js (offline-robust, no CDN dependency).
- Built the demo as a single self-contained page public/demo.html (160KB) from 10 part files in build_parts/: CSS design system (obsidian + clay-gold + ember + verify-teal palette; Fraunces/Space Grotesk/JetBrains Mono), hero, 9 content sections, JS engine, markdown article renderer.
- Implemented interactive experiences:
  1) Hero "Fifty-Year Wall": Three.js instanced wall — orderly teal P-plain vs chaotic ember NP tower with floating rubble, gold seam, scroll-dolly camera, drag orbit, color-pulse waves, dust particles.
  2) SIM-01 Verify-vs-Solve: Hamiltonian cycle on 2D canvas; builds 40 candidate graphs and ships the hardest (silent DFS measurement, adversarial adjacency ordering) so backtracking is visible; verify = O(n) certificate check vs solve counter against n!.
  3) Three Barriers: 3 clickable 3D monuments (oracle bubbles, truth-table slab + random/PRF clouds, polynomial surface + oracle spike) with inspector cards fed from the article.
  4) SAT Lab: live DPLL sweep across random 3-SAT phase transition (alpha 2->6), two solvers head-to-head (blind backtracking vs +unit propagation) on same instances, log-scale chart with alpha_c=4.267 marker, verified DPLL correct vs brute force.
  5) Karp Reduction Web: 3D force-laid graph of 13 NP-complete problems around SAT with projected DOM labels, edge pulses, click-for-details.
  6) Five Worlds: Impagliazzo spectrum slider (Algorithmica->Cryptomania) with per-world crypto artifact survival states.
  7) Collapse Cascade: exponent slider c=2..100 pricing the apocalypse (ops model, verdict bands matching article's O(N^2)-disastrous vs Omega(N^4)-safe framing) + order-of-collapse timeline.
  8) Defense Stack: 5 accordions (OTP/QKD, bounded storage, physics, exponent arbitrage, doctrine) + "what does NOT defend" strikethrough list.
  9) Siege Timeline: 14 milestone cards 1955-2024.
  10) Full article rendered from embedded markdown via custom parser (headings, tables, lists, blockquotes, links) with sticky TOC, scrollspy, abstract callout.
- Fixed during browser verification: TOC display:block, article reveal-observer race, HC canvas device/logical pixel mismatch, DPLL too-strong unit propagation (added blind-solver comparison curve), solver lucky-path (adversarial graph selection), SAT sweep pacing, mobile polish (520px breakpoint).
- Wired src/app/page.tsx to redirect / -> /demo.html; excluded public/ from ESLint; lint clean; dev server logs clean.
- Agent Browser end-to-end verified: hero render + orbit drag, all 3 sims interactive, barriers tabs, worlds slider, collapse verdicts, defense accordions, article TOC/scrollspy, footer sticky-bottom, mobile 390px layout, zero console errors.

Stage Summary:
- Deliverable: public/demo.html — approve/iterate before building the real Next.js journal.
- Design language established: "The Fifty-Year Wall" — obsidian bg, clay gold (#f0b13e), ember (#ff6a3d), verify-teal (#3ddbb0), Fraunces display serif + JetBrains Mono kickers, grain + vignette atmosphere.
- All simulations are client-side, dependency-free, honest implementations (real DPLL, real DFS backtracking).
- Next step (pending user approval): production Next.js 16 build — MDX article engine, simulation components, Prisma-backed reading progress/comments, remaining roadmap items.
