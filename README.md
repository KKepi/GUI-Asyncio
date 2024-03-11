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
# Synchronní vs asynchroní programování
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

# Multithreading/vícevláknové programování
+ Funkce se spouští najednou (nečekají než se vykonají ostatní)
### jak spouštění probíhá
| kroky | CPU1       | CPU2       | CPU3       |
|------------|------------|------------|------------|
| 1 | funkce1 🕐 | funkce2 🕐 | funkce3 🕐 |
| 2 | funkce1 ✔️ | funkce2 🕐 | funkce3 ✔️ |
| 3 | ...        | funkce2 ✔️ | ...        |


**->** **spouštění** **všech** **funkcí/procedur** **najednou** **a** **snaha** **o** **dokončení** **všech** **najednou**
