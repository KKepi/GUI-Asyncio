# AsyncIO 


## Instalace knihovny
```
pip install asyncio
```
## Principy programování v rámci synchronizace
```
funkce1()
funkce2()
funkce3()
```
# Synchronní programování 🕐 ✔️ 🔒
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
**->** **snaha** **o** **spouštění** **všech** **funkcí/procedur** **najednou**


