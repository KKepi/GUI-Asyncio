# AsyncIO 


## Instalace knihovny
```
pip install asyncio
```
## Principy programování v rámci synchronizace
```
def funkce1():
  ....
def funkce2():
  ....
def funkce3():
  ....
```
```
funkce1()
funkce2()
funkce3()
```
# Vykonávání kódu
+ Synchronní programování
+ Asynchronní programování

## Synchronní programování
+ Funkce se spouští postupně, každá funkce musí být dokončena než začne následující
### Pro lepší představení:
*zavolání funkcí*  
funkce1 🔒  
funkce2 🔒  
funkce3 🔒  

*krok 1*  
funkce1 ▶️  
funkce2 🔒  
funkce3 🔒  

*krok 2*  
funkce1 ✔️  
funkce2 ▶️  
funkce3 🔒  

*krok 3*  
funkce1 ✔️  
funkce2 ✔️  
funkce3 ▶️  

*krok 4*  
funkce1 ✔️  
funkce2 ✔️  
funkce3 ✔️  

**funkce1** **->** **funkce2** **->** **funkce3**

## Asynchronní programování
+ Funkce se spouští dle volného prostoru (spustí se jedna a pokud je prostor spustí se jiná)
### Pro lepší pochopení:

*krok 1*  
funkce1 ▶️  
funkce2 🔒  

*krok 2*  
funkce1 🕐  
funkce2 ▶️  

*krok 3*  
funkce1 ▶️  
funkce2 ✔️ 

*krok 4*  
funkce1 ✔️  
funkce2 ✔️ 

# Spouštění kódu
+ váže se na hardware

+ single-thread
+ multi-thread
+ multi-process

## single-thread
+ všechny funkce se spouští v rámci jednoho vlákna 'kontextu'
+ typicky pro synchronní ale i asynchronní model

### sychronní
| kroky | CPU: Thread1       |
|------------|------------|
| 1 | funkce1 ▶️ |
|  | funkce2 🔒 |
| 2 | funkce1 ✔️ |
|  | funkce2 ▶️ |
| 3 | funkce1 ✔️ |
|  | funkce2 ✔️ |

### asynchronní
| kroky | CPU: Thread1       |
|------------|------------|
| 1 | funkce1 ▶️ |
|  | funkce2 🔒 |
| 2 | funkce1 🕐 |
|  | funkce2 ▶️ |
| 3 | funkce1 ▶️ |
|  | funkce2 ✔️ |
| 4 | funkce1 ✔️ |
|  | funkce2 ✔️ |

## multi-thread
+ funkce jsou rozdělený do určitého počtu vláken tj. jedno vlákno spouští x funkcí, druhé vlákno spouští y funkcí, ....
+ funkce se mohou spouštět paralélně (najednou)  
+ **! správa vláken a synchronizace mezi nimi**
+ **! společný paměťový prostor !**

| kroky | CPU       | ...       |
|------------|------------|------------|
| ... | Thread1       | Thread2       |
| 1 | funkce1 ▶️ | funkce2 ▶️ |
| 2 | funkce1 ✔️ | funkce2 ▶️ |
| 3 | funkce1 ✔️ | funkce2 ✔️ |

## multi-process
+ podobné multi-thread
+ místo vláken využívá procesy, tj. využívá jádra procesoru  
+ **každý proces má svůj paměťový prostor**

| kroky | CPU       | ...       |
|------------|------------|------------|
| ... | CPU1       | CPU2       |
| 1 | funkce1 ▶️ | funkce2 ▶️ |
| 2 | funkce1 ▶️ | funkce2 ▶️ |
| 3 | funkce1 ✔️ | funkce2 ✔️ |

# AsyncIO
importujeme asyncio
```
import asyncio
```
Asynchronní programování nejčastěji využíváme při I/O operacích. Tyto operace (čekání na odpověď serveru) budeme simulovat pomocí příkazu ''*await asyncio.sleep(x)*'', kde x představuje čas.

vytvoříme asynchronní funkci a spustíme ji 
```
async def main():
  print("A")
  await asyncio.sleep(1)
  print("B")

asyncio.run(main())
```
Prodleva mezi vypsáním "A" a "B" je znatelná. Co kdybychom tuhle prodlevu (v praxi čekání na odpoveď během které program stojí a nic nedělá) využili k vykonání jiné funkce.  pojďme tedy vytvořit další asynchronní funkci, která toto místo vyplní.
```
async def main():
  print("A")
  await vyplnujici_funkce()
  print("B")

async def vyplnujici_funkce():
  print("1")
  print("2")

asyncio.run(main())
```
Zdá se vám toto jako asynchronní spuštění? - Ne. Pomocí příkazu "*await*" jsme vynutili spuštění vyplňující funkce. Toto vynucení je, ale velmi podobné synchronnímu programování, kde prostě během výpisu spustíme jinou funkci - tj. nevyužíváme volného prostoru (čas)  

Pojďme tedy, využívat volného prostoru v rámci času a využijme tak opravdové asynchronní programování.



