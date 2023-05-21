# Best Practises und Design Patterns

- [Best Practises und Design Patterns](#best-practises-und-design-patterns)
  - [Allgemein](#allgemein)
  - [Linter verwenden](#linter-verwenden)
  - [Methodenlänge reduzieren](#methodenlänge-reduzieren)
  - [If Bedingungen nur zu Beginn einer Methode](#if-bedingungen-nur-zu-beginn-einer-methode)
  - [Verwendung von Exceptions](#verwendung-von-exceptions)
  - [Exceptions dürfen nur abgefangen und in speziellere Exceptions wieder geworfen werden](#exceptions-dürfen-nur-abgefangen-und-in-speziellere-exceptions-wieder-geworfen-werden)
  - [Exceptions dürfen nur geloggt werden, wenn sie nicht geworfen werden](#exceptions-dürfen-nur-geloggt-werden-wenn-sie-nicht-geworfen-werden)
  - [Attribute nur mit protected Sichtbarkeit versehen](#attribute-nur-mit-protected-sichtbarkeit-versehen)
  - [Attribute komplexer Typen sollten nicht mit Getter und Setter veröffentlicht werden](#attribute-komplexer-typen-sollten-nicht-mit-getter-und-setter-veröffentlicht-werden)
  - [Stream-API verwenden](#stream-api-verwenden)
  - [JavaDoc-Kommentierung im Code](#javadoc-kommentierung-im-code)
  - [JetBrains Annotations](#jetbrains-annotations)
  - [Eingabeprüfungen in REST-API mit Annotation](#eingabeprüfungen-in-rest-api-mit-annotation)
  - [Final für alle Attribute, Variablen und Parameter verwenden](#final-für-alle-attribute-variablen-und-parameter-verwenden)
  - [Guard Pattern in Java](#guard-pattern-in-java)
  - [Positiv formulierte If-Bedingungen und Auslagerung komplexer Bedingungen](#positiv-formulierte-if-bedingungen-und-auslagerung-komplexer-bedingungen)
  - [Begrenzte Zeilenanzahl in Methoden/Funktionen](#begrenzte-zeilenanzahl-in-methodenfunktionen)
  - [Verwendung von Optional als Funktionswert](#verwendung-von-optional-als-funktionswert)
  - [If-Bedingungen ohne Else und mit Return](#if-bedingungen-ohne-else-und-mit-return)
  - [Richtiges Verwenden von Platzhaltern beim Logging mit SLF4J](#richtiges-verwenden-von-platzhaltern-beim-logging-mit-slf4j)
  - [Rückgabe von nur unveränderlichen (immutable) Objekten in Java-Methoden](#rückgabe-von-nur-unveränderlichen-immutable-objekten-in-java-methoden)
  - [Klassen sollten interne Objekte nur über spezielle Methoden veränderbar machen](#klassen-sollten-interne-objekte-nur-über-spezielle-methoden-veränderbar-machen)
  - [Methoden/Funktionen sollten niemals null zurückgeben, sondern immer eine leere Liste, HashMap oder Array](#methodenfunktionen-sollten-niemals-null-zurückgeben-sondern-immer-eine-leere-liste-hashmap-oder-array)
  - [Verwendung von `computeIfAbsent` und `putIfAbsent` für HashMaps in Java](#verwendung-von-computeifabsent-und-putifabsent-für-hashmaps-in-java)
  - [Verwendung von `com.machinezoo.noexception` in Callbacks wie z.B. `forEach` in Java](#verwendung-von-commachinezoonoexception-in-callbacks-wie-zb-foreach-in-java)

## Allgemein

1. **Folgen des DRY-Prinzips (Don't Repeat Yourself)**: Wird festgestellt, dass derselbe Code an mehreren Stellen verwendet wird, sollte in Betracht gezogen werden, diesen Code in eine Methode oder eine Klasse zu extrahieren und es dann jedes Mal zu verwenden, wenn es benötigt wird.

2. **Konsistente Benennung von Variablen und Methoden**: Es sollte sichergestellt werden, dass die verwendeten Namen aussagekräftig sind und den Zweck des Codes genau beschreiben. Die Benennung sollte auch konsistent sein.

3. **Anwendung von neuen Java Features**: Mit Java 11 bis 17 stehen viele neue Möglichkeiten zur Verfügung, um den Code zu verbessern. Beispielsweise könnten Var-Typinferenz, Lambda-Ausdrücke und Streams, optionale Typen, neue Methoden für String-Verarbeitung, neue APIs für HTTP-Clients und vieles mehr verwendet werden, um den Code kürzer und leichter lesbar zu machen.

4. **Vermeidung von tief verschachteltem Code**: Tief verschachtelter Code sollte vermieden werden, da er den Code schwer lesbar und wartbar macht. Die Verwendung von flachen Hierarchien und kurzen Methoden kann die Lesbarkeit und Wartbarkeit erheblich verbessern.

5. **Einsatz von Linter und Formatter**: Tools wie Checkstyle, PMD oder SpotBugs können dabei helfen, den Code konsistent und fehlerfrei zu halten.

6. **Schreiben von Unit-Tests**: Guter refaktorierter Code sollte immer von Tests begleitet werden. Sie helfen dabei, sicherzustellen, dass der Code nach dem Refactoring immer noch wie erwartet funktioniert.

7. **Anwendung Modulare Architektur**: Der Code sollte in kleinere, wiederverwendbare Klassen und Pakete aufgeteilt werden. Dies erhöht die Lesbarkeit und erleichtert die Wartung und das Testen.

8. **Selbsterklärender Code**: Kommentare sollten vermieden werden, wo der Code selbst klar sein kann. Guter Code sollte größtenteils selbsterklärend sein.

9. **Anwendung des SOLID-Prinzips**: SOLID ist ein Akronym für fünf Prinzipien des objektorientierten Designs und der Programmierung, die dazu beitragen, dass der Code sauber, robust und wartbar bleibt.

10. **Performance-Optimierungen**: Auf teure Operationen wie ineffiziente Schleifen oder wiederholte Objektinstanziierungen sollte geachtet werden. Performance-Tools wie JProfiler oder VisualVM können genutzt werden, um Flaschenhälse zu identifizieren und zu beheben.

11. **Anwendung Funktionale Programmierkonzepte**: Funktionale Programmierung kann dazu beitragen, dass der Code besser strukturiert und leichter zu testen ist. Konzepte wie Unveränderlichkeit (Immutability), Stream-Operationen und Lambda-Ausdrücke sind besonders nützlich in Java.

12. **Fehlerbehandlung**: Es sollte sichergestellt werden, dass der Code ordnungsgemäß mit Fehlern umgeht. Dazu gehört das Werfen spezifischer benutzerdefinierter Ausnahmen, um den Fehlerzustand genau zu beschreiben. Weiterhin sollten `try/catch`-Blöcke und möglicherweise auch das `finally`-Keyword verwendet werden, um Fehler effektiv zu behandeln und Ressourcen ordnungsgemäß freizugeben.

13. **Anwendung von Design Patterns**: Design Patterns bieten eine wiederverwendbare Vorlage zur Lösung von Softwareentwicklungsproblemen in einem bestimmten Kontext. Sie dienen dazu, den Code sauberer, effizienter und einfacher zu verstehen zu machen. Einige Beispiele für Design Patterns, die in Java häufig verwendet werden, sind:

- Klassenfabrik (Factory Pattern)
- Singleton Pattern
- Builder Pattern
- [weitere Java Design Patterns](https://refactoring.guru/design-patterns/java)

14. **Verwenden aussagekräftige Rückgabewerte und -typen**: Wenn eine Methode einen Wert zurückgibt, sollte dieser Wert aussagekräftig sein und genau das darstellen, was die Methode tut. Es ist auch hilfreich, konsistente Rückgabetypen zu verwenden.

15. **Verwenden von JavaDoc für Dokumentation**: JavaDoc ist ein Standard für das Kommentieren von Java-Code, der dabei hilft, den Code zu dokumentieren und zu verstehen. Es ist besonders nützlich für größere Codebasen oder wenn mehrere Entwickler an einem Projekt arbeiten. Mit JavaDoc können Methoden, Parameter, Rückgabewerte und mehr dokumentiert werden. Diese Dokumentation kann dann von verschiedenen Tools verwendet werden, um automatisch API-Dokumentation zu generieren, oder um in einer integrierten Entwicklungsumgebung (IDE) bessere Hinweise und Autovervollständigungen zu bieten.

## Linter verwenden

### Problem

In großen Codeprojekten kann es schwierig sein, sicherzustellen, dass der Code konsistent und fehlerfrei is.
Insbesondere können stilistische Probleme und kleinere Fehler, die zu schwerwiegenden Fehlern führen können, übersehen werden.

### Vorteile

Durch die Verwendung von Lintern können stilistische Probleme und kleinere Fehler automatisch erkannt und behoben werde.
Linter sind Werkzeuge, die den Code analysieren und auf stilistische Probleme, Code-Duplizierung, potenzielle Fehler und andere Probleme überprüfe.
Dadurch kann die Codequalität verbessert, die Lesbarkeit erhöht und die Fehleranfälligkeit reduziert werden.

### Ausnahmen

Es gibt keine Ausnahmen von der Verwendung von Lintern, da es sich um eine bewährte Methode handelt, um sicherzustellen, dass der Code konsistent und fehlerfrei is.
Allerdings können Linter nicht alle Probleme erkennen und sollten daher nicht als Ersatz für manuelle Code-Reviews oder umfangreiche Tests betrachtet werden.

### Bekannte Linter

- Checkstyle
- FindBugs
- PMD
- SonarQube
- SonarLint

Alle diese Linter sind Werkzeuge für die statische Codeanalyse in Java-Codeprojekten und können dazu beitragen, stilistische Probleme, potenzielle Fehler, Bugs und Schwachstellen zu identifiziere.
Sie können entweder als eigenständige Werkzeuge oder als Plugins für integrierte Entwicklungsumgebungen wie Eclipse, IntelliJ oder NetBeans verwendet werde.
Es ist empfehlenswert, mehrere Linter-Tools in Kombination zu verwenden, um eine umfassende statische Codeanalyse durchzuführen und sicherzustellen, dass der Code konsistent und fehlerfrei ist.

### JetBrains Linter

- SonarLint
- Linter von Jetbrains

## Methodenlänge reduzieren

Methoden sollten auf eine maximale Länge von 10-15 Codezeilen begrenzt werden, um die Lesbarkeit und Wartbarkeit des Codes zu verbessern.

### Problem

Lange Methoden sind schwerer zu verstehen und zu warten, da sie zu viele Verantwortlichkeiten haben und mehrere Aufgaben gleichzeitig erledigen können.

### Beispielcode

Eine Methode, die zu lange ist, könnte beispielsweise viele Verzweigungen, Schleifen oder switch-Statements enthalten.

### Refactoring

Um die Methodenlänge zu reduzieren, sollte man die Methode in kleinere Unter-Methoden aufteilen, die jeweils nur eine spezifische Aufgabe erledige.
Alternativ kann man auch überflüssigen Code entfernen oder redundante Schleifen und Verzweigungen eliminieren.

### Vorteile

- Kürzerer Code ist einfacher zu verstehen und zu warten, da jeder Methodenaufruf eine klare Funktion hat und weniger Verantwortlichkeiten hat.
- Kürzerer Code ist einfacher zu testen, da es weniger Verzweigungen und Schleifen gibt, die möglicherweise verschiedene Testpfade erforder.
Darüber hinaus müssen weniger Mockings durchgeführt werden, da weniger Abhängigkeiten in einer Methode vorhanden sind.
- Der Code wird lesbarer und verständlicher, was die Wartbarkeit und Erweiterbarkeit des Codes verbessert.

### Nachteile

- Es kann schwierig sein, eine große Methode in kleinere Unter-Methoden aufzuteilen, da dies möglicherweise eine umfangreiche Analyse und Überarbeitung des Codes erfordert.
- Es kann vorkommen, dass eine Methode aufgrund ihrer Aufgabe unvermeidlich länger als 10-15 Zeilen sein mus.
In solchen Fällen ist es sinnvoller, die Methode so kurz wie möglich zu gestalten, anstatt sie auf Biegen und Brechen zu kürzen.

### Ausnahmen

Es gibt Situationen, in denen längere Methoden notwendig sein können, z.B. bei der Implementierung von komplexer Logi.
In solchen Fällen sollten Methoden jedoch so kurz wie möglich gehalten werden und auf spezifische Aufgaben fok

## If Bedingungen nur zu Beginn einer Methode

If-Bedingungen sollten möglichst nur zu Beginn einer Methode verwendet werden, um die Lesbarkeit, Wartbarkeit und Testbarkeit des Codes zu verbessern.

### Problem

Wenn If-Bedingungen über den Code verteilt werden, kann es schwieriger sein, den Überblick zu behalten und die Absichten des Codes zu verstehe.
Zudem können mehrere If-Statements in einer Methode zu komplexer Logik führen und zu schwer verständlichem Code führe.
Dies erschwert auch die Testbarkeit des Codes, da jedes If-Statement einen neuen Testpfad erfordert und es schwierig werden kann, alle möglichen Pfade zu testen.

### Beispielcode

Ein Beispiel für schlechte Verwendung von If-Statements:

```java
public void calculatePrice(boolean isPremiumUser) {
   if (isPremiumUser) {
      // do something
   } else {
      // do something else
   }

   // more code
   if (someOtherCondition) {
      // do something
   } else {
      // do something else
   }

   // more code
   if (anotherCondition) {
      // do something
   } else {
      // do something else
   }
}
```

### Refactoring

Um die Verwendung von If-Bedingungen zu verbessern, sollten sie möglichst nur am Anfang einer Methode verwendet werde.
Falls nötig, kann man mehrere Methoden schreiben, um komplexe Bedingungen zu vereinfache.
Eine weitere Option ist die Verwendung von Polymorphismus, um die Logik in unterschiedliche Klassen aufzuteilen.

```java
public void calculatePrice(boolean isPremiumUser) {
   if (!isPremiumUser) {
      // do something else
      return;
   }

   // do something

   // more code
}
```

### Vorteile

- Der Code wird lesbarer und verständlicher, da If-Statements nur am Anfang der Methode vorkommen und die Absichten des Codes klarer sind.
- Der Code ist leichter zu warten und zu erweitern, da der Kontrollfluss der Methode klarer ist und weniger komplexe Logik vorhanden ist.
- Die Testbarkeit des Codes wird verbessert, da weniger Testpfade vorhanden sind und es einfacher ist, alle möglichen Pfade zu testen.

### Nachteile

- Es kann vorkommen, dass in manchen Fällen eine If-Bedingung innerhalb einer Methode verwendet werden muss, um eine bestimmte Funktionalität zu erreiche.
In solchen Fällen sollte man jedoch darauf achten, dass die Bedingung so einfach und klar wie möglich formuliert wird.

### Ausnahmen

Es gibt Situationen, in denen es notwendig sein kann, If-Bedingungen innerhalb einer Methode zu verwende.
Zum Beispiel, wenn die Methode eine Schnittstelle implementiert, die eine bestimmte Signatur erforder.
In solchen Fällen sollte man jedoch darauf achten, dass die Bedingungen so einfach und klar wie möglich formuliert werden und die Methode nicht zu komplex wir.
Es ist auch möglich, eine abstrakte Klasse oder ein Interface zu erstellen, das die Funktionalität aufteilt und eine bessere Lesbarkeit und Testbarkeit ermöglicht.

## Verwendung von Exceptions

Exceptions sollten in Java nur für unerwartete Situationen verwendet werden, um eine saubere Trennung von Fehlerbehandlung und regulärem Code zu ermöglichen.

### Problem

Wenn Exceptions unangemessen verwendet werden, kann dies zu schlechter Leistung, inkonsistentem Verhalten und schwer zu findenden Fehlern führe.
Eine übermäßige Verwendung von Exceptions kann auch die Lesbarkeit des Codes beeinträchtigen und dazu führen, dass der Code schwer verständlich ist.

### Beispielcode

Ein Beispiel für eine schlechte Verwendung von Exceptions:

```java
public void calculatePrice(int quantity) throws Exception {
   if (quantity < 0) {
      throw new Exception("Invalid quantity");
   }

   // do something

   // more code

   // throw another exception
   throw new Exception("Another error occurred");
}
```

### Refactoring

Um die Verwendung von Exceptions zu verbessern, sollte man sie nur für unerwartete Situationen verwenden, wie zum Beispiel unerwartete Eingaben, Netzwerkprobleme oder Systemfehle.
Für erwartete Situationen sollte man eine andere Methode der Fehlerbehandlung verwenden, wie zum Beispiel die Rückgabe eines Fehlercodes oder die Verwendung von booleschen Rückgabewerten.

```java
public void calculatePrice(int quantity) throws InvalidQuantityException {
   if (quantity < 0) {
      throw new InvalidQuantityException("Invalid quantity: {}. Must be greater or equal than zero.", quantity);
   }

   // do something

   // more code

   if (someCondition) {
      throw new AnotherException("Another error occurred");
   }
}
```

### Vorteile

- Eine angemessene Verwendung von Exceptions führt zu einem saubereren Code, der einfacher zu verstehen und zu warten ist.
- Exceptions ermöglichen eine saubere Trennung von Fehlerbehandlung und regulärem Code.
- Durch eine bessere Strukturierung des Codes kann die Leistung verbessert werden.

### Nachteile

- Eine übermäßige Verwendung von Exceptions kann die Leistung beeinträchtigen und die Lesbarkeit des Codes erschweren.
- Es kann schwierig sein, zwischen erwarteten und unerwarteten Situationen zu unterscheiden, was zu Fehlern führen kann, wenn Ausnahmen falsch verwendet werden.

## Exceptions dürfen nur abgefangen und in speziellere Exceptions wieder geworfen werden

Exceptions sollten in speziellere Exceptions umgewandelt und abgefangen werden, um sie an höhere Ebenen weiterzugebe.
Dies erleichtert das Debugging, da der Fehlersachverhalt über den Exception-Typ deutlich gemacht wir.
Die aufrufende Methode kann dann den speziellen Fehler behandeln, ohne den Fehlertext der Exception vergleichen zu müssen.

### Problem

Die Fehlersuche kann erschwert werden, wenn Exceptions bei einem Fehler geworfen werden und die Namen dieser Exceptions nichts mit dem Fehler zu tun habe.
In solchen Fällen kann das Exception-Handling schwierig sein und die Identifizierung der Ursache des Fehlers erschweren.

### Beispielcode

Ein Beispiel für unbehandeltes Weiterschicken von Exceptions:

```java
public void readFromFile(String filePath) throws Exception {
   try {
      BufferedReader reader = new BufferedReader(new FileReader(filePath));
      String line = reader.readLine();
      while (line != null) {
         // do something
         line = reader.readLine();
      }
   } catch (IOException e) {
      // ... weiterer Code
      throw e;
   }
}
```

### Refactoring

Um Exceptions richtig zu behandeln, sollten sie entweder in der aktuellen Methode behandelt oder an eine höhere Ebene weitergegeben werde.
Die Behandlung von Exceptions sollte klar und verständlich sein und nicht einfach nur Fehlermeldungen ausgebe.
Exceptions sollten in speziellere Exceptions umgewandelt werden, um den Fehlersachverhalt über den Exception-Typ deutlich zu machen und die aufrufende Methode es zu ermöglichen diesen speziellen Fehler behandeln zu können.

```java
public void readFromFile(String filePath) throws IOException {
   try (BufferedReader reader = new BufferedReader(new FileReader(filePath))) {
      String line = reader.readLine();
      while (line != null) {
         // do something
         line = reader.readLine();
      }
   } catch (IOException e) {
      throw new MySpecificException("The file {} could not be read.", filePath, e);
   }
}
```

### Vorteile

- Ein Vorteil der Kapselung von Exceptions zusammen mit ihrem Grund in einer neuen Exception ist, dass die aufrufende Methode dadurch die Möglichkeit erhält, auf den Grund der Exception spezifisch zu reagieren und eine entsprechende Fehlerbehandlung durchzuführen.

### Ausnahmen

Es gibt Situationen, in denen es nicht sinnvoll ist, Exceptions in speziellere Exceptions umzuwandeln, z.B. wenn es darum geht, Fehler zu ignorieren oder nicht weiterzugebe.
In solchen Fällen sollte jedoch darauf geachtet werden, dass dies dokumentiert und klar verständlich ist.

## Exceptions dürfen nur geloggt werden, wenn sie nicht geworfen werden

Exceptions sollten nur dann geloggt werden, wenn sie nicht an höhere Ebenen weitergegeben werden und keine Auswirkungen auf den weiteren Ablauf des Programms haben.

### Problem

Das Loggen von Exceptions in Methoden, in denen sie bereits abgefangen werden, führt zu einer unnötigen Vermehrung von Exception-Stacktraces in den Log.
Dies erschwert das Lesen der Logs und kann zu einer höheren Belastung des Speichers führen.

### Beispielcode

Ein Beispiel für ungeprüftes Weiterschicken von Exceptions:

```java
public void readFromFile(String filePath) {
   try {
      BufferedReader reader = new BufferedReader(new FileReader(filePath));
      String line = reader.readLine();
      while (line != null) {
         // do something
         line = reader.readLine();
      }
   } catch (IOException e) {
      logger.error("Unknown error occurred", e);
      throw e;
   }
}
```

### Refactoring

Um Exceptions richtig zu behandeln, sollten sie entweder in der aktuellen Methode behandelt oder an eine höhere Ebene weitergegeben werde.
Nur im ersten Fall sollte ein Logging ausgeben werden.

```java
public void readFromFile(String filePath) throws IOException {
   try (BufferedReader reader = new BufferedReader(new FileReader(filePath))) {
      String line = reader.readLine();
      while (line != null) {
         // do something
         line = reader.readLine();
      }
   } catch (IOException e) {
      throw new MySpecificException("The file {} could not be read.", filePath, e);
   }
}
```

### Vorteile

- Logs beinhalten keine doppelten Fehlermeldungen.
- Logs werden kleiner.

### Ausnahmen

In manchen Fällen für Debugging kann es sinnvoll sein, Exceptions auszuloggen, bevor sie an höhere Ebenen weitergegeben werden, um mehr Informationen über den Fehler zu sammel.
In solchen Fällen sollte jedoch darauf geachtet werden, dass keine vertraulichen Informationen offengelegt werden und dass die Exception nicht einfach nur ignoriert wird.

## Attribute nur mit protected Sichtbarkeit versehen

### Problem

Wenn Attribute mit `private` Sichtbarkeit versehen sind, können sie nicht direkt von Testfällen aufgerufen oder geändert werden, was die Testbarkeit erschwert.

### Beispielcode

```java
public class MyClass {
    private int myPrivateAttribute;

    // ...
}
```

### Refactoring

```java
public class MyClass {
    protected int myProtectedAttribute;

    // ...
}
```

### Vorteile

Durch die Verwendung von `protected` Sichtbarkeit können Testfälle geschrieben werden, die auf die Attribute zugreifen und sie ändern können, um die Testbarkeit der Klasse zu erleichtern.

### Ausnahmen

Es ist jedoch zu beachten, dass die Verwendung von `protected` Sichtbarkeit zu einer Verminderung der Abstraktion und Kapselung von Daten führen kan.
Es sollte nur dann `protected` Sichtbarkeit verwendet werden, wenn es wirklich notwendig ist, um die Testbarkeit zu erleichtern, und wenn es keine anderen Möglichkeiten gibt, die Testbarkeit der Klasse zu gewährleisten.

## Attribute komplexer Typen sollten nicht mit Getter und Setter veröffentlicht werden

### Problem

Wenn Attribute komplexer Typen mit Getter- und Setter-Methoden veröffentlicht werden, kann dies zu unerwartetem Verhalten und schwerwiegenden Fehlern führe.
Insbesondere kann es zu Inkonsistenzen bei der Verwendung von Referenzen auf dieselben Objekte kommen, die das Attribut referenzieren.

### Beispielcode

```java
public class MyClass {
    private List<String> myList;

    public List<String> getMyList() {
        return myList;
    }

    public void setMyList(List<String> myList) {
        this.myList = myList;
    }
}

// ...

MyClass obj1 = new MyClass();
obj1.getMyList().add("Hello");

MyClass obj2 = new MyClass();
System.out.println(obj2.getMyList()); // Output: [Hello]
```

### Refactoring

```java
public class MyClass {
    private List<String> myList;

    public void addToList(String item) {
        this.myList.add(item);
    }

    public List<String> getList() {
        return Collections.unmodifiableList(myList);
    }
}

// ...

MyClass obj1 = new MyClass();
obj1.addToList("Hello");

MyClass obj2 = new MyClass();
System.out.println(obj2.getList()); // Output: []
```

### Vorteile

Indem die Verwendung von Getter- und Setter-Methoden für Attribute komplexer Typen vermieden wird, können Inkonsistenzen bei der Verwendung von Referenzen auf dieselben Objekte verhindert werde.
Stattdessen sollten notwendige Methoden über das Parent-Objekt bereitgestellt werden, um sicherzustellen, dass das Attribut konsistent und korrekt verwendet wird.

### Ausnahmen

Es kann jedoch Fälle geben, in denen die Verwendung von Getter- und Setter-Methoden sinnvoll ist, z.B. wenn das Attribut nicht referenzierbare Objekte enthält oder wenn das Attribut geändert werden kann, ohne dass Inkonsistenzen entstehe.
Es ist daher wichtig, die Verwendung von Getter- und Setter-Methoden sorgfältig zu prüfen und nur dann zu verwenden, wenn es notwendig und sinnvoll ist.

## Stream-API verwenden

### Problem

Die Verwendung von Schleifen und Iteratoren kann zu unleserlichem und unübersichtlichem Code führen, insbesondere wenn komplexe Filter- oder Transformationsoperationen durchgeführt werden müsse.
Darüber hinaus kann es zu Fehlern kommen, wenn Schleifen und Iteratoren nicht korrekt implementiert oder angewendet werden.

### Beispielcode

```java
List<Integer> myList = Arrays.asList(1, 2, 3, 4, 5);

int sum = 0;
for (Integer num : myList) {
    if (num % 2 == 0) {
        sum += num;
    }
}

System.out.println(sum); // Output: 6
```

### Refactoring

```java
List<Integer> myList = Arrays.asList(1, 2, 3, 4, 5);

int sum = myList.stream()
               .filter(num -> num % 2 == 0)
               .mapToInt(Integer::intValue)
               .sum();

System.out.println(sum); // Output: 6
```

### Vorteile

Die Verwendung der Stream-API kann zu einem einfacheren, übersichtlicheren und fehlersichereren Code führe.
Durch die Verwendung von Stream-Operationen wie `filter`, `map`, `reduce`, `distinct` us.
können komplexe Filter- und Transformationsoperationen auf eine klare und konsistente Weise durchgeführt werde.
Darüber hinaus kann die Stream-API auch Parallelverarbeitung unterstützen, um die Leistung von Multi-Core-Systemen voll auszuschöpfen.

### Nachteile

- Potentielle Performance-Probleme
- Komplizierte Verkettung von Befehlen
- Keine Zwischenergebnisse
- Schwierige Fehlerbehandlung (kann durch Stream*Debugger in IntelliJ entgegengewirkt werden)
- Komplexität

### Ausnahmen

Es kann jedoch Fälle geben, in denen die Verwendung von Schleifen und Iteratoren sinnvoller ist,
z.B. wenn es sich um eine einfache Iteration ohne komplexe Filter- oder Transformationsoperationen handelt oder wenn es notwendig ist, auf Elemente in einer bestimmten Reihenfolge zuzugreife.
Es ist daher wichtig, die Verwendung von Stream-Operationen sorgfältig zu prüfen und nur dann zu verwenden, wenn es notwendig und sinnvoll ist.

## JavaDoc-Kommentierung im Code

### Problem

Die Dokumentation des Codes ist eine wichtige Komponente, um die Lesbarkeit und Wartbarkeit des Codes zu verbesser.
Insbesondere in großen Codeprojekten kann es schwierig sein, den Zweck und die Verwendung von Klassen, Methoden und Variablen zu verstehen.

### Beispielcode

```java
/**
 * A class representing a book.
 */
public class Book {
    private String title;
    private String author;

    /**
     * Creates a new Book object with the given title and author.
     *
     * @param title The title of the book.
     * @param author The author of the book.
     */
    public Book(String title, String author) {
        this.title = title;
        this.author = author;
    }

    /**
     * Returns the title of the book.
     *
     * @return The title of the book.
     */
    public String getTitle() {
        return title;
    }

    /**
     * Returns the author of the book.
     *
     * @return The author of the book.
     */
    public String getAuthor() {
        return author;
    }
}
```

### Refactoring

JavaDoc ist eine Möglichkeit, um den Code zu dokumentieren und seine Lesbarkeit und Wartbarkeit zu verbesser.
JavaDoc-Kommentare können verwendet werden, um den Zweck und die Verwendung von Klassen, Methoden und Variablen zu erkläre.
Durch das Hinzufügen von JavaDoc-Kommentaren können andere Entwickler den Code besser verstehen und die Wartbarkeit des Codes verbessern.

### Vorteile

Durch die Verwendung von JavaDoc-Kommentaren kann der Code besser dokumentiert werden, was dazu beiträgt, dass andere Entwickler den Code besser verstehen und die Wartbarkeit des Codes verbessern könne.
JavaDoc-Kommentare können auch automatisch generiert werden, um API-Dokumentationen zu erstellen, die anderen Entwicklern die Verwendung von Bibliotheken und Frameworks erleichtern können.

### Ausnahmen

Es gibt keine Ausnahmen von der Verwendung von JavaDoc, da es eine bewährte Methode ist, um den Code zu dokumentieren und seine Lesbarkeit und Wartbarkeit zu verbesser.
Allerdings können JavaDoc-Kommentare zu einem höheren Aufwand führen, insbesondere in kleineren Codeprojekten oder in Projekten, die nur von einem einzigen Entwickler gewartet werden.

Gerne! Hier ist der erweiterte Text mit einer Liste von möglichen Annotations-Typen:

## JetBrains Annotations

### Problem

Es kann schwierig sein, den Code auf Null-Referenzen und andere Probleme zu überprüfen, die während der Laufzeit auftreten könne.
Außerdem können schlecht dokumentierte Methoden und Klassen zu Verwirrung und Fehlern führen.

### Beispielcode

```java
public void foo(String s) {
    if (s == null) {
        throw new NullPointerException();
    }
    // ...
}
```

### Refactoring

Mit den Annotations von JetBrains können Entwickler Methoden und Klassen genau dokumentieren und auf Null-Referenzen und andere Probleme hinweise.
Zum Beispiel kann die `@NotNull`-Annotation verwendet werden, um anzuzeigen, dass eine Variable, ein Parameter oder ein Rückgabewert einer Methode nicht null sein dar.
Die `@Nullable`-Annotation kann verwendet werden, um anzuzeigen, dass ein Parameter oder Rückgabewert einer Methode null sein kann.

Andere mögliche [Annotations-Typen von Jetbrains](https://javadoc.io/doc/org.jetbrains/annotations/latest/index.html) sind:

- `org.intellij.lang.annotations.Flow`: Verwendet zur Angabe von Flussbedingungen, die von einem Code-Analyse-Tool verwendet werden können, um mögliche Fehler im Code zu identifizieren.
- `org.intellij.lang.annotations.JdkConstants`: Verwendet zur Verwendung von Konstanten aus der JDK-Codebasis, um Compilerwarnungen und -fehler zu vermeiden.
- `org.intellij.lang.annotations.Language`: Verwendet zur Angabe der Sprache, die in einem String-Literal verwendet wird, um Tools wie Code-Analyse-Tools und IDEs zu unterstützen.
- `org.jetbrains.annotations.ApiStatus`: Verwendet zur Kennzeichnung von API-Elementen (Methoden, Klassen usw.) mit ihrem aktuellen Stabilitätsstatus (experimentell, stabil, veraltet usw.).
- `org.jetbrains.annotations.Contract`: Verwendet zur Angabe von Vertragsbedingungen, die eine Methode erfüllen muss, wie z.B. dass sie keine `null`-Rückgabewerte liefern darf oder dass sie einen bestimmten Wertebereich zurückgeben muss.
- `org.jetbrains.annotations.Debug`: Verwendet zur Markierung von Code-Elementen (Klassen, Methoden usw.), die nur für Debugging-Zwecke verwendet werden sollten und nicht in einer Produktionsumgebung aufgerufen werden sollten.
- `org.jetbrains.annotations.DependsOn`: Verwendet zur Angabe von Abhängigkeiten zwischen Code-Elementen (Klassen, Methoden usw.), um Tools wie IDEs und Build-Tools bei der Erstellung von Abhängigkeitsdiagrammen zu unterstützen.
- `org.jetbrains.annotations.ExpectedFailure`: Verwendet zur Markierung von Tests, die auf fehlgeschlagene Tests warten oder darauf, dass bestimmte Ausnahmen ausgelöst werden.
- `org.jetbrains.annotations.FileCharset`: Verwendet zur Angabe des Zeichensatzes, der für eine bestimmte Datei verwendet werden soll.
- `org.jetbrains.annotations.MagicConstant`: Verwendet zur Verwendung von Enum-ähnlichen Konstanten mit einem bestimmten Wertebereich und einem vordefinierten Satz von Konstantenwerten.
- `org.jetbrains.annotations.Nls`: Verwendet zur Angabe von lokalisierten Strings, um Tools wie IDEs und Code-Analyse-Tools bei der Lokalisierung von Code zu unterstützen.
- `org.jetbrains.annotations.NotNull`: Verwendet zur Angabe von Argumenten, die nicht `null` sein dürfen.
- `org.jetbrains.annotations.Nullable`: Verwendet zur Angabe von Argumenten, die `null` sein dürfen.
- `org.jetbrains.annotations.Pattern`: Verwendet zur Überprüfung von Strings mit einem regulären Ausdruck.
- `org.jetbrains.annotations.PropertyKey`: Verwendet zur Angabe von Schlüsseln für lokalisierte Strings.
- `org.jetbrains.annotations.Range`: Verwendet zur Überprüfung von Argumenten auf einen bestimmten Wertebereich.
- `org.jetbrains.annotations.RegExp`: Verwendet zur Überprüfung von Strings mit einem regulären Ausdruck.
- `org.jetbrains.annotations.Subst`: Verwendet zur Ersetzung von Platzhaltern in Strings durch bestimmte Werte.
- `org.jetbrains.annotations.TestOnly`: Verwendet zur Markierung von Code-Elementen (Klassen, Methoden usw.), die nur für Tests verwendet werden sollten und nicht in einer Produktionsumgebung aufgerufen werden sollten

### Beispiele

- `@Contract`:

  ```java
  public static void divide(@Contract("_,0 -> fail") int a, int b) {
      if (b == 0) {
          throw new IllegalArgumentException("Divisor cannot be zero");
      }
      int result = a / b;
      System.out.println(result);
  }
  ```

- `@MagicConstant`:

  ```java
  public class PaymentMethod {
      public static final String CREDIT_CARD = "credit_card";
      public static final String PAYPAL = "paypal";
      public static final String GOOGLE_PAY = "google_pay";

      private String method;

      public PaymentMethod(@MagicConstant(stringValues = {CREDIT_CARD, PAYPAL, GOOGLE_PAY}) String method) {
          this.method = method;
      }

      // ...
  }
  ```

- `@NotNull`:

  ```java
  public static String formatName(@NotNull String firstName, @NotNull String lastName) {
      return lastName + ", " + firstName;
  }
  ```

- `@Range`:

  ```java
  public static void validateAge(@Range(from = 18, to = 99) int age) {
      if (age < 18 || age > 99) {
          throw new IllegalArgumentException("Age must be between 18 and 99");
      }
      System.out.println("Valid age: " + age);
  }
  ```

- `@Pattern`:

  ```java
  public static void validateEmail(@Pattern(regexp = "^[\\w-\\.]+@([\\w-]+\\.)+[\\w-]{2,4}$") String email) {
      if (!email.matches("^[\\w-\\.]+@([\\w-]+\\.)+[\\w-]{2,4}$")) {
          throw new IllegalArgumentException("Invalid email format");
      }
      System.out.println("Valid email: " + email);
  }
  ```

### Vorteile

- Reduziert die Anzahl von Null-Referenz-Exceptions
- Verbessert die Dokumentation von Code
- Unterstützt statische Analysewerkzeuge und IDEs bei der Fehlererkennung
- Verbessert die Lesbarkeit von Code für andere Entwickler

### Nachteile

- Erfordert zusätzliche Zeit und Arbeit, um Annotations in den Code zu integrieren
- Kann dazu führen, dass der Code unübersichtlich wird, wenn zu viele Annotations verwendet werden

### Ausnahmen

- Für kleine und einfache Projekte können Annotations möglicherweise nicht erforderlich sein
- Es kann Fälle geben, in denen der Aufwand, Annotations zu verwenden, den Nutzen überwiegt.

### weiterführende Literatur/Links

- JetBrains Annotations Dokumentation: <https://www.jetbrains.com/help/idea/nullable-and-notnull-annotations.html>
- "Effective Java" von Joshua Bloch: Ein Buch, das die Verwendung von Annotations in Java detailliert beschreibt.

## Eingabeprüfungen in REST-API mit Annotation

### Problem

RESTful Web Services erlauben den Austausch von Daten zwischen verschiedenen Systemen über HTTP-Anfrage.
Diese Daten können jedoch in unerwarteter Weise falsch formatiert oder ungültig sei.
Eine fehlgeschlagene Eingabeprüfung kann zu unerwarteten Ergebnissen oder sogar zu Sicherheitsproblemen führen.

### Beispielcode

```java
@Path("/products/{category}/{productId}")
public class ProductResource {
    @GET
    @Produces(MediaType.APPLICATION_JSON)
    public Response getProduct(
            @PathParam("category") String category,
            @PathParam("productId") int productId) {
        // ...
    }
}
```

In diesem Beispiel gibt es zwei Pfadparameter: `category` und `productId`. Der `category`-Parameter kann einen beliebigen String enthalten und `productId` muss eine ganze Zahl sei.
Es gibt keine Eingabeprüfung auf die Werte der Parameter.

### Refactoring

Eine Möglichkeit, die Eingabeprüfung in RESTful Web Services zu verbessern, besteht darin, Annotationen zu verwenden, um die zulässigen Werte und Formate von Parametern zu definiere.
JAX-RS bietet eine Vielzahl von Annotationen an, die dazu verwendet werden können, Eingabeprüfungen durchzuführen.

Einige der wichtigsten Annotationen, die in REST-Methoden verwendet werden können, um Eingabeprüfungen durchzuführen:

- `@PathParam` - Ermöglicht den Zugriff auf den Wert eines Pfadparameters in einer REST-Anfrage.
- `@QueryParam` - Ermöglicht den Zugriff auf den Wert eines Abfrageparameters in einer REST-Anfrage.
- `@HeaderParam` - Ermöglicht den Zugriff auf den Wert eines Header-Parameters in einer REST-Anfrage.
- `@CookieParam` - Ermöglicht den Zugriff auf den Wert eines Cookie-Parameters in einer REST-Anfrage.
- `@FormParam` - Ermöglicht den Zugriff auf den Wert eines Formular-Parameters in einer REST-Anfrage.
- `@BeanParam` - Ermöglicht die Verwendung eines POJOs, das mit `@PathParam`, `@QueryParam`, `@HeaderParam`, `@CookieParam` und `@FormParam` annotiert ist, um eine Gruppe von Parametern zu erfassen.
- `@DefaultValue` - Legt einen Standardwert für einen Parameter fest, falls er in der REST-Anfrage nicht vorhanden ist.
- `@Min` - Legt den minimalen Wert für eine numerische Eingabe fest.
- `@Max` - Legt den maximalen Wert für eine numerische Eingabe fest.
- `@NotNull` - Legt fest, dass ein Parameter in der REST-Anfrage nicht null sein darf.
- `@Size` - Legt die Größe eines Parameters in der REST-Anfrage fest.
- `@UUID` - Legt fest, dass ein Parameter in der REST-Anfrage eine gültige UUID sein muss.
- `@Pattern` - Legt ein reguläres Ausdrucksmuster fest, das ein Parameter in der REST-Anfrage erfüllen muss.

Diese Annotationen können verwendet werden, um sicherzustellen, dass die Eingaben in einer REST-Anfrage korrekt sind und um unerwartete Fehler bei der Verarbeitung zu vermeiden.

Beispiel:

```java
@Path("/products/{category}/{productId : \\d+}")
public class ProductResource {
    @GET
    @Produces(MediaType.APPLICATION_JSON)
    public Response getProduct(
            @PathParam("category") @Pattern(regexp = "^(books|electronics|clothing)$") String category,
            @PathParam("productId") int productId) {
        // ...
    }
}
```

- Prüfung einer UUID:

```java
@GET
@Path("/{id}")
public Response getResource(@PathParam("id") @UUID String id) {
    // code here
}
```

- Prüfung einer Zahl zwischen 1 und 10:

```java
@GET
@Path("/{number}")
public Response getNumber(@PathParam("number") @Min(1) @Max(10) int number) {
    // code here
}
```

```java
@POST
@Path("/example/{name}/{age}/{email}/{password}")
@Consumes(MediaType.APPLICATION_JSON)
public Response exampleMethod(
        @PathParam("name") final String name,
        @PathParam("age") @Min(value = 18, message = "Age must be at least 18") @Max(value = 120, message = "Age must not exceed 120") final int age,
        @PathParam("email") @Email(message = "Invalid email address") final String email,
        @PathParam("password") @Pattern(regexp = "^(?=.*[A-Za-z])(?=.*\\d)[A-Za-z\\d]{8,}$", message = "Password must be at least 8 characters long and contain at least one letter and one number") final String password
) {
    // Methodenlogik hier...

    return Response.ok().build();
}


```

In diesem Beispiel wird die Annotation `@Min(1)` und `@Max(10)` verwendet, um sicherzustellen, dass der `number`-Parameter zwischen 1 und 10 lieg.
Sollte dies nicht der Fall sein, wird ebenfalls ein 400-Fehler zurückgegeben.

In diesem Beispiel gibt es wieder die beiden Pfadparameter `category` und `productId`. Der `category`-Parameter muss entweder "books", "electronics" oder "clothing" sei.
Der `productId`-Parameter muss eine ganze Zahl sein.

### Vorteile

- Bessere Eingabeprüfung: Annotationen ermöglichen eine präzisere Definition der zulässigen Werte und Formate von Parametern, was zu einer besseren Eingabeprüfung führt.
- Sicherheit: Eine effektive Eingabeprüfung kann dazu beitragen, Sicherheitsprobleme zu verhindern, die durch unerwartete oder ungültige Eingaben verursacht werden können.
- In der Regel wird der HTTP-Statuscode "400 Bad Request" zurückgegeben, wenn eine Eingabeprüfung in einer REST-API fehlschlägt.

### Nachteile

### Ausnahmen

Es gibt keine strikten Ausnahmen für die Verwendung von Eingabeprüfungen in RESTful Web Service.
In einigen Fällen kann jedoch eine weniger strenge Überprüfung der Eingaben erforderlich sein, um eine nahtlose Integration zwischen verschiedenen Systemen zu ermöglichen.

### weiterführende Literatur/Links

- [Java EE 7 Tutorial: Using Path Parameters](https://docs.oracle.com/javaee/7/tutorial/jaxrs-advanced004.htm)
- [Java EE 7 Tutorial: Using Query Parameters](https://docs.oracle.com/javaee/7/tutorial/jax)

## Final für alle Attribute, Variablen und Parameter verwenden

### Problem

In Java können Variablen, Attribute und Parameter mit dem Schlüsselwort `final` als unveränderlich deklariert werde.
Trotzdem wird in vielen Fällen darauf verzichtet, `final` zu verwende.
Dies kann dazu führen, dass sich der Wert von Variablen, Attributen oder Parametern unerwartet ändert und dadurch unerwünschte Nebeneffekte auftreten könne.
Dadurch wird die Lesbarkeit und Nachvollziehbarkeit des Codes erschwert.

### Beispielcode

In diesem Beispiel kann das Alter einer `Person` mit der `setAge()`-Methode geändert werden, obwohl es eigentlich unveränderlich sein sollte.

```java
public class Person {
    private String name;
    private int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    public int getAge() {
        return age;
    }
}

public class Main {
    public static void main(String[] args) {
        Person person = new Person("Max", 25);
        System.out.println("Age before: " + person.getAge());
        person.setAge(30);
        System.out.println("Age after: " + person.getAge());
    }
}
```

Beispielcode mit mehrfacher Änderung von Variablen innerhalb einer Methode:

```java
public void calculateTotalPrice(double basePrice, double discountRate, int quantity) {
   double totalPrice = basePrice;
   double discountAmount = totalPrice * discountRate;
   totalPrice -= discountAmount;
   int quantityPurchased = quantity;
   if (quantityPurchased > 10) {
      double additionalDiscount = 0.1 * totalPrice;
      totalPrice -= additionalDiscount;
   }
   double taxRate = 0.2;
   double taxAmount = totalPrice * taxRate;
   totalPrice += taxAmount;
   System.out.println("Total price is: " + totalPrice);
}
```

### Refactoring

Alle Variablen, Attribute und Parameter sollten mit `final` deklariert werden, um sie unveränderlich zu mache.
Der Refactoring-Schritt besteht darin, alle Stellen im Code zu finden, an denen eine Variable, ein Attribut oder ein Parameter verändert wird, und das `final`-Schlüsselwort hinzuzufügen.
Variablen und Attribute, die mit Absicht nicht-final sind, müssen mit `/*nonfinal*/` kommentiert werden.

```java
public class Person {
    private final String name;
    private final int age;

    public Person(final String name, final int age) {
        this.name = name;
        this.age = age;
    }

    public int getAge() {
        return age;
    }
}

public class Main {
    public static void main(String[] args) {
        final Person person = new Person("Max", 25);
        System.out.println("Age before: " + person.getAge());
        // person.setAge(30); // Compilerfehler, da age als final deklariert wurde
        System.out.println("Age after: " + person.getAge());
    }
}
```

```java
public void calculateTotalPrice(final double basePrice, final double discountRate, final int quantity) {
   final double totalPrice = basePrice;
   final double discountAmount = totalPrice * discountRate;
   final double discountedPrice = totalPrice - discountAmount;
   final int quantityPurchased = quantity;
   /*nonfinal*/ double finalPrice = discountedPrice;
   if (quantityPurchased > 10) {
      final double additionalDiscount = 0.1 * discountedPrice;
      finalPrice -= additionalDiscount;
   }
   final double taxRate = 0.2;
   final double taxAmount = finalPrice * taxRate;
   final double totalPriceWithTax = finalPrice + taxAmount;
   System.out.println("Total price is: " + totalPriceWithTax);
}
```

### Vorteile

- Unveränderliche Variablen, Attribute und Parameter machen den Code robuster und fehleranfälliger, da sie unerwartete Änderungen von Werten verhindern.
- Lesbarkeit und Nachvollziehbarkeit des Codes werden durch `final` verbessert, da es klarer ist, welche Werte sich nicht ändern können.

### Ausnahmen

- In manchen Fällen kann es sinnvoll sein, Variablen, Attribute oder Parameter nicht als `final` zu deklarieren, wenn sich der Wert häufig ändern muss oder wenn es aus anderen Gründen sinnvoll erschein.
In diesen Fällen muss mit `/*nonfinal*/` kommentiert werden.

## Guard Pattern in Java

Das Guard Pattern ist eine bewährte Praxis, um die Lesbarkeit und Robustheit von Code zu verbessern, insbesondere bei Bedingungsprüfungen in Java.

### Problem

In Java müssen oft komplexe Bedingungen überprüft werden, um unerwünschte Ausführungszweige zu verhindern oder ungültige Eingaben abzufangen. Dies kann zu verschachteltem Code führen, der schwer zu lesen und zu warten ist.

```java
public void processInput(String input) {
    if (input != null && !input.isEmpty()) {
        // Code zur Verarbeitung des Eingabewerts
    }
}
```

### Refactoring

Das Guard Pattern ermöglicht es uns, Bedingungsprüfungen klarer und lesbarer zu gestalten, indem wir unerwünschte Fälle frühzeitig abfangen und den Code beenden.

```java
public void processInput(String input) {
    if (input == null || input.isEmpty()) {
        return;
    }

    // Code zur Verarbeitung des Eingabewerts
}
```

### Vorteile

- Verbesserte Lesbarkeit des Codes durch eine klare und frühzeitige Abhandlung unerwünschter Fälle
- Reduzierung der Verschachtelung von Bedingungsprüfungen
- Einfache Erweiterbarkeit und Wartbarkeit des Codes

### Nachteile

- Das Guard Pattern kann zu einem erhöhten Rückgabewert führen, wenn in jedem Guard-Zweig ein `return`-Statement verwendet wird. Dies sollte jedoch kein Problem sein, solange die Methode einen void-Rückgabetyp hat oder der Rückgabewert keine weitere Bedeutung hat.

### Ausnahmen

Das Guard Pattern sollte nicht blindlings auf jede Bedingungsprüfung angewendet werden. In einigen Fällen kann es sinnvoll sein, spezifische Fehlermeldungen zu generieren oder detailliertere Prüfungen durchzuführen, bevor der Code beendet wird.

### Weiterführende Literatur/Links

- [Guard Clause - Martin Fowler](https://martinfowler.com/bliki/GuardClause.html)

## Positiv formulierte If-Bedingungen und Auslagerung komplexer Bedingungen

Positiv formulierte If-Bedingungen und die Auslagerung komplexer Bedingungen in temporäre Variablen verbessern die Lesbarkeit und Wartbarkeit des Codes.

### Problem

Komplexe Bedingungen in If-Anweisungen können den Code schwer verständlich machen, insbesondere wenn sie negativ formuliert sind. Lange und verschachtelte Bedingungen erschweren die Lesbarkeit und können zu Fehlern führen.

```java
if (!(name.isEmpty() || age < 18 || !isAuthorized)) {
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

```java
public void processUserData(User user) {
    // Schritt 1: Validierung der Benutzerdaten
    if (user != null && !user.getName().isEmpty()) {
        if (validateName(user.getName())) {
            if (validateEmail(user.getEmail())) {
                if (validateAge(user.getAge())) {
                    // ...
                }
            }
        }
    }

    // Schritt 2: Speichern der Benutzerdaten
    if (user != null && !user.getName().isEmpty()) {
        if (saveUserData(user)) {
            // ...
        }
    }

    // Schritt 3: Senden einer Bestätigungs-E-Mail
    if (user != null && !user.getEmail().isEmpty()) {
        if (sendConfirmationEmail(user.getEmail())) {
            // ...
        }
    }

    // Schritt 4: Aktualisierung des Benutzerstatus
    if (user != null && !user.getName().isEmpty()) {
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

```java
public void processUserData(User user) {
    validateUser(user);
    saveUser(user);
    sendConfirmationEmail(user.getEmail());
    updateUserStatus(user);
}

private void validateUser(User user) {
    if (user == null || user.getName().isEmpty()) {
        throw ...;
    }

    if (!validateName(user.getName())) {
        throw ...;
    }

    if (!validateEmail(user.getEmail())) {
        throw ...;
    }

    if (!validateAge(user.getAge())) {
        throw ...;
    }

    // Weitere Validierungen...
}

private void saveUser(User user) {
    if (user == null || user.getName().isEmpty()) {
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

1. **Bessere Isolierung**: Kleine Methoden behandeln normalerweise nur eine spezifische Aufgabe oder Verantwortlichkeit. Dadurch können sie isoliert und unabhängig von anderen Teilen des Codes getestet werden. Durch die Fokussierung auf eine spezifische Funktion können Tests effektiver und einfacher geschrieben werden.

2. **Lesbarkeit**: Kleine Methoden sind in der Regel einfacher zu verstehen, da sie nur eine begrenzte Anzahl von Zeilen umfassen und sich auf eine bestimmte Funktionalität konzentrieren. Dadurch wird die Lesbarkeit des Codes verbessert und es ist einfacher, den Zweck und das Verhalten der Methode zu erfassen.

3. **Wiederverwendbarkeit**: Kleine Methoden können leichter wiederverwendet werden. Da sie in der Regel spezifische Aufgaben erfüllen, können sie in verschiedenen Teilen des Codes wiederverwendet werden, wenn ähnliche Funktionalität benötigt wird. Dies fördert die Modularität und reduziert die Duplizierung von Code.

4. **Einfache Wartbarkeit**: Kleine Methoden sind einfacher zu warten, da sie in sich abgeschlossen sind und Änderungen an einer Methode weniger Auswirkungen auf andere Teile des Codes haben. Bei einem Fehler oder einer gewünschten Änderung ist es einfacher, den relevanten Code zu lokalisieren und anzupassen, ohne den gesamten Kontext berücksichtigen zu müssen.

5. **Bessere Testabdeckung**: Durch die Aufteilung des Codes in kleine Methoden wird die Testabdeckung verbessert, da jede Methode spezifische Tests erhalten kann. Dadurch können verschiedene Szenarien und Randbedingungen gezielt getestet werden, um die Fehleranfälligkeit zu reduzieren.

6. **Einfacheres Mocking**: Darüber hinaus ist das Mocking in Tests einfacher, wenn der Code in kleine Methoden aufgeteilt ist. Beim Schreiben von Unit-Tests ist es häufig erforderlich, externe Abhängigkeiten zu mocken oder zu fälschen, um den Fokus auf die zu testende Methode zu legen. Mit kleinen Methoden ist es einfacher, diese Abhängigkeiten zu identifizieren und zu isolieren, da sie in der Regel explizit als Parameter an die Methode übergeben werden. Das Mocking-Setup ist zudem kleiner und einfacher, weil aufgespaltete Methoden einfach diese Methoden mocken können, statt die fremde (externe) API, die darin verwendet wird.

7. **Förderung des Single Responsibility Principle**: Kleine Methoden unterstützen das Single Responsibility Principle, das besagt, dass eine Methode oder Funktion nur eine einzige Verantwortlichkeit haben sollte. Durch die Aufteilung des Codes in kleine Methoden wird die Verantwortlichkeit klarer definiert und das Prinzip der klaren Trennung von Aufgaben eingehalten.

Die Verwendung kleiner Methoden verbessert die Qualität und Wartbarkeit des Codes, indem sie die Testbarkeit, Lesbarkeit, Wiederverwendbarkeit und Modularität fördern. Es ist jedoch wichtig, ein Gleichgewicht zu finden, um eine übermäßige Fragmentierung des Codes zu vermeiden und die Lesbarkeit nicht zu beeinträchtigen.

### Nachteile

- Die strikte Begrenzung der Zeilenanzahl kann zu einer übermäßigen Fragmentierung des Codes führen, wenn kleinere Methoden oder Funktionen unnötig erstellt werden.

### Ausnahmen

Die Anzahl der Codezeilen in einer Methode oder Funktion kann je nach Kontext und Komplexität des Codes variieren. Es ist wichtig, das Gleichgewicht zwischen einer angemessenen Zeilenzahl und einer klaren, verständlichen und wartbaren Struktur zu finden.

### Weiterführende Literatur/Links

- [Clean Code: A Handbook of Agile Software Craftsmanship](https://www.amazon.com/dp/0132350882)
- [Refactoring: Improving the Design of Existing Code](https://www.amazon.com/dp/0201485672)
- [Effective JavaScript: 68 Specific Ways to Harness the Power of JavaScript](https://www.amazon.com/dp/0321812182)

## Verwendung von Optional als Funktionswert

### Problem

Bei der Rückgabe von Werten aus einer Funktion in Java besteht oft die Möglichkeit, dass kein Wert vorhanden ist. In solchen Fällen wird häufig null zurückgegeben, was zu potenziellen NullPointerExceptions führen kann.

```java
public String getUserName() {
    if (benutzernameExistiert) {
        return benutzername;
    }
    return null;    
}
```

### Refactoring

Statt null als Rückgabewert zu verwenden, empfiehlt es sich, die Klasse `Optional` aus dem Java-Standardpaket zu verwenden. Mit `Optional` können wir explizit angeben, dass ein Wert optional sein kann und den Entwicklern ermöglichen, damit umzugehen.

```java
public Optional<String> getUserName() {
    // Logik, um den Benutzernamen abzurufen
    // ...
    if (benutzernameExistiert) {
        return Optional.of(benutzername);
    } 
     
    return Optional.empty();
}
```

### Vorteile

- Klarere Aussage über die Möglichkeit eines fehlenden Werts
- Vermeidung von NullPointerExceptions
- Zwingt Entwickler dazu, explizit mit dem möglichen Fehlen des Werts umzugehen

### Nachteile

- Erfordert, dass Entwickler den `Optional`-Typ verstehen und richtig damit umgehen

### Ausnahmen

Es kann Ausnahmefälle geben, in denen die Verwendung von `Optional` nicht sinnvoll ist, z. B. wenn die Performance eine Rolle spielt und die Verwendung von `Optional` zu unnötiger Komplexität führen würde.

### weiterführende Literatur/Links

- [Effective Java: Third Edition](https://www.amazon.com/dp/0134685997)
- [Java Optional - Oracle Documentation](https://docs.oracle.com/en/java/javase/16/docs/api/java.base/java/util/Optional.html)

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

### Vorteile

- Verbesserte Lesbarkeit und Klarheit des Codes
- Reduzierung der Verschachtelung von Bedingungen
- Vereinfachte Struktur und Fluss des Codes

### Nachteile

- Es gibt keine spezifischen Nachteile, da dies eine stilistische Entscheidung ist und die Funktionalität des Codes nicht beeinflusst wird.

### Ausnahmen

- Es kann Ausnahmen geben, in denen ein else-Block sinnvoll ist, um zusätzliche Logik auszuführen, die nicht direkt mit der Bedingung und dem Rückgabewert zusammenhängt.

### Weiterführende Literatur/Links

- [Clean Code: A Handbook of Agile Software Craftsmanship](https://www.amazon.com/dp/0132350882)
- [JavaScript: The Good Parts](https://www.amazon.com/dp/0596517742)

## Richtiges Verwenden von Platzhaltern beim Logging mit SLF4J

Beim Logging mit SLF4J ist es wichtig, die Platzhalter-Zeichen korrekt zu verwenden und nicht mit den Platzhaltern von String.Format zu verwechseln.

### Problem

SLF4J bietet Platzhalter für das Einfügen von Werten in Log-Nachrichten. Die Platzhalter werden jedoch manchmal mit den Platzhaltern von String.Format verwechselt, was zu unerwartetem Verhalten oder sogar Fehlern führen kann.

```java
String name = "John";
int age = 30;
log.info("Name: %s, Age: %d", name, age);
String.format("Name: %s, Age: %d", name, age);
```

### Refactoring

Zu beachten ist, dass Platzhalter die geschweiften Klammer sind und die Reihenfolge der Platzhalter mit der Reihenfolge der Variablen übereinstimmt.
Das Logging für Exceptions erfordert keinen Platzhalter, wenn das Objekt der Exception als letzter Parameter für das Logging übergeben wird.

```java
String name = "John";
int age = 30;
log.info("Name: {}, Age: {}", name, age);

try {}
catch (Exception ex) {
    log.error("Error foo because of bla.", ex);

    log.error("Error {} because of bla.", name, ex);
}

```

### Vorteile

- Klarheit und Konsistenz bei der Verwendung von Platzhaltern in Log-Nachrichten
- Vermeidung von Verwechslungen mit den Platzhaltern von String.Format
- Bessere Lesbarkeit und Verständlichkeit des Codes

### Weiterführende Literatur/Links

- [SLF4J Documentation](http://www.slf4j.org/manual.html)
- [Best Practices for Logging in Java](https://stackify.com/best-practices-logging-java/)

## Rückgabe von nur unveränderlichen (immutable) Objekten in Java-Methoden

Es ist eine bewährte Praxis, dass Methoden in Java nur unveränderliche (immutable) Objekte zurückgeben sollten. Dadurch wird sichergestellt, dass der Zustand des zurückgegebenen Objekts nicht versehentlich geändert werden kann.

### Problem

Wenn eine Methode ein veränderliches (mutable) Objekt zurückgibt, besteht das Risiko, dass der Aufrufer unerwartet den Zustand des Objekts ändert. Dies kann zu unvorhersehbarem Verhalten und Fehlern führen.

```java
public List<String> getNames() {
    return new ArrayList<>(names);
}
```

### Refactoring

Um sicherzustellen, dass Methoden nur unveränderliche Objekte zurückgeben, sollten unveränderliche Implementierungen wie z.B. `Collections.unmodifiableList` oder das Kopieren der Daten in ein neues Objekt verwendet werden.

```java
public List<String> getNames() {
    return Collections.unmodifiableList(names);
}
```

### Vorteile

- Vermeidung unerwarteter Seiteneffekte durch Änderungen des zurückgegebenen Objekts
- Sicherstellung der Integrität der Daten und des Zustands
- Bessere Wartbarkeit und Testbarkeit des Codes

### Ausnahmen

Es kann Situationen geben, in denen die Rückgabe eines veränderbaren Objekts erforderlich oder sinnvoll ist, z. B. bei einer bewussten Verwendung von Builder-Patterns oder Mutable Objects. In solchen Fällen ist es wichtig, dies in der Dokumentation der Methode deutlich zu kennzeichnen und die Risiken und Vorteile zu erläutern.

### Weiterführende Literatur/Links

- [Effective Java: Item 15 - Minimize Mutability](https://www.amazon.com/dp/0321356683)
- [Immutable Objects in Java](https://www.baeldung.com/java-immutable-object)

## Klassen sollten interne Objekte nur über spezielle Methoden veränderbar machen

Es ist eine bewährte Praxis, dass Klassen in Java ihre internen Objekte nur über spezielle Methoden veränderbar machen sollten und nicht direkt als Felder extern zugreifbar machen sollten. Dadurch wird die Kontrolle über den Zustand und das Verhalten der Klasse verbessert.

### Problem

Wenn interne Objekte einer Klasse direkt als öffentliche Felder zugänglich sind, besteht die Gefahr, dass der Zustand der Klasse unkontrolliert geändert wird. Dies kann zu Inkonsistenzen, unerwartetem Verhalten und schwer zu findenden Fehlern führen.

```java
public class MyClass {
    public List<String> names;

    // ...
}
```

### Refactoring

Um die Kontrolle über den Zustand der Klasse zu verbessern, sollten die internen Objekte als [protected Felder](#attribute-nur-mit-protected-sichtbarkeit-versehen) deklariert und über spezielle Methoden zugänglich gemacht werden.

```java
public class MyClass {
    protected List<String> names;

    public List<String> getNames() {
        return Collections.unmodifiableList(names);
    }

    public void addName(String name) {
        names.add(name);
    }

    // ...
}
```

### Vorteile

- Verbesserte Kontrolle über den Zustand und das Verhalten der Klasse
- Vermeidung unerwünschter Seiteneffekte und unvorhersehbarer Änderungen
- Bessere Wartbarkeit, Testbarkeit und Erweiterbarkeit des Codes

### Ausnahmen

Es kann Situationen geben, in denen der direkte Zugriff auf interne Objekte notwendig ist, z. B. in Performance-kritischen Anwendungen oder wenn spezielle Anforderungen dies erfordern. In solchen Fällen ist es wichtig, die Risiken und Vorteile klar zu dokumentieren und sorgfältig zu evaluieren.

### Weiterführende Literatur/Links

- [Effective Java: Item 16 - Favor Composition over Inheritance](https://www.amazon.com/dp/0321356683)
- [Encapsulation in Java](https://www.baeldung.com/java-encapsulation)

## Methoden/Funktionen sollten niemals null zurückgeben, sondern immer eine leere Liste, HashMap oder Array

Es ist eine bewährte Praxis in Java und JavaScript, dass Methoden/Funktionen, die Listen, Hashmaps oder Arrays zurückgeben, niemals null zurückgeben sollten. Stattdessen sollte immer eine leere Liste, HashMap oder ein leeres Array zurückgegeben werden.

> Alternativ kann auch [Verwendung von Optional als Funktionswert](#verwendung-von-optional-als-funktionswert) angewendet werden.

### Problem

Das Zurückgeben von null als Ergebnis einer Methode/Funktion, die eine Liste, HashMap oder ein Array zurückgibt, kann zu NullPointerExceptions und unerwartetem Verhalten führen. Es erfordert zusätzliche Überprüfungen auf null und erhöht die Komplexität des Aufrufercodes.

```java
public List<String> getNames() {
    if (condition) {
        return null;
    }
    // ...
}
```

### Refactoring

Um NullPointerExceptions und unerwartetes Verhalten zu vermeiden, sollten Methoden/Funktionen stattdessen eine leere Liste, HashMap oder ein leeres Array zurückgeben.

```java
public List<String> getNames() {
    if (condition) {
        return Collections.emptyList();
    }
    // ...

    return ObjectUtils.defaultIfNull(list, Collections.emptyList());
}
```

### Vorteile

- Vermeidung von NullPointerExceptions und unerwartetem Verhalten
- Einfachere Handhabung und weniger Überprüfungen auf null im Aufrufercode
- Verbesserte Robustheit und Stabilität des Codes

### Ausnahmen

Es kann Situationen geben, in denen die Rückgabe von null sinnvoll ist, z. B. wenn null einen speziellen Zustand oder eine Bedeutung hat. In solchen Fällen ist es wichtig, die Risiken und Vorteile sorgfältig abzuwägen und die Entscheidung angemessen zu dokumentieren.

### Weiterführende Literatur/Links

- [Effective Java: Item 54 - Return Empty Arrays or Collections, Not Nulls](https://www.amazon.com/dp/0321356683)
- [Null or Empty Collection in Java](https://www.baeldung.com/java-null-empty-collection) (für Java)
- [Avoiding Null in JavaScript](https://dmitripavlutin.com/avoid-null-undefined-javascript/) (für JavaScript)

## Verwendung von `computeIfAbsent` und `putIfAbsent` für HashMaps in Java

Es ist eine bewährte Praxis, die Methoden `computeIfAbsent` und `putIfAbsent` für HashMaps in Java zu verwenden. Diese Methoden bieten eine sicherere und effizientere Möglichkeit, Werte zu einem Schlüssel hinzuzufügen, wenn der Schlüssel nicht vorhanden ist.

### Problem

Bei der Arbeit mit HashMaps in Java besteht das Risiko von Race Conditions oder unerwarteten Überschreibungen von Werten, wenn mehrere Threads gleichzeitig auf die HashMap zugreifen und Werte hinzufügen möchten.

```java
HashMap<String, List<String>> map = new HashMap<>();

// Unerwünschtes Überschreiben von Werten bei gleichzeitigem Zugriff
if (!map.containsKey(key)) {
    map.put(key, new ArrayList<>());
}
map.get(key).add(value);
```

### Refactoring

Die Verwendung von `computeIfAbsent` und `putIfAbsent` löst die oben genannten Probleme und bietet eine sichere und effiziente Möglichkeit, Werte zu einem Schlüssel hinzuzufügen, wenn der Schlüssel nicht vorhanden ist.

```java
HashMap<String, List<String>> map = new HashMap<>();

// Verwendung von computeIfAbsent
map.computeIfAbsent(key, k -> new ArrayList<>()).add(value);

// Verwendung von putIfAbsent
var defaultList = new ArrayList<>();
// ...
map.putIfAbsent(key, defaultList);
// return value of putIfAbsent returns last value which may be null.
defaultList.add(value);
```

### Vorteile

- Vermeidung von Race Conditions und unerwarteten Überschreibungen von Werten in HashMaps
- Einfachere und sicherere Handhabung beim Hinzufügen von Werten zu einem Schlüssel, wenn der Schlüssel nicht vorhanden ist
- Verbesserte Effizienz und Lesbarkeit des Codes

### Nachteile

- `computeIfAbsent` und `putIfAbsent` verhalten sich unterschiedlich in Bezug auf den Rückgabewert. `putIfAbsent` liefert als Rückgabe den vorherigen Wert, während `computeIfAbsent` den berechneten (computed) zurückgibt. Damit ist es mit `computeIfAbsent` möglich einen Wert mit `add` sofort hinzuzufügen, während dies mit `putIfAbsent` nicht funktioniert.

### Weiterführende Literatur/Links

- [HashMap computeIfAbsent() method in Java with examples](https://www.geeksforgeeks.org/hashmap-computeifabsent-method-in-java-with-examples/)
- [HashMap putIfAbsent(key, value) method in Java with examples](https://www.geeksforgeeks.org/hashmap-putifabsentkey-value-method-in-java-with-examples/)

## Verwendung von `com.machinezoo.noexception` in Callbacks wie z.B. `forEach` in Java

Es ist eine bewährte Praxis in Java, die Bibliothek `com.machinezoo.noexception` zu verwenden, um die Verwendung von `try-catch`-Blöcken in Callback-Funktionen wie `forEach` zu reduzieren. Durch die Verwendung dieser Bibliothek wird der Code sauberer und lesbarer, da die Ausnahmebehandlung von Callbacks elegant behandelt wird.

### Problem

Bei der Verwendung von Callback-Funktionen wie `forEach` in Java besteht die Notwendigkeit, Ausnahmen innerhalb des Callbacks zu behandeln. Dies führt zu zusätzlichem Code und erhöht die Komplexität, insbesondere wenn mehrere Ausnahmen behandelt werden müssen.

```java
List<String> list = Arrays.asList("apple", "banana", "cherry");

try {
    list.forEach(item -> {
        try {
            // Operationen, die eine Ausnahme werfen können
            // ...
        } catch (Exception e) {
            // Ausnahmebehandlung
            // ...
        }
    });
} catch (Exception e) {
    // Ausnahmebehandlung
    // ...
}
```

### Refactoring

Durch die Verwendung von `com.machinezoo.noexception` kann die Ausnahmebehandlung in Callback-Funktionen eleganter gehandhabt werden. Die Bibliothek bietet verschiedene Hilfsmethoden an, um Ausnahmen in Callbacks zu behandeln, ohne dass zusätzliche `try-catch`-Blöcke erforderlich sind.

```java
import com.machinezoo.noexception.Exceptions;

List<String> list = Arrays.asList("apple", "banana", "cherry");

list.forEach(Exceptions.sneak().consumer(item -> {
    // Operationen, die eine Ausnahme werfen können
    // ...
}));
```

### Vorteile

- Reduzierung des Boilerplate-Codes durch die Verwendung von `com.machinezoo.noexception`
- Sauberer und lesbarer Code ohne zusätzliche `try-catch`-Blöcke in Callback-Funktionen
- Bessere Trennung von Geschäftslogik und Ausnahmebehandlung

### Nachteile

- Einführung einer zusätzlichen Abhängigkeit durch die Verwendung von `com.machinezoo.noexception`
- Erhöhte Komplexität des Codes durch die Verwendung von Hilfsmethoden

### Ausnahmen

Es kann Situationen geben, in denen die Verwendung von `com.machinezoo.noexception` nicht angemessen ist, z. B. wenn das Projekt bereits eine andere Lösung für die Behandlung von Ausnahmen verwendet oder wenn die Einführung einer zusätzlichen Abhängigkeit vermieden werden soll.

### Weiterführende Literatur/Links

- [com.machinezoo.noexception - GitHub](https://github.com/robertvazan/com.machinezoo.noexception)
- [Avoiding Exceptions in Callbacks](https://dzone.com/articles/avoiding-exceptions-in-callbacks)
