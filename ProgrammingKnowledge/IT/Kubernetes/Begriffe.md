
# Day1 vs Day2 Deployments

**Day1** = Wenn ein Cluster das erste Mal aufgesetzt wird.
**Day2** = Laufendes Update eines Cluster bzw. der Container -> ist um einiges schwieriger als Day1

# Blue/Green Deployment

**Blue–green Deployment** ist eine Methode im Bereich der Softwareentwicklung, um Änderungen an einem Web-, App- oder Datenbankserver durch den Wechsel zwischen Produktions- und Staging-Servern zu installieren. Hier sind die wichtigsten Punkte:

1. **Blue–green Deployment**: Bei dieser Methode werden zwei Server aufrechterhalten: ein “blauer” Server und ein “grüner” Server. Zu jedem Zeitpunkt bearbeitet nur ein Server Anfragen (z. B. über DNS). Der blaue Server ist der Produktions-Server, während der grüne Server nur über ein privates Netzwerk zugänglich ist und als Staging-Server fungiert. Änderungen werden auf dem nicht aktiven Server installiert und über das private Netzwerk getestet. [Sobald die Änderungen erfolgreich verifiziert wurden, wird der nicht aktive Server mit dem aktiven Server ausgetauscht, wodurch die Änderungen live werden](https://en.wikipedia.org/wiki/Blue%E2%80%93green_deployment)[1](https://en.wikipedia.org/wiki/Blue%E2%80%93green_deployment).
    
2. **Vorteile**:
    
    - **Schnelles Rollback**: Falls etwas schief geht, kann einfach der Verkehr auf den vorherigen Live-Server umgeleitet werden, der die Änderungen noch nicht enthält.
    - [**Minimale Ausfallzeit**: Da Anfragen sofort von einem Server zum anderen umgeleitet werden, entsteht idealerweise keine Phase, in der Anfragen nicht erfüllt werden können](https://en.wikipedia.org/wiki/Blue%E2%80%93green_deployment)[1](https://en.wikipedia.org/wiki/Blue%E2%80%93green_deployment).
3. **Ursprung**: Die Methode wurde von Dan North und Jez Humble entwickelt, die während ihrer Arbeit mit Oracle WebLogic Server Unterschiede zwischen Testumgebungen und der Produktionsumgebung feststellten. Sie führten eine Methode ein, bei der die neue Anwendungsversion neben dem Live-System bereitgestellt wurde. Dies ermöglichte gründliche Tests und einfaches Rollback bei Problemen. Die Farbnamen “blau” und “grün” wurden gewählt, um eine Hierarchie zu vermeiden. [Diese Konvention wurde später in der Branche weit verbreitet](https://en.wikipedia.org/wiki/Blue%E2%80%93green_deployment)[2](https://en.wikipedia.org/wiki/Main_Page).
    

[Die Blue–green-Methode wird oft mit der Canary-Release-Methode verglichen und weist Ähnlichkeiten mit A/B-Tests auf](https://en.wikipedia.org/wiki/Blue%E2%80%93green_deployment)[1](https://en.wikipedia.org/wiki/Blue%E2%80%93green_deployment)[.](https://en.wikipedia.org/wiki/Blue%E2%80%93green_deployment)[2](https://en.wikipedia.org/wiki/Main_Page)


# Canary Deployment

Ein **Canary-Update** ist eine Technik im Bereich der Softwareentwicklung, bei der eine neue Version einer Anwendung zunächst nur an eine kleine Teilmenge der Benutzer oder in eine spezifische Umgebung ausgerollt wird. [Währenddessen bleibt der Großteil des Datenverkehrs auf der stabilen Version](https://canariasacross.com/blog/canary-update-kubernetes-the-ultimate-guide-to-ensuring-smooth-deployments)[1](https://canariasacross.com/blog/canary-update-kubernetes-the-ultimate-guide-to-ensuring-smooth-deployments). Hier sind die wichtigsten Punkte:

1. **Canary-Deployment**: Bei dieser Methode wird die neue Version schrittweise an einen kleinen Benutzerkreis ausgeliefert. Die Infrastruktur in der Zielumgebung wird in kleinen Phasen aktualisiert (z. B. 2%, 25%, 75%, 100%). [Ein Canary-Release ist im Vergleich zu anderen Bereitstellungsmethoden das risikoärmste Vorgehen, da es eine präzise Kontrolle ermöglicht](https://www.harness.io/blog/blue-green-canary-deployment-strategies)[2](https://www.harness.io/blog/blue-green-canary-deployment-strategies).
    
2. **Vorteile**:
    
    - **Geringes Risiko**: Durch die schrittweise Aktualisierung wird das Risiko minimiert.
    - [**Benutzerfeedback**: Die ausgewählte Benutzergruppe kann die Änderungen testen und Feedback geben, bevor sie auf alle Benutzer ausgerollt werden](https://canariasacross.com/blog/canary-update-kubernetes-the-ultimate-guide-to-ensuring-smooth-deployments)[2](https://www.harness.io/blog/blue-green-canary-deployment-strategies).
3. **Herkunft**: Die Bezeichnung “Canary” stammt von der Praxis, in Bergwerken Kanarienvögel mitzunehmen. Diese Vögel reagierten empfindlich auf giftige Gase. Wenn der Vogel krank wurde oder starb, wussten die Bergleute, dass die Luftqualität schlecht war. [Ähnlich dient das Canary-Update als Frühwarnsystem für mögliche Probleme in der neuen Version](https://canariasacross.com/blog/canary-update-kubernetes-the-ultimate-guide-to-ensuring-smooth-deployments)[1](https://canariasacross.com/blog/canary-update-kubernetes-the-ultimate-guide-to-ensuring-smooth-deployments).
    

[Die Canary-Methode wird oft mit der Blue-Green-Deployment-Methode verglichen und weist Ähnlichkeiten mit A/B-Tests auf](https://canariasacross.com/blog/canary-update-kubernetes-the-ultimate-guide-to-ensuring-smooth-deployments)[2](https://www.harness.io/blog/blue-green-canary-deployment-strategies).

#Kubernetes