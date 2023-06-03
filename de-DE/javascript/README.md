# JavaScript Best Practices und Design Patterns

- [JavaScript Best Practices und Design Patterns](#javascript-best-practices-und-design-patterns)
  - [Allgemein](#allgemein)
  - [Optionaler Operator ?. / Optional Chaining verwenden](#optionaler-operator---optional-chaining-verwenden)
  - [Auf null und undefined prüfen](#auf-null-und-undefined-prüfen)
  - [Object destructuring / Object Eigenschaften bekommen](#object-destructuring--object-eigenschaften-bekommen)
  - [Verwendung von async und await](#verwendung-von-async-und-await)
  - [Guard Pattern](#guard-pattern)
  - [Positiv formulierte If-Bedingungen und Auslagerung komplexer Bedingungen](#positiv-formulierte-if-bedingungen-und-auslagerung-komplexer-bedingungen)
  - [Begrenzte Zeilenanzahl in Methoden/Funktionen](#begrenzte-zeilenanzahl-in-methodenfunktionen)
  - [Verwendung von `Optional` in JavaScript-Funktionen](#verwendung-von-optional-in-javascript-funktionen)
  - [Verwendung der npm-Bibliothek optional.js zur Rückgabe von Optional in JavaScript](#verwendung-der-npm-bibliothek-optionaljs-zur-rückgabe-von-optional-in-javascript)
  - [If-Bedingungen ohne Else und mit Return](#if-bedingungen-ohne-else-und-mit-return)
  - [Exceptions in JavaScript nicht einfach loggen und unverändert wieder werfen](#exceptions-in-javascript-nicht-einfach-loggen-und-unverändert-wieder-werfen)
  - [Verwendung von `const` für alle Variablen in JavaScript und Kennzeichnung von Nicht-Konstanten](#verwendung-von-const-für-alle-variablen-in-javascript-und-kennzeichnung-von-nicht-konstanten)
  - [Methoden/Funktionen sollten niemals null zurückgeben, sondern immer eine leere Liste, HashMap oder Array](#methodenfunktionen-sollten-niemals-null-zurückgeben-sondern-immer-eine-leere-liste-hashmap-oder-array)
  - [Benennung von Methoden mit verschiedenen Präfixen für Synchronität und Ergebnisverhalten](#benennung-von-methoden-mit-verschiedenen-präfixen-für-synchronität-und-ergebnisverhalten)
  - [Kurz-Übersicht weiterer Themen zur Ausgestaltung](#kurz-übersicht-weiterer-themen-zur-ausgestaltung)

<!-- /TOC -->

## Allgemein

1. **Folgen des KISS-Prinzips (Keep it simple and stupid)**: Die Entwicklung von Software sollte nicht der Selbstverwirklichung des Entwicklers dienen, sondern der Lösung eines Problems. Daher sollte Architektur, Code und Dokumentation so einfach wie möglich gehalten werden. Komplexe Lösungen sollten vermieden werden, wenn einfachere Lösungen möglich sind.

2. **Folgen des DRY-Prinzips (Don't Repeat Yourself)**: Wird festgestellt, dass derselbe Code an mehreren Stellen verwendet wird, sollte in Betracht gezogen werden, diesen Code in eine Funktion oder ein Modul zu extrahieren und es dann jedes Mal zu verwenden, wenn es benötigt wird.

3. **Konsistente Benennung von Variablen und Funktionen**: Es sollte sichergestellt werden, dass die verwendeten Namen aussagekräftig sind und den Zweck des Codes genau beschreiben. Die Benennung sollte auch konsistent sein.

4. **Anwendung von ES6 Features**: Mit ES6 stehen viele neue Möglichkeiten zur Verfügung, um den Code zu verbessern. Beispielsweise könnten Pfeilfunktionen, Template-Strings, Default-Parameter, Rest- und Spread-Operator, Destructuring-Zuweisungen, `const` und `let` anstelle von `var` für eine bessere Kontrolle des Scopings, Klassen, Module, Promises und Iteratoren verwendet werden, um den Code kürzer und leichter lesbar zu machen.

5. **Vermeidung von Callback-Hölle**: Verschachtelte Callbacks sollten vermieden werden, da sie den Code schwer lesbar und wartbar machen. Promises oder `async/await` können verwendet werden, um den asynchronen Code besser handhaben zu können.

6. **Einsatz von Linter und Formatter**: Tools wie ESLint und Prettier können dabei helfen, den Code konsistent und fehlerfrei zu halten.

7. **Schreiben von Unit-Tests**: Guter refaktorierter Code sollte immer von Tests begleitet werden. Sie helfen dabei, sicherzustellen, dass der Code nach dem Refactoring immer noch wie erwartet funktioniert.

8. **Anwendung Modulare Architektur**: Der Code sollte in kleinere, wiederverwendbare Module aufgeteilt werden. Dies erhöht die Lesbarkeit und erleichtert die Wartung und das Testen.

9.  **Selbsterklärender Code**: Kommentare sollten vermieden werden, wo der Code selbst klar sein kann. Guter Code sollte größtenteils selbsterklärend sein.

10. **Anwendung des SOLID-Prinzips**: SOLID ist ein Akronym für fünf Prinzipien des objektorientierten Designs und der Programmierung, die dazu beitragen, dass der Code sauber, robust und wartbar bleibt.

11. **Performance-Optimierungen**: Auf teure Operationen wie unnötige DOM-Manipulationen oder ineffiziente Schleifen sollte geachtet werden. Performance-Tools wie die Chrome DevTools können genutzt werden, um Flaschenhälse zu identifizieren und zu beheben.

12. **Anwendung Funktionale Programmierkonzepte**: Funktionale Programmierung kann dazu beitragen, dass der Code besser strukturiert und leichter zu testen ist. Konzepte wie Unveränderlichkeit (Immutability), reine Funktionen und höherwertige Funktionen (Higher Order Functions) sind besonders nützlich.

13. **Fehlerbehandlung**: Es sollte sichergestellt werden, dass der Code ordnungsgemäß mit Fehlern umgeht. Dies könnte beinhalten, dass versucht wird, Fehler frühzeitig zu werfen, anstatt sie zu ignorieren, und dass `try/catch`-Blöcke verwendet werden, um Fehler effektiv zu behandeln.

## Optionaler Operator ?. / Optional Chaining verwenden

Der optionale Operator `?.` oder Optional Chaining ermöglicht den Zugriff auf Unterschlüssel, ohne explizit auf `null` oder `undefined` prüfen zu müssen.

> Alternativ kann auch das [Optional-Klassen-Pattern](#verwendung-von-optional-in-javascript-funktionen) verwendet werden.

### Problem

In JavaScript besteht oft die Notwendigkeit, auf verschachtelte Schlüssel in Objekten oder Arrays zuzugreifen. Dabei kann es vorkommen, dass einige der Zwischenschlüssel nicht existieren oder dass Methoden undefiniert sein können. In solchen Fällen wird häufig eine Reihe von `if`-Bedingungen verwendet, um sicherzustellen, dass jeder Schlüssel existiert, bevor auf ihn zugegriffen wird. Dieser Ansatz führt jedoch zu redundantem Code und macht den Code schwerer lesbar und fehleranfällig.

```javascript
// Pfad zur Methode könnte nicht existieren
if (myObject && myObject.myKey) {
    myObject.myKey.myMethod();
}

// Falls eine Methode undefiniert sein könnte
if (myObject && myObject.myKey && myObject.myKey.myMethod) {
    myObject.myKey.myMethod();
}

// Prüfung, ob a,b,e und e[0] sowie f nicht null oder undefined sind.
if (a && a.b && a.b.e && a.b.e[0] && a.b.e[0].f != null) {
    // Code ausführen
}
```

### Refactoring

Um den Code übersichtlicher und robuster zu gestalten, kann der optionale Operator `?.` (Optional Chaining) verwendet werden. Dieser Operator prüft automatisch, ob der vorherige Schlüssel existiert, und greift nur dann auf den nächsten Schlüssel zu, wenn er vorhanden ist.
Sollte ein Schlüssel nicht existieren, wird keine weitere Aktion ausgeführt und das Ergebnis ist `undefined`.

```javascript
// Pfad zur Methode könnte nicht existieren
myObject.myKey?.myMethod();
// Rückgabe ist `undefined`, falls der Pfad nicht existiert

// Falls eine Methode undefiniert sein könnte
anotherObject.myMethod?.();
// Rückgabe ist `undefined`, falls der Pfad oder die Methode nicht existieren

// Feldzugriff oder Array
anotherObject?.["field"];

if (myNullValue == null) {
    // Code ausführen
}

if (myObject?.myKey?.myMethod()) {
    // Code ausführen
}

// Prüfung, ob a,b,e und e[0] sowie f nicht null oder undefined sind.
a.b.e[0]?.f != null;

// Wenn einer der Schlüssel null oder undefined ist, ist das Ergebnis ebenfalls undefined.
console.log('Defined', a.b.e[0]?.f == null);
```

### Vorteile

- Vereinfachung des Codes durch Reduzierung von redundanten `if`-Bedingungen
- Lesbarkeit und Wartbarkeit des Codes werden verbessert
- Verringertes Risiko von Fehlern durch Vergessen oder falsche Anwendung von `null`- oder `undefined`-Prüfungen

### Nachteile

- Keine direkte Unterstützung in älteren JavaScript-Versionen (vor ECMAScript 2020)
- Verwendung des optionalen Operators kann dazu führen, dass Fehler später erkannt werden, da `undefined`-Werte nicht sofort als solche erkannt werden

### Weiterführende Informationen

Weitere Informationen zur Verwendung des optionalen Operators `?.` oder Optional Chaining in JavaScript findest du in der [Mozilla Developer Network (MDN) Dokumentation](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Optional_chaining). Dort werden die Funktionsweise und die verschiedenen Anwendungsfälle ausführlich erläutert.

## Auf null und undefined prüfen

Bei der Überprüfung auf `null` oder `undefined` ist es wichtig, die korrekte Überprüfung durchzuführen, da andernfalls unerwartet auch Werte wie 0, "", oder false fälschlicherweise als falsy-Werte erkannt werden können.

### Problem

```javascript
if (!myObject) {
    //myObject === null oder
    //myObject === undefined oder
    //myObject === 0 oder
    //myObject === "" oder
    //myObject === false
}

if (myObject === null || myObject === undefined || typeof myObject === 'undefined') {
    // myObject === null oder
    // myObject === undefined
}
```

### Refactoring

Um sicherzustellen, dass **nur** `null` oder `undefined` erkannt werden und andere falsy-Werte ausgeschlossen werden, kann die folgende Überprüfung verwendet werden:

```javascript
if (myObject == null) {
    //myObject === null oder
    //myObject === undefined
}
```

Die VErwendung von zwei Gleichheitszeichen `==` anstelle von drei `===` ist hierbei wichtig, da so `undefined` und `null` erkannten werden.

### Vorteile

- Korrekte Überprüfung auf `null` oder `undefined`
- Vermeidung von unerwarteten Fehlern durch falsche Erkennung von falsy-Werten

### Nachteile

- Werte wie NaN werden nicht erkannt
- ESLint muss entsprechend konfiguriert werden, um die Verwendung von `==` bei null Vergleich zu erlauben. Dies ist möglich, indem die Regel `eqeqeq` auf [smart](https://eslint.org/docs/latest/rules/eqeqeq#smart) umgestellt wird.

## Object destructuring / Object Eigenschaften bekommen

Beim Object Destructuring werden die Eigenschaften eines Objekts in einzelne Variablen aufgeteilt und gespeichert.

### Problem

```javascript
const car = {
    speed: 10,
    color: "red"
}

const speed = car.speed;
const color = car.color;
```

### Refactoring

Um den Code zu vereinfachen und die Eigenschaften eines Objekts direkt in Variablen zu speichern, kann das Object Destructuring verwendet werden:

```javascript
const car = {
    speed: 10,
    color: "red"
}

const { speed, color } = car;
```

### Vorteile

- Kürzerer und lesbarerer Code
- Direkter Zugriff auf die gewünschten Eigenschaften des Objekts

## Verwendung von async und await

Die Verwendung von `async` und `await` bietet eine elegante Möglichkeit, asynchrone Funktionen in JavaScript zu schreiben und zu verwalten.

### Problem

Traditionell wurden asynchrone Operationen in JavaScript mithilfe von Callback-Funktionen oder Promises behandelt. Dies führte jedoch oft zu sogenanntem "Callback-Hell" oder zu komplexem und schwer verständlichem Code, insbesondere bei mehreren aufeinanderfolgenden asynchronen Operationen.

```javascript
getData(function(result) {
    processData(result, function(data) {
        saveData(data, function(response) {
            // Weitere Operationen...
        });
    });
});
```

### Refactoring

Dank `async` und `await` kann asynchroner Code lesbarer und besser handhabbar gemacht werden.
Durch das Hinzufügen des `async`-Schlüsselworts zu einer Funktion wird diese automatisch zu einer asynchronen Funktion.
Das `await`-Schlüsselwort wird verwendet, um auf das Ergebnis einer asynchronen Operation zu warten.
Fehlerbehandlung wird durch `try/catch` durchgeführt.

```javascript
async function myAsyncFunction() {
    const result = await getData();
    const data = await processData(result);
    try {
      const response = await saveData(data);
    } catch (e) {
        // ...
    }
    // Weitere Operationen...
}
```

### Vorteile

- Lesbarer und verständlicher Code
- Reduzierung der Verschachtelung von Callbacks ("Callback-Hell")
- Einfachere Fehlerbehandlung durch Verwendung von `try-catch`-Blöcken
- Bessere Kontrolle über asynchrone Abläufe und Reihenfolge der Operationen
- Einfachere Fehlerbehandlung

### Nachteile

- Verwendung von `async` und `await` erfordert ECMAScript 2017 (ES8) oder höher

### Weiterführende Literatur/Links

- [Async functions - MDN Web Docs](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/async_function)

## Guard Pattern

Das Guard Pattern ist eine Best Practice, um die Lesbarkeit und Robustheit von Code zu verbessern, insbesondere bei Bedingungsprüfungen.

### Problem

In JavaScript müssen oft komplexe Bedingungen geprüft werden, um unerwünschte Ausführungszweige zu verhindern oder ungültige Eingaben abzufangen. Dies kann zu verschachteltem Code führen, der schwer zu lesen und zu warten ist.

```javascript
function processInput(input) {
    if (input !== null && input !== undefined && input !== '') {
        // Code zur Verarbeitung des Eingabewerts
    }
}
```

### Refactoring

Das Guard Pattern ermöglicht es uns, Bedingungsprüfungen klarer und lesbarer zu gestalten, indem wir unerwünschte Fälle frühzeitig abfangen und beenden.

```javascript
function processInput(input) {
    if (input == null || input === '') {
        return;
    }

    // Code zur Verarbeitung des Eingabewerts
}
```

### Vorteile

- Verbesserte Lesbarkeit des Codes durch eine klare und frühzeitige Abhandlung unerwünschter Fälle
- Reduzierung der Verschachtelung von Bedingungsprüfungen
- Einfache Erweiterbarkeit und Wartbarkeit des Codes

### Weiterführende Literatur/Links

- [Guard Clause Pattern - Refactoring.Guru](https://refactoring.guru/smells/guard-clauses)

## Positiv formulierte If-Bedingungen und Auslagerung komplexer Bedingungen

Positiv formulierte If-Bedingungen und die Auslagerung komplexer Bedingungen in temporäre Variablen verbessern die Lesbarkeit und Wartbarkeit des Codes.

> Die Aufsplittung von If-Bedingungen ist sehr abhängig vom Verständnis des Entwicklers und sollte mit Sinn und Verstand eingesetzt werden.
### Problem

Komplexe Bedingungen in If-Anweisungen können den Code schwer verständlich machen, insbesondere wenn sie negativ formuliert sind. Lange und verschachtelte Bedingungen erschweren die Lesbarkeit und können zu Fehlern führen.

```java
if (!(name.isEmpty() || age < 18 || !isAuthorized)) {
    // Code ausführen
}
```

```javascript
if (!(name === "" || age < 18 || !isAuthorized)) {
    // Code ausführen
}
```

### Refactoring

Durch die positive Formulierung der Bedingungen und die Auslagerung komplexer Ausdrücke in temporäre Variablen wird der Code lesbarer und verständlicher.

> Die Aufsplittung von If-Bedingungen ist sehr abhängig vom Verständnis des Entwicklers und sollte mit Sinn und Verstand eingesetzt werden.

```java
boolean isNameEmpty = name.isEmpty();
boolean isUnderAge = age < 18;
boolean isNotAuthorized = !isAuthorized;

if (!isNameEmpty && !isUnderAge && isNotAuthorized) {
    // Code ausführen
}
```

```javascript
const isNameEmpty = name === "";
const isUnderAge = age < 18;
const isNotAuthorized = !isAuthorized;

if (!isNameEmpty && !isUnderAge && isNotAuthorized) {
    // Code ausführen
}
```

### Vorteile

- Verbesserte Lesbarkeit des Codes durch positiv formulierte Bedingungen
- Reduzierung der Verschachtelung und Komplexität von If-Anweisungen
- Bessere Wartbarkeit des Codes durch klare und beschreibende Variablen

### Nachteile

- Alternativ kann ein Kommentar die If-Bedingung beschreiben, aber bei einer Änderung muss daran gedacht werden auch den Kommentar anzupassen.
- Das Auslagern von Bedingungen in temporäre Variablen kann zu einem erhöhten Speicherverbrauch führen, insbesondere bei komplexen Ausdrücken. Dies ist normalerweise vernachlässigbar, kann jedoch in speziellen Situationen berücksichtigt werden.

### Ausnahmen

Es gibt Fälle, in denen das Auslagern von Bedingungen in temporäre Variablen nicht sinnvoll ist, z. B. wenn die Bedingung nur an einer Stelle verwendet wird und keine weitere Klarheit oder Wartbarkeit gewonnen wird.

### Weiterführende Literatur/Links

- [The Art of Readable Code - Simple Conditionals](https://www.amazon.com/dp/0596802293)
- [Clean Code: A Handbook of Agile Software Craftsmanship](https://www.amazon.com/dp/0132350882)

## Begrenzte Zeilenanzahl in Methoden/Funktionen

Die Begrenzung der Anzahl von Codezeilen in Methoden und Funktionen verbessert die Lesbarkeit, Wartbarkeit und Verständlichkeit des Codes. Es ermöglicht auch eine bessere Testbarkeit des Codes.

### Problem

Methoden oder Funktionen mit einer großen Anzahl von Codezeilen können schwer zu lesen, zu verstehen und zu warten sein. Lange Methoden können verschiedene Aufgaben vermischen und die Einhaltung des Single Responsibility Principle erschweren.

```javascript
function processUserData(user) {
    // Schritt 1: Validierung der Benutzerdaten
    if (user !== null && user !== undefined) {
        if (validateName(user.name)) {
            if (validateEmail(user.email)) {
                if (validateAge(user.age)) {
                    // ...
                }
            }
        }
    }

    // Schritt 2: Speichern der Benutzerdaten
    if (user !== null && user !== undefined) {
        if (saveUserData(user)) {
            // ...
        }
    }

    // Schritt 3: Senden einer Bestätigungs-E-Mail
    if (user !== null && user !== undefined) {
        if (sendConfirmationEmail(user.email)) {
            // ...
        }
    }

    // Schritt 4: Aktualisierung des Benutzerstatus
    if (user !== null && user !== undefined) {
        if (updateUserStatus(user)) {
            // ...
        }
    }

    // ...
}
```

### Refactoring

Um die Lesbarkeit und Verständlichkeit des Codes zu verbessern, sollten Methoden und Funktionen auf eine begrenzte Anzahl von Zeilen beschränkt sein. Komplexe Aufgaben sollten in kleinere Teilfunktionen ausgelagert werden, um die Verantwortlichkeiten klarer zu trennen.

> Die Anzahl von Zeilen sollte allgemein so klein wie möglich gehalten werden. Sie sollte allerdings nie über eine Bildschirmhöhe hinausgehen, d.h. mehr als 25 Zeilen sollten vermieden werden.

Allgemeine Code-Refactorings sind:

- Code-Blöcke oder Scopes (durch geschweifte Klammern separiert) können in Methoden ausgelagert werden.
- Kommentare, die eine Sektion kommentieren können im Allgemeinen in eine Methode ausgelagert werden.
- For-Schleifen, welche If-Bedingungen beinhalten, können als Methode geschrieben werden.
- Mehrdimensionale For-Schleifen können in Methoden ausgelagert werden,
- If-Bedingungen innerhalb einer Methode können als Methode geschrieben werden.

```javascript
function processUserData(user) {
    validateUser(user);
    saveUser(user);
    sendConfirmationEmail(user.email);
    updateUserStatus(user);
}

function validateUser(user) {
    if (user === null || user === undefined) {
        throw ...;
    }

    if (!validateName(user.name)) {
        throw ...;
    }

    if (!validateEmail(user.email)) {
        throw ...;
    }

    if (!validateAge(user.age)) {
        throw ...;
    }

    // Weitere Validierungen...
}

function saveUser(user) {
    if (user === null || user === undefined) {
        throw ...;
    }

    if (!saveUserData(user)) {
        throw ...;
    }

    // Weitere Speicheroperationen...
}

// Weitere Teilfunktionen...

```

### Vorteile

- Verbesserte Lesbarkeit und Verständlichkeit des Codes durch kleinere und fokussierte Methoden/Funktionen
- Einfachere Wartbarkeit und Testbarkeit durch klar abgegrenzte Verantwortlichkeiten
- Bessere Übersichtlichkeit und Strukturierung des Codes
- Bessere Testbarkeit des Codes, da kleinere Methoden leichter isoliert und getestet werden können

Kleine Methoden haben den Vorteil, dass sie leichter testbar und wartbar sind. Hier sind einige Gründe dafür:

1. **KISS-Prinzip**: Das KISS-Prinzip kann leichter eingehalten werden, wenn Methoden und Funktionen auf eine begrenzte Anzahl von Zeilen beschränkt sind. Der Entwickler kommt nicht dazu überkomplexe Methoden zu schreiben, da er sich an die Zeilenbeschränkung halten muss.

2. **Bessere Isolierung**: Kleine Methoden behandeln normalerweise nur eine spezifische Aufgabe oder Verantwortlichkeit. Dadurch können sie isoliert und unabhängig von anderen Teilen des Codes getestet werden. Durch die Fokussierung auf eine spezifische Funktion können Tests effektiver und einfacher geschrieben werden.

3. **Lesbarkeit**: Kleine Methoden sind in der Regel einfacher zu verstehen, da sie nur eine begrenzte Anzahl von Zeilen umfassen und sich auf eine bestimmte Funktionalität konzentrieren. Dadurch wird die Lesbarkeit des Codes verbessert und es ist einfacher, den Zweck und das Verhalten der Methode zu erfassen.

4. **Wiederverwendbarkeit**: Kleine Methoden können leichter wiederverwendet werden. Da sie in der Regel spezifische Aufgaben erfüllen, können sie in verschiedenen Teilen des Codes wiederverwendet werden, wenn ähnliche Funktionalität benötigt wird. Dies fördert die Modularität und reduziert die Duplizierung von Code.

5. **Einfache Wartbarkeit**: Kleine Methoden sind einfacher zu warten, da sie in sich abgeschlossen sind und Änderungen an einer Methode weniger Auswirkungen auf andere Teile des Codes haben. Bei einem Fehler oder einer gewünschten Änderung ist es einfacher, den relevanten Code zu lokalisieren und anzupassen, ohne den gesamten Kontext berücksichtigen zu müssen.

6. **Bessere Testabdeckung**: Durch die Aufteilung des Codes in kleine Methoden wird die Testabdeckung verbessert, da jede Methode spezifische Tests erhalten kann. Dadurch können verschiedene Szenarien und Randbedingungen gezielt getestet werden, um die Fehleranfälligkeit zu reduzieren.

7. **Einfacheres Mocking**: Darüber hinaus ist das Mocking in Tests einfacher, wenn der Code in kleine Methoden aufgeteilt ist. Beim Schreiben von Unit-Tests ist es häufig erforderlich, externe Abhängigkeiten zu mocken oder zu fälschen, um den Fokus auf die zu testende Methode zu legen. Mit kleinen Methoden ist es einfacher, diese Abhängigkeiten zu identifizieren und zu isolieren, da sie in der Regel explizit als Parameter an die Methode übergeben werden. Das Mocking-Setup ist zudem kleiner und einfacher, weil aufgespaltete Methoden einfach diese Methoden mocken können, statt die fremde (externe) API, die darin verwendet wird.

8. **Förderung des Single Responsibility Principle**: Kleine Methoden unterstützen das Single Responsibility Principle, das besagt, dass eine Methode oder Funktion nur eine einzige Verantwortlichkeit haben sollte. Durch die Aufteilung des Codes in kleine Methoden wird die Verantwortlichkeit klarer definiert und das Prinzip der klaren Trennung von Aufgaben eingehalten.

Die Verwendung kleiner Methoden verbessert die Qualität und Wartbarkeit des Codes, indem sie die Testbarkeit, Lesbarkeit, Wiederverwendbarkeit und Modularität fördern. Es ist jedoch wichtig, ein Gleichgewicht zu finden, um eine übermäßige Fragmentierung des Codes zu vermeiden und die Lesbarkeit nicht zu beeinträchtigen.

### Nachteile

- Die strikte Begrenzung der Zeilenanzahl kann zu einer übermäßigen Fragmentierung des Codes führen, wenn kleinere Methoden oder Funktionen unnötig erstellt werden.

### Ausnahmen

Die Anzahl der Codezeilen in einer Methode oder Funktion kann je nach Kontext und Komplexität des Codes variieren. Es ist wichtig, das Gleichgewicht zwischen einer angemessenen Zeilenzahl und einer klaren, verständlichen und wartbaren Struktur zu finden.

## Verwendung von `Optional` in JavaScript-Funktionen

Eine Funktion sollte niemals `null`, `undefined` oder `NaN` zurückgeben und stattdessen die `Optional`-Klasse verwenden, um den Status des Ergebnisses zu kennzeichnen.

> Alternativ kann auch der Optional-Operator `.?` verwendet werden. Siehe das [Kapitel dazu](#optionaler-operator---optional-chaining-verwenden).
> Alternativ auch [Verwendung von `Optional` in JavaScript-Funktionen](#verwendung-von-optional-in-javascript-funktionen)

### Problem

Das Zurückgeben von `null`, `undefined` oder `NaN` aus einer Funktion kann zu Fehlern führen, insbesondere wenn nicht überprüft wird, ob das Ergebnis vorhanden ist oder nicht.

```javascript
function divide(a, b) {
  if (b !== 0) {
    return a / b;
  }
  return null;
}
```

### Refactoring

Die Verwendung des `Optional`-Objekts ermöglicht es uns, den Status des Ergebnisses klar zu kennzeichnen, anstatt `null`, `undefined` oder `NaN` zurückzugeben.

```javascript
function divide(a, b) {
  if (b !== 0) {
    return Optional.of(a / b);
  }

  return Optional.empty();
}
```

### Vorteile

- Klarere Kennzeichnung des Zustands des Ergebnisses durch Verwendung von `Optional`
- Bessere Fehlervermeidung durch explizite Behandlung von leeren Ergebnissen
- Verbesserte Lesbarkeit des Codes durch den Verzicht auf `null` oder `undefined`

### Nachteile

- Zusätzlicher Overhead durch die Verwendung von `Optional`
- Potenziell erhöhter Komplexitätsgrad in der Verwendung des `Optional`-Objekts

### Ausnahmen

Die Verwendung von `Optional` in JavaScript ist eine Designentscheidung und keine Sprachfunktion. Es ist optional und sollte basierend auf den Anforderungen des Projekts und der Teampräferenz eingesetzt werden.

### Weiterführende Literatur/Links

- [Optional Chaining Operator - JavaScript](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Optional_chaining) (Alternatives Muster zur Behandlung von `null`- und `undefined`-Werten)

### Code für Optional

```javascript

/**
 * Klasse, die ein optionales Ergebnis repräsentiert.
 * @param {*} value - Der Wert des optionalen Ergebnisses.
 * @class
 * @readonly
 */
function Optional(value) {
  /**
   * Der Wert des optionalen Ergebnisses.
   * @type {*}
   * @readonly
   */
  Object.defineProperty(this, 'result', {
    value: value,
    writable: false
  });

  /**
   * Gibt an, ob das optionale Ergebnis vorhanden ist.
   * @type {boolean}
   * @readonly
   */
  Object.defineProperty(this, 'isPresent', {
    get: function() {
      return this.result !== null && !isNaN(this.result);
    }
  });

  /**
   * Gibt an, ob das optionale Ergebnis fehlt.
   * @type {boolean}
   * @readonly
   */
  Object.defineProperty(this, 'isMissing', {
    get: function() {
      return !this.isPresent;
    }
  });

  Object.freeze(this);
}

/**
 * Erstellt ein `Optional`-Objekt mit dem angegebenen Wert.
 * @param {*} value - Der Wert für das optionale Ergebnis.
 * @returns {Optional} - Das erstellte `Optional`-Objekt.
 * @static
 * @example
 * var myResult = Optional.of(42);
 */
Optional.of = function(value) {
  return new Optional(value);
};

/**
 * Erstellt ein leeres `Optional`-Objekt.
 * @returns {Optional} - Das erstellte leere `Optional`-Objekt.
 * @static
 * @example
 * var emptyResult = Optional.empty();
 */
Optional.empty = function() {
  return new Optional(null);
};

/**
 * Überprüft, ob ein gegebener Wert eine Instanz von `Optional` ist.
 * @param {*} optional - Der zu überprüfende Wert.
 * @returns {boolean} - `true`, wenn der Wert eine `Optional`-Instanz ist, andernfalls `false`.
 * @static
 * @example
 * var myResult = Optional.of(42);
 * console.log(Optional.isOptional(myResult)); // true
 */
Optional.isOptional = function(optional) {
  return optional instanceof Optional;
};
```

## Verwendung der npm-Bibliothek optional.js zur Rückgabe von Optional in JavaScript

Es ist einfach in JavaScript, die npm-Bibliothek optional.js zu verwenden, um die Rückgabe von Optional-Objekten anstelle von null oder anderen Fehlertypen zu ermöglichen.
Durch die Verwendung von Optional-Objekten wird deutlich, dass eine Funktion möglicherweise keinen Wert zurückgibt und ermöglicht eine bessere Behandlung von optionalen Werten.

### Problem

In JavaScript ist es üblich, dass Funktionen null, undefined oder andere Werte zurückgeben, um das Fehlen eines erwarteten Werts zu kennzeichnen.
Dies kann zu Verwirrung und unerwartetem Verhalten führen, da der Rückgabewert möglicherweise nicht explizit auf das Fehlen des Werts überprüft wird.

```javascript
function findUserById(id) {
  const user = db.findUser(id);
  if (user) {
    return user;
  }
  return null;
}

const user = findUserById(123);
if (user) {
  // Do something with the user
}
```

### Refactoring

Durch die Verwendung der optional.js-Bibliothek können Funktionen Optional-Objekte zurückgeben, um das Fehlen eines Werts explizit zu kennzeichnen. Dadurch wird die Code-Klarheit verbessert und die Behandlung von optionalen Werten erleichtert.

```javascript
const Optional = require('optional-js');

function findUserById(id) {
  const user = db.findUser(id);
  return Optional.ofNullable(user);
}

const userOptional = findUserById(123);
if (userOptional.isPresent()) {
  const user = userOptional.get();
  // Do something with the user
}
```

### Vorteile

- Bessere Behandlung von optionalen Werten durch die Verwendung von Optional-Objekten
- Explizite Kennzeichnung des Fehlens eines Werts
- Einfachere Überprüfung des Vorhandenseins eines Werts und Zugriff auf den Wert mit den Methoden von Optional

### Nachteile

- Einführung einer zusätzlichen Abhängigkeit durch die Verwendung der optional.js-Bibliothek
- API Methoden, die optional.js-Bibliothek verwenden erfordern, dass Nutzer der API die optional.js-Bibliothek einbinden, kennen und verwenden müssen.

### Ausnahmen

Es kann Situationen geben, in denen die Verwendung der optional.js-Bibliothek nicht angemessen ist, z. B. wenn das Projekt bereits eine andere Lösung für die Behandlung von optionalen Werten verwendet oder wenn die Einführung einer zusätzlichen Abhängigkeit vermieden werden soll.

### Weiterführende Literatur/Links

- [optional.js - npm](https://www.npmjs.com/package/optional-js)
- [Avoiding Null in JavaScript: An Introduction to Optional Values](https://dev.to/marcellomontemagno/avoiding-null-in-javascript-an-introduction-to-optional-values-4m22)

## If-Bedingungen ohne Else und mit Return

If-Bedingungen, die ein Return enthalten, sollten kein else enthalten, um die Lesbarkeit des Codes zu verbessern und die Verschachtelung von Bedingungen zu reduzieren.

### Problem

If-Bedingungen mit einem Return und einem dazugehörigen else-Block können die Lesbarkeit des Codes beeinträchtigen und zu unnötiger Verschachtelung führen.

```java
public int calculate(int x) {
    if (x > 0) {
        return x * 2;
    } else {
        return x;
    }
}
```

```javascript
function calculate(x) {
    if (x > 0) {
        return x * 2;
    } else {
        return x;
    }
}
```

### Refactoring

Durch Entfernen des else-Blocks und direktes Rückgabestatement wird der Code lesbarer und die Verschachtelung von Bedingungen reduziert.

```java
public int calculate(int x) {
    if (x > 0) {
        return x * 2;
    }
    return x;
}
```

```javascript
function calculate(x) {
    if (x > 0) {
        return x * 2;
    }
    return x;
}
```

### Vorteile

- Verbesserte Lesbarkeit und Klarheit des Codes
- Reduzierung der Verschachtelung von Bedingungen
- Vereinfachte Struktur und Fluss des Codes

### Weiterführende Literatur/Links

- [Clean Code: A Handbook of Agile Software Craftsmanship](https://www.amazon.com/dp/0132350882)
- [JavaScript: The Good Parts](https://www.amazon.com/dp/0596517742)

## Exceptions in JavaScript nicht einfach loggen und unverändert wieder werfen

Exceptions sollten in JavaScript nicht einfach nur geloggt und unverändert wieder geworfen werden.
Stattdessen ist es wichtig, Exceptions sinnvoll zu behandeln und angemessene Maßnahmen zu ergreifen.
Entweder wird die Exception geloggt und behandelt oder in eine andere Form umgewandelt und geworfen.

### Problem

Das einfache Loggen und unveränderte Werfen von Exceptions führt oft dazu, dass die eigentliche Ursache des Problems verschleiert wird.
Es erschwert auch die Fehlerbehandlung und das Debugging des Codes.

```javascript
try {
  // Code, der eine Exception auslöst
} catch (error) {
  console.log('Exception aufgetreten:', error);
  throw error;
}
```

### Refactoring

Es ist wichtig, die Ursache der Exception zu verstehen und entsprechend zu reagieren. Dies kann das Ergreifen von Fehlerbehandlungsmaßnahmen, das Aufzeigen von aussagekräftigen Fehlermeldungen oder das Umwandeln der Exception in eine andere Form sein.

```javascript
try {
  // Code, der eine Exception auslöst
} catch (error) {
  // Fehlerbehandlung und angemessene Maßnahmen ergreifen
  console.error('Ein Fehler ist aufgetreten:', error);
  // Weitere Maßnahmen wie Fehlermeldung anzeigen, alternative Verarbeitung, etc.
}
```

### Vorteile

- Klare Behandlung und Reaktion auf Exceptions
- Verbesserte Fehlerbehandlung und Debugging-Möglichkeiten
- Besseres Verständnis der Ursachen von Fehlern

### Ausnahmen

In einigen Fällen kann es sinnvoll sein, Exceptions zu loggen und unverändert wieder zu werfen. Dies ist jedoch eher die Ausnahme und sollte gut begründet sein, z.B. wenn der Code in einem bestimmten Kontext läuft, der spezielle Anforderungen hat.

### Weiterführende Literatur/Links

- [Exception Handling Best Practices in JavaScript](https://www.toptal.com/javascript/exception-handling-javascript-best-practices)
- [JavaScript Error Handling: Best Practices](https://blog.bitsrc.io/javascript-error-handling-best-practices-329c5f6e5d33)

## Verwendung von `const` für alle Variablen in JavaScript und Kennzeichnung von Nicht-Konstanten

Um unbeabsichtigtes Ändern von Variablen zu vermeiden, sollte in JavaScript das Schlüsselwort `const` für alle Variablen verwendet werden.
In Fällen, in denen die Verwendung von `const` nicht möglich ist, sollte ein Kommentar mit dem Inhalt "nonconst" hinzugefügt werden.

### Problem

Die Verwendung von `const` sorgt dafür, dass Variablen nicht versehentlich geändert werden. Ohne die Verwendung von `const` besteht die Gefahr, dass Variablen unbeabsichtigt überschrieben werden.
Dies kann dazu führen, dass sich der Wert von Variablen, Attributen oder Parametern unerwartet ändert und dadurch unerwünschte Nebeneffekte auftreten können. Dies passiert beispielsweise dann, wenn die Variable, das Attribut oder der Parameter in einem anderen Teil des Codes nachträglich und von einer anderen Person unerwartet geändert wird.
Dadurch wird die Lesbarkeit und Nachvollziehbarkeit des Codes erschwert.

```javascript
let name = "John";
let age = 30;

// ...

name = "Jane"; // Unbeabsichtigte Änderung der Variable
```

### Refactoring

Um unbeabsichtigtes Ändern von Variablen zu vermeiden, sollten alle Variablen mit `const` deklariert werden. In Fällen, in denen die Verwendung von `const` nicht möglich ist (z. B. bei Variablen, die sich ändern müssen), sollte ein Kommentar mit dem Inhalt "nonconst" hinzugefügt werden, um darauf hinzuweisen.

```javascript
const name = "John";
const age = 30;

// ...

// nonconst: Variable muss sich ändern
let count = 0;
count++;
```

### Vorteile

- Vermeidung unbeabsichtigter Änderungen von Variablen
- Klarheit in Bezug auf die Veränderlichkeit von Variablen
- Verbesserte Code-Qualität und Verständlichkeit

### Ausnahmen

Es gibt Situationen, in denen die Verwendung von `const` nicht möglich oder sinnvoll ist, z. B. bei Variablen, die sich ändern müssen oder in komplexen Legacy-Code.
In solchen Fällen kann die Kennzeichnung mit einem Kommentar "nonconst" helfen, auf die Ausnahme hinzuweisen.

### Weiterführende Literatur/Links

- [MDN Web Docs: const](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/const)
- [JavaScript: const, let, or var?](https://www.freecodecamp.org/news/var-let-and-const-whats-the-difference/)

## Methoden/Funktionen sollten niemals null zurückgeben, sondern immer eine leere Liste, HashMap oder Array

Es ist eine bewährte Praxis in Java und JavaScript, dass Methoden/Funktionen, die Listen, Hashmaps oder Arrays zurückgeben, niemals null zurückgeben sollten. Stattdessen sollte immer eine leere Liste, HashMap oder ein leeres Array zurückgegeben werden.

### Problem

Das Zurückgeben von null als Ergebnis einer Methode/Funktion, die eine Liste, HashMap oder ein Array zurückgibt, kann zu Zugriffsfehlern (undefined) und unerwartetem Verhalten führen.
Es erfordert zusätzliche Überprüfungen auf null und erhöht die Komplexität des Aufrufercodes.

```javascript
getNames() {
    if (condition) {
        return null;
    }
    // ...
}
```

### Refactoring

Um Zugriffsfehler und unerwartetes Verhalten zu vermeiden, sollten Methoden/Funktionen stattdessen ein leeres Objekt oder Array zurückgeben.

> Alternativ kann auch der Optional-Operator `.?` verwendet werden. Siehe das [Kapitel dazu](#optionaler-operator---optional-chaining-verwenden).
> Alternativ kann auch das [Optional-Klassen-Pattern](#verwendung-von-optional-in-javascript-funktionen) verwendet werden.

```javascript
function getNames() {
    if (condition) {
        return [];
    }
    // ...
}
```

### Vorteile

- Vermeidung von Zugriffsfehlern und unerwartetem Verhalten
- Einfachere Handhabung und weniger Überprüfungen auf null im Aufrufercode
- Verbesserte Robustheit und Stabilität des Codes

### Ausnahmen

Es kann Situationen geben, in denen die Rückgabe von null sinnvoll ist, z. B. wenn null einen speziellen Zustand oder eine Bedeutung hat. In solchen Fällen ist es wichtig, die Risiken und Vorteile sorgfältig abzuwägen und die Entscheidung angemessen zu dokumentieren.

### Weiterführende Literatur/Links

- [Effective Java: Item 54 - Return Empty Arrays or Collections, Not Nulls](https://www.amazon.com/dp/0321356683)
- [Null or Empty Collection in Java](https://www.baeldung.com/java-null-empty-collection) (für Java)
- [Avoiding Null in JavaScript](https://dmitripavlutin.com/avoid-null-undefined-javascript/) (für JavaScript)

## Benennung von Methoden mit verschiedenen Präfixen für Synchronität und Ergebnisverhalten

Es ist eine bewährte Praxis bei der Benennung von Methoden in JavaScript und Java, unterschiedliche Präfixe zu verwenden, um die Synchronität und das Ergebnisverhalten der Methode zu kennzeichnen. Das Präfix "get" sollte für synchronen Zugriff verwendet werden und immer einen Wert zurückgeben, während die Präfixe "fetch" oder "request" für asynchronen Zugriff stehen, der länger dauern und auch fehlschlagen kann.

### Problem

Bei der Benennung von Methoden ist es wichtig, klare Hinweise auf die Synchronität und das Ergebnisverhalten der Methode zu geben.
Unklare oder inkonsistente Benennung kann zu Missverständnissen und unerwartetem Verhalten führen.

```javascript
// Unklare Benennung ohne klare Angabe zur Synchronität und zum Ergebnisverhalten
function getData() {
  // ...
}

// Unklare Benennung ohne klare Angabe zur Synchronität und zum Ergebnisverhalten
async function getAsyncData() {
  // ...
}
```

### Refactoring

Um die Synchronität und das Ergebnisverhalten einer Methode klarer zu kennzeichnen, sollten unterschiedliche Präfixe verwendet werden. Das Präfix "get" sollte für synchronen Zugriff verwendet werden und immer einen Wert zurückgeben. Die Präfixe "fetch" oder "request" sollten für asynchronen Zugriff stehen, der länger dauern und auch fehlschlagen kann.

> get-Präfixe sollten nie async sein, dagegen sollten fetch- oder request- Präfixe immer async sein.

```javascript
// Synchroner Zugriff mit Wert-Rückgabe
function getValue() {
  // ...
}

// Asynchroner Zugriff mit Möglichkeit eines Fehlschlags
async function fetchResource() {
  // ...
}
```

### Vorteile

- Klare und eindeutige Benennung, die die Synchronität und das Ergebnisverhalten einer Methode widerspiegelt
- Verbesserte Lesbarkeit und Verständlichkeit des Codes
- Einfachere Fehlersuche und Debugging-Möglichkeiten

### Ausnahmen

Es kann Situationen geben, in denen die Verwendung von anderen Präfixen oder Benennungsmustern angemessen ist, abhängig von den spezifischen Anforderungen und Konventionen des Projekts.
Es ist wichtig, einheitliche Benennungsstandards innerhalb des Projekts festzulegen und zu dokumentieren.

### Weiterführende Literatur/Links

- [Method Naming Conventions in Java](https://www.baeldung.com/java-method-naming-conventions)
- [JavaScript Naming Conventions](https://www.robinwieruch.de/javascript-naming-conventions)

## Kurz-Übersicht weiterer Themen zur Ausgestaltung

1. Verwende `let` und `const` anstelle von `var`, um Blockscope zu nutzen und unerwartete Seiteneffekte zu vermeiden.

2. Nutze Template Literals (`` ` ``) für die einfache Einbettung von Variablen in Strings.

3. Nutze den Spread-Operator (`...`) für das Zusammenführen von Arrays oder das Kopieren von Objekten.

4. Verwende Arrow Functions (`() => {}`) für eine kürzere und prägnantere Schreibweise von Funktionen. Vermeide `me = this`.

5. Nutze Objekt-Destrukturierung, um bequem auf Eigenschaften eines Objekts zuzugreifen.

6. Verwende den ternären Operator (`condition ? expression1 : expression2`) für kurze bedingte Ausdrücke.

7. Verwende `Array.prototype.forEach()`, `Array.prototype.map()`, `Array.prototype.filter()` und andere Array-Methoden anstelle von Schleifen, um den Code lesbarer zu machen.

8. Nutze den `import`- und `export`-Mechanismus für die Modulorganisation in deinem Code.

9. Verwende `Set` und `Map` für die Verwaltung eindeutiger Werte und Schlüssel-Wert-Paare.
