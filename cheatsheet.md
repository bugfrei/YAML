# YAML

YAML ist ähnlich wie JSON eine „Data serialization language“.

Sie verwendet keine Klammern sondern Whitespaces und ein paar Sonderzeichen um die Struktur festzulegen:

`:` : Definiert eine Property, gefolgt von Number,Boolean,String,Array oder Object

`-` : Definiert ein Item innerhalb eines Arrays. Kann auch weg gelassen werden falls dieses Item nur

   einen einzelnen Wert darstellt (und kein Object)

# Einfache Properties verschiedener Datentypen

## String

JSON: `"aString1": "Weil es mit Buchstaben anfängt“,` YAML:

- `aString1: Weil es mit Buchstaben anfängt`
- `aString2: "In Anführungszeichen ist es besser!“`

`“` oder `’` sind möglich.

## Einzeiligen langen String

JSON: NICHT MÖGLICH

YAML:

```bash
aString3: >
  Als eine einzige Zeile.
  Auch wenn es hier mehrere Zeilen sind.
  Das > steht für: in eine Zeile.
```

## Mehrzeiligen String

JSON:

- `"aString4": "Mehrere Zeilen.\nInklusive Zeilenumbrüche.\nDas Pipe-Zeichen steht für: Zeilenweise Strings\n“,`
- `"aString4": "Mehrere Zeilen.
Inklusive Zeilenumbrüche.
Das Pipe-Zeichen steht für: Zeilenweise Strings“,`

YAML:

```bash
aString4: |
  Mehrere Zeilen.
  Inklusive Zeilenumbrüche.
  Das Pipe-Zeichen steht für: Zeilenweise Strings
```

# Zahl

JSON: `"aNumber": 12345,`

YAML: `aNumber: 12345`

## Properties mit Variable und deren Verwendung

JSON: NICHT MÖGLICH

YAML:

```bash
aNumberWithVariable: &var 55555
aNumberUseVar: *var
```

## Boolean

JSON:

- `"aBoolean1": false,`
- `“aBoolean2": true,`

YAML:

- `aBoolean1: false`
- `aBoolean2: true`

# Arrays

Können in `[ ]`  geschrieben werden (wie in JSON), Zeilenweise eingerückt mit oder ohne `-`

JSON:

```bash
"anArray1": [             "anArray2": [
  1,                        "Max",
  2,                        "Moritz",
  3                        "Hans"
],                        ]
```

YAML:

- `anArray1: [ 1, 2, 3 ]`
```bash
anArray1:
  1
  2
  3
```

```bash
anArray1:
  - 1
  - 2
  - 3
```

- `anArray2: [ "Max“, "Moritz“, "Hans“ ]`
```bash
anArray2:
  "Max"
  "Moritz"
  "Hans"
```

```bash
anArray:
  - "Max"
  - "Moritz"
  - "Hans"
```

# Objekt

Auch hier kann die JSON Variante genutzt werden oder Angaben mehrere Properties in je einer eingerückten Zeile.

JSON:

```bash
"anObject1": {
  "firstName": "Max",
  "lastName": "Mustermann"
},
```

YAML:

- `anObject1: { firstName: "Max“, lastName: "Mustermann“ }`
```bash
anObject1:
  firstName: "Max"
  lastName: "Mustermann"
```

```bash
anObject1:
  - firstName: "Max"
  - lastName: "Mustermann"
```

# Ein Array von Objekten

JSON:

```bash
"anArrayOfObjects": [
  {
    "firstName": "Max",
    "lastName": "Mustermann"
  },
  {
    "firstName": "Moritz",
    "lastName": "Zwei"
  },
  {
    "firstName": "Hans",
    "lastName": "Drei"
  }
],
```

YAML:

```bash
anArrayOfObjects:
  - firstName: "Max"
    lastName: "Mustermann"
  - firstName: "Moritz"
    lastName: "Zwei"
  - firstName: "Hans"
    lastName: "Drei"
```

# Komplexes Objekt

Mit einem Array aus

- Objekt mit einer Property mit Arrays von Objekten [ { [ {} ] } ]
- Objekt mit einer Property mit Array von Zahlen [ { [] } ]
- Drei Properties mit einem String, Number und Boolean als Wert

JSON:

```bash
"aComplexObject": [
  {
    "users": [
      {
        "name": "Max Mustermann",
        "email": "mm@user.de",
        "id": 815,
        "active": true
      },
      {
        "name": "Moritz Zwei",
        "email": "hz@user.de",
        "id": 4711
      },
      {
        "name": "Hans Drei",
        "email": "hd@user.de",
        "id": 1234
      }
    ]
  },
  {
    "ids": [
      815,
      4711,
      1234
    ]
  },
  {
    "mainuser": "Max Mustermann"
  },
  {
    "defaultid": 815
  },
  {
    "checked": true
  }
],
```

YAML:

```bash
aComplexObject:
  - users:
    - name: "Max Mustermann"
      email: "mm@user.de"
      id: 815
      active: true
    - name: "Moritz Zwei"
      email: "hz@user.de"
      id: 4711
    - name: "Hans Drei"
      email: "hd@user.de"
      id: 1234
  - ids:
    - 815
    - 4711
    - 1234
  - mainuser: "Max Mustermann"
  - defaultid: 815
  - checked: true
```


