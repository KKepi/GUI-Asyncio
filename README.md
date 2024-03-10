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

CPU 1
*funkce1()* 🕐

CPU 2
*funkce2()* 🕐

CPU 3
*funkce3()* 🕐

**->** **snaha** **o** **spouštění** **všech** **funkcí/procedur** **najednou**


