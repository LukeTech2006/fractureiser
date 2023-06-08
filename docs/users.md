# Leitfaden für modifizierte Spieler

Wenn du **nur** Vanilla über einen vertrauenswürdigen Launcher spielst, wie den offiziellen Launcher oder
Prism spielst und noch nie Mods benutzt hast, bist du 100% sicher. Haltet euch sich vorerst von Mods fern.

Wenn du ein moddded-Minecraft-Spieler bist, musst du überprüfen, ob du von der
fractureiser-Malware infiziert wurdest, um sicherzustellen, dass dein Rechner und deine persönlichen Daten nicht gefährdet sind. Das kannst du mit Hilfe dieses Dokuments tun.

Zusätzliche Informationen darüber, was zu tun ist, wenn du infiziert bist oder nicht, findest du nach den Diagnoseschritten.

## Was ist eigentlich passiert?

Eine Reihe von Curseforge- und dev.bukkit.org-Konten (nicht die Bukkit-Software selbst) wurden kompromittiert, und bösartige Software wurde in Kopien vieler beliebter Plugins und Mods injiziert. Einige dieser bösartigen Kopien wurden in beliebte Modpacks wie Better Minecraft eingeschleust. *Es gibt Berichte über bösartige Plugin/Mod-JARs, die bereits Mitte April veröffentlicht wurden.

Diese Malware besteht aus mehreren "Stufen", wobei jede Stufe für das Herunterladen und Ausführen der nächsten Stufe verantwortlich ist.
und Ausführen der nächsten Stufe. Insgesamt sind drei Stadien bekannt (Stadium 1, 2 und 3),
wobei infizierte Mod-Dateien als "Phase 0" dienen, um den gesamten Prozess in Gang zu setzen.

Stufe 3 ist das "Superhirn" der Malware, und wir haben Beweise dafür, dass sie versucht, alles Folgende zu tun:

* sich auf *alle* `jar`-Dateien im Dateisystem auszubreiten und möglicherweise Mods zu infizieren, die
  die nicht von CurseForge oder BukkitDev heruntergeladen wurden, oder andere Java-Programme
* Stehlen von Cookies und Anmeldeinformationen für viele Webbrowser
* Ersetzen von Kryptowährungsadressen in der Zwischenablage durch Alternativen, die vermutlich dem Angreifer gehören
* Stehlen von Discord-Anmeldeinformationen
* Stehlen von Microsoft- und Minecraft-Anmeldeinformationen

(Siehe [technische Details](tech.md) für weitere Informationen)

Aufgrund seines Verhaltens sind wir **sehr zuversichtlich**, dass es sich um einen **gezielten Angriff gegen das modifizierte Minecraft-Ökosystem** handelt. Es ist ziemlich schlimm.

**Bis auf weiteres sollten Sie beim Herunterladen von Minecraft-Mods extreme Vorsicht walten lassen, unabhängig von der Herkunft.
Während der Kontrollserver für diese Malware derzeit offline ist, **ist jeder
Download von Curseforge oder dem Bukkit-Plugin-Repository in den letzten 2-3 Wochen als
als potentiell bösartig behandelt werden**. Einige Malware-Scanner haben begonnen, Signaturen
in ihre Datenbanken aufzunehmen, aber bis dies bei allen der Fall ist, sollten Sie Vorsicht walten lassen.

*Zum jetzigen Zeitpunkt können wir nicht mit Sicherheit behaupten, dass kein Hosting-Dienst betroffen ist. Bitte
Vorsicht walten lassen, unabhängig davon, welche Seite du nutzt. Auch Maven-Repositories können infiziert sein,
und diese Malware reicht potenziell Monate zurück.

Derzeit sind neue Infektionen unmöglich, da der Server des Angreifers abgeschaltet wurde,
Bestehende Infektionen können jedoch noch aktiv sein.

### Was ist eine Stufe?

![](media/stages.png)

### Wie kann ich das reparieren?

![Flowchart](media/flowchart.png)

## Bin ich infiziert?

Die Malware hat mehrere Stufen, so dass die Frage, ob Sie infiziert sind, eigentlich aus zwei Fragen besteht.

### Ist eine meiner Mod-Dateien mit Stufe 0 infiziert?
Es gibt eine Reihe von Scannern, die anhand einer Mod-Datei feststellen, ob sie mit der Stufe 0 der Malware infiziert ist.

- Overwolfs [Scanner](https://github.com/overwolf/jar-infection-scanner/releases)
- cortex's [nekodetector](https://github.com/MCRcortex/nekodetector/releases) (klicke auf "Assets", um die Binärdatei anzuzeigen)

### Befinden sich Dateien der Stufe 2 auf meinem System?

Wenn sich Dateien der Stufe 2 auf deinem System befinden, bedeutet das, dass Stufe 0 und 1 der Malware erfolgreich ausgeführt wurden.

Viele Virenscanner beginnen, Dateien der Stufe 2 zu erkennen. Wenn du eine Warnung erhältst, dass solche
Dateien gefunden und entfernt wurden, fahre mit dem Abschnitt "Ich bin infiziert, was nun?" fort.

Andernfalls kannst du je nach Plattform wie folgt manuell prüfen:

#### Windows Anleitung

* Öffne dein Startmenü mit der Windows-Taste und gib "%localappdata%" ein - so sollte es erscheinen:
![Suchergebnisse für die obige Abfrage](media/localappdata.png)

* Im Ordner Local appdata musst du sicherstellen, dass dein Explorer so eingestellt ist, dass er sowohl "Versteckte Elemente" als auch "Geschützte Betriebssystemdateien" anzeigt. 
  * Dies kannst du über Ansicht > Optionen tun.
  * Wenn du dir nicht sicher bist, wie das geht, findest du eine Videoerklärung [hier] (https://youtu.be/KLTlTlnXeKs).


* Finde einen Ordner mit dem Namen "Microsoft Edge". Die Leerstelle zwischen "Microsoft" und "Edge" ist
  wichtig - denn `MicrosoftEdge` ist ein legitimer Ordner, der von Edge verwendet wird.  Der Virus
  hat ihn einfach so benannt, um sich zu tarnen.  Der legitime Ordner könnte auch
  Der legitime Ordner könnte auch "Microsoft Edge" heißen (ein "Edge"-Ordner innerhalb eines "Microsoft"-Ordners).
* Wenn `Microsoft Edge` vorhanden ist, wurdest du infiziert. Wenn dies der Fall ist, lösche den Ordner und alles, was sich darin befindet, endgültig.
  * Wenn der Ordner nicht gelöscht werden kann, musst du alle Java-Programme, die gerade laufen, über den Task-Manager stoppen.

#### Linux Anleitung

Vergewissere dich zunächst, dass die Methode, die du zum Auflisten von Dateien verwendest, die Möglichkeit bietet, versteckte Dateien anzuzeigen. Die meisten GUI-Dateimanager haben die Tastenkombination Strg+H, um versteckte Dateien anzuzeigen. Wenn du dies über ein Terminal machst, benutze `ls -A` in den entsprechenden Verzeichnissen oder `ls -lha` für eine detailliertere Auflistung.

Wenn eine der folgenden Dateien vorhanden ist, wurdest du infiziert. Wenn das der Fall ist, lösche sie alle:
* `~/.config/systemd/user/systemd-utility.service`
* `/etc/systemd/system/systemd-utility.service`
* `~/.config/.data/lib.jar`

Überprüfe danach, falls zutreffend, dein `journalctl` auf alle Änderungen, die du vielleicht nicht erkennst. Du kannst dies mit den Befehlen `journalctl -exb` (für Systemprotokolle) und `journalctl -exb --user` (für Benutzerprotokolle) tun. Führe die folgenden Befehle aus, um deine systemd-Dienste zu aktualisieren:
```sh
sudo systemctl daemon-reload # Gib dein Benutzerpasswort ein
systemctl --user daemon-reload 
```

#### MacOS Informationen

Die Malware scheint sich nicht auf MacOS auszuwirken, du solltest also keine Probleme haben. *Sieh in Zukunft in diesem Dokument nach, wenn sich das ändert*

#### Skripte

*Wenn du nicht weißt, wie man ein PowerShell- oder Bash-Skript ausführt, ist dies nichts für dich.  
Automatisierte PowerShell- oder Bash-Skripte sind auch [auf der PrismLauncher
Website](https://prismlauncher.org/news/cf-compromised-alert/#automated-script) verfügbar, die
für Stage 2 zu überprüfen, wenn du das technische Know-how hast, sie auszuführen. Overwolf (die Muttergesellschaft von Curseforge)
Muttergesellschaft) hat auch ein Tool zur Erkennung von C# Stage 2 veröffentlicht:
https://github.com/overwolf/detection-tool

## Ich bin infiziert, was nun?

**WICHTIG**: Wir kennen derzeit weder das volle Ausmaß dessen, was es anrichten kann, noch was es bezweckt. Daher ist äußerste Vorsicht geboten, bis ein vollständiger Weg zur Beseitigung aller Symptome gefunden wurde. Alles, was hier steht, ist nur *was wir wissen* - bitte behalte die Kommunikation des Teams im Auge, um Updates zu erhalten, wenn etwas Kritisches gefunden wird.

Wenn du Dateien der Stufe 2 von Fractureiser auf deinem System findest, ist deine beste Option jetzt
davon auszugehen, dass alles auf dem System *völlig kompromittiert* ist. Du solltest:

* Sichere alles, was du nicht verlieren willst, auf einem Flash-Laufwerk oder einer externen Festplatte (das solltest du sowieso regelmäßig tun!)
* Ändere auf einem anderen Gerät die Passwörter für alle Dienste, bei denen du auf dem alten Rechner angemeldet warst
  dem alten Rechner angemeldet warst (Discord, E-Mail usw.). Verwende dazu am besten einen Passwortmanager wie
  [BitWarden](https://bitwarden.com).
* Wenn du noch nicht die Zwei-Faktor-Authentifizierung (Authenticator-App oder SMS) für alle Dienste, die sie unterstützen, benutzt hast, fang bitte sofort damit an.
* Wenn du dazu in der Lage bist, wende dich an einen professionellen Dienst in deiner Nähe, der deinen Rechner auf
  Diagnose deines Rechners auf verdächtige Dinge oder lösche das System und installiere es neu.
  und installiere das System neu.
* Lies den folgenden Abschnitt darüber, was zu tun ist, wenn du nicht infiziert bist, denn die Schritte dort gelten auch für dich.

## Ich bin nicht infiziert, was nun?

Das absolut Sicherste, was du im Moment tun kannst, ist, Minecraft **überhaupt nicht zu starten**. Ja, sogar Vanilla. 

Das heißt, wenn zunächst nichts gefunden wurde, ist wahrscheinlich auch nichts passiert.
Wenn du das Spiel trotzdem spielen willst:

* Nach unserem derzeitigen Kenntnisstand ist das nicht riskant, aber wir können nicht garantieren, dass dies der Fall ist - du setzt dich *willentlich einem Risiko aus*.
* Überprüfe nach jeder Sitzung die Infektionsdateien im vorherigen Schritt, um sicherzustellen, dass nichts passiert ist, seit
* Lade unter **keinen Umständen** Mods, Modpacks oder Plugins herunter oder aktualisiere sie, die du verwendest, oder führe sie aus, die du heruntergeladen und noch nie ausgeführt hast - bleib bei den Instanzen, die du bereits verwendet hast, und zwar **ausschließlich**