# Rossz PR példák

Példák arra hogy hol mehet félre egy PR és mi ennek az oka. 
## 1. Beküldött merge conflict maradványok  

Példa:  
https://github.com/run-llama/llama_index/pull/20636/files

A merge conflict maradványok olyan jelölések, amelyek akkor jelennek meg, amikor két olyan változtatás ütközik, amelyek ugyanazon a kódon történnek. 

Ezek a maradványok általában `<<<<<<<`, `=======`, és `>>>>>>>` jelölésekkel vannak ellátva, amelyek megmutatják a konfliktusos részeket. (Erre amúgy néztünk már példát)

Hogy kerül be ilyen?  
- Figyelmetlenség
- Lustaság
- Nem tudja, hogy ez egy probléma (ez a legrosszabb eset)

Miért nem veszi észre a code review?
- Nem figyelnek eléggé (pl. LGTM)
- Nem tudják, hogy ez egy probléma (ez a legrosszabb eset)  

Mi az a CICD? Miért van itt jelentősége?

![image.png](https://cdn2.hubspot.net/hubfs/3937956/CICDBlog.png)

A Continuous Integration Continous Development (CI/CD) egy szoftverfejlesztési gyakorlat. Leginkább a fejlesztési folyamat automatizálására szolgál, beleértve a kód integrációját, tesztelését és telepítését. 

Ez segíthet gyorsan észrevenni a hibákat és problémákat, mielőtt azok bekerülnének a kódbázisba. Ez akár commit előtt is megvalósítható egy pre-commit hook segítségével.

Mit lehet ebben a PR-ban észrevenni? Hogy nem volt megfelelő CICD, holott az egyik leggyakrabban használt LLM package-ről van szó.

## 2. LGTM

https://github.com/run-llama/llama_index/pull/20666

Mit jelent?
- Looks Good To Me
- Let's Get This Merged
- Legitimate
- Let's Gamble, try merge

Miért rossz szokás?
- Gyakran felületes
- Sokszor inkább bürokratikus, mint hasznos
- Nem ad valódi visszajelzést a kód minőségéről
- Nem segít a fejlesztőknek fejlődni és tanulni a hibáikból

## 3. Nincs teszt a PR-ben  

https://github.com/docling-project/docling/pull/534/files

Mi itt a baj?
- Nem biztos, hogy a változtatások helyesen működnek
- Nem biztos, hogy a változtatások nem törnek meg más részeket
- Nem biztos, hogy a változtatások megfelelnek a követelményeknek

Konkrét eset:  
A PR pont elrontja a Magyar Word dokumentumok feldolgozhatóságát. 

Ez pl a felhasznált package dokumentációjából ki is derül egyébként:  
https://python-docx.readthedocs.io/en/latest/user/styles-understanding.html

# Formatting, linting és type checking

Amikor programozunk, általában szeretnénk, hogy a kódunk:
- Működjön, azaz megfeleljen az adott nyelv szintaxisának
- Kövesse az ajánlott gyakorlatokat a jó minőségért (például konstanst használata, nevek következetes használata, stb.)
- Azonos formátumot használjon (például tabulátorokat, egységes sorhosszúságot, stb.)

## Formatting, linting

Mi a különbség a linting és a formatting között? Mindkettő Absztrakt Szintaxisfa (AST) alapú, de:
- a linting az első két pontra fókuszál
- a formatting a harmadikra

Kielégítik teljességében a fenti igényeket?

![AST](https://www.scaler.com/topics/images/python-ast_thumbnail.webp)

## Type checking

Python egy dinamikusan nyelv, ami azt jelenti, hogy a változók típusát futásidőben határozza meg. Ennek vannak előnyei (pl. notebook, gyors prototípus), de vannak hátrányai is (pl. lassú)

## Eszközök

- Formatter/linter (ruff)
- Type checker (mypy).

## Example

```python
def moo_moo_IΙI11I (buzz_buzz_buzz_O00ΟΟΟ ):
    buzz_buzz_buzz_IIΙlΙI ,b =0 ,1 
    for _ in range (buzz_buzz_buzz_O00ΟΟΟ ):
        yield buzz_buzz_buzz_IIΙlΙI 
        buzz_buzz_buzz_IIΙlΙI ,b =b ,buzz_buzz_buzz_IIΙlΙI +b 


if __name__ =="__main__":
    for num in moo_moo_IΙI11I (10 ):
        print (num )
```