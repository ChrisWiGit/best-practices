# VueJs 2 Best Practises und Design Patterns

<!-- TOC -->

- [VueJs 2 Best Practises und Design Patterns](#vuejs-2-best-practises-und-design-patterns)
  - [Allgemein](#allgemein)
  - [Vermeiden der Verwendung von v-if mit v-for-Elementen](#vermeiden-der-verwendung-von-v-if-mit-v-for-elementen)
  - [Verwenden von Computed-Property zur Filterung von Daten](#verwenden-von-computed-property-zur-filterung-von-daten)
  - [Verwenden von :key-Attribut mit v-for](#verwenden-von-key-attribut-mit-v-for)
  - [Verwenden der Kebab-Schreibweise, um Ereignisse zu benennen](#verwenden-der-kebab-schreibweise-um-ereignisse-zu-benennen)
  - [Verwenden der Kebab- oder Pascal-Schreibweise, um Komponenten zu erstellen](#verwenden-der-kebab--oder-pascal-schreibweise-um-komponenten-zu-erstellen)
  - [Prop-Namen mit Camel-Case im Template und Kebab-Case im Script-Tag](#prop-namen-mit-camel-case-im-template-und-kebab-case-im-script-tag)
  - [Die Daten einer Komponente sollten als Funktion zurückgegeben werden](#die-daten-einer-komponente-sollten-als-funktion-zurückgegeben-werden)
  - [Scoping der Komponentenstile](#scoping-der-komponentenstile)

<!-- /TOC -->

## Allgemein

## Vermeiden der Verwendung von v-if mit v-for-Elementen

### Problem

Bei der Verwendung von Vue.js besteht die Versuchung, die Direktiven v-if und v-for zusammen zu verwenden, um Daten bedingt zu rendern. Diese Kombination kann jedoch zu Performance-Problemen und unerwartetem Verhalten führen.

```html
<!-- Falsch -->
<ul>
  <li v-for="item in items">
    <span v-if="item.isActive">>{{ item.name }}</span>
  </li>
</ul>
```

### Refactoring

Es ist empfehlenswert, die Verwendung von v-if mit v-for zu vermeiden und stattdessen die Daten vor dem Rendern zu filtern.

```html
<ul>
  <li v-for="item in activeItems">{{ item.name }}</li>
</ul>
```

```javascript
computed: {
  activeItems() {
    return this.items.filter(item => item.isActive);
  }
}
```

### Vorteile

- Bessere Performance, da die Filterung vor dem Rendern erfolgt.
- Verbesserte Lesbarkeit des Codes, da die Absicht klarer ist.
- Vermeidung von unerwartetem Verhalten, das durch die Kombination von v-if und v-for entstehen kann.

### Ausnahmen

Es gibt Fälle, in denen die Verwendung von v-if mit v-for sinnvoll sein kann, z. B. wenn komplexe bedingte Logik auf einzelnen Elementen basiert. In solchen Situationen sollten Sie jedoch sicherstellen, dass die Performance-Auswirkungen minimiert sind.

### Weiterführende Literatur/Links

- [Vue.js Dokumentation - v-if](https://vuejs.org/v2/guide/conditional.html#v-if)
- [Vue.js Dokumentation - v-for](https://vuejs.org/v2/guide/list.html#v-for)
- [Vue.js Style Guide - Avoid v-if with v-for](https://vuejs.org/v2/style-guide/#Avoid-v-if-with-v-for)

## Verwenden von Computed-Property zur Filterung von Daten

### Problem

Bei der Entwicklung mit Vue.js müssen häufig Daten gefiltert werden, um nur bestimmte Teile anzuzeigen. Es gibt verschiedene Ansätze, dies zu erreichen, aber die Verwendung einer Computed-Property ist eine bewährte Methode, um sauberen und effizienten Code zu schreiben.

```javascript
// Falsch
data() {
  return {
    items: [...],
    filter: 'active'
  };
},
computed: {
  filteredItems() {
    if (this.filter === 'active') {
      return this.items.filter(item => item.isActive);
    } else if (this.filter === 'completed') {
      return this.items.filter(item => item.isCompleted);
    } else {
      return this.items;
    }
  }
}
```

### Refactoring

Es ist empfehlenswert, eine Computed-Property zu verwenden, um die Daten zu filtern und das Ergebnis zu speichern. Dadurch wird der Code lesbarer und ermöglicht eine einfache Aktualisierung der Filterlogik.

```javascript
// Richtig
data() {
  return {
    items: [...],
    filter: 'active'
  };
},
computed: {
  filteredItems() {
    switch (this.filter) {
      case 'active':
        return this.items.filter(item => item.isActive);
      case 'completed':
        return this.items.filter(item => item.isCompleted);
      default:
        return this.items;
    }
  }
}
```

### Vorteile

- Verbesserte Lesbarkeit des Codes durch Verwendung einer Computed-Property zur Filterung.
- Einfache Aktualisierung der Filterlogik, da sie zentralisiert in der Computed-Property definiert ist.
- Effiziente Ausführung, da die Computed-Property nur bei Änderungen der abhängigen Daten neu berechnet wird.

### Ausnahmen

In einigen Fällen kann die Verwendung einer Computed-Property zur Filterung von Daten nicht erforderlich sein, wenn die Filterlogik einfach ist und keine weiteren Abhängigkeiten besteht. In solchen Fällen können Sie die Filterung auch direkt in Methoden oder Vorlagen durchführen.

### Weiterführende Literatur/Links

- [Vue.js Dokumentation - Computed Properties](https://vuejs.org/v2/guide/computed.html)
- [Vue.js Style Guide - Use Computed Properties](https://vuejs.org/v2/style-guide/#Use-computed-properties)

## Verwenden von :key-Attribut mit v-for

### Problem

Bei der Verwendung der `v-for`-Direktive in Vue.js zur Darstellung von Listen ist es wichtig, jedem gerenderten Element ein eindeutiges `:key`-Attribut zuzuweisen. Dieses Attribut dient als eindeutiger Identifikator für Vue, um effizientere Updates und Re-Rendering von Elementen durchzuführen.

```html
<!-- Falsch -->
<ul>
  <li v-for="item in items">
    {{ item.name }}
  </li>
</ul>
```

### Refactoring

Um das Problem zu lösen, sollte immer das `:key`-Attribut mit `v-for` verwendet werden und ein eindeutiger Schlüsselwert für jedes Element bereitgestellt werden. Dies kann beispielsweise die ID oder einen anderen eindeutigen Wert aus den Daten darstellen.

```html
<!-- Richtig -->
<ul>
  <li v-for="item in items" :key="item.id">
    {{ item.name }}
  </li>
</ul>
```

### Vorteile

- Effizientes Rendering und Aktualisierung von Listen durch Verwendung des `:key`-Attributs.
- Bessere Performance bei der Aktualisierung von Elementen in der Liste.
- Vermeidung von Fehlern und unerwartetem Verhalten durch eindeutige Identifikatoren für Elemente.

### Nachteile

- Wenn kein eindeutiger Schlüsselwert für jedes Element vorhanden ist, kann es schwierig sein, Updates korrekt durchzuführen und unerwartetes Verhalten kann auftreten.

### Ausnahmen

In seltenen Fällen, in denen die Liste nicht aktualisiert wird oder die Reihenfolge der Elemente nicht wichtig ist, kann das `:key`-Attribut weggelassen werden. Dies sollte jedoch nur in spezifischen Fällen erfolgen und mit Bedacht eingesetzt werden.

### Weiterführende Literatur/Links

- [Vue.js Dokumentation - Listen-Rendering mit v-for](https://vuejs.org/v2/guide/list.html)
- [Vue.js Style Guide - Keyed v-for](https://vuejs.org/v2/style-guide/#Keyed-v-for)

## Verwenden der Kebab-Schreibweise, um Ereignisse zu benennen

### Problem

Bei der Arbeit mit Ereignissen in Vue.js, wie dem Auslösen oder Zuhören von Ereignissen, ist es eine bewährte Praxis, Kebab-Schreibweise für die Benennung von Ereignissen zu verwenden. Dies hat mit der "HTML-Attribute-Groß-/Kleinschreibung" zu tun.

```html
<template>
  <button @click="HandleClick">Klick mich</button>
</template>
```

### Refactoring

Um das Problem zu beheben, sollten Ereignisse mit Kebab-Schreibweise benannt werden. Dies erleichtert das Zuhören von Ereignissen in den Vorlagen und vermeidet potenzielle Probleme mit der Groß-/Kleinschreibung von HTML-Attributen.

```html
<template>
  <button @click="handleClick">Klick mich</button>
</template>
```

### Vorteile

- Einheitliche Benennung von Ereignissen in der Vue.js-Anwendung.
- Vermeidung von potenziellen Problemen mit der Groß-/Kleinschreibung von HTML-Attributen.
- Bessere Lesbarkeit und Verständlichkeit des Codes.

### Ausnahmen

Es gibt keine spezifischen Ausnahmen, in denen von der Verwendung von Kebab-Schreibweise für die Benennung von Ereignissen abgewichen werden sollte. Es wird jedoch empfohlen, sich an diese Best Practice zu halten, um eine einheitliche und konsistente Codebasis zu gewährleisten.

### Weiterführende Literatur/Links

- [Vue.js Dokumentation - Event Handling](https://vuejs.org/v2/guide/events.html)
- [Vue.js Style Guide - Event Names](https://vuejs.org/v2/style-guide/#Event-names)

## Verwenden der Kebab- oder Pascal-Schreibweise, um Komponenten zu erstellen

### Problem

Bei der Erstellung von Komponenten in Vue.js ist es wichtig, eine konsistente und eindeutige Schreibweise für die Komponentennamen zu verwenden. Eine klare Namenskonvention erleichtert das Lesen und Verstehen des Codes.

```html
<!-- Falsch -->
<template>
  <myComponent></myComponent>
</template>
```

### Refactoring

Um das Problem zu lösen, sollten bei der Erstellung von Komponenten in Vue.js entweder Kebab-Schreibweise oder Pascal-Schreibweise verwendet werden. Beide Schreibweisen haben sich in der Vue.js-Community etabliert.
Der Dateiname sollte genaus heißen wie die Komponente in PascalCase.

`MyComponent.vue`

```html
<!-- Richtig (Kebab-Schreibweise) -->
<template>
  <my-component></my-component>
</template>
```

`MyComponent.vue`

```html
<!-- Richtig (Pascal-Schreibweise) -->
<template>
  <MyComponent></MyComponent>
</template>
```

### Vorteile

- Konsistente und eindeutige Namensgebung für Komponenten.
- Verbesserte Lesbarkeit und Verständlichkeit des Codes.
- Einfache Autocompletion von Komponentennamen.

### Ausnahmen

Es gibt keine spezifischen Ausnahmen, in denen von der Verwendung von Kebab- oder Pascal-Schreibweise für Komponentennamen abgewichen werden sollte. Es wird jedoch empfohlen, sich an eine konsistente Namenskonvention zu halten, um die Lesbarkeit des Codes zu verbessern.

### Weiterführende Literatur/Links

- [Vue.js Style Guide - Component Names](https://vuejs.org/v2/style-guide/#Component-names)

## Prop-Namen mit Camel-Case im Template und Kebab-Case im Script-Tag

### Problem

Bei der Verwendung von Propertys (Props) in Vue.js, die an Komponenten übergeben werden, ist es wichtig, eine konsistente Namenskonvention für Props zu verwenden. Dies erleichtert das Lesen und Verstehen des Codes.

```html
<template>
  <my-component :myProperty="data"></my-component>
</template>
```

### Refactoring

Um das Problem zu lösen, sollten Propertys in Vue.js mit der Kebab-Schreibweise benannt werden. Dies ist eine weit verbreitete Konvention in der Vue.js-Community.
Die Propertys im Script Tag werden mit camelCase benannt,

```html
<template>
  <my-component :my-property="data"></my-component>
</template>

<script>
export default {
  props: {
    myProperty: String,
  },
}
</script>
```

### Vorteile

- Konsistente Namensgebung für Props.
- Verbesserte Lesbarkeit und Verständlichkeit des Codes.
- Einfache Autocompletion von Prop-Namen.

### Ausnahmen

Es gibt keine spezifischen Ausnahmen, in denen von der Verwendung von Camelcase für die Schreibweise von Prop-Namen abgewichen werden sollte. Es wird jedoch empfohlen, sich an diese Best Practice zu halten, um eine einheitliche Codebasis zu gewährleisten.

### Weiterführende Literatur/Links

- [Vue.js Dokumentation - Komponenten-

Props](<https://vuejs.org/v2/guide/components-props.html>)

## Die Daten einer Komponente sollten als Funktion zurückgegeben werden

### Problem

Bei der Deklaration von Daten in Vue.js-Komponenten ist es wichtig, eine Funktion zu verwenden, um die Daten zurückzugeben, anstatt ein Objekt direkt zu verwenden. Dies gewährleistet, dass jede Instanz der Komponente ihre eigenen Daten hat und Änderungen an den Daten einer Instanz nicht die Daten anderer Instanzen beeinflussen.

```javascript
// Falsch
export default {
  data: {
    count: 0
  }
}
```

### Refactoring

Um das Problem zu lösen, sollten die Daten einer Vue.js-Komponente als Funktion zurückgegeben werden. Auf diese Weise wird sichergestellt, dass jede Instanz der Komponente ihre eigenen Daten hat.

```javascript
// Richtig
export default {
  data() {
    return {
      count: 0
    }
  }
}
```

### Vorteile

- Jede Instanz der Komponente hat ihre eigenen Daten.
- Verhindert unerwartete Nebeneffekte durch gemeinsam genutzte Daten.
- Bessere Skalierbarkeit und Wiederverwendbarkeit von Komponenten.

### Nachteile

- Es gibt keine direkten Nachteile bei der Verwendung einer Funktion zur Rückgabe von Komponentendaten.

### Ausnahmen

Es gibt keine spezifischen Ausnahmen, in denen von der Verwendung einer Funktion zur Rückgabe von Komponentendaten abgewichen werden sollte. Es wird jedoch empfohlen, sich an diese Best Practice zu halten, um unerwartete Verhaltensweisen zu vermeiden.

### Weiterführende Literatur/Links

- [Vue.js Dokumentation - Komponenten-Daten](https://vuejs.org/v2/guide/components.html#data-Must-Be-a-Function)

## Scoping der Komponentenstile

### Problem

Bei der Arbeit mit CSS-Stilen in Vue.js-Komponenten ist es wichtig, die Stile so zu scopen, dass Änderungen an einem bestimmten Stil nur die Komponente selbst betreffen und nicht auf andere Teile der Anwendung durchsickern.

```html
<!-- Falsch -->
<template>
  <div class="my-component">
    <h1 class="heading">My Component</h1>
  </div>
</template>

<style>
.my-component {
  background-color: #f2f2f2;
}

.heading {
  font-size: 24px;
}
</style>
```

### Refactoring

Um das Problem zu lösen, sollten die Stile einer Vue.js-Komponente gescopet werden. Dies kann durch die Verwendung des `scoped`-Attributs im `<style>`-Block erreicht werden.

```html
<!-- Richtig -->
<template>
  <div class="my-component">
    <h1 class="heading">My Component</h1>
  </div>
</template>

<style scoped>
.my-component {
  background-color: #f2f2f2;
}

.heading {
  font-size: 24px;
}
</style>
```

### Vorteile

- Verhindert Stilüberschreibungen und Konflikte mit anderen Komponenten oder globalen Stilen.
- Einfache Wartung und Aktualisierung von Komponentenstilen.
- Bessere Kapselung und Isolation von Komponenten.

### Nachteile

- Bei der Verwendung des `scoped`-Attributs kann es zu einer erhöhten Spezifität der CSS-Selektoren kommen, was die Verwendung von `!important`-Regeln erforderlich machen kann.

### Ausnahmen

Es gibt bestimmte Fälle, in denen das Scoping von Komponentenstilen möglicherweise nicht erforderlich oder sinnvoll ist. Zum Beispiel, wenn globale Stile für die gesamte Anwendung benötigt werden oder wenn spezifische Anpassungen an den Stilen von Drittanbieter-Komponenten erforderlich sind.

### Weiterführende Literatur/Links

- [Vue.js Dokumentation - Komponentenstile](https://vuejs.org/v2/guide/components.html#Scoped-Styles)

### Best Practise: Rufen Sie keine Methode in created und watch auf

#### Problem

Ein häufiger Fehler, den Vue-Entwickler machen, ist das unnötige Aufrufen einer Methode in den Lifecycle-Hooks `created` und `watch`. Der Gedanke dahinter ist, dass der Watcher-Hook sofort ausgeführt werden soll, sobald eine Komponente initialisiert wird. Dabei kann die Logik jedoch oft anders strukturiert werden.

```javascript
export default {
  export default {
   created: () {
    this.handleChange()
   },
   methods: {
    handleChange() {
     // stuff happens
    }
   },
   watch () {
    property() {
     this.handleChange()
    }
   }
  }
}
```

#### Refactoring

Um dieses Problem zu beheben, kann die Logik so umstrukturiert werden, dass die Methodenaufrufe in `created` und `watch` vermieden werden. Stattdessen sollten die Methoden direkt aufgerufen werden, wenn sie benötigt werden.

```javascript
export default {
  created: () {
    this.handleChange()
  },
  methods: {
    handleChange() {
    // stuff happens
  }
  },
  watch () {
    property() {
      this.handleChange()
    }
  }
}
}
```

#### Vorteile

- Verbesserte Klarheit und Lesbarkeit des Codes.
- Vermeidung unnötiger Methodenaufrufe in den Lifecycle-Hooks.
- Bessere Organisation der Logik in den entsprechenden Methoden.

#### Nachteile

- Keine direkten Nachteile bei der Anwendung dieser Best Practise.

#### Ausnahmen

Es gibt Fälle, in denen ein Methodenaufruf in `created` oder `watch` erforderlich sein kann, z.B. wenn bestimmte Initialisierungen oder Datenabrufe direkt beim Start der Komponente erfolgen sollen.

#### Weiterführende Literatur/Links

- [Vue.js Dokumentation - Lifecycle-Hooks](https://vuejs.org/v2/guide/instance.html#Lifecycle-Diagram)

### Best Practise: Template-Ausdrücke sollten nur einfache JavaScript-Ausdrücke enthalten

#### Problem

Es ist natürlich, so viel Funktionalität wie möglich in unsere Templates einzubauen. Jedoch führt dies dazu, dass unsere Templates weniger deklarativ und komplexer werden. Dadurch wird unser Template sehr unübersichtlich.

```html
<template>
  <div>
    {{ fullName.toUpperCase().split(' ')[0] }} is {{ age > 18 ? 'adult' : 'minor' }}
  </div>
</template>
```

#### Refactoring

Um dieses Problem zu lösen, sollten wir komplexe JavaScript-Ausdrücke aus unseren Template-Ausdrücken entfernen und stattdessen auf die Verwendung von Methoden und berechneten Eigenschaften zurückgreifen.

```html
<template>
  <div>
    {{ getFirstName() }} is {{ getAgeCategory() }}
  </

div>
</template>

<script>
export default {
  methods: {
    getFirstName() {
      return this.fullName.toUpperCase().split(' ')[0];
    },
    getAgeCategory() {
      return this.age > 18 ? 'adult' : 'minor';
    },
  },
}
</script>
```

#### Vorteile

- Verbesserte Lesbarkeit und Verständlichkeit des Templates.
- Trennung von Logik und Darstellung.
- Einfachere Wartung und Erweiterbarkeit des Codes.

#### Ausnahmen

Es gibt Situationen, in denen komplexe Ausdrücke in den Template-Ausdrücken akzeptabel sein können, insbesondere wenn es sich um einfache, nicht wiederverwendbare Logik handelt und die Verwendung von Methoden oder berechneten Eigenschaften unnötig komplex erscheint.

#### Weiterführende Literatur/Links

- [Vue.js Dokumentation - Template-Syntax](https://vuejs.org/v2/guide/syntax.html)
