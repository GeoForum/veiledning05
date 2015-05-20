# Kartprojeksjoner og koordinater: Hvorfor ligger dataene mine feil i kartet?


Når man jobber med kart blir man raskt klar over at stedfestede data ikke kommer i ett format eller i en form. Er man ikke nøyaktig med dataene kan punktet, linja eller flaten du jobber med havne på et helt annet sted i kartet enn det som var tiltenkt. Å bruke norske data som er tilpasset til bruk i norske kart kan by på utfordringer i implementasjoner med APIer med et globalt fokus. De beste kartdataene for Norge kan du laste ned gratis fra Kartverket, og for å kunne bruke disse må projeksjonen som kartet ditt bruker matche dataene. Hvorfor er det slik? Og hva kan du gjøre for at dine geometrier havner på rett plass? Denne artikkelen tar for seg utfordringer utviklere ofte møter i kartapplikasjoner, hvordan man behandler data i ulike projeksjoner, og hvordan du kan løse de.

## Hvorfor har vi så mange kartprojeksjoner?

Jordas form er en sammentrykt kule og kan sammenlignes med formen til en appelsin. For å lage et kart i to dimensjoner av denne tredimensjonale figuren må vi "skrelle" appelsinen og strekke den flat. Denne strekkingen forvrenger appelsinskallet og kartet det representerer. Kartprojeksjoner handler om hvordan vi velger å strekke kartet, og hvilke egenskaper vi ønsker å beholde fra den opprinnelige formen. Noen kart har korrekte vinkler og egner seg til bruk i navigasjon, mens andre er slik at arealet bevares. Visste du at Afrika er fjorten ganger større enn Grønland? Den mest vanlige projeksjonen "Mercator"  bevarer ikke areal og forvrenger kartet slik at Grønland ser ut til å ha samme størrelse som Afrika. I denne projeksjonen forvrenges kartet mer jo lengre fra ekvator man kommer. Siden Norge ligger ganske langt nord vil det få en ganske stor forvrenging i denne projeksjonen. For å få bukt på dette problemet finnes det projeksjoner som forvrenger lite i et bestemte områder. Norske kart blir derfor ofte lagret i en projeksjon som forvrenger kartet lite i Norge. Norges offisielle projeksjon heter "Universal Transversal Mercator" (UTM) og finnes i flere soner tilpasset ulike deler av landet. UTM sone 32 anbefales brukt for Sør-Norge til og med Nord-Trøndelag, sone 33 brukes i Nordland og Troms, mens sone 35 brukes for Finnmark. Kartverkets nasjonale datasett gis ut i UTM sone 33 da dette er en god middelvei for hele landet.

## Slik bruker APIene projeksjoner

Kartbiblioteker som Leaflet, OpenLayers, ArcGIS for JavaScript og Google Maps API bruker "Web Mercator" som standard kartprojeksjon. Kartprojeksjonene eller koordinatsystemet som disse APIene bruker blir spesifisert med en unik kode som kalles SRID (Spatial Reference Identifier) som oftest er en standardisert kode fra EPSG (European Petroleum Survey Group). Web Mercator identifiseres med "EPSG:3857", men kan også finnes som "900913" (Google stavet med tall!) eller "ESRI:102113". Enda mer forvirrende er det at disse bibliotekene ofte bruker "EPSG:4326", som svarer til WGS84, som formen de vil ha input på til geometri. Dette kjenner vi som lengde- og breddegrad, eller latitude/longitude. Bibliotekene tar da disse geografiske koordinatene (lengde- og breddegrad) og reprojeserer de til "Web Mercator" som kartet tegnes i. Dataene fra kartverket har også slike koder og representeres av henholdsvis 25832, 25833 og 25835 for UTM sone 32, 33 og 35. 

## Hvordan bruker vi data og kart med forskjellige projeksjoner sammen?

Men hvordan skal vi bruke data i en annen kartprojeksjon sammen med kartbiblioteker som bruker "Web Mercator"? Da har vi to muligheter:

1.  Reprojesere bakgrunnskartet brukt av biblioteket til å matche dataene.
2.  Reprojesere dataene til "Web Mercator".

Skrevet for http://www.geoforum.no/om-geforum/prosjekt-innovasjon/

**ARTIKKELEN ER UNDER UTARBEIDELSE**
