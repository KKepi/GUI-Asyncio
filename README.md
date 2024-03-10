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
# Synchronní programování
+ Funkce se spouští postupně (čekají než se vykoná předchozí)
### jak spouštění probíhá

*zavolání funkcí*  
funkce1 🔒  
funkce2 🔒  
funkce3 🔒  

*krok 1*  
funkce1 🕐  
funkce2 🔒  
funkce3 🔒  

*krok 2*  
funkce1 ✔️  
funkce2 🕐  
funkce3 🔒  

*krok 3*  
funkce1 ✔️  
funkce2 ✔️  
funkce3 🕐  

*krok 4*  
funkce1 ✔️  
funkce2 ✔️  
funkce3 ✔️  

**funkce1** **->** **funkce2** **->** **funkce3**

# Multithreading/vícevláknové programování
+ Funkce se spouští najednou (nečekají než se vykonají ostatní)
### jak spouštění probíhá
| kroky | CPU1       | CPU2       | CPU3       |
|------------|------------|------------|------------|
| 1 | funkce1 🕐 | funkce2 🕐 | funkce3 🕐 |
| 2 | funkce1 ✔️ | funkce2 🕐 | funkce3 ✔️ |
| 3 | ...        | funkce2 ✔️ | ...        |


**->** **spouštění** **všech** **funkcí/procedur** **najednou** **a** **snaha** **o** **dokončení** **všech** **najednou**

# Asynchronní programování
+ Funkce se spouští dle volného prostoru (vždy se spustí jedna a pokud je prostor spustí se jiná)
