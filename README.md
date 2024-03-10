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
# Synchronní programování
+ Funkce se spouští postupně (čekají než se vykoná předchozí)
```
funkce1()
funkce2()
funkce3()
```
### jak spouštění probíhá
funkce1 🔒  
funkce2 🔒  
funkce3 🔒  

funkce1 🕐  
funkce2 🔒  
funkce3 🔒  

funkce1 ✔️  
funkce2 🕐  
funkce3 🔒  

funkce1 ✔️  
funkce2 ✔️  
funkce3 🕐  

funkce1 ✔️  
funkce2 ✔️  
funkce3 ✔️  

**funkce1** **->** **funkce2** **->** **funkce3**

# Multithreading/vícevláknové programování
+ Funkce se spouští najednou (nečekají než se vykonají ostatní)
```
funkce1()
funkce2()
funkce3()
```
### jak spouštění probíhá
CPU 1  
funkce1 🕐 -> funkce1 ✔️

CPU 2  
funkce2 🕐 -> funkce2 🕐 -> funkce2 ✔️

CPU 3  
funkce3 🕐 -> funkce3 ✔️

**->** **spouštění** **všech** **funkcí/procedur** **najednou** **a** **snaha** **o** **dokončení** **všech** **najednou**

# Asynchronní programování
+ Funkce se spouští dle volného prostoru (vždy se spustí jedna a pokud je prostor spustí se jiná)
```
funkce1()
funkce2()
funkce3()
```
