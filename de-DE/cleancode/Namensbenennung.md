# Namensbenennung in der Programmierung

## Einführung

Die Benennung ist ein großes Problem in der Programmierung.
Namen sollten dem Leser helfen, den Code zu verstehen, und nicht verwirren.
Nur durch eine konsistente Namensgebung wird der Code leichter lesbar und verständlicher.

## Allgemeine Regel

1. Namen sollten so kurz wie möglich und so lang wie nötig sein.
2. Abkürzungen sollten vermieden werden. Auch ein erklärender Kommentar macht es nicht besser.
3. Namen sollten so gewählt werden, dass sie den Zweck der Variablen klar und präzise beschreiben.
4. Je globaler eine Variable ist (Funktion, Klasse, statische Klasse, global), desto besser sollte der Name gewählt sein.
5. Namen, wenn einmal gewählt, sollten nicht geändert werden, um Konstanz zu gewährleisten.

## Variablen

### Einige Entitäten, die in Variablen stecken, sind selbserklärend

Variablen wie Age oder Year sind selbsterklärend und benötigen keinen Typen-Suffix.
Es kann Ausnahmen geben, wenn das Alter in Monaten oder Tagen angegeben wird.
Dann sollte es besser als AgeInMonths oder AgeInDays benannt werden.
Zeiteinheiten sollten immer angegeben werden, statt showDelay sollte beispielweise showDelayInMilliseconds oder showDelayInSeconds verwendet werden.

### Namen für die Anzahl von Elementen

Variablen sollten einen Prä- oder Suffix haben, wie numberOf<Thing> oder <Thing>Count, wie in numberOfCars oder carCount.

### Fließkommazahlen

Variablen mit Fließkommawerten kommt nicht so oft vor wie Variablen mit Ganzzahlen.
Entsprechend kann es bei ihrer Auswertung zu Problemen kommen, wenn ihr Wert beispielsweise einen direkten Vergleich unterzogen wird.
* Die Variable sollte daher mit einem Suffix Amount wie beispielweise rainFallAmount angegeben werden.
* Geldbeträge sollten immer in Cent und als Ganzzahl angegeben werden, um Probleme mit Rundungsfehlern zu vermeiden.
* Wenn die Einheit der Fließkommazahl nicht offensichtlich ist, sollte sie im Namen angegeben werden, wie in rainFallAmountInMillimeters.

#### Positiv
* rainFallAmount
* rainFallAmountInMillimeters
* widthInCentimeters
* angleInDegrees
* energyConsumptionInKilowattHours
* waterUsageAmountInLiters
* oxygenLevelAmountInPercent
* stressLevelAmountInCortisolUnits
* pollutionAmountInPartsPerMillion
* verticalSpeedAmountInMetersPerSecond
* accelerationAmountInMetersPerSecondSquared

#### Negativ
* rainFall
* width
* angle
* money
* degree
* energy
* waterUsage
* oxygenLevel
* stressLevel
* pollution
* verticalSpeed

### Boolean

Variablen, die einen boolschen Wert enthalten, sollten mit einem Präfix wie is, has, can oder should beginnen, beispielsweise isEnabled, hasChildren, canPlay oder shouldClose.
Sie sollten nicht mit einem passiven Verb beginnen, wie in enabled, sondern mit einem aktiven Verb, wie in isEnabled.

Werte sollten immer positiv formuliert sein.

#### Positiv
* isEnabled
* hasChildren
* canPlay
* shouldClose
* containsText
* wasFound
* willBeShown
* doesExist
* didSucceed
* allowsMultiple

#### Negativ
* enabled
* children
* played
* closed


### Strings

### Enum/Aufzählungen

### Array, Listen, Sets

### Maps

### Pairs, Tuples

### Objekte

### Optionale Werte

### Funktionsvariablen (Callbacks)

### Klasseneigenschaften (Properties)

### statische Klassenvariable

Variablen, die in einer Klasse als statisch deklariert sind, sollten den Standardregeln folgen.
Dass eine Variable statisch ist, ist leicht daran zu erkennen, dass ihr Zugriff über den Klassennamen erfolgt.

### finale statische Klassenvariablen

Variablen, die in einer Klasse als statisch und final deklariert sind, sollten in Großbuchstaben geschrieben werden, mit Unterstrichen als Trennzeichen (KEBAB_CASE), wie in MAX_TIMEOUT_IN_SECONDS oder DEFAULT_TIMEOUT_IN_MILLISECONDS.

#### Positiv
* MAX_TIMEOUT_IN_SECONDS
* DEFAULT_TIMEOUT_IN_MILLISECONDS

#### Negativ
* maxTimeoutInSeconds
* defaultTimeoutInMilliseconds

## Klassennamen

## Interface-Namen

## spezielle Präfixe

Einige Frameworks, insbesondere in der Webentwicklung, verwenden spezielle Präfixe, um den Zweck einer Variablen zu kennzeichnen. In Vue wird $ für öffentliche Variablen und _ für private Variablen verwendet.
Dies soll zudem dem Entwickler mitteilen, dass die Variable von außerhalb stammt und nicht aus dem aktuellen Kontext stammt.


## Abkürzungen



Beispiele