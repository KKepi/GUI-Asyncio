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
# Asynchronní programování
+ Jako první se spustí *funkce1()*
+ Po dokončení *funkce1()* přichází na řadu *funkce2()*
+ Po skončení *funkce2()* se spouští *funkce3()*
```
funkce1()
|
V
funkce2()
|
V
funkce3()
```
