# Git

[Heb je deze pagina al gelezen, maar wil je snel even kijken welke git commandos er ook alweer allemaal waren? Gebruik dan de Git cheatsheet!](https://education.github.com/git-cheat-sheet-education.pdf)

Git is een systeem om de broncode van softwareprojecten te beheren. Er zijn twee belangrijke redenen om zo'n speciaal systeem te gebruiken:

- Tijdens de ontwikkeling van een applicatie maak je steeds wijzigingen, soms gooi je zelfs grote delen weg of schrijf je weer een heel stuk. Je wil misschien wat dingen helemaal omgooien, maar niet alles kwijtraken als het mislukt. Een beheerssysteem kan steeds weer versies opslaan die je makkelijk kunt terughalen.

- Bijna alle software wordt in samenwerking met anderen geschreven. Dat betekent niet dat iedereen samen achter één computer zit, maar wel dat er veel afgestemd moet worden en ook dat mensen van verschillende computers kunnen bijdragen aan het geheel.

Git faciliteert deze behoeftes door elke ontwikkelaar de mogelijkheid te geven versies van bestanden te markeren (of versies van complete *sets* bestanden) en deze versies met andere ontwikkelaars te delen. In de meeste gevallen is er sprake van één centrale opslagplaats (*repository*) waar iedereen versies heen kan versturen (in Git termen *pushen*).

GitHub is een service die Git repositories host op het internet. Deze service is gratis en kan gebruikt worden door jouw groep zodat je één centrale plek hebt, die altijd beschikbaar is, waarop al jullie code staat.

## Git klaarzetten

Om Git te kunnen gebruiken op je computer, zijn er een aantal commando's op de command line die je zal moeten leren gebruiken. We beginnen met het opzetten van één repository voor jullie hele groep. Deze koppelen we dan aan ieder van de computers van de groepsleden.

> Git werkt niet hetzelfde als Dropbox! Het houdt je bestanden niet automatisch up-to-date. Dit is precies wat we willen, want we willen natuurlijk geen kapotte code of code die niet af is naar onze groepsleden sturen.

1. Ieder groepslid begint door een account aan te maken op [GitHub](https://github.com/). Als je deze al hebt, gebruik die dan.

2. Na het inloggen, gebruikt **één** van de groepsleden de [New repository](https://github.com/new)-knop om een nieuwe repository voor de gehele groep aan te maken. Bedenk een leuke naam voor jullie groep, die je dan ook direct kan gebruiken als naam voor jullie repository. Selecteer hier `Public`, zodat we later bij het nakijken direct toegang hebben tot jullie code. Klik ook op de vinkjes voor "Add a README file" en "Add .gitignore". Selecteer Python voor je `.gitignore`-template. Dit zorgt ervoor dat er geen onnodige files worden opgeslagen in je repository. Klik daarna op "Create repository" om het process af te ronden.

    * Werkt tenminste één van jullie met MacOS? Voeg dan direct handmatig de regel `.DS_Store` toe aan de `.gitignore`!

3. Zodra de groeps-repository aangemaakt is, klik op "Settings -> Manage access". Hier kan de eigenaar van de repository (degene die het aangemaakt heeft) instellen wie er toegang heeft om veranderingen te mogen maken aan de repository met de knop "Invite a collaborator". Voeg alle andere groepsleden toe d.m.v. hun gebruikersnaam.

4. Ieder groepslid kan nu een terminal openen en navigeren naar de folder waar ze hun project willen opslaan. Op de hoofdpagina van jullie repository staat een knop waar "Code" op staat. Als je hier op drukt staan er onder het woord "Clone" drie tabjes, druk op "SSH". Nu komt er als het goed is een link tevoorschijn die lijkt op: `git@github.com:<gebruikersnaam>/<teamnaam>.git`. Kopieer deze link en gebruik het volgende commando, waar je `<link>` vervangt door de link die je zojuist gekopieerd hebt:

    `git clone <link>`

Hiermee zou de git repository naar de computer gedownload moeten worden. De repository kan nu worden gebruikt alsof het een folder is op je computer.

> **LET OP: Als je op enig moment niet zeker weet hoe je verder moet, terug wilt naar een eerdere versie van je code, of andere problemen hebt met Git, neem dan contact op met een van de ervaren TAs of docenten van dit vak. Het gebruik van commandos die je vindt op Stackoverflow of Google kunnen onherstelbare effecten hebben, en resulteren in een hoop verloren werk.**

## SSH instellen

Voor de meeste acties die interactie vereisen met de GitHub servers is het nodig om jezelf via de terminal te identificeren. GitHub staat sinds 13 augustus 2021 niet meer toe dat je dit doet middels je gebruikersnaam en wachtwoord. Om dit toch mogelijk te maken is het nodig om een SSH key aan te maken, en deze bij GitHub te registreren.

> SSH (Secure Shell) is een protocol dat wordt gebruikt voor het veilig communiceren over een netwerk.

1. Voer om een SSH key aan te maken in een terminal het volgende commando uit: `ssh-keygen`. Wanneer je een prompt krijgt om de key ergens op te slaan, druk op Enter. Hiermee sla je de key op op de standaard locatie.
2. Je wordt nu gevraagd of je de een wachtwoord wilt invullen voor het gebruik van je SSH key. Druk ook hier gewoon op Enter. Je krijgt nu als het goed is een "randomart" plaatje wat je kunt negeren.
3. Voer nu het volgende uit in een terminal: `cat ~/.ssh/id_rsa.pub`. Dit laat je "openbare sleutel" op het scherm zien; een reeks regels met willekeurige karakters. Selecteer deze regels, en kopieer ze. Let er op dat je de prompts van je terminal (met $) niet mee kopieert!
4. Ga naar https://github.com/settings/keys en log in met je GitHub gegevens.
5. Klik op "New SSH Key" en plak je public SSH key in het tekstvak onder "Key". Eventueel kan je ook een titel invoeren, zoals "Minor". Klik daarna op "Add SSH Key".
6. Voer in de terminal het volgende uit: `ssh -T git@ssh.github.com -p 443`. Je wordt nu gevraagd of je verbinding wilt maken met Git, waarop je "yes" intypt en op Enter drukt. Als het goed is zie je nu: `Hi <USERNAME>! You've successfully authenticated, but GitHub does not provide shell access.`

Je zou nu gebruik moeten kunnen maken van Git zonder dat je iedere keer je gebruikersnaam en wachtwoord hoeft in te vullen!

## Git gebruiken

Het gebruik van Git zou nu vrij simpel moeten zijn! Iedere keer dat je iets wilt doen in de Git repository, navigeer je naar de folder in de terminal. Er zijn 5 commando's die je moet kennen:

- **`git pull`:** Dit commando haalt de huidige versie van de repository van GitHub *en zou daarom altijd het eerste commando moeten zijn wat je uitvoert als je begint met werken!* Let op: als je lokaal al veranderingen hebt gemaakt, werkt dit commando niet tot je `git commit` hebt gebruikt om je lokale veranderingen op te slaan.
- **`git add <filepath>`:** Dit commando voegt de bestanden in `filepath` toe aan de bestanden waar Git op let. Bijvoorbeeld: als je lokaal een folder hebt aangemaakt die `coole_dingen` heet, met een bestand daarin dat `lees_data.py` heet, zou je dat kunnen toevoegen aan git door het commando `git add /coole_dingen/read_data.py` uit te voeren. Het is ook mogelijk om `git add .` uit te voegen om _alle ongeregistreerde files in de huidige folder_ toe te voegen aan de repository. Als een file eenmaal toegevoegd is aan de Git, hoef je dat daarna nooit meer te doen.
- **`git commit -am "<some message>"`:** Dit commando slaat alle veranderingen aan de geregistreerde files en folders in je Git repository _lokaal_ op met een bericht erbij. Het kan misschien veel werk lijken, maar gebruik een bericht dat duidelijk uitlegt wat je gedaan hebt. Dat maakt het een stuk makkelijker om oude versies van specifieke stukken code terug te vinden.
- **`git push`:** Dit commando "duwt" alle `commits` die je lokaal gemaakt hebt naar de GitHub server. Totdat je dit gedaan hebt staat dus niets wat je lokaal hebt opgeslagen op GitHub. Als de repository tussentijds veranderd is, zal je eerst `git pull` moeten uitvoeren om de veranderingen te "mergen" met de veranderingen die je lokaal gemaakt hebt.
- **`git status`:** Dit commando laat je een lijst van alle files en folder zien die je hebt aangepast, welke files je wel hebt ge-`commit` maar niet hebt ge-`push`t, en welke files nog niet geregistreerd zijn. Ongeregistreerde files zijn files die lokaal wel bestaan, maar nog niet zijn ge-`add` naar de Git repository.

En dat is het! Als je lokale veranderingen naar de online Git repository wilt sturen zou je altijd het volgende doen:

1. `add` alle files die je wilt opslaan in de git repository,
2. `commit` je aanpassingen met een gepast bericht,
3. `pull` aanpassingen die andere gemaakt hebben van GitHub af,
4. `push` jouw aanpassingen naar GitHub.

Als je niet zeker weet hoe het op enig moment staat, kan je altijd `git status` gebruiken om te kijken welke files je nog moet toevoegen, of welke veranderingen nog niet opgeslagen zijn.

## Mergen

Wanneer je samenwerkt met anderen is het altijd mogelijk dat iemand in dezelfde file als jij heeft gewerkt, maar eerder hun veranderingen naar de repository heeft ge-`push`t dan jij. Git zal dan proberen om de aanpassingen met elkaar te _mergen_ wanneer je `git pull` gebruikt. Git is normaal best wel goed hierin, maar voor sommige filetypes, of wanneer jullie beiden iets aangepast hebben op dezelfde regels in een file, weet Git niet goed wat er moet gebeuren. Git zal dan een _merge conflict_ maken. Deze conflicten gebeuren alleen op de computer van de persoon die `git pull` heeft gebruikt. Andere mensen die aan hetzelfde project werken zullen hier niets van merken.

Je kunt de conflicten niet onopgelost laten. Git wil dat je de conflicten oplost voordat je je aanpassingen daadwerkelijk kan opsturen naar GitHub. Git zal altijd laten weten wanneer een conflict plaatsvind, en geeft daarbij ook aan in welke files dit zo was. Als je dit gemist hebt, of als je meer informatie wilt, kun je altijd `git status` uitvoeren.

Als je een van de files met een merge conflict opent in een editor zal je zien dat tenminste één keer, maar soms ook meerdere keren, de volgende regels voorkomen:

    <<<<<<< HEAD
    *Jouw variant van de code*
    ======
    *De variant van de code die nu online staat*
    >>>>>>> *een boel getallen en letters*

Ieder stuk van de code dat tussen de "kleiner dan" en "gelijk aan"-tekens staat is code die je lokaal hebt staan. Alle code die tussen de "gelijk aan" en "groter dan"-tekens staat is code die van de online versie van de file komt. Na de laatste "groter dan"-tekens staat een reeks getallen en letters. Dit is een ID voor de online versie, en kan gebruikt worden om exact te vinden waar de code vandaan komt.

Om het merge conflict op te lossen verwijder je de variant van de code die je niet nodig hebt, en alle extra regels die het conflict aangeven (regels met `<`, `=`, en `>`). Sla de file op, en gebruik `git commit` om je veranderingen op te slaan. Nu kan je `git push` gebruiken om je aanpassingen ook online te zetten.

## Oefenen met Git

Om nu even te oefenen met de workflow van Git, kan je een korte interactieve cursus [online](https://learngitbranching.js.org/) doen. Dit is niet noodzakelijk, maar geeft je mogelijk wat meer zelfvertrouwen in het gebruik van Git. Ook is er een handige korte referentie: [Simple Guide to Git](http://rogerdudler.github.io/git-guide/).
