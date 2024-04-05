# Testing and Documentation
Das Ziel dieses Projekts ist es, alle geschriebene Klassen **vollständig zu testen und zu dokumentieren**. Durch die Entwicklung von Microservices wird ein Onlineshop modelliert. Das folgende Schema wird dies etwas näher erläutern:

![Testing](images/testing.jpg)

## Technologie:
- Spring MVC & Spring Reactive
- Spring Security & OAuth2 & Keycloak
- PostgreSQL & Reactive MongoDB
- AsciiDoc & OpenAPI & Swagger
- Mock & JUnit & Testcontainers
- Lombok & Thymeleaf & Devtools

# Microservice:

- ## Keycloak

Keycloak ist ein Open-Source-Identity- und Access-Management-System, das Login-Funktionalität bietet. Es ermöglicht die Verwaltung von Benutzern, die Authentifizierung und Autorisierung von Benutzerzugriffen auf verschiedene Anwendungen und Dienste sowie die Integration von externen Identitätsanbietern.

Um einen Keycloak-Container zu erstellen, können Sie den folgenden Befehl verwenden:
```
docker run --name shopping4you-keycloak -p 8082:8080 -e KEYCLOAK_USER=admin -e KEYCLOAK_PASSWORD=admin quay.io/keycloak/keycloak:23.0.7
```
Dieser Befehl erstellt einen Container mit dem Namen "shopping4you-keycloak", der den Keycloak-Server auf Port 8082 (externer Port) und Port 8080 (Container-Port) startet. Die Umgebungsvariablen KEYCLOAK_USER und KEYCLOAK_PASSWORD werden verwendet, um das Administratorkonto von Keycloak zu konfigurieren. Sie können diese Werte entsprechend Ihren Anforderungen ändern.

#### Einloggen und Realm erstellen

Um sich bei Keycloak einzuloggen und den erstellten Realm "shopping2" auszuwählen, können Sie wie folgt vorgehen:

1. Öffnen Sie einen Webbrowser und navigieren Sie zur Adresse [http://localhost:8082/auth/admin](http://localhost:8082/auth/admin).
2. Geben Sie den Benutzername und das Passwort ein, die Sie beim Starten des Keycloak-Containers festgelegt haben (in diesem Fall sind es "admin" und "admin"). 
3. Klicken Sie auf den Dropdown-Menü neben dem aktuellen Realm-Namen (normalerweise "master") in der oberen linken Ecke der Seite.
4. Wählen Sie "Add realm" aus und geben Sie "shopping2" als Namen des neuen Realms ein und klicken Sie auf "Create" oder "Erstellen". 
5. Klicken Sie auf "Add user" und geben Sie die erforderlichen Informationen für den Benutzer ein.
6. Weitere Informationen zu Keycloak finden Sie unter [Link zur weiteren Information](https://www.keycloak.org/documentation).

- ## Manager-app:

Mithilfe von Thymeleaf wird eine UI für die Steuerung des Katalogs bereitgestellt. Sie ermöglicht das Erstellen, Ändern und Löschen von Waren.

- ## Customer-app:

Mithilfe von Thymeleaf wird eine UI für das Anschauen von Waren aus dem Katalog bereitgestellt. Sie ermöglicht das Erstellen von Feedback wie Bewertungen und Benotungen sowie das Hinzufügen und Löschen von Lieblingswaren(Einkaufskorb).

- ## Catalogue-service:

REST-API zum Speichern von Waren aus dem Katalog mithilfe von PostgreSQL.
Um einen PostgreSQL-Container mithilfe von Docker zu erstellen, verwenden Sie den folgenden Befehl:
```
docker run --name catalogue-db -p 5433 -e POSTGRES_USER=postgre -e POSTGRES_PASSWORD=12345678 -e POSTGRES_DB=shopping2 postgres:16
```
Diese Version weist darauf hin, dass Sie das Passwort und den Benutzernamen entsprechend Ihren Anforderungen ändern müssen, und empfiehlt, dass Sie diese Änderungen auch in der `application-standalone.yaml` -Datei des Microservices vornehmen.

#### Das Aufrufen der Catalogue-Service-Endpunkte mit der Hilfe von Swagger:
```
http://localhost:8081/swagger-ui/index.html
```
Um Swagger zu verwenden, müssen Sie einen neuen Client mit der Client-ID "catalogue-service-swagger-ui" in Keycloak erstellen und ihm die Rolle "ROLE_MANAGER" zuweisen.

- ## Feedback-service

Der Feedback-Service ermöglicht das Speichern und Steuern von Bewertungen und Benotungen sowie das Hinzufügen und Löschen von Waren in den Favoriten (ähnlich wie der Warenkorb in einem Online-Shop). Alle Daten werden in MongoDB gespeichert.
Um einen MongoDB-Container zu erstellen, können Sie den folgenden Befehl verwenden:
```
docker run --name feedback-db -p 27017:27017 mongo:7
```

# Dokumentation für den Feedback-Service

Die Dokumentation für den Feedback-Service wurde mithilfe des Asciidoctor-Maven-Plugins erstellt, das Snippets verwendet, um die relevanten Informationen über die API-Endpunkte, Anfragen und Antworten sowie andere Details zu generieren.

Um sicherzustellen, dass die Dokumentation korrekt ist, wurde am Ende des Erstellungsprozesses `maven verify` ausgeführt.

Die vollständige Dokumentation ist [hier](feedbackDocumentation.html) verfügbar. (feedbackDocumentation.html)

# Testen

Um das Testprotokoll einzusehen, klicken Sie [hier](test.log). (test.log)



