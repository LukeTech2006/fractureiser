### Zeitleiste

Die Zeitachse verläuft von unten nach oben. Die Ereignisse ganz oben sind die jüngsten.

---
*2023-06-08 05:11 UTC*

Prospector kündigt das Folgende an:

> Ein Update von Modrinth, alle in den letzten 10 Monaten hochgeladenen Dateien
> (etwa die Hälfte unserer Dateien) wurden gescannt und keine einzige infizierte
> Datei wurde gefunden.

---
*2023-06-08 01:12 UTC*

Die Dinge haben sich größtenteils wieder beruhigt, Virenscanner haben begonnen, die Stage 1+
Jars als bösartig zu erkennen, und für den nächsten Morgen ist in den USA ein Treffen für die nächsten Schritte geplant.

Das Treffen wird halbprivat sein, aber Aufzeichnungen/Protokolle werden im Anschluss veröffentlicht.

CurseForge scannt alle Mods, aber dieser Prozess ist noch nicht abgeschlossen.

---
*2023-06-07 18:51 UTC*

Der zweite C&C-Server 107[.]189.3.101 wurde von seinem Hosting-Provider gesperrt

---
*2023-06-07 16:00 UTC* *2023-06-07 16:00 UTC*

Aufgrund einer Verzögerung im HackMD wurde dieses Dokument in das GitHub-Repository übertragen
https://github.com/fractureiser-investigation/fractureiser

---
*2023-06-07 14:40 UTC*

Die unverschleierte Stufe 3 wurde durch eine verschleierte ersetzt, dann weiter durch eine andere
Nutzlast.

Diese Nutzlast ist der Skyrage Updater, eine bekannte Minecraft-Malware, die auf Spigot
Server abzielt.

Nachdem er skyrage eine Zeit lang bedient hatte, wechselte er wieder zum gehackten Meteor-Client.

(TODO dieser Zeitrahmen ist nicht ganz korrekt)

---
*2023-06-07 14:20 UTC*

Die Analyse der neuen IP-Adresse ergab eine vollständig entschleierte Stufe 3, die anscheinend versehentlich hochgeladen wurde.
Sie wurde hier archiviert: https://github.com/clrxbl/NekoClient

---
*2023-06-07 14:19 UTC*

Die Domain der Cloudflare-Seiten wurde entfernt.

---
*2023-06-07 14:05 UTC* *2023-06-07 14:05 UTC*

Die Domain der Cloudflare-Seiten verweist jetzt auf eine neue IP-Adresse, 107.189.3.101.

---


*2023-06-07 08:52 UTC* *2023-06-07 08:52 UTC*

Der Staub hat sich vorerst weitgehend gelegt. Wir haben eine gute Vorstellung von den frühen Stadien der Malware, und Stadium 3 wird gerade zurückentwickelt. Die erste Stufe ist vorübergehend inaktiv.

Wir werden die Aktualisierungen am nächsten Morgen US-Zeit (oder so ähnlich) wieder aufnehmen.

----
*2023-06-07 08:09 UTC*

Wir arbeiten immer noch an der Umkehrung von Stufe 3, siehe den Abschnitt unten für technische Details.

----
*2023-06-07 07:37 UTC*

CurseForge hat folgendes Statement im #news channel ihres Discords veröffentlicht:

> Hey everyone,
> 
> We would like to address the current situation that is ongoing and highlight some important points:
> 
> * A malicious user has created several accounts and uploaded projects containing malware to the platform
> * Separately a user belonging to Luna Pixel Studios (LPS) was hacked and was used to upload similar malware
> * We have banned all accounts relevant to this and disabled the LPS one as well. We are in direct contact with the LPS team to help them restore their access
> * We are in the process of going through ALL new projects and files to guarantee your safety. We are of course <u>holding the approval process of all new files until this is resolved</u>
> * Deleting your CF client isn’t a recommended solution as it will not solve the issue and will prevent us from deploying a fix. We are working on a tool to help you make sure you weren’t exposed to any of this. In the meantime refer to information published in #current-issues.
> * This is relevant ONLY to Minecraft users
> * To be clear **CurseForge is not compromised! No admin account was hacked.**
>
> We are working on this to make sure the platform remains a safe place to download and share mods. Thank you to all authors and users who help us with highlighting, we appreciate your cooperation and patience ❤️ 
>
> Stay tuned for more updates and we will clear this issue.

----
*2023-06-07 07:24 UTC*

Darkhax hat sich mit Vertretern von Curseforge in Verbindung gesetzt, die bestätigt haben, dass die betroffenen Dateien über die Benutzeroberfläche hochgeladen wurden, nicht über die API.

Curseforge hat die Freigabe von Uploads gestoppt, während sich die Situation entwickelt, und hat viele infizierte Dateien heruntergenommen.

Sie untersuchen auch die IPs der Uploader der bösartigen Dateien, um zu sehen, ob sie mit früheren Anfragen der rechtmäßigen Kontoinhaber übereinstimmen.

----
*2023-06-07 7:03 UTC*

Wir glauben, dass wir die wahre Funktion von Stage3 (`client.jar`) entdeckt haben und versuchen, sie hier zu dokumentieren. Es ist nicht gut, Leute.

Die Kurzversion, während wir dieses Dokument in Form bringen: client.jar durchsucht *das gesamte Dateisystem* nach Dateien, die wie mod JARs aussehen, und infiziert sie mit Stage0. Dazu gehören *gesamte Gradle- und Maven-Caches*, sowie tonnenweise Dinge, die Mod-Entwickler wahrscheinlich nie überprüfen würden. Das potenzielle Ausmaß und der Umfang dieser Infektion hat sich von "ein paar seltsamen Mods" auf *potenziell unendlich* erhöht.

Wir glauben, dass sich die Infektion ursprünglich auf diese Weise verbreitet hat und dass Curseforge möglicherweise nicht der ursprüngliche Angriffsvektor gewesen ist.

----

*2023-06-07 6:27 UTC*

Die Untersuchungen haben sich verlangsamt und die meisten Mitglieder des Teams gehen schlafen. unascribed hat einen E-Mail-Posteingang eröffnet, an den Leute Proben oder andere nützliche Informationen senden können. williewillus arbeitet derzeit daran, die von D3SL vorgelegten Informationen zu bereinigen und in dieses Dokument aufzunehmen.

----

*2023-06-07 6:20 UTC*

D3SL teilt dem inoffiziellen Discord mit, dass sie eine Kopie der vollständigen (nicht gekürzten) Stage 3 `client.jar` sowie eine detaillierte Analyse der Malware haben. Sie haben dies bereits vor Wochen bemerkt und eine gründliche Analyse durchgeführt, wodurch sie in der Lage waren, vollständige Kopien aller Payloads zu erhalten.

----

*2023-06-07 5:27 UTC*

Wir haben eine potenzielle (gekürzte) Stage 3-Datei entdeckt; sie ist stark verschleiert und enthält eine native Nutzlast-DLL, die versucht, Anmeldeinformationen aus dem Windows-Anmeldeinformationsspeicher zu stehlen.

----

*2023-06-07 4:57 UTC*

Es wurden Dateien entdeckt, die im April hochgeladen wurden; entweder werden die Daten gefälscht, oder das Ganze dauert schon länger an. Viele der Accounts haben Last Active Zeiten im Jahr 1999 - wahrscheinlich eine Eigenart alter CurseForge Accounts, aber dennoch bemerkenswert.

Die Mitarbeiter von Modrinth untersuchen derzeit, ob irgendwelche Uploads dort kompromittiert sind. Ein schneller Durchlauf durch kürzlich aktualisierte Projekte sah OK aus.

----
    
*2023-06-07 4:40 UTC*

Das Ausmaß dieser Kompromittierung scheint größer zu sein als zunächst angenommen. Die bösartigen Dateien reichen mehrere Wochen zurück, sogar bis zum 20. Mai. Wir haben es erst heute bemerkt, weil sie ein beliebtes Modpack kompromittiert haben.

---

*2023-06-07 3:38 UTC*


Der C&C-Server wurde vom Server-Provider abgeschaltet. Ein neuer wird wahrscheinlich auftauchen, wenn die Cloudflare-Seite bestehen bleibt, wir beobachten sie.

----

*2023-06-07 3:26 UTC*

Wir haben ein mögliches Stage 2 jar von einem anonymen Benutzer erhalten, der behauptet, bei einem Server-Host zu arbeiten.

----

*2023-06-07 2:26 UTC*

Der #cfmalware EsperNet-Kanal wurde eingerichtet, um die Diskussionen zu koordinieren, die in verschiedenen Discord-Gilden und Matrix-Räumen stattfanden.

----

*2023-06-07 0:40 UTC*

Das Team hinter diesem Dokument erfährt von den bösartigen Dateien, die in einem nicht autorisierten Update für Better Minecraft enthalten sind.

----

*2023-06-01 bis 2023-06-04*

D3SL wird misstrauisch, weil die bösartigen Dateien CPU und RAM verbrauchen, und beginnt
Ermittlungen. Reihenfolge der Operationen:

1. Der Verdacht auf die Firewall-Anfrage der Java-Datei führt dazu, dass sie blockiert wird.
2. Die Unfähigkeit, selbst gehostete Dienste zu erreichen, führt zu einer Ereignisanzeige, die alle tcpip-Ports
   blockiert
3. Netstat zeigt massiven Portverbrauch über die PID der feindlichen jar-Datei an
4. Die Identifizierung der bösartigen javaw.exe, die libwebgl64.jar ausführt, bestätigt Malware

Von hier aus half Tzalumen beim anfänglichen Reverse Engineering
des byte[]-verschleierten Codes und der manuellen Erfassung eines kompletten Satzes von Dateien der Ziele.

Vollständige Kopien aller Originaldateien (einschließlich Entschlüsselung) mit Ausnahme von lib.dll, Übersetzungen von
Übersetzungen aller kontaktierten entfernten Ziele sowie ein Bericht über den Infektionsprozess und mehrere
feindlichen Fähigkeiten wurden über Kanäle an Windows Defender und
Malwarebytes übermittelt. Curseforge wurde ebenfalls benachrichtigt. Das Wissen über die Malware wurde nicht
wurde zu diesem Zeitpunkt nicht veröffentlicht, um die Angreifer nicht zu verraten.

----
