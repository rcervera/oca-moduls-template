
# ACTIVITAT SÍNTESI UF2

## Implementar el joc de l'Oca


### Les normes del joc 

Tots els jugadors comencen situats a l'inici del laberint, situats vora la casella 1, i llencen per torns 2 daus. Avancen pel laberint tantes caselles com la suma de punts dels daus. Per exemple, al començar el joc un jugador llença els daus, i la suma dels 2 daus és 6, és col·loca a la casella número 6.

El jugador que comença el joc és l’1, i es va jugant a torns de forma seqüencial.

Hi ha caselles especials dins del tauler, que poden fer retrocedir, avançar fent salts i també perdre torns.

Normes:

   - Si cau en una casella “normal”: s'hi queda fins al següent torn

  -  Si cau en una casella “oca”: es busca la següent oca al tauler i s'hi col·loca. El jugador torna a llençar els daus.

   - Si cau en una casella “pou”: s'hi queda un número aleatori de torns perduts

  -  Si cau en una casella “la mort”: es torna a la casella inicial

- La darrera casella és sempre de tipus “oca”.


### El laberint 

El laberint el podem representar en format lineal:
![laberint oca](https://github.com/rcervera/oca-moduls-template/blob/main/recursos/laberint-oca.png "Laberint Oca")



Per emmagatzemar el laberint farem servir un array unidimensional:
```Java
String[] laberint = new String[63];
```

### Els jugadors 

Per desar la informació dels jugadors farem servir un array bidimensional:
```Java
int[][] jugadors = new int[4][2];

``` 
- Cada fila desa les dades d’un dels jugadors.
-  La primera columna de cada fila indica en quina casella està col·locat el jugador. 
- La segona columna indica quants torns estarà un jugador sense poder tirar els daus (degut a que ha caigut dins una casella “pou”).

![jugadors](https://github.com/rcervera/oca-moduls-template/blob/main/recursos/jugadors.png "Jugadors")

### L'Algorisme del joc 

L'algorisme del programa el podem escriure en pseucodi de la següent manera. 



  >Inicialitzar caselles laberint (posem oques, ponts, morts, .....)
  >
  >Mostrar el laberint
  >
  >inicialitzem jugador actual (comença el jugador 1)
  >
  >>**mentre** un jugador no arriba exactament a la darrera oca **fer**
  >>
  >>>Mostrar informacions dels jugadors (on estan i quants torns perduts tenen tots els jugadors)
  >>>
  >>>**si** el jugador actual té torns perduts **llavors**
  >>>
  >>>>  restem un als número de torns perduts
  >>>
  >>>**sino**
  >>>>  Llençar 2 daus
  >>>>
  >>>>  Moure fitxa del jugador actual
  >>>>  Acció al caure dins una casella per al jugador actual (segons on hem caigut mostrem missatge, canviem posició o actualitzem torns perduts)
  >>>>
  >>>>**si**  jugador  actual no ha caigut en una oca **llavors**
  >>>>
  >>>>>canviem el torn
  >>>>
  >>>>**fsi**
  >>>
  >>>**fsi**
  >>
 >>**fmentre**


### Mètodes a implementar

Mètodes que s'han d'implementar i fer el test JUNIT corresponent:

#### 1. Mètode “Llençar 2 daus”
Aquest mètode retorna quantes caselles ha d’avançar el jugador que té el torn. Simula el llançament simultani de 2 daus i quan es crida s’ha de quedar aturat fins que l’usuari prem la tecla retorn (només cal posar una instrucció teclat.netxLine())

Per implementar aquest mètode haureu de tenir implementat un altre mètode tirarUnDau() que retorna un número de l’1 al 6.

Exemple d’execució:
```
Pulsa intro per tirar els daus

RESULTAT DAUS: 4+1 = 5
```

#### 2. Mètode per “Inicialitzar caselles laberint”:
Aquest mètode ens servirà per configurar on estan situades els diferents tipus de caselles.

Dins d’aquest mètode hi haurà declarats 3 arrays d’enters. El primer guardarà les posicions on hi haurà “Oques”. Heu de tenir en compte que sempre a la posició 63 hi haurà una oca. El segon desarà les caselles de tipus “La mort”. El tercer i darrer guardarà les posicions on hi haurà “Pous”. El contingut de cada array pot canviar i el codi del programa ha de funcionar sense fer-ne cap més modificació.

![arrays inicials](https://github.com/rcervera/oca-moduls-template/blob/main/recursos/arrays-inicials.png "arrays inicials")

La resta de caselles que no estan dins de cap dels 3 arrays del laberint contindran la paraula “NORMAL”.

El laberint després de la crida a aquests mètodes tindrà la paraula “OCA” en cada una de les posicions que marca l’array d’oques. La paraula serà «MORT» i «POU» per als 2 arrays de morts i pous respectivament.

Si es repeteix un mateix conjunt d'instruccions dins d'aquest mètode penseu en implementar un mètode extra per evitar-ho!



#### 3. Mètode per “Mostrar el laberint”: 
mostra per pantalla el contingut de l’array laberint en el format del següent exemple

![laberint mode text](https://github.com/rcervera/oca-moduls-template/blob/main/recursos/laberint-mode-text.png "Laberint mode text")


####  4. Mètode per “Mostrar informacions dels jugadors”:  
Mostra per pantalla a partir de l’array de jugador les dades que conté segons el següent format:
```
Jugador 1: està a casella 15 i no té torns perduts.

Jugador 2: està a casella 29 i estarà 2 torns sense jugar.

Jugador 3: està a casella 25 i no té torns perduts.

Jugador 4: està a casella 12 i no té torns perduts.

Va guanyat el jugador 2!
```

Per calcular quin és el jugador que va guanyat heu d’implementar un altre mètode que retorni el número de jugador que està més avançat dins el laberint



####  5. Mètode “on està la següent Oca”: 
Mètode al que se li passa una posició del laberint (normalment, una posició on hi ha una oca) i el laberint , i retorna la posició on hi ha la següent Oca dins del laberint.    

Per exemple, i segons la configuració de l'exemple anterior, el mètode retornarà 32 si li passo per paràmetre la posició 27.


####  6. Mètode “Acció al caure dins una casella”:
 Aquest mètode ens servirà per saber que haurem de fer quan un usuari cau dins una casella determinada. Se li passa per paràmetre el jugador actual (el que té el torn) . Es necessita la matriu jugadors per saber on està situat actualment el jugador actual i el laberint, per saber el contingut de la posició.

Aquest mètode retorna true si el jugador està dins una oca i false en cas contrari. Aquest mètode modifica també la matriu Jugadors. A més mostra per pantalla un text explicatiu de la casella.

| Tipus         | Missatge                                     | Acció                                                                                                |
| ------------- | ------------------------------------------------------------ |--------------------------------------------------------------------------------------|
| OCA           |D'Oca a Oca i llenço daus perquè em pertoca!  |  El jugador anirà a parar a la casella on hi hagi la següent oca. Retorna true                       |
| POU           | Al pou he caigut i si no ve un bomber, 2 torns m'hi quedaré  | Assigna 2 torns perduts al jugador actual. Retorna false |
| MORT          | Si toques la calavera, l'u t'espera. | El jugador anirà a parar a la casella 1. Retorna false
| NORMAL        | He caigut a una casella normal, no m'espera cap mal |  Cap. Retorna false |
   


####  7. Mètode «Moure fitxa del jugador actual» : 
Aquest mètode col·loca la fitxa del jugador actual a la casella següent segons el valors dels daus (serà un dels paràmetres) . Actualitzarà la posició on es troba el jugador actual. Per exemple, si el jugador actual està a la casella 10 i el valor dels daus és 7, s’actualitza a 17 el valor de la posició del jugador actual. Ara bé, hem de tenir en compte, que si es sobrepassa la darrera posició del laberint, la nova posició serà tantes caselles endarrere com el valor sobrepassat del laberint!

Exemple: estic a la casella 60, els daus sumen 5. La fitxa avança per les caselles: 61, 62, 63..i es torna endarrere 62, 61. La nova posició és la 61.


####  8. Mètode main:  

En el mètode main del programa crida als mètodes implementats per a que es pugui jugar una partideta....








