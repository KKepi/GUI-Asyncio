#  knihovnu AsyncIO, která nám poskytuje nástroje, díky kterým můžeme asynchronně programovat.
-> Z názvu si můžete všimnout posledních 2 písmen - IO, což je zkratka pro I/O neboli input a output. 
Jedná se o situaci během které dochází k vnější komunikaci mezi interpreterem a jiným systémem. Klient představuje input tj. požadavek
během kterého čeká na output (odpověď) od serveru. Ve všedním synchronním programováním by program během čekání na odpověď stál a nic nevykonával.  
To je z časového hlediska nepraktické a proto přichází na stage asynchronní programování, které nabízí možnost během čekání vykonávat jinou funkci.
-> alternativně bychom to mohli vyřešit pomocí využití více vláken nebo více procesů, což je ale v pythonu problematický.  

Dnes se tedy naučíme jak pomocí knihovny asyncio vykonávat více funkcí paralélně, kde se běh funkcí bude střídat dle volného časového prostoru.

středobodem synchronního a asynchronního programování je interpreter  

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
3.1) importujeme asyncio  
3.2)  
+ Asynchronní programování nejčastěji využíváme při I/O operacích. Tyto operace (čekání na odpověď serveru) budeme simulovat pomocí příkazu ''*await asyncio.sleep(x)*'', kde x představuje čas.

vytvoříme asynchronní funkci a spustíme ji  
3.3)  
+ Prodleva mezi vypsáním "A" a "B" je znatelná. Co kdybychom tuhle prodlevu (v praxi čekání na odpoveď během které program stojí a nic nedělá) využili k vykonání jiné funkce.  pojďme tedy vytvořit další asynchronní funkci, která toto místo vyplní.  
3.4)
+ Zdá se vám toto jako asynchronní spuštění? - Ne.   
+ Pomocí příkazu "*await*" jsme vynutili spuštění vyplňující funkce - program ale čekal na dokončení vyplňující funkce i přesto, že se v ní nachází volný prostor (asyncio.sleep(2)).   
+ Toto vynucení je, ale velmi podobné synchronnímu programování, kde prostě během výpisu spustíme jinou funkci - tj. nevyužíváme volného prostoru (čas).

Pojďme tedy, využívat volného prostoru v rámci času a využijme tak opravdové asynchronní programování.  
Toho dosáhneme pokud v prostředí připravíme task, ten obsahuje funkci, která se spustí jestliže na spuštění bude volný časový prostor.  

3.5)  
+ Po spuštění funkce "*main()*" jsme zjistili, že v ní existuje volný časový prostor až na konci funkce tj. po vykonání poslední operace (print("B")).  
+ Následně se spustila vyplňující funkce, která ale nedoběhla celá - existuje v ní volný prostor (asyncio.sleep()) a to se hlavní funkci nelíbí.  
  
+ Jestliže chceme, aby hlavní funkce na vyplňující funkci i tak počkala můžeme přidat příkaz "*await task*".  
+ Tento příkaz se postará o to, aby si vyplňující funkce našla alespoň jeden prostor na spuštění - typicky na konci hlavní funkce

3.6)  
+ Názornějším scénářem nám bude situace, kde je časový prostor na spuštění alespoň části vyplňující funkce.
 
(main.sleep < vyplnujici_funkce.sleep)  

3.7)  
+ Pojďme hlavní funkci požádat o pokračování vyplnujici funkce ve více časových prostorech tj. využití sleep() a prostoru na konci hlavní funkce.  
3.8)
+ Pořád, ale neelegantně vynucujeme časový prostor a nevyužíváme "samovolné" asynchronní spouštění těchto funkcí.  
+ Pojďme vytvořit scénář, kde žádne vynucování neexistuje a funkce se spouští číste vzhledem k volnému časovému prostoru.

3.9)  
+ Pokud chceme, aby vyplňující funkce vracela nějakou hodnotu použijeme příkaz "*await task*"  
> ! Tento přikaz použijeme jen když jsme si jisti, že vyplňující funkce byla již dokončena !  
> ! Pokud vyplňující funkce ještě nebyla dokončena tento příkaz vynutí spuštění vyplňující funkce a bude na ni čekat nehledě na volný časový prostor !

3.10)  
+ V případě, že máme více vyplňujících funkcí (tasků), které chceme pustit "současně" tj. zahájení je současné (doopravdy se vykonává funkce pro kterou je časový prostor - !nejedná se o multi-thread nebo multi-process! využijeme nástroje "*gather(funkce1,funkce2,funkce3, ....)*"  
+ await asyncio.gather(x,y) se postará o to, aby se funkce *x,y* spustily a počká než se všechny dokončí.

Ten nám tasky shromáždí a bude je spouštět dle volného časového prostoru -> horší manévrování, ale stejná podstata předešlých úkolů  

3.11)  
+ Pokud bychom chtěli spouštět více vyplňujících funkcích, ale jen v případě, že na ně bude prostor vzhledem k dění v hlavní funkci, můžeme toto shromaždění (gather) zaobalit v nove funkci.  
-> lepší manévrování než v předešlém kroku
