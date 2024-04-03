# xml-python

En el següent repositori veurem un resum del que hem après en aquest curs sobre Python i XML, ara es presenta una llista ordenada del que es presenta:

1. Sobre Python:
  -Conceptes Bàsics
  -Llistes, diccionaris i manipulació de fitxers

2. Sobre XML:
   -Conceptes Bàsics
   -Sobre DOM i XSLT
   
Tot anirà acompanyat d'exemples de codi i imatges. 

# Sobre Python

## Conceptes bàsics: 

Hem vist com crear un programa bàsic en Python, començant poc a poc des del pseudocodi fins als bucles for i while. Això ho hem fet practicant amb diversos programes (exercicis) com per exemple, crear un programa de conversió d'unitats, o practicant els [range](https://www.w3schools.com/python/ref_func_range.asp) amb exercicis dedicats. 

**Exemple de la utilització del bucle FOR a Python**:

![Imatge sobre la utilització simple del bucle FOR](https://i.ytimg.com/vi/9LgyKiq_hU0/maxresdefault.jpg)



## Llistes, Diccionaris i manipulació de fitxers a Python:

He aprés a crear una llista i recorrer-la seleccionant els elements demanats. Això inclou utilizar correctament un for o un while per obtenir els resultats demanats. 

A través del següent [link](https://www.w3schools.com/python/python_for_loops.asp) és com he après a recorrer llistes. També hem practicat **els diccionaris** i com crear claus i diferents valors entre ells (tota la informació es troba en el següent [link](https://www.w3schools.com/python/python_dictionaries.asp)).

Finalment, els coneixements més recents són sobre *creació de fitxers, escritura i tancament*. He après com crear un nou fitxer i afegir-li la informació necessària (el que m'ha ajudat a comprendre els continguts donats a llenguatge de marques). 

# Sobre Llenguatge de Marques: 

## Conceptes bàsics: 

Al començament vam aprendre una mica sobre què és l'XML i per a què serveix, practicant com crear uns documents ben estructurats en format XML, i assegurar que l'anàlisi que es fa del document funciona correctament i, per tant, el document està ben format. Tota la introducció i pràctica incial la vam veure en [aquesta presentació](https://drive.google.com/file/d/1LbDhBWXuFD3vhonYY_HiukKoruCT0v1P/view), però encara i així deixo un exemple de codi en XML per a mostrar de manera visual com és un XML simple. 

**Codi simple en XML**

```
<?xml version="1.0" encoding="UTF-8"?>
<jugadores>
  <jugador posicion="portero">
    <nombre>Javier Jiménez</nombre>
    <nacionalidad>española</nacionalidad>
  </jugador>
  <jugador posicion="delantero">
    <nombre>Nong</nombre>
    <nacionalidad>camerunés</nacionalidad>
  </jugador>
  <jugador posicion="portero">
    <nombre>Mikel González</nombre>
    <nacionalidad>española</nacionalidad>
  </jugador>
</jugadores>
```
**Imatge sobre el conjunt de tecnologies que representen l'XML**


![Imatge sobre el conjunt de tecnologies que representen l'XML](https://th.bing.com/th/id/R.c5344959c039e1864923aee43524226b?rik=6mYYPwkLLtSItQ&riu=http%3a%2f%2ftcpschool.com%2flectures%2fimg_xml_xdm.png&ehk=ZEblftyWuhbVtfziHdNtKaq3dPRwfiHL7SwWlSYKN1o%3d&risl=&pid=ImgRaw&r=0)



## Sobre DOM i XSLT: 

L'últim que hem après és utilitzar minidom i XSLT, i per a fer-ho hem estudiat la teoría i hem fet alguns exercicis. Aprendre sobre Python ha anat molt bé per a dominar amb una mica més de facilitat minidom. Minidom ens permet treballar amb fitxers XML per obtenir dades i afegir-les al document que necessitem. Això s'aconsegueix important minidom al nostre entorn Python i treballant amb aquest. A continuació es mostra un exemple d'exercici fet amb Minidom, amb el que havíem de fer un horari en el que havíem d'extreure les dades d'un XML: 

**Exercici fet amb Minidom**

```
from xml.dom import minidom

file=open("Horario_final_2.html", "w")
file.write("<html><head><title>Horari de l'alumne</title></head><body>\n")

doc=minidom.parse("Horario_xml_minidom.xml")

tag_horari=doc.documentElement

tag_alumne=tag_horari.getElementsByTagName('alumne')[0]

nom=tag_alumne.getElementsByTagName('nom')[0].firstChild.data
curs=tag_alumne.getElementsByTagName('curs')[0].firstChild.data
foto=tag_alumne.getElementsByTagName('foto')[0].firstChild.data

file.write(f'''<h1>{nom}</h1>
<h1>{curs}</h1>
<p><img src='{foto}' alt='Foto de l'alumne' width='100' height='100' />/<p>\n''')

colors={}

tag_colors=tag_horari.getElementsByTagName('colors')[0]

for tag_assignatura in tag_colors.getElementsByTagName("assignatura"):
    color=tag_assignatura.getAttribute('color')
    assignatura=tag_assignatura.firstChild.data
    colors[assignatura]=color
    
franjes=[]

tag_franjes=tag_horari.getElementsByTagName('franges')[0]

for tag_franja in tag_franjes.getElementsByTagName('franja'):
    franja=tag_franja.firstChild.data
    franjes.append(franja)

dies=[]
clases={}

tag_clases=tag_horari.getElementsByTagName('classes')[0]

for tag_dia in tag_clases.getElementsByTagName('dia'):
    dia=tag_dia.getElementsByTagName("nom")[0].firstChild.data
    dies.append(dia)
    
    clases[dia]=[]
    
    tag_assignatures=tag_dia.getElementsByTagName("assignatures")[0]
    
    for tag_assignatura in tag_assignatures.getElementsByTagName("assignatura"):
        assignatura=tag_assignatura.firstChild.data
        clases[dia].append(assignatura)


file.write("<table border='1'>\n")

file.write("<tr><th></th>")

for dia in dies:
    file.write(f"<th>{dia}</th>")

file.write("</tr>\n")

num_franjes=len(franjes)

for i in range(num_franjes):
    file.write ("<tr>\n")
    file.write (f"\t<td>{franjes[i]}</td>\n")
    for dia in dies:
        assignatura=clases[dia][i]
        file.write(f"\t<td style='background-color: {colors[assignatura]}'>{assignatura}</td>\n") #Aquest color és d'aquesta assignatura 
    file.write("</tr>\n")

file.write("</table>\n")

file.write("</body></html>") 

file.close()

print("Horario disponible en: Horari_final_2.html")

```
També hem après XSLT i XPATH, per a conseguir el mateix objectiu de treure les dades de l'XML i treballar amb aquestes per aconseguir el resultat desitjat, realitzant exercicis com el proposat [en aquest enllaç](https://docs.google.com/document/d/1N-hikCVcUrXkQ3fn056_M45mSgQBVP54A3Ivz0swL5M/edit). Poc a poc hem anat dominant-lo i ara ja podem fer un horari a la tasca de control i tots els exercicis plantejats amb èxit. 

I així hem acabat, de moment, tots els conceptes del primer i segon trimestre de les dues assignatures. Esperem que el tercer trimestre ens doni més llenguatges i maneres d'aconseguir tots els objectius que necessitem assolir als exercicis. 


