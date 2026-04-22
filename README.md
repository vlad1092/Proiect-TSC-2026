# Proiect-TSC-2026

# PROIECT-TSC-2026

# InkTime Smartwatch PCB

## Descriere generala

Proiectul consta in realizarea unui PCB pentru un smartwatch open-source numit InkTime, bazat pe microcontroller-ul nRF52840. Scopul proiectului a fost integrarea tuturor componentelor necesare functionarii sistemului, incluzand partea de procesare, senzori, alimentare si interfata utilizator, pe o placa compacta, care sa respecte atat constrangerile electrice, cat si limitarile de spatiu specifice unui dispozitiv purtabil.

Design-ul a fost realizat in Fusion 360 Electronics, pornind de la schema electrica oferita si urmand regulile generale de layout discutate la laborator. In realizarea placii s-a pus accent pe rutare corecta, organizarea componentelor in functie de functionalitate si folosirea planurilor de masa pentru imbunatatirea stabilitatii electrice.

---

## Diagrama bloc

Componentele principale ale sistemului sunt:

- nRF52840 - microcontroller principal, cu suport BLE
- IMU - accelerometru si giroscop
- Display E-Paper
- PMIC - circuit de management al alimentarii
- Baterie Li-Po
- Conector USB-C pentru incarcare si alimentare
- Motor haptic pentru feedback prin vibratii

Conectarea dintre componente este realizata astfel:

- IMU este conectat la microcontroller prin interfata I2C
- Display-ul este conectat prin interfata SPI
- PMIC gestioneaza alimentarea intregului sistem
- USB-C este conectat la circuitul de incarcare si alimentare
- Motorul haptic este controlat printr-un pin GPIO al microcontroller-ului

---

## BOM (Bill of Materials)

| Componenta | Tip | Rol |
|-----------|-----|-----|
| nRF52840 | MCU | Controlul principal al sistemului si comunicatie BLE |
| IMU | Senzor | Detectarea miscarii |
| Display E-Paper | Display | Afisarea informatiilor |
| PMIC | Power Management | Gestionarea alimentarii |
| USB-C Connector | Conector | Alimentare si incarcare |
| Rezistente | Pasive | Polarizare, limitare curent, configurari |
| Condensatori | Pasive | Decuplare, filtrare si stabilizare |

BOM-ul contine componentele esentiale utilizate in proiect. Selectia lor a fost facuta astfel incat sa permita integrarea functionala a sistemului si sa fie compatibila cu procesul de fabricatie.

---

## Functionalitate hardware

Sistemul este construit in jurul microcontroller-ului nRF52840, care coordoneaza comunicatia cu toate perifericele si gestioneaza logica principala a dispozitivului.

Interfetele utilizate sunt:

- SPI pentru comunicatia cu display-ul, datorita necesitatii unui transfer mai rapid de date
- I2C pentru comunicatia cu IMU, fiind o solutie simpla si eficienta pentru senzori

Alimentarea este realizata de la o baterie Li-Po, prin intermediul unui circuit PMIC care are rolul de a:

- stabiliza tensiunea de alimentare
- gestiona procesul de incarcare
- distribui energia catre toate componentele sistemului

Conectorul USB-C este utilizat pentru:

- incarcarea bateriei
- alimentarea directa a placii in timpul testarii sau utilizarii

Motorul haptic este comandat printr-un semnal digital si este folosit pentru feedback tactil.

Din punct de vedere al consumului:

- microcontroller-ul are consum redus in modurile de economisire
- display-ul E-Paper are consum redus, mai ales deoarece nu necesita refresh constant
- IMU are consum mic si comunica eficient prin I2C

---

## Pini folositi (nRF52840)

### Interfata SPI
- MOSI
- SCK
- CS
- DC
- RST

### Interfata I2C
- SDA
- SCL

### GPIO-uri
- control motor haptic
- intrerupere IMU
- semnale de control pentru PMIC
- alte semnale auxiliare necesare functionarii sistemului

Alegerea pinilor a fost facuta astfel incat sa permita o rutare cat mai simpla, sa evite intersectiile inutile si sa mentina o organizare clara a conexiunilor dintre componente.

---

## Layout PCB

PCB-ul a fost proiectat pe 2 layere:

- Top Layer, folosit pentru amplasarea majoritatii componentelor si pentru o mare parte din rutare
- Bottom Layer, utilizat pentru rutare suplimentara si completarea planului de masa

In realizarea layout-ului au fost urmate cateva reguli generale:

- traseele de alimentare au fost facute mai groase decat traseele de semnal
- traseele de semnal au fost mentinute la dimensiuni reduse, conform regulilor de fabricatie
- s-a evitat folosirea unghiurilor de 90 de grade
- condensatorii de decuplare au fost plasati cat mai aproape de pinii de alimentare ai componentelor importante

Planurile de masa au fost realizate prin:

- polygon GND pe Top Layer
- polygon GND pe Bottom Layer
- conectare intre layere prin via stitching in zonele relevante

Pentru zona antenei au fost respectate reguli speciale:

- fara plan de cupru sub antena
- fara rutare in acea zona
- respectarea zonei de keepout pentru a nu afecta performanta RF

---

## Probleme intampinate

Pe parcursul proiectarii au aparut mai multe dificultati, dintre care cele mai importante au fost:

- erori DRC de tip overlap si clearance
- spatiu limitat pentru rutare in anumite zone aglomerate
- apropierea via-urilor de anumite pad-uri
- organizarea dificila a conexiunilor in jurul componentelor centrale

Pentru rezolvarea acestor probleme au fost aplicate urmatoarele solutii:

- refacerea rutarii in zonele critice
- utilizarea via-urilor pentru escape routing
- reorganizarea unor trasee pentru a respecta clearance-ul
- adaugarea planurilor de masa
- eliminarea rutarii din zona antenei

Au ramas si cateva zone foarte dense, unde solutia aleasa a reprezentat un compromis rezonabil intre spatiul disponibil si functionalitatea generala a placii.

---

## Mechanical

Integrarea mecanica a fost luata in considerare in timpul proiectarii PCB-ului, prin respectarea dimensiunilor componentelor conform datasheet-urilor si prin amplasarea acestora astfel incat sa permita integrarea intr-un format compact.

Nu a fost realizat un model 3D complet al ansamblului, insa dimensiunile componentelor importante, precum bateria si display-ul, au fost avute in vedere pentru a evita conflictele mecanice evidente si pentru a permite o viitoare integrare intr-o carcasa.

---

## Imagini

Pentru prezentarea proiectului pot fi incluse:

- capturi ale schemei electrice
- imagini 2D ale PCB-ului
- capturi ale rutarii finale
- imagini cu verificarile DRC/ERC, daca este cazul

---

## Decizii de design si compromisuri

Pe parcursul realizarii PCB-ului au fost luate cateva decizii de design considerate acceptabile in contextul spatiului limitat si al complexitatii proiectului:

- in unele zone, via-urile au ramas apropiate de anumite pad-uri SMD pentru a permite escape routing-ul
- anumite trasee sunt rutate foarte aproape unele de altele, dar raman in limitele impuse de regulile de proiectare
- via stitching a fost aplicat doar in zonele in care a adus un avantaj clar, pentru a evita aglomerarea inutila
- in zona antenei a fost eliminat complet planul de masa si orice traseu, chiar daca acest lucru a complicat rutarea in restul placii
- organizarea componentelor a fost facuta cu prioritate pentru functionalitate si trasee cat mai scurte, chiar daca in unele zone aspectul final este mai incarcat

Aceste compromisuri au fost necesare pentru a putea finaliza un design functional fara modificarea majora a topologiei generale a placii.

---

## Concluzie

Design-ul final al PCB-ului este functional si respecta in mare parte regulile de proiectare urmarite in cadrul proiectului. Au fost identificate si corectate problemele importante aparute pe parcurs, iar layout-ul a fost ajustat pentru a imbunatati rutarea, alimentarea si organizarea componentelor.

Chiar daca au existat limitari de spatiu si unele compromisuri de layout, rezultatul final reprezinta o solutie utilizabila pentru integrarea componentelor unui smartwatch compact bazat pe nRF52840.
