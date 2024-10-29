# Power BI & Česko
Vizualizace českých prostorových dat v Power BI. 

Toto repo na příkladu ukazuje, kterak v rámci Power BI snadno a rychle uživatelům ukázat česká prostorová data (hodnoty za okresy či kraje).

<p align="center">
  <img src="https://github.com/jlacko/powerbi-cesko/blob/main/screenshot.png?raw=true" alt="Power BI aplikace v kontextu České republiky"/>
</p>

Vzorovou aplikaci můžete vidět běžet na<br>https://app.powerbi.com/view?r=eyJrIjoiOGJiNzMwZWMtNGRjNS00YWQzLWE4ZTEtOWViMzY3NmNkNzQ5IiwidCI6ImZlOWQ2NzQwLTg5NTctNDc1OS1iNjRjLWM0NTgwYTNlNjQ0MiIsImMiOjl9

<hr>

### Obsahem repozitáře je:
- OD_CRU02_2020051415510736.CSV - soubor s daty o [kapacitě hromadných ubytovávacích zařízeních](https://www.czso.cz/csu/czso/kapacity-hromadnych-ubytovacich-zarizeni) z ČSÚ.<br>Je výhodný v tom, že v jednom datovém souboru obsahuje současně krajská a okresní čísla, ale zde vystupuje čistě jako záminka - repo je o formě, ne o obsahu.
- kraje.json - topojson českých krajů, včetně klíčů (metodou číselníku #100 podle ČSÚ  a číselníku NUTS3 podle Eurostatu)
- okresy.json - topojson českých okresů, včetně klíčů (metodou číselníku #101 podle ČSÚ a číselníku LAU1 podle Eurostatu)
- powerbi-cesko.pbix - vzorový Power BI report s dimenzí okresů a krajů, postavený nad daty v prvním bodu a shapefily v druhém a třetím bodu

Prostorové objekty zohledňují uspořádání Česka po vstupu zákona [51/2020 Sb. o územním členení státu](https://www.zakonyprolidi.cz/cs/2020-51) v platnost.

<hr>

### Při tvorbě vlastního dashboardu:

1) v rámci projektu založte Shape map (preview funkce; vyžaduje povolení v settings a restart Power BI). <br>Návod například zde https://docs.microsoft.com/cs-cz/power-bi/visuals/desktop-shape-map
2) po založení mapy (klidně defaultní lower 48) zvolte v rozbalovacím meníčku Map settings na záložce Format your visual (sloupečky se štětcem; je prostřední) pro Map type poslední volbu Custom, a nahrajte json okresů či krajů
3) ve svém datovém zdroji vyberte pole, které odpovídá klíči (může být ve formátu ČSÚ nebo Eurostat, název je též možný, ale zranitelný; doporučuji použít číselník) a namapujte ho na Location na záložce Fields (dva obdélníčky nalevo vedle válečku). <br>
Je zcela klíčové, aby se klíče potkaly :) To jest abyste ve svém datovém zdroji měli některé z polí, které topojson zná, a na které se dovede připojit - v rámci ukázkové aplikace to řeším technickým polem - KOD_OKRES či KOD_KRAJ - které nabývá relevantní hodnoty podle toho, zda jde o kraje či okresy. Pamatujte na to, aby pole v datech a shapefilu byly stejného typu; ideální je připojovat podle Eurostatových číselníků NUTS3 / LAU1, které vždycky začínají řetězcem CZ a jsou tedy jasný string. U kódů podle českého staťáku je riziko záměny (číslo jako číslo, nebo číslo jako text?) a tak pamatujte, že v "mých" topojsonech jsou vždy klíče jako text. Pokud máte v datech číslo jako číslo tak ho musíte převézt na text, jinak se klíče nepotkají (a mapa zůstane defaultně šedivá).
4) dále vyberte hodnotu datové položky; kategorické proměnné můžete namapovat na Legend, číselné hodnoty na Color saturation
5) můžete, a nemusíte, namapovat další položky na pole Tooltips
6) můžete, a nemusíte dataset propojit s dalšími filtračními poli - v případě ukázkové aplikace je to *Typ hodnoty* (počet hotelů či lůžek?) a *rok platnosti* z podkladového CSV.

### Závěrem:
Repo je pod MIT licencí, tj. máte můj souhlas si se zahrnutými objekty nakládat jak uznáte za potřebné, včetně komerčního využití (s výhradou vydávání je za své a popotahování mě po soudech). 

V případě zájmu, či potřeby hlouběji personalizovaných dat (například vlastní obchodní regiony?) mne kontaktujte.


