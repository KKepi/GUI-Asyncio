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
+ Jedna funkce po druhé + čekání než se předchozí funkce vykoná
```
funkce1()
funkce2()
funkce3()
```
### jak spouštění probíhá
*funkce1()* 🔒  
*funkce2()* 🔒  
*funkce3()* 🔒  

*funkce1()* 🕐  
*funkce2()* 🔒  
*funkce3()* 🔒  

*funkce1()* ✔️  
*funkce2()* 🕐  
*funkce3()* 🔒  

*funkce1()* ✔️  
*funkce2()* ✔️  
*funkce3()* 🕐  

*funkce1()* ✔️  
*funkce2()* ✔️  
*funkce3()* ✔️  

**funkce1** **->** **funkce2** **->** **funkce3**

# Multithreading/vícevláknové programování
+ Víc funkcí najednou
```
funkce1()
funkce2()
funkce3()
```
### jak spouštění probíhá
CPU 1  
*funkce1()* 🕐 -> *funkce1()* **+-** ✔️

CPU 2  
*funkce2()* 🕐 -> *funkce2()* **+-** ✔️

CPU 3  
*funkce3()* 🕐 -> *funkce3()* **+-** ✔️

**->** **spouštění** **všech** **funkcí/procedur** **najednou** **a** **snaha** **o** **dokončení** **všech** **najednou**

# Asynchronní programování
+ Vždy běží jen jedna funkce - ostatní funkce se můžou spustit dle prostoru
```
funkce1()
funkce2()
funkce3()
```
