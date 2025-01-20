# Case: Protein Pow(d)er
![een fotomontage met vooraan kleurige spiraalvormige dingen, achter links een uitsnede van een pot weipoeder en rechts een stock foto van een stel medewerkers in een laboratorium, met op de voorgrond een persoon met een veiligheidsbril, mondkapje en een flinke pipet](Proteinpowder.jpg){:.inline}

Eiwitten zijn lange strengen van aminozuren die veel belangrijke processen in het menselijk lichaam beregelen. Het is bekend dat eiwitten 'opgevouwen' in de lichaamscellen opgeborgen zitten, en dat de specifieke vouwing bepalend is voor het functioneren; verkeerd gevouwen eiwitten staan aan de basis van onder andere kanker, Alzheimer en taaislijmziekte. Het is daarom van groot belang voor zowel de farmaceutische industrie als de medische wetenschap om iets te kunnen zeggen over de exacte vorm van de vouwing.

Nu is er is het één en ander bekend over het mechanisme: hydrofobe aminozuren (H) willen graag 'naast elkaar' liggen, polaire aminozuren (P) hebben die voorkeur niet. Als twee hydrofobe aminozuren naast elkaar liggen ontstaat er namelijk een 'H-bond' door de aantrekkende kachten tussen de twee. En hoe meer bonds, hoe stabieler het eiwit. Voor de wetenschappers en farmaceuten is het belangrijk om te weten tot welke stabiliteit van het eiwit maximaal gevouwen zou kunnen worden. Het doel is dus de gegeven eiwitten zo op te vouwen, dat ze zo stabiel mogelijk zijn.

![](GoodBadFoldings.jpg)

**Links:** een eiwit van vier polaire en vier hydrofobe aminozuren. **Midden:** een relatief stabiele vouwing met twee H-bonds. **Rechts:** een onstabiele vouwing vanwege het ontbreken van H-bonds.

Om de boel enigzins beheersbaar te houden gaan we uit van een 2D grid waarbij we ieder aminozuur op een gridpunt komt te liggen. Het volgende aminozuur ligt op één van de aangrenzende gridpunten waardoor we eiwitten 'gevouwen' kunnen neerleggen, met hoeken van telkens 90 graden. Als twee H's naast elkaar op het grid liggen krijgt het totale eiwit een -1 op de score. Hoe lager de score, hoe stabieler het eiwit.


## Opdracht
1. Schrijf een algoritme dat het eiwit HHPHHHPH zo goed mogelijk vouwt. Probeer ook te kwantificeren ''hoe goed'' de vouwing is.
2. Vouw de volgende eiwitten zo goed mogelijk. Ze zijn langer, maar zijn ze ook moeilijker?

    * HHPHHHPHPHHHPH

    * HPHPPHHPHPPHPHHPPHPH

    * PPPHHPPHHPPPPPHHHHHHHPPHHPPPPHHPPHPP

    * HHPHPHPHPHHHHPHPPPHPPPHPPPPHPPPHPPPHPHHHHPHPHPHPHH
3. Het aminozuur Cysteine (C) heeft hele sterke bonds. Als twee Cysteine-aminozuren naast elkaar liggen krijgt het eiwit -5 op de score.
Tussen C's en H's is de score -1, en met P's is er geen bindingseffect, dus score nul. Bepaal de beste vouwing.

    * PPCHHPPCHPPPPCHHHHCHHPPHHPPPPHHPPHPP

    * CPPCHPPCHPPCPPHHHHHHCCPCHPPCPCHPPHPC

    * HCPHPCPHPCHCHPHPPPHPPPHPPPPHPCPHPPPHPHHHCCHCHCHCHH

    * HCPHPHPHCHHHHPCCPPHPPPHPPPPCPPPHPPPHPHHHHCHPHPHPHH


## Advanced

{:start="4"}
4. Voeg een dimensie toe. Vouw de eiwitten zo goed mogelijk in 3D.


## Output
Om resultaten te kunnen verifiëren is het handig om in een uniform format je output te genereren.
Bekijk [het voorbeeld](example_output.csv) en zorg ervoor dat jouw programma een oplossing in hetzelfde format kan omzetten.
De 0 bij het laatste aminozuur geeft aan dat er geen buiging gedaan hoeft te worden.
Een vereiste aan de output zijn de header-regel (regel 1) en de footer-regel (regel 11).
Deze moeten in jouw output ook voorkomen, waarbij alleen het getal voor de score zal verschillen.

N.B. Je programma hoeft hier verder niets mee te doen. Het programma hoeft dit enkel als laatste stap in het process te kunnen doen.

#### Opbouw output
Deze output is gebaseerd op het format zoals bedacht door Bas Terwijn:

     "1" betekent een positieve stap in de eerste dimensie (X-as richting).
    "-1" betekent een negatieve stap in de eerste dimensie (X-as richting).
     "2" betekent een positieve stap in de tweede dimensie (Y-as richting).
    "-2" betekent een negatieve stap in de tweede dimensie (Y-as richting).
     "3" betekent een positieve stap in de derde dimensie  (Z-as richting).
     etc..

De stappen kunnen oplopen tot in arbitraire dimensies.
Het antwoord in `example_output.csv` kan als volgt geïnterpreteerd worden:

We beginnen met hey eerste element van de proteïne 'H':

               H

De eerste stap is 1, dus maken we een stap in de positieve X-richting en
plaatsen daar het volgende element 'H':

               H-H

De tweede stap is 2, dus maken we een stap in de positieve Y-richting en
plaatsen daar het volgende element 'P':

                 P
                 |
               H-H

De volgende stap is -1, dus maken we een stap in de negatieve X-richting en
plaatsen daar het volgende element 'H':

               H-P
                 |
               H-H

De overige stappen resulteren in:

             P-H-P
                 |
               H-H


             P
             |
             P-H-P
                 |
               H-H


             P
             |
             P
             |
             P-H-P
                 |
               H-H


             P-P
             |
             P
             |
             P-H-P
                 |
               H-H


             P-P
             | |
             P H
             |
             P-H-P
                 |
               H-H


De score is het aantal paren van 'H' elementen die naast elkaar liggen,
maar niet verbonden zijn binnen de keten. Dit is hieronder aangegeven met de '*'
karakters:

             P-P
             | |
             P H
             | *
             P-H-P
               * |
               H-H

De score van de bovenstaande vouwing van het proteïne is dus: -2.


## Check50
Je kan je programma's testen door de output mee te geven aan de check50. Dit kan in drie eenvoudige stappen:

1. Genereer een antwoord en sla deze met het bovenstaande formaat op in een nieuw bestand met de naam `output.csv`
2. Open een terminal in de folder waar je `output.csv` hebt opgeslagen
3. Run het commando `check50 -l minprog/theorie-check50/master/protein_powder`


## Links & Trivia
De eerste versie van deze case is ontwikkeld door Misha Paauw en Anneliek ter Horst in het kader van Advanced Heuristics, januari 2017.
