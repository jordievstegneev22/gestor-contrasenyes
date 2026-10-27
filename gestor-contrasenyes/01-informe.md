# Informe: Gestor de contrasenyes per a EverPia

**Mòdul:** 0226 Seguretat Informàtica
**Activitat:** 0226NF1.AA3 – Gestor de contrasenyes
**Autor:** Jordi

---

## 1. Introducció i justificació

EverPia ha patit una fuita d'informació (*data breach*). La investigació interna ha demostrat que un compte tècnic va ser compromès per l'ús d'una **contrasenya feble o reutilitzada**. Per això, la Direcció Tècnica ha decidit que tot el personal tècnic utilitzi un gestor de contrasenyes.

### 1.1 Per què les contrasenyes febles o reutilitzades són un risc

| Atac | Com funciona | Per què és perillós |
|---|---|---|
| **Atac de diccionari** | L'atacant prova llistes de contrasenyes comunes i paraules (`123456`, `password`, `everpia2024`...). | Les contrasenyes fàcils de recordar solen estar en aquestes llistes i cauen en segons. |
| **Força bruta** | Es proven totes les combinacions possibles de caràcters. | Una contrasenya curta (8 caràcters o menys) es pot trencar en poc temps. |
| **Credential stuffing** | Es fan servir usuaris i contrasenyes filtrats d'una altra web per entrar als serveis de l'empresa. | Si un treballador reutilitza la mateixa contrasenya, una filtració externa dona accés a EverPia. |
| **Phishing** | Es crea una web falsa idèntica a la real per robar credencials. | L'usuari escriu la contrasenya sense adonar-se que la web és falsa. |

### 1.2 La funció d'un gestor de contrasenyes

Un gestor de contrasenyes és una **caixa forta digital xifrada** on es guarden totes les credencials. Mitiga els riscos anteriors perquè:

- **Genera contrasenyes llargues i aleatòries**, impossibles de trobar amb diccionaris i molt difícils de trencar per força bruta.
- Permet tenir **una contrasenya diferent per a cada servei**, cosa que elimina el risc del *credential stuffing*.
- **Només emplena les credencials al domini correcte**, i això ajuda a detectar webs de *phishing*.
- L'usuari només ha de recordar **una contrasenya mestra**.

---

## 2. Comparativa tècnica

| Criteri | Bitwarden (online / núvol) | KeePassXC (offline / escriptori) |
|---|---|---|
| **Emmagatzematge** | Servidors de Bitwarden (EUA o UE) | Arxiu local `.kdbx` a l'ordinador de l'usuari |
| **Model de seguretat** | Xifratge *end-to-end* AES-256. Les dades es xifren al dispositiu i el servidor no pot llegir-les. | Xifratge AES-256 o ChaCha20, amb la clau derivada amb Argon2 |
| **Sincronització** | Automàtica entre tots els dispositius | Manual: cal copiar l'arxiu o usar un núvol propi |
| **Accés multidispositiu** | Web, aplicació d'escriptori, mòbil i extensió de navegador | Escriptori (Windows, Linux, macOS); al mòbil cal usar apps de tercers |
| **Dependència del núvol** | Sí (tot i que es pot autoallotjar) | Cap |
| **Codi obert** | Sí, amb auditories de seguretat externes | Sí |
| **Compartir amb l'equip** | Sí, amb organitzacions i col·leccions | Només compartint l'arxiu sencer |
| **Portabilitat** | Exportació en JSON (xifrat o no) i CSV | Arxiu `.kdbx` portàtil i versió portable sense instal·lació |
| **Cost** | Model *freemium*: versió gratuïta i plans Premium i Empresa de pagament | Totalment gratuït |

---

## 3. Avantatges i inconvenients

### Model online (Bitwarden)

| | Avantatges | Inconvenients |
|---|---|---|
| **Seguretat** | Xifratge *end-to-end*, verificació en dos passos (2FA) i servidor a la UE (RGPD) | Depèn d'una empresa externa; si el servei patís un atac, les dades estarien xifrades però exposades |
| **Usabilitat** | Molt fàcil: sincronització automàtica i extensió que emplena les dades | Cal connexió a Internet per sincronitzar |
| **Continuïtat del negoci** | Si es perd un ordinador, les contrasenyes continuen disponibles des de qualsevol altre dispositiu | Si el servei cau, l'accés pot quedar limitat temporalment |

### Model offline (KeePassXC)

| | Avantatges | Inconvenients |
|---|---|---|
| **Seguretat** | Control total: les dades no surten mai de l'ordinador | La seguretat depèn de com l'usuari protegeixi i copiï l'arxiu |
| **Usabilitat** | Funciona sense Internet | Menys còmode: sincronització manual i menys integració amb el mòbil |
| **Continuïtat del negoci** | No depèn de cap proveïdor extern | Si es perd l'arxiu i no hi ha còpia, es perden totes les contrasenyes |

---

## 4. Recomanació

L'eina recomanada per al personal tècnic d'EverPia és **Bitwarden**, pels motius següents:

1. **Treball en diversos dispositius:** el personal tècnic treballa des de diferents ordinadors i mòbils, i Bitwarden sincronitza les credencials automàticament.
2. **Treball en equip:** permet compartir credencials entre tècnics de forma controlada amb organitzacions, sense haver de passar-se arxius.
3. **Seguretat:** ofereix xifratge *end-to-end*, verificació en dos passos (2FA) i servidor europeu, que facilita complir el RGPD.
4. **Facilitat d'ús:** l'extensió del navegador emplena les credencials automàticament, i això fa que el personal l'adopti més fàcilment.

El principal inconvenient és la **dependència d'un servei extern**. Es mitiga amb el xifratge *end-to-end* (Bitwarden no pot llegir les dades), l'activació obligatòria del 2FA i **còpies de seguretat xifrades periòdiques**, tal com s'explica a la [Guia d'ús](02-guia-us.md).
