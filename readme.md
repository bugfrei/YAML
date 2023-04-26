# PowerShell Support mittels folgenden Modul

- [PSYaml Github Repository](https://github.com/Phil-Factor/PSYaml.git)
- [Craft Yaml CheatSheet](https://www.craft.do/s/izvzZvhMwSQEON)

👉 Installation:

- Repo klonen
- in diesem Repo ist folgender Inhalt:

```
    Directory: /Users/carstenschlegel/temp/yaml/PSYaml

UnixMode   User             Group                 LastWriteTime           Size Name
--------   ----             -----                 -------------           ---- ----
drwxr-xr-x carstenschlegel  staff              26.04.2023 01:36             96 Media
drwxr-xr-x carstenschlegel  staff              26.04.2023 01:36             96 PSDeploy
drwxr-xr-x carstenschlegel  staff              26.04.2023 01:36            256 PSYaml
drwxr-xr-x carstenschlegel  staff              26.04.2023 01:36            224 Tests
-rw-r--r-- carstenschlegel  staff              26.04.2023 01:36           1017 appveyor.yml
-rw-r--r-- carstenschlegel  staff              26.04.2023 01:36          21758 Documentation.md
-rw-r--r-- carstenschlegel  staff              26.04.2023 01:36          24242 Legacy_Documentation.adoc
-rw-r--r-- carstenschlegel  staff              26.04.2023 01:36           1076 LICENSE
-rw-r--r-- carstenschlegel  staff              26.04.2023 01:36           2500 README.md
```

- PSYaml Ordner in Modulpfad kopieren

Hier ist primär nur der `PSYaml` Ordner wichtig. Diesen in den Modulpfad kopieren

`($env:PSModulePath.Replace(":", ";").Split(";"))`

listet alle Modulpfade auf. Hier am besten den nehmen, der den aktuellen Benutzernamen im Pfad beinhaltet.

Am besten mit Hilfe einer Variable den Zielort "merken":
`$d = ($env:PSModulePath.Replace(":", ";").Split(";"))[0]`

Nun kopieren mit

`copy PSYaml $d/PSYaml -Recurse`

- Modul im Profile importieren

`Test-Path $profile`

Liefert diese Zeile `False` nur `$profile` eingeben und die in dem Pfad angegebenen Ordner erstellen.

`New-Item -ItemType Directory -Path ($profile | Split-Path -Parent) -Force`

Nun (oder falls Test-Path `True` zurück gegeben hat) folgende Zeile ausführen:

`"Import-Module -Name PSYaml | Out-Null" >> $profile`

Nun sollte in jeder neuen PowerShell diese Befehle zur Verfügung stehen:

`ConvertFrom-Yaml` und `ConvertTo-Yaml`

# Testen

Laden des Yaml (test.yaml):

`$c = (Get-Content ./test.yaml -Raw)`

Nun befindet sich in der Variable `$c` der Yaml-String

Umwandeln als PS Objekt:

`$o = (ConvertFrom-Yaml $c)`

Nun kann man mit `$o` das ganze Objekt sehen oder mit `.` auf einzelne Elemente zugreifen:

`$o.anArray[1]`
`$o.aComplexObject.users[2].id`

## Umwandeln in JSON

`$j = (ConvertTo-JSon $o -Depth 10)`

## Umwandeln in Yaml

`$y = (ConvertTo-Yaml $o -Depth 10)`

Der Parameter `NestingLevel` kann den erzeugten Yaml-String gleich um die angegebene Zahl von Stufen einrücken.

```
$yy = "alles:`n$(ConvertTo-Yaml $o -NestingLevel 1)"
$oo = (ConvertFrom-Yaml $yy)
```

Zeile 1: Erstellt ein neues Yaml mit einer Property `alles` in dem die vorherien Properties eingenestet sind.
Zeile 2: Wandelt diesen als neues Objekt um

`$oo.alles` zeigt nun das an, was in `$o` enthalten war. In eine eigene Property `alles` "verpackt".

