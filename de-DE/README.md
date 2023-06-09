# Entwicklung - Best Practices
<!-- TOC -->

- [Entwicklung - Best Practices](#entwicklung---best-practices)
  - [Themen](#themen)
  - [Begriffsdefinition](#begriffsdefinition)
  - [Allgemeines Code-Refactoring](#allgemeines-code-refactoring)

<!-- /TOC -->

## Themen

Die speziellen Themen sind hier zu finden:

- [Java](java/README.md)
- [JavaScript](javascript/README.md)
- [Vue 2](vuejs/README.md)
<!-- [scss/css](scss/README.md)-->

## Begriffsdefinition

### Code Refactoring

Code Refactoring bezieht sich auf den Prozess der Überarbeitung von vorhandenem Code, um dessen interne Struktur zu verbessern, ohne dabei das externe Verhalten zu ändern. Das Hauptziel des Refactorings besteht darin, den Code lesbarer, verständlicher und leichter wartbar zu machen. 
Es beinhaltet das Umstrukturieren des Codes, um ihn effizienter, besser organisiert und robuster zu gestalten. 
Dabei werden Code-Duplikate entfernt, komplexe Teile vereinfacht, Code-Standards angepasst und die Code-Qualität verbessert.

> Es ist wichtig zu beachten, dass Refactoring kein Zwang ist, sondern eine empfohlene Praxis, um die Qualität des Codes im Laufe der Zeit kontinuierlich zu verbessern.

### Best Practices (Beste Vorgehensweisen)

Best Practices sind bewährte Methoden oder Techniken, die in der Softwareentwicklung angewendet werden, um qualitativ hochwertigen und effizienten Code zu schreiben. Sie repräsentieren bewährte Ansätze und Lösungen für häufig auftretende Probleme oder Herausforderungen. Best Practices helfen dabei, den Entwicklungsprozess zu verbessern, die Code-Qualität zu steigern und potenzielle Fehler oder Probleme zu vermeiden. Sie basieren auf Erfahrungen, bewährten Methoden und Industriestandards und dienen als Richtlinien für Entwickler, um bessere Software zu entwickeln.

### Design Patterns (Entwurfsmuster)

Design Patterns sind bewährte Lösungsansätze für häufig auftretende Probleme in der Softwareentwicklung. Sie bieten allgemeine Lösungen, die in bestimmten Situationen angewendet werden können, um den Entwurfsprozess zu erleichtern und die Wiederverwendbarkeit, Flexibilität und Erweiterbarkeit von Software zu verbessern. Design Patterns helfen Entwicklern, wiederkehrende Designprobleme zu identifizieren und bieten Lösungen in Form von abstrakten Mustern und Strukturen. Sie dienen als Baupläne für den Aufbau von Softwarekomponenten und fördern bewährte Entwurfsprinzipien wie die Trennung von Verantwortlichkeiten, die Erweiterbarkeit und die lose Kopplung von Komponenten.

> Es ist wichtig zu beachten, dass Design Patterns ebenfalls kein Zwang sind und nicht in jeder Situation angewendet werden müssen. Sie sind eher Empfehlungen, die je nach Anforderungen und Kontext angewendet werden können, um den Entwurfsprozess zu unterstützen und bewährte Lösungen anzubieten.

## Allgemeines Code-Refactoring

Code Refactoring (Code-Überarbeitung) ist der Prozess der Überarbeitung und Umstrukturierung des Quellcodes einer Software, um ihn effizienter, lesbarer und einfacher zu warten, ohne dabei das externe Verhalten der Anwendung zu ändern. Dabei werden technische Schulden abgebaut und die Codequalität verbessert.

1. **Code Refactoring als Teil der Programmierung**: Code Refactoring sollte als integraler Bestandteil der normalen Programmiertätigkeit betrachtet werden.

2. **Prüfung auf Code Smells**: Bevor du mit einer Aufgabe beginnst, sollte bestehender Code zunächst auf "Code Smells" geprüft werden. "Code Smells" sind Anzeichen in deinem Code, die auf tiefer liegende Probleme hinweisen können. Beispiele hierfür sind überlange Funktionen, verschachtelte Schleifen, globale Variablen und duplizierter Code. Durch das Identifizieren dieser "Code Smells" kannst du gezielt Verbesserungen vornehmen.

3. **Inkrementelles Refactoring**: Anstatt große Teile des Codes auf einmal zu ändern, ist es ratsam, kleine, schrittweise Änderungen vorzunehmen. Dies erleichtert das Finden und Beheben von Fehlern und hilft, den Überblick zu behalten.

4. **Anwendung von Best Practices während der Programmierung**: Die Durchführung der Programmiertätigkeit sollte immer unter Anwendung bewährter Methoden (Best Practices) erfolgen.

5. **Bewusstsein für Seiteneffekte**: Während des Refactorings ist es wichtig, sicherzustellen, dass dein Code noch immer das tut, was er soll. Änderungen, die unerwartete Seiteneffekte verursachen könnten, sollten mit Vorsicht behandelt werden. Teste deinen Code gründlich, um sicherzustellen, dass er immer noch korrekt funktioniert.

6. **Weiteres Refactoring nach Programmierung**: Nach der Durchführung der Programmiertätigkeit sollte ein weiteres Refactoring auf den geänderten Code angewendet werden, um ständige Verbesserungen zu gewährleisten.

7. **Dokumentation von Legacy-Code**: Bestehender Code, der bisher nicht dokumentiert wurde, sollte im Nachhinein auch nicht kommentiert werden. Dokumentation von Legacy-Code ist auch im Nachhinein kaum eine Hilfe, den Code zu verstehen, denn die Dokumentation kann veraltet, irreführend oder unverständlich sein. Beim Lesen von alten Code besteht die Gefahr, dass er falsch verstanden wird und die Dokumentation dadurch nutzlos und verwirrend wird. Vielmehr sollte alter Code selbst im Zuge eines Refactorings verbessert werden, damit er selbsterklärend ist und nur neue Dokumentation braucht.

8. **Kontinuierliche und sorgfältige Dokumentation für API-Benutzer**: Die Dokumentation des öffentlichen Schnittstellen sollte während des gesamten Programmierprozesses stattfinden, anstatt sie bis zum Ende zu verschieben, wo sie möglicherweise überhastet und unvollständig umgesetzt wird. Insbesondere beim öffentlich zugänglichen Teil des Codes, der API, sollte besonderer Wert auf Vollständigkeit und Verständlichkeit gelegt werden. Eine umfassende und klar strukturierte Dokumentation würdigt die Zeit der API-Benutzer und erleichtert ihnen die Arbeit erheblich. Beispiele können einen wertvollen Beitrag leisten, indem sie das Verständnis vertiefen und die Anwendung der API in verschiedenen Kontexten veranschaulichen. Es ist von entscheidender Bedeutung, dass die Dokumentation stets den aktuellen Entwicklungsstand widerspiegelt und keine veralteten oder falschen Informationen enthält.

9. **Dokumentation von internen Code**: Die Dokumentation von internen Code gestaltet sich einfacher als für Dokumentation von öffentlichen Schnittstellen. Es sollte zuallererst beachtet werden, dass der Code selbst erklärend ist, andernfalls muss er überarbeitet werden. Wenn der Code klein genug und verständlich ist, können Kommentare und Methoden-Dokumentation gespart werden, um so die Wahrscheinlichkeit von veralteter und irreführender Dokumentation zu verringern. Der Code spricht für sich selbst und dokumentiert sollte daher die Intention des Entwicklers, warum bestimmte Codestellen sich auf eine bestimmte Art und Weise verhalten. 
