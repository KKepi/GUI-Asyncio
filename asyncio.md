#  knihovnu AsyncIO, která nám poskytuje nástroje, díky kterým můžeme asynchronně programovat.
-> Z názvu si můžete všimnout posledních 2 písmen - IO, což je zkratka pro I/O neboli input a output. 
Jedná se o situaci během které dochází k vnější komunikaci mezi interpreterem a jiným systémem. Klient představuje input tj. požadavek
během kterého čeká na output (odpověď) od serveru. Ve všedním synchronním programováním by program během čekání na odpověď stál a nic nevykonával.  
To je z časového hlediska nepraktické a proto přichází na stage asynchronní programování, které nabízí možnost během čekání vykonávat jinou funkci.
-> alternativně bychom to mohli vyřešit pomocí využití více vláken nebo více procesů, což je ale v pythonu problematický.  

Dnes se tedy naučíme jak pomocí knihovny asyncio vykonávat více funkcí paralélně, kde se běh funkcí bude střídat dle volného časového prostoru.

# 1) Pythonovský interpreter má GIL - global interpreter lock - a ten má právě nevýhody, kvůli kterým je použití více-vláknového programování problematický.
GIL je zámek, který se stará o to, aby se náš kód v interpreteru vykonával jen v jednom vlákně (threadu). Kvůli tomu dokážou být procesy zdlouhavý. Bohužel je teda v pythonu opravdový více-vláknový programování nemožné. Některý knihovny se snaží tenhle proces obejít tím, že pomocí jednoho vlákna pouští střídavě více "pseudo-vláken". Efektivnější ještě může být multi-processing, kde se vlastně spouští více python interpreterů najednou. My budeme dneska používat asyncio, asynchronní programování, který pracuje s jedním vláknem. Jeho efektivita spočívá v tom, že se s ostatníma funkcema o volný časový prostor střídá.

V podstatě jde o algoritmus jakým lze efektivně obejít nevýhody global interpreter locku, který přistupuje k řádkům kódu.

Synchronní, asynchronní, multi-thread, multi-process....?

Synchronní programování je nám velmi známé a mnozí z nás pracovali doposud jen s ním. 
Jeho podstatou je, že se funkce spouští postupně dle řádku a každá funkce musí být dokončena než začne další.
Pro lepší představu jsem vytvořil diagram.

U Asynchronního programování se taky spouští jen jedna funkce, ale výhodou je, že funkce o sobě navzájem ví a střídají se dle volného prostoru.
Tento volný prostor je chápán ve smyslu času. To znamená, že pokud je spuštěna nějaká funkce a zrovna čeká na odpověď typicky z nějakého externího zdroje spustí se mezi tím jiná funkce.
Pro lepší představu jsem vytvořil diagram.

# 2) Synchronní a asynchronní programování je to jak se softwarově spouští kód v interpreteru. 
Co se týče fyzického spouštění můžeme způsoby klasifikovat na 3 kategorie dle toho jak probíhá spouštění kódu vzhledem k hardwaru.
### multi-thread  
1 jádro CPUčka řídí více vláken v kterých běží různé funkce, kde tyhle vlákna běží paralélně - najednou  

### multi-process  
více jáder v kterých běží libovolný počet vláken v kterých běží různé funkce, kde tyhle jádra a vlákna běží paralélně najednou


# 3)
3.1) 
3.2)
3.3)
3.4)
3.5)
3.6)
3.7)
3.8)
3.9)
3.10)
