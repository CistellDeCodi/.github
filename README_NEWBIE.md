# 🛸 Organització CistellDeCodi: Guia de Supervivència

Aquest document detalla el flux de treball per mantenir la integritat de la organització **Cistell de Codi**, el sandbox **srustullet** a GitHub i la gestió del terminal de Linux sense fricció.

---

## 💡 Tinc una idea nova: Per on començo?

Segurament hauràs utilitzat AI studio o Manus per crear un prototip, i hauràs sincronitzat a GitHub, per defecte s'envia a la sandbox. 
**NO creis el repositori de l'organització a GitHub manualment.** El sistema crea la simetria per tu mitjançant scripts.

1. **Pas 1:** Obre el fitxer de configuració al terminal de Linux:
   `nano ~/repos.txt`
2. **Pas 2:** Afegeix la línia seguint la **Lògica de Noms**:
   `nom-sandbox, fil-XX-nom-sandbox`
   * **Sandbox (Personal):** Nom curt (ex: `meu-invent`).
   * **Cistell (Organització):** Prefix de l'experiment (ex: `fil-17-meu-invent`).
3. **Pas 3:** Executa el Setup:
   `./cistell_setup.sh`
   *Això crearà el repo a l'Org, el baixarà al teu Linux (`~/cistell/`) i configurarà els enllaços (remotes).*

---

## 🚀 Comandes del Dia a Dia (Sincronització)

### 1. `git basket` (L'Àlies Maestro)
Aquesta comanda connecta el teu Linux amb els dos mons de GitHub simultàniament.
* **Què fa?** `Pull` + `Push Origin` (**Sandbox**) + `Push Org` (**Cistell Oficial**).
* **On s'usa?** Dins de les carpetes d'experiments: `~/cistell/nom-sandbox`.

### 2. `cistell_setup.sh` (L'Arquitecte)
Aquest script prepara la infraestructura abans de començar a programar.
* **Què fa?** Llegeix el `repos.txt`, crea els repositoris a l'Organització si no existeixen, els clona al teu Linux i configura els enllaços (`remotes`) de Git automàticament.
* **On s'usa?** A la Home (`~`), sempre que afegeixis un projecte nou al `repos.txt`.

### 3. `cistell_sync_all.sh` (El Sincronitzador Massiu)
La comanda per fer un "Guardar Tot" sense haver d'entrar carpeta per carpeta.
* **Què fa?** Recorre tots els teus projectes de `~/cistell/` i executa un `git basket` a cadascun. També fa un `pull` per portar canvis del núvol al Linux.
* **On s'usa?** A la Home (`~`), al final de la jornada o per sincronitzar-ho tot d'un cop.

### 4. `cistell_orchestrator.sh` (El Cervell)
L'eina de gestió total que coordina totes les fases del sistema en ordre.
* **Què fa?** Executa en seqüència: Provisionament (`setup`) + Execució (`sync_all`) + Auditoria (`issues`). Garanteix que tot el sistema estigui alineat.
* **On s'usa?** A la Home (`~`), al matí per començar el dia o després de canvis estructurals.

### 5. `issues_to_cistell.sh` (L'Auditor de Tasques)
Manté el teu tauler de control visual actualitzat sense intervenció manual.
* **Què fa?** Escaneja les "Issues" (tasques) obertes als teus repositoris i les sincronitza amb el **Project 4 Board** de l'Organització.
* **On s'usa?** S'executa automàticament a través de l'Orchestrator.

### 6. `sync_templates.sh` (El Guardià de la Governança)
Assegura que tots els teus projectes tinguin les mateixes regles i plantilles.
* **Què fa?** Copia les plantilles de `~/.github/ISSUE_TEMPLATE` a tots els repositoris del teu ecosistema.
* **On s'usa?** A la Home (`~`), **només** quan modifiquis els fitxers de configuració oficials a la carpeta `.github`.

## El Cicle de Git (Fases de Sincronització)
Si edites un fitxer, segueix aquest ordre per "oficialitzar-lo":

| Fase | Comanda | Significat Lògic |
| :--- | :--- | :--- |
| **Position** | `cd ~/.github` | **On ets?** Posa't a la carpeta del repositori. |
| **Stage** | `git add .` | **Preparació.** Poses els canvis a la "caixa" d'enviament. |
| **Commit** | `git commit -m "msg"` | **Segellat.** Tanques la caixa amb una etiqueta (què has fet?). |
| **Pull** | `git pull --rebase` | **Reconciliació.** Miro si GitHub té canvis que jo no tinc. |
| **Push** | `git push origin main` | **Execució.** Envies la caixa tancada al núvol. |

---

## ⚙️ Centre d'Operacions i Governança

La carpeta `~/.github` és el **Cervell del Sistema**. Conté les plantilles i el README oficial.

### 📍 Accés i Visibilitat (Fitxers Ocults)
A Linux, les carpetes que comencen amb un punt són **invisibles** per defecte.
* **Per entrar-hi:** `cd ~/.github` (hi pots anar encara que no la vegis).
* **Per veure-la:** `ls -la` (el flag `-a` mostra els ocults; `-l` mostra detalls d'auditoria).

### 🔄 Sincronització Especial (NO usis basket aquí)
Dins de `~/.github`, el destí és únic (l'Organització). El protocol és:
`git add .` → `git commit` → `git pull --rebase` → `git push origin main`.

---

## 🗺️ Mapa de Correlació (Linux ↔ GitHub)

| Localització Linux | Destí Sandbox (Personal) | Destí Cistell (Oficial) |
| :--- | :--- | :--- |
| `~/.github/` | (Cap) | `CistellDeCodi/.github` |
| `~/cistell/nom/` | `srustullet/nom` | `CistellDeCodi/fil-XX-nom` |

---

## 🔍 Resolució de Problemes (Audit Tips)

* **Error "Not a git repository":** Estàs a la Home (`/home/srustullet`). Mou-te a una carpeta oficial amb `cd`.
* **Error "Rejected":** GitHub té canvis més nous. Fes sempre `git pull --rebase` abans de fer el `push`.
* **He editat a la Home per error:** Si el fitxer bo és a `/home/srustullet`, mou-lo abans de pujar:
  `cp ~/README.md ~/.github/README.md`

## 🚀 Dreceres de Control (Àlies)

Per facilitar la gestió dels 16 fils, s'han configurat els següents àlies al fitxer `~/.bash_aliases`. Aquestes ordres permeten orquestrar tot el sistema amb el mínim d'esforç cognitiu.

### 📂 Navegació
* `admin`: Et porta directament a la torre de control (`~/cistell-admin`).
* `cistell`: Et porta a la carpeta on viuen els 16 repositoris/fils (`~/cistell`).

### 🛠️ Manteniment
* `setup-cistell`: Executa l'auditoria en bulk per configurar els remots (`origin` i `org`) a cada carpeta segons el `repos.txt`.
* `edita-repos`: Obre el fitxer de configuració de fils per afegir-ne de nous.
* `check-fil`: Mostra cap a on apunten els "túnels" (remots) del repositori on et trobes.

### 🔄 Sincronització (El Flux de Treball)
* `basket`: L'ordre mestre. Dins de qualsevol fil, fa: `pull` -> `add` -> `commit` -> `push` (Personal + Org).
* `push-admin`: Puja els canvis dels teus scripts de control i de la documentació al teu GitHub personal.

> **Nota de seguretat:** Si afegeixes un àlies nou manualment a `~/.bash_aliases`, recorda executar `source ~/.bashrc` perquè el terminal l'aprengui.

---
*Mantra: Sandbox per jugar (nom curt), Cistell per guardar (fil-XX). Si et sents perdut, "ls -la" i torna a la lògica.*
