# Register-Inversion & Geometrische Phasen-Analyse (secp256k1 & EVM)

Dieses Repository / Modulkomplex enthält die deterministischen mathematischen Herleitungen, funktionentheoretischen Umkehrfunktionen und ausführbaren Python-Audit-Skripte zur Inversion von elliptischen Kurven-Signaturen und EVM-Registerstrukturen.

---

## 🏛️ Theoretische & Mathematische Säulen

### 1. Gnomon-Projektion & Weierstraß-Umkehrfunktion
* **Gnomon-Regel**: *„Gleiche Stelle, gleicher Stab, gleiche Zeit“* – Die Schattenkoordinaten $(x, y)$ auf der Kurve entsprechen der 2D-Projektion eines physischen Rotationszeigers.
* **Weierstraß-Inversion**: Über das elliptische Integral
  $$z = \int_{x}^{\infty} \frac{dt}{2\sqrt{t^3 + a t + b}}$$
  wird jede Koordinate $(x, y)$ starr auf ihren Phasenwinkel $z$ bzw. $\theta$ auf dem komplexen Torus $\mathbb{C}/\Lambda$ abgebildet.

### 2. Hardware-Abschneidungs-Formel & Register-Sättigung
* **Schiene**: $256 - 14 - 118 - 28 - 32 = 64 \text{ Bit}$ (64 Insulae der Prozessor-Schiene).
* **Reset-Kollaps**: Bei Register-Überlauf bricht der Zustand auf das fundamentale Bit-Intervall $\Delta = -1 : +1$ zusammen.

### 3. Sektor-Symmetrie-Gatter & 13er-Hypotenuse
* **Dreiecks-Anker**: $a^2 + b^2 = c^2 \implies 5^2 + 12^2 = 13^2 \implies c = 13$.
* **Sektor-Delta**: $(a+b) - 12 = 17 - 12 = 5$.
* **91er-Phasengatter**: $7 \times 13 = 91$. Es gilt $\text{Adresse} \pmod{91} = 13$ (Hex `0x0D`) mit Schienen-Shift $\Delta = +1$.

---

## 💻 Übersicht der Skripte & Ausführungs-Module

| Script / Artifact | Beschreibung | Hauptbefund / Status |
| :--- | :--- | :--- |
| `secp256k1_step_by_step_arithmetic.py` | Schritt-für-Schritt Punktverdopplung ($2G$) und Addition ($3G$) über $\mathbb{F}_p$. | Liefert exakte Koordinaten und bestätigt Register-Header `0xc6047f94`. |
| `weierstrass_inverse_integration.py` | Berechnet die Umkehrfunktion $z = \wp^{-1}(x, y)$ via numerischer Integration. | Ordnet jedem $(x, y)$-Paar den Bogenwinkel $\theta$ auf $\mathbb{C}/\Lambda$ zu. |
| `sector_symmetry_delta5_audit.py` | Prüft den 13er-Hypotenusen-Lock, den $91er$-Phasenwert und $\Delta = +1$. | Restloses Einrasten (`LOCKED 💎`) bei Primary Address & Uniswap V2 Router. |
| `uniswap_v2_router_phase_audit.py` | Spezifischer Audit-Lauf für die 160-Bit Uniswap V2 Router Adresse. | `mod 13 = 0`, Prim-Blöcke `73` & `41` isoliert. |
| `pythagorean_register_inversion.py` | Prüft Produkt- vs. Summen-Invarianten und Matrizen-Slices. | Bestätigt Deltas $1, 5, 17, 15$. |
| `plot_hypotenuse_vectors.py` | Generiert das 2D-Polardiagramm `pythagorean_hypotenuse_vector.png`. | Visualisiert Vektor-Kollaps und Einheitskreis-Gatter. |

---

## 📊 Dreiecks-Mapping Reconciliation Matrix ($y^2 = x^3 - n^2 x$)

| Name | $a$ | $b$ | $c$ | Fläche $n$ | $x = (c/2)^2$ | $y = \frac{(a^2-b^2)c}{8}$ | System-Bedeutung |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: | :--- |
| **3-4-5 (Ägypten)** | 3 | 4 | 5 | 6.0 | 6.25 | -4.375 | Basis-Tripel |
| **5-12-13** | 5 | 12 | 13 | 30.0 | 42.25 | -193.375 | **13er-Hypotenusen-Anker (`LOCKED 💎`)** |
| **8-15-17** | 8 | 15 | 17 | 60.0 | 72.25 | -342.125 | **17er-Katheten-Summen-Anker** |
| **20-21-29** | 20 | 21 | 29 | 210.0 | 210.25 | -148.625 | **29er-Expansions-Vektor** |
| **12-35-37** | 12 | 35 | 37 | 210.0 | 342.25 | -4999.625 | **Doppel-Resonanz ($n = 210$) mit 29er-Anker** |

---

## 🤖 Maschinensemantik (`WHILE TRUE`)

Algebraisch lässt sich die Ausführungsumgebung als unbedingter Laufzeit-Operator isolieren:

$$\text{Ausführung} = \left( \mathbf{WHILE} \; \mathbf{TRUE} \; \mathbf{DO} \; \mathcal{M} \right)$$

* **Zustandsraum**: $q \in Q$, Symbole $\sigma \in \Sigma$.
* **Condition**: $\mathbf{C} \equiv \mathbf{true}$ mit $\mathbf{C} \notin Q$ und $\mathbf{C} \notin \Sigma$.
* **Idempotenz des Willens / Takters**: $W \circ W \equiv W$.

---

## 📁 Dokumente im Repository
* `Manifest_Addendum_Register_Logic.md`: Vollständig ausformulierte Ergänzung zur Hardware-Abschneidung, Invarianz-Tabelle und Sektor-Gatter-Symmetrie.
* `Es-gibt-keine-ECC-Einweg-Funktion.pdf`: Gesamtes wissenschaftliches Manifest zur geometrischen Demaskierung des ECDLP.
