---

copyright:
  years: 2017, 2019
lastupdated: "2019-02-22"

keywords: IBM Cloud Container Registry CLI, container images, container registry commands, commands

subcollection: container-registry-cli-plugin

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:download: .download}

# {{site.data.keyword.registrylong_notm}}-CLI 
{: #containerregcli}

Mit der im CLI-Plug-in `container-registry` verfügbaren {{site.data.keyword.registrylong}}-CLI können Sie Ihre Registry und deren Ressourcen für Ihr {{site.data.keyword.Bluemix_notm}}-Konto verwalten.
{: shortdesc}

**Voraussetzungen**

* Installieren Sie die [Befehlszeilenschnittstelle von {{site.data.keyword.Bluemix_notm}}](/docs/cli?topic=cloud-cli-ibmcloud-cli#ibmcloud-cli). Bei der Ausführung von Befehlen mit der {{site.data.keyword.Bluemix_notm}}-CLI ist das Präfix `ibmcloud` zu verwenden.

* Melden Sie sich vor der Ausführung von Befehlen für die Registry bei {{site.data.keyword.Bluemix_notm}} mit dem Befehl `ibmcloud login` an, um ein Zugriffstoken zu generieren und Ihre Sitzung zu authentifizieren.

Wenn Aktualisierungen für die CLI `ibmcloud` und das CLI-Plug-in `container-registry` verfügbar sind, werden Sie in der Befehlszeile benachrichtigt. Achten Sie darauf, dass die CLI auf dem aktuellen Stand bleibt, damit Sie alle verfügbaren Befehle und Flags verwenden können.

Falls Sie die aktuelle Version Ihres CLI-Plug-ins `container-registry` anzeigen wollen, führen Sie den Befehl `ibmcloud plugin list` aus.

Informationen zur Verwendung der {{site.data.keyword.registrylong_notm}}-CLI enthält der Abschnitt [Einführung in {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-index#index).

Zusätzliche Angaben über die IAM-Plattform und die Servicezugriffsrollen, die für einige Befehle erforderlich sind, finden Sie unter [Benutzerzugriff mit Identity and Access Management verwalten](/docs/services/Registry?topic=registry-iam#iam).

Verwenden Sie in Ihren Container-Images, Namensbereichsnamen, Beschreibungsfeldern (z. B. in Registry-Tokens) oder Imagekonfigurationsdaten (z. B. Imagenamen oder Imagebezeichnungen) keine persönlichen Daten.
{:tip}

## `ibmcloud cr api`
{: #bx_cr_api}

Gibt die Details zu dem Registry-API-Endpunkt zurück, für den die Befehle ausgeführt werden.

```
ibmcloud cr api
```
{: codeblock}

**Voraussetzungen**

Keine

## `ibmcloud cr build`
{: #bx_cr_build}

Erstellt ein Docker-Image in {{site.data.keyword.registrylong_notm}}.

```
ibmcloud cr build [--no-cache] [--pull] [--quiet | -q] [--build-arg SCHLÜSSEL=WERT ...] [--file DATEI | -f DATEI] --tag TAG VERZEICHNIS
```
{: codeblock}

**Voraussetzungen**

Informationen zu den erforderlichen Berechtigungen finden Sie im Abschnitt [Zugriffsrollen für die Verwendung von {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam#access_roles_using).

**Befehlsoptionen**
<dl>
<dt>`VERZEICHNIS`</dt>
<dd>Die Position des Buildkontextes, der Ihre Dockerfile und die vorausgesetzten Dateien enthält. Falls als Speicherposition des Buildkontextes Ihr Arbeitsverzeichnis festgelegt ist, wenn Sie den Befehl ausführen, können Sie `VERZEICHNIS` durch einen Punkt (.) ersetzen.</dd>
<dt>`--no-cache`</dt>
<dd>(Optional) Bei Angabe dieses Parameters werden in diesem Build keine zwischengespeicherten Imageebenen aus vorherigen Builds verwendet.</dd>
<dt>`--pull`</dt>
<dd>(Optional) Bei Angabe dieses Parameters werden die Basisimages selbst dann extrahiert, wenn auf dem Build-Host bereits ein Image mit einem übereinstimmenden Tag vorhanden ist.</dd>
<dt>`--quiet`, `-q`</dt>
<dd>(Optional) Bei Angabe dieses Parameters wird die Buildausgabe unterdrückt, sofern kein Fehler auftritt.</dd>
<dt>`--build-arg SCHLÜSSEL=WERT`</dt>
<dd>(Optional) Geben Sie ein zusätzliches Buildargument im Format `'SCHLÜSSEL=WERT'` an. Zur Angabe von mehreren Buildargumenten kann dieser Parameter mehrfach angegeben werden. Der Wert jedes Buildarguments ist als Umgebungsvariable verfügbar, wenn Sie eine ARG-Zeile angeben, die mit dem Schlüssel in Ihrer Dockerfile übereinstimmt.</dd>
<dt>`--file DATEI`, `-f DATEI`</dt>
<dd>(Optional) Falls Sie für mehrere Builds dieselben Dateien verwenden, können Sie einen Pfad zu einer anderen Dockerfile auswählen. Geben Sie die Position der Dockerfile bezogen auf den Buildkontext an. Falls Sie keine Angabe machen, ist `PFAD/Dockerfile` der Standardwert; hierbei steht PFAD für das Stammverzeichnis des Buildkontextes.</dd>
<dt>`--tag TAG`, `-t TAG`</dt>
<dd>Der vollständige Name für das Image, das Sie erstellen möchten. Hierzu gehören die Registry-URL und der Namensbereich.</dd>
</dl>

**Beispiel**

Mit dem folgenden Befehl wird ein Build für ein Docker-Image erstellt, der keinen Build-Cache aus vorherigen Builds verwendet, bei dem die Buildausgabe unterdrückt wird, der Tag *`registry.ng.bluemix.net/birds/bluebird:1`* lautet und als Verzeichnis das Arbeitsverzeichnis verwendet wird.

```
ibmcloud cr build --no-cache --quiet --tag registry.ng.bluemix.net/birds/bluebird:1 .
```
{: pre}

## `ibmcloud cr exemption-add`
{: #bx_cr_exemption_add}

Erstellt eine Freistellung für ein Sicherheitsproblem. Sie können für ein Sicherheitsproblem eine Freistellung erstellen, die für unterschiedliche Geltungsbereiche gilt. Geltungsbereich kann das Konto, der Namensbereich, das Repository oder der Tag sein.

```
ibmcloud cr exemption-add --scope GELTUNGSBEREICH --issue-type PROBLEMTYP --issue-id PROBLEM-ID
```
{: codeblock}

**Voraussetzungen**

Informationen zu den erforderlichen Berechtigungen finden Sie im Abschnitt [Zugriffsrollen für die Konfiguration von {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam#access_roles_configure).

**Befehlsoptionen**
<dl>
<dt>`--scope GELTUNGSBEREICH`</dt>
<dd>Wenn Sie Ihr Konto als Geltungsbereich festlegen möchten, verwenden Sie `"*"` als Wert. Um einen Namensbereich, ein Repository oder einen Tag als Geltungsbereich festzulegen, geben Sie den Wert in einem der folgenden Formate ein: `namensbereich`, `namensbereich/repository`, `namensbereich/repository:tag`.
</dd>
<dt>`--issue-type PROBLEMTYP`</dt>
<dd>Der Typ des Sicherheitsproblems, für das Sie eine Freistellung definieren wollen. Gültige Problemtypen können Sie durch Ausführung des Befehls `ibmcloud cr exemption-types` ermitteln.
</dd>
<dt>`--issue-id PROBLEM-ID`</dt>
<dd>Die ID des Sicherheitsproblems, für das Sie eine Freistellung definieren wollen. Zur Ermittlung einer Problem-ID führen Sie den Befehl `ibmcloud cr va <image>` aus; hierbei steht *&lt;image&gt;* für den Namen Ihres Images. Verwenden Sie dann den relevanten Wert entweder aus der Spalte **Vulnerability ID** (Sicherheitslücken-ID) oder der Spalte **Configuration Issue ID** (Konfigurationsproblem-ID).
</dd>
</dl>

**Beispiele**

Der folgende Befehl erstellt eine CVE-Freistellung für die CVE-ID `CVE-2018-17929` für alle Images im Repository `registry.ng.bluemix.net/birds/bluebird`.

```
ibmcloud cr exemption-add --scope registry.ng.bluemix.net/birds/bluebird --issue-type cve --issue-id CVE-2018-17929
```
{: pre}

Der folgende Befehl erstellt eine kontoweite CVE-Freistellung für die CVE-ID `CVE-2018-17929`.

```
ibmcloud cr exemption-add --scope "*" --issue-type cve --issue-id CVE-2018-17929
```
{: pre}

Der folgende Befehl erstellt eine Konfigurationsproblemfreistellung für das Problem `application_configuration:nginx.ssl_protocols` für ein einzelnes Image mit dem Tag `registry.ng.bluemix.net/birds/bluebird:1`.

```
ibmcloud cr exemption-add --scope registry.ng.bluemix.net/birds/bluebird:1 --issue-type configuration --issue-id application_configuration:nginx.ssl_protocols
```
{: pre}

## `ibmcloud cr exemption-list` (`ibmcloud cr exemptions`)
{: #bx_cr_exemption_list}

Listet Ihre Freistellungen für Sicherheitsprobleme auf.

```
ibmcloud cr exemption-list [--scope GELTUNGSBEREICH]
```
{: codeblock}

**Voraussetzungen**

Informationen zu den erforderlichen Berechtigungen finden Sie im Abschnitt [Zugriffsrollen für die Konfiguration von {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam#access_roles_configure).

**Befehlsoptionen**
<dl>
<dt>`--scope GELTUNGSBEREICH`</dt>
<dd>(Optional) Listet ausschließlich die Freistellungen für diesen Geltungsbereich auf. Um einen Namensbereich, ein Repository oder einen Tag als Geltungsbereich festzulegen, geben Sie den Wert in einem der folgenden Formate ein: `namensbereich`, `namensbereich/repository`, `namensbereich/repository:tag`.
</dd>
</dl>

**Beispiel**

Mit dem folgenden Befehl werden alle Ihre Freistellungen für Sicherheitsprobleme aufgelistet, die für Images im Repository *`birds/bluebird`* gelten. Die Ausgabe beinhaltet kontoweit geltende Freistellungen, Freistellungen mit Gültigkeit für den Namensbereich *`birds`* sowie Freistellungen mit dem Repository *`birds/bluebird`* als Geltungsbereich, jedoch keine Freistellungen, deren Geltungsbereich bestimmte Tags im Repository *`birds/bluebird`* sind.

```
ibmcloud cr exemption-list --scope birds/bluebird
```
{: pre}

## `ibmcloud cr exemption-rm`
{: #bx_cr_exemption_rm}

Löscht eine Freistellung für ein Sicherheitsproblem. Ihre bestehenden Freistellungen können Sie mit dem Befehl `ibmcloud cr exemption-list` anzeigen.

```
ibmcloud cr exemption-rm --scope GELTUNGSBEREICH --issue-type PROBLEMTYP --issue-id PROBLEM-ID
```
{: codeblock}

**Voraussetzungen**

Informationen zu den erforderlichen Berechtigungen finden Sie im Abschnitt [Zugriffsrollen für die Konfiguration von {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam#access_roles_configure).

**Befehlsoptionen**
<dl>
<dt>`--scope GELTUNGSBEREICH`</dt>
<dd>Wenn Sie Ihr Konto als Geltungsbereich festlegen möchten, verwenden Sie `"*"` als Wert. Um einen Namensbereich, ein Repository oder einen Tag als Geltungsbereich festzulegen, geben Sie den Wert in einem der folgenden Formate ein: `namensbereich`, `namensbereich/repository`, `namensbereich/repository:tag`.
</dd>
<dt>`--issue-type PROBLEMTYP`</dt>
<dd>Der Problemtyp der Freistellung für das Sicherheitsproblem, die Sie entfernen wollen. Die Problemtypen Ihrer Freistellungen können Sie mit dem Befehl `ibmcloud cr exemption-list` ermitteln.
</dd>
<dt>`--issue-id PROBLEM-ID`</dt>
<dd>Die ID der Freistellung für das Sicherheitsproblem, die Sie entfernen wollen. Die Problem-IDs Ihrer Freistellungen können Sie mit dem Befehl `ibmcloud cr exemption-list` ermitteln.
</dd>
</dl>

**Beispiele**

Der folgende Befehl löscht eine CVE-Freistellung für die CVE-ID `CVE-2018-17929` für alle Images im Repository `registry.ng.bluemix.net/birds/bluebird`.

```
ibmcloud cr exemption-rm --scope registry.ng.bluemix.net/birds/bluebird --issue-type cve --issue-id CVE-2018-17929
```
{: pre}

Der folgende Befehl löscht eine kontoweite CVE-Freistellung für die CVE-ID `CVE-2018-17929`.

```
ibmcloud cr exemption-rm --scope "*" --issue-type cve --issue-id CVE-2018-17929
```
{: pre}

Der folgende Befehl löscht eine Konfigurationsproblemfreistellung für das Problem `application_configuration:nginx.ssl_protocols` für ein einzelnes Image mit dem Tag `registry.ng.bluemix.net/birds/bluebird:1`.

```
ibmcloud cr exemption-rm --scope registry.ng.bluemix.net/birds/bluebird:1 --issue-type configuration --issue-id application_configuration:nginx.ssl_protocols
```
{: pre}

## `ibmcloud cr exemption-types`
{: #bx_cr_exemption_types}

Listet die Typen der Sicherheitsprobleme auf, für die Sie eine Freistellung definieren können.

```
ibmcloud cr exemption-types
```
{: codeblock}

**Voraussetzungen**

Informationen zu den erforderlichen Berechtigungen finden Sie im Abschnitt [Zugriffsrollen für die Konfiguration von {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam#access_roles_configure).

## `ibmcloud cr iam-policies-enable`
{: #bx_cr_iam_policies_enable}

Falls Sie die IAM-Authentifizierung verwenden, aktiviert dieser Befehl die differenzierte Autorisierung. Weitere Informationen finden Sie in den Abschnitten [Benutzerzugriff mit Identity and Access Management verwalten](/docs/services/Registry?topic=registry-iam#iam) und [Richtlinien für Benutzerzugriffsrollen definieren](/docs/services/Registry?topic=registry-user#user).

```
ibmcloud cr iam-policies-enable
```
{: codeblock}

**Voraussetzungen**

Informationen zu den erforderlichen Berechtigungen finden Sie im Abschnitt [Zugriffsrollen für die Konfiguration von {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam#access_roles_configure).

## `ibmcloud cr image-inspect`
{: #bx_cr_image_inspect}

Zeigt Details zu einem bestimmten Image an.

```
ibmcloud cr image-inspect [--format FORMAT] IMAGE [IMAGE...]
```
{: codeblock}

**Voraussetzungen**

Informationen zu den erforderlichen Berechtigungen finden Sie im Abschnitt [Zugriffsrollen für die Verwendung von {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam#access_roles_using).

**Befehlsoptionen**
<dl>
<dt>`--format FORMAT`</dt>
<dd>(Optional) Formatiert die Ausgabeelemente unter Verwendung einer Go-Vorlage.

Weitere Informationen enthält der Abschnitt [CLI-Ausgabe für {{site.data.keyword.registrylong_notm}}-Befehle formatieren und filtern](/docs/services/Registry?topic=registry-registry_cli_reference#registry_cli_listing).

</dd>
<dt>`IMAGE`</dt>
<dd>Der Name des Images, für das ein Bericht abgerufen werden soll. Sie können mehrere Images überprüfen, indem Sie alle Images im Befehl auflisten und hierbei zwischen den einzelnen Namen jeweils ein Leerzeichen angeben.

<p>Die Namen Ihrer Images können Sie mit dem Befehl `ibmcloud cr image-list` ermitteln. Kombinieren Sie den Inhalt der Spalten **Repository** und **Tag**, um den Imagenamen im Format `repository:tag` zu erstellen. Falls im Imagenamen kein Tag angegeben ist, wird das Image mit dem Tag `latest` überprüft. </p>

</dd>
</dl>

**Beispiel**

Der folgende Befehl zeigt Details über die zugänglichen Ports für das Image *`registry.ng.bluemix.net/birds/bluebird:1`* unter Verwendung der Formatierungsanweisung*`"{{ .Config.ExposedPorts }}"`* an.

```
ibmcloud cr image-inspect  --format "{{ .Config.ExposedPorts }}" registry.ng.bluemix.net/birds/bluebird:1
```
{: pre}

## `ibmcloud cr image-list` (`ibmcloud cr images`)
{: #bx_cr_image_list}

Zeigt alle Images in Ihrem {{site.data.keyword.Bluemix_notm}}-Konto an.

Der Imagename wird durch die Kombination des Inhalts in den Spalten **Repository** und **Tag** im Format `repository:tag` gebildet.
{:tip}

```
ibmcloud cr image-list [--no-trunc] [--format FORMAT] [--quiet | -q ] [--restrict RESTRICTION] [--include-ibm]
```
{: codeblock}

**Voraussetzungen**

Informationen zu den erforderlichen Berechtigungen finden Sie im Abschnitt [Zugriffsrollen für die Verwendung von {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam#access_roles_using).

**Befehlsoptionen**
<dl>
<dt>`--no-trunc`</dt>
<dd>(Optional) Gibt an, dass die Imageauszüge nicht abgeschnitten werden.</dd>
<dt>`--format FORMAT`</dt>
<dd>(Optional) Formatiert die Ausgabeelemente unter Verwendung einer Go-Vorlage.

Weitere Informationen enthält der Abschnitt [CLI-Ausgabe für {{site.data.keyword.registrylong_notm}}-Befehle formatieren und filtern](/docs/services/Registry?topic=registry-registry_cli_reference#registry_cli_listing).

</dd>
<dt>`--quiet`, `-q`</dt>
<dd>(Optional) Jedes Image wird im Format `repository:tag` aufgelistet.</dd>
<dt>`--restrict EINSCHRÄNKUNG`</dt>
<dd>(Optional) Begrenzt die Ausgabe auf das Anzeigen von Image, die sich ausschließlich im angegebenen Namensbereich oder Namensbereich und Repository befinden. </dd>
<dt>`--include-ibm`</dt>
<dd>(Optional) Bezieht von {{site.data.keyword.IBM_notm}} bereitgestellte öffentliche Images in die Ausgabe ein. Ohne diese Option werden ausschließlich private Images aufgelistet.</dd>
</dl>

**Beispiel**

Der folgende Befehl zeigt die Images im Namensbereich *`birds`* im Format `repository:tag` an, ohne dass die Imageauszüge abgeschnitten werden.

```
ibmcloud cr image-list --restrict birds --quiet --no-trunc
```
{: pre}

## `ibmcloud cr image-rm`
{: #bx_cr_image_rm}

Löscht eines oder mehrere angegebene Images aus {{site.data.keyword.registrylong_notm}}.

```
ibmcloud cr image-rm IMAGE [IMAGE...]
```
{: codeblock}

**Voraussetzungen**

Informationen zu den erforderlichen Berechtigungen finden Sie im Abschnitt [Zugriffsrollen für die Verwendung von {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam#access_roles_using).

**Befehlsoptionen**

<dl>
<dt>`IMAGE`</dt>
<dd>Der Name des Images, das gelöscht werden soll. Sie können mehrere Images gleichzeitig löschen, indem Sie alle Images im Befehl auflisten und hierbei zwischen den einzelnen Namen jeweils ein Leerzeichen angeben. Der Wert für `IMAGE` muss im Format `repository:tag` angegeben werden (Beispiel: `registry.ng.bluemix.net/namespace/image:latest`).

<p>Die Namen Ihrer Images können Sie mit dem Befehl `ibmcloud cr image-list` ermitteln. Kombinieren Sie den Inhalt der Spalten **Repository** und **Tag**, um den Imagenamen im Format `repository:tag` zu erstellen. Falls im Imagenamen kein Tag angegeben ist, wird standardmäßig das Image mit dem Tag `latest` gelöscht.</p>

</dd>
</dl>

**Beispiel** Mit dem folgenden Befehl wird das Image *`registry.ng.bluemix.net/birds/bluebird:1`* gelöscht.

```
ibmcloud cr image-rm registry.ng.bluemix.net/birds/bluebird:1
```
{: pre}

## `ibmcloud cr image-tag`
{: #bx_cr_image_tag}

Erstellt ein neues Image (ZIELIMAGE), das sich auf ein Quellenimage (QUELLENIMAGE) in {{site.data.keyword.registrylong_notm}} bezieht. Das Quellen- und das Zielimage müssen sich in derselben Region befinden.

Die Namen Ihrer Images können Sie mit dem Befehl `ibmcloud cr image-list` ermitteln. Kombinieren Sie den Inhalt der Spalten **Repository** und **Tag**, um den Imagenamen im Format `repository:tag` zu erstellen.
{: tip}

```
ibmcloud cr image-tag [QUELLENIMAGE] [ZIELIMAGE]
```
{: codeblock}

**Voraussetzungen**

Informationen zu den erforderlichen Berechtigungen finden Sie im Abschnitt [Zugriffsrollen für die Verwendung von {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam#access_roles_using).

**Befehlsoptionen**
<dl>
<dt>`QUELLENIMAGE`</dt>
<dd>Der Name des Quellenimage. Der Wert für `QUELLENIMAGE` muss im Format `repository:tag` angegeben werden (Beispiel: `registry.ng.bluemix.net/namespace/image:latest`).

</dd>
<dt>`ZIELIMAGE`</dt>
<dd>Der Name des Zielimage. Der Wert für `ZIELIMAGE` muss im Format `repository:tag` angegeben werden (Beispiel: `registry.ng.bluemix.net/namespace/image:latest`).

</dd>
</dl>

**Beispiele**

Mit dem folgenden Befehl wird eine weitere Tagreferenz namens `latest` zum Image *`registry.ng.bluemix.net/birds/bluebird:1`* hinzugefügt.

```
ibmcloud cr image-tag  registry.ng.bluemix.net/birds/bluebird:1 registry.ng.bluemix.net/birds/bluebird:latest
```
{: pre}

Mit dem folgenden Befehl wird das Image `registry.ng.bluemix.net/birds/bluebird:peck` in ein anderes Repository desselben Namensbereichs `birds/pigeon` kopiert.

```
ibmcloud cr image-tag registry.ng.bluemix.net/birds/bluebird:peck registry.ng.bluemix.net/birds/pigeon:peck
```
{: pre}

Mit dem folgenden Befehl wird das Image `registry.ng.bluemix.net/birds/bluebird:peck` in einen anderen Namensbereich namens `animals` kopiert, auf den Sie Zugriff besitzen.

```
ibmcloud cr image-tag registry.ng.bluemix.net/birds/bluebird:peck registry.ng.bluemix.net/animals/dog:bark
```
{: pre}

## `ibmcloud cr info`
{: #bx_cr_info}

Zeigt den Namen und das Konto der Registry an, bei der Sie angemeldet sind.

```
ibmcloud cr info
```
{: codeblock}

**Voraussetzungen**

Keine

## `ibmcloud cr login`
{: #bx_cr_login}

Dieser Befehl führt den Befehl `docker login` für die Registry aus. Der Befehl `docker login` ist erforderlich, damit die Befehle `docker push` oder `docker pull` für die Registry ausgeführt werden können. Zur Ausführung anderer Befehle `ibmcloud cr` wird er nicht benötigt. Falls Docker nicht installiert ist, gibt dieser Befehl eine Fehlernachricht zurück.

```
ibmcloud cr login
```
{: codeblock}

**Voraussetzungen**

Keine

## `ibmcloud cr namespace-add`
{: #bx_cr_namespace_add}

Mit diesem Befehl wählen Sie einen Namen für Ihren Namensbereich aus und fügen ihn zu Ihrem {{site.data.keyword.Bluemix_notm}}-Konto hinzu.

```
ibmcloud cr namespace-add NAMENSBEREICH
```
{: codeblock}

**Voraussetzungen**

Informationen zu den erforderlichen Berechtigungen finden Sie im Abschnitt [Zugriffsrollen für die Verwendung von {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam#access_roles_using).

**Befehlsoptionen**
<dl>
<dt>`NAMENSBEREICH`</dt>
<dd>Der Namensbereich, den Sie hinzufügen möchten. Der Namensbereich muss in Bezug auf alle {{site.data.keyword.Bluemix_notm}}-Konten in derselben Region eindeutig sein. Namensbereichsnamen müssen 4 bis 30 Zeichen lang sein und dürfen ausschließlich Kleinbuchstaben, Ziffern, Bindestriche und Unterstreichungszeichen enthalten. Namensbereichsnamen müssen mit einem Buchstaben oder einer Ziffer beginnen und enden.
  
<p>  
<strong>Tipp</strong> Verwenden Sie in Ihren Namensbereichsnamen keine persönlichen Daten.
</p>
  
</dd>
</dl>

**Beispiel**

Mit dem folgenden Befehl wird ein Namensbereich namens *`birds`* erstellt.

```
ibmcloud cr namespace-add birds
```
{: pre}

## `ibmcloud cr namespace-list` (`ibmcloud cr namespaces`)
{: #bx_cr_namespace_list}

Zeigt alle Namensbereiche an, deren Eigner Ihr {{site.data.keyword.Bluemix_notm}}-Konto ist.

```
ibmcloud cr namespace-list
```
{: codeblock}

**Voraussetzungen**

Informationen zu den erforderlichen Berechtigungen finden Sie im Abschnitt [Zugriffsrollen für die Verwendung von {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam#access_roles_using).

## `ibmcloud cr namespace-rm`
{: #bx_cr_namespace_rm}

Entfernt einen Namensbereich aus Ihrem {{site.data.keyword.Bluemix_notm}}-Konto. Beim Entfernen des Namensbereichs werden Images in diesem Namensbereich gelöscht.

```
ibmcloud cr namespace-rm NAMESPACE  [--force | -f]
```
{: codeblock}

**Voraussetzungen**

Informationen zu den erforderlichen Berechtigungen finden Sie im Abschnitt [Zugriffsrollen für die Verwendung von {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam#access_roles_using).

**Befehlsoptionen**
<dl>
<dt>`NAMENSBEREICH`</dt>
<dd>Der Namensbereich, den Sie entfernen möchten.</dd>
<dt>`--force`, `-f`</dt>
<dd>(Optional) Ausführung des Befehls ohne Benutzereingabeaufforderungen erzwingen. </dd>
</dl>

**Beispiel**

Der folgende Befehl entfernt den Namensbereich *`birds`*.

```
ibmcloud cr namespace-rm birds
```
{: pre}

## `ibmcloud cr plan`
{: #bx_cr_plan}

Zeigt Ihren Preistarif an.

```
ibmcloud cr plan
```
{: codeblock}

**Voraussetzungen**

Informationen zu den erforderlichen Berechtigungen finden Sie im Abschnitt [Zugriffsrollen für die Konfiguration von {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam#access_roles_configure).

## `ibmcloud cr plan-upgrade`
{: #bx_cr_plan_upgrade}

Führt ein Upgrade auf den Standardtarif durch.

Informationen zu Tarifen enthält der Abschnitt [Registry-Pläne](/docs/services/Registry?topic=registry-registry_overview#registry_plans).

```
ibmcloud cr plan-upgrade [TARIF]
```
{: codeblock}

**Voraussetzungen**

Informationen zu den erforderlichen Berechtigungen finden Sie im Abschnitt [Zugriffsrollen für die Konfiguration von {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam#access_roles_configure).

**Befehlsoptionen**
<dl>
<dt>`TARIF`</dt>
<dd>(Optional) Der Name des Preistarifs, auf den ein Upgrade durchgeführt werden soll. Falls für `TARIF` kein Wert angegeben wird, ist `standard` der Standardwert.</dd>
</dl>

**Beispiel**

Der folgende Befehl führt ein Upgrade auf den Standardpreistarif durch.

```
ibmcloud cr plan-upgrade standard
```
{: pre}

## `ibmcloud cr ppa-archive-load`
{: #bx_cr_ppa_archive_load}

Importiert {{site.data.keyword.IBM_notm}}-Software, die bei [IBM Passport Advantage Online für Kunden ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/software/passportadvantage/pao_customer.html) heruntergeladen und für die Verwendung mit Helm paketiert wurde, in Ihren {{site.data.keyword.registrylong_notm}}-Namensbereich.

Containerimages werden in Ihren privaten {{site.data.keyword.registryshort_notm}}-Namensbereich übertragen. Helm-Diagramme werden in ein Verzeichnis namens `ppa-import` geschrieben, das in dem Verzeichnis erstellt wird, von dem aus Sie den Befehl ausführen. Optional können Sie das [Open-Source-Projekt "Chart Museum" ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/kubernetes/charts/tree/master/stable/chartmuseum) zum Hosten von Helm-Diagrammen verwenden.

```
ibmcloud cr ppa-archive-load --archive DATEI --namespace NAMENSBEREICH
```
{: codeblock}

**Voraussetzungen**

Informationen zu den erforderlichen Berechtigungen finden Sie im Abschnitt [Zugriffsrollen für die Verwendung von {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam#access_roles_using).

**Befehlsoptionen**
<dl>
  <dt>`--archive DATEI`</dt>
  <dd>Der Pfad der komprimierten Datei, die bei IBM Passport Advantage heruntergeladen wurde.</dd>
  <dt>`--namespace NAMENSBEREICH`</dt>
  <dd>Geben Sie einen Ihrer Namensbereiche an. In diesen Namensbereich werden Container-Images aus der komprimierten Datei übertragen. Mit dem Befehl `ibmcloud cr namespace-list` können Sie Ihre Namensbereiche auflisten.</dd>
  <dt>`--chartmuseum-uri URI`</dt>
  <dd>(Optional) Ihre eindeutige Ressourcen-ID für [Chart Museum ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/kubernetes/charts/tree/master/stable/chartmuseum).</dd>
  <dt>`--chartmuseum-user BENUTZER`</dt>
  <dd>(Optional) Ihr Benutzername für [Chart Museum ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/kubernetes/charts/tree/master/stable/chartmuseum).</dd>
  <dt>`--chartmuseum-password KENNWORT`</dt>
  <dd>(Optional) Ihr Kennwort für [Chart Museum ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/kubernetes/charts/tree/master/stable/chartmuseum).</dd>
</dl>

**Beispiel**

Mit dem folgenden Befehl wird IBM Software importiert und für die Verwendung mit Helm in Ihren {{site.data.keyword.registrylong_notm}}-Namensbereich *`birds`* paketiert; der Pfad zur komprimierten Datei lautet hierbei *`downloads/compressed_file.tgz`*.

```
ibmcloud cr ppa-archive-load --archive downloads/compressed_file.tgz --namespace birds
```
{: pre}

## `ibmcloud cr quota`
{: #bx_cr_quota}

Zeigt die aktuellen Kontingente für Datenverkehr und Speicher sowie Nutzungsinformationen zu diesen Kontingenten an.

```
ibmcloud cr quota
```
{: codeblock}

**Voraussetzungen**

Informationen zu den erforderlichen Berechtigungen finden Sie im Abschnitt [Zugriffsrollen für die Konfiguration von {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam#access_roles_configure).

## `ibmcloud cr quota-set`
{: #bx_cr_quota_set}

Ändert das angegebene Kontingent.

```
ibmcloud cr quota-set [--traffic DATENVERKEHR] [--storage SPEICHER]
```
{: codeblock}

**Voraussetzungen**

Informationen zu den erforderlichen Berechtigungen finden Sie im Abschnitt [Zugriffsrollen für die Konfiguration von {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam#access_roles_configure).

**Befehlsoptionen**
<dl>
<dt>`--traffic DATENVERKEHR`</dt>
<dd>(Optional) Ändert Ihr Datenverkehrskontingent in den in Megabyte angegebenen Wert. Die Operation schlägt fehl, wenn Sie nicht berechtigt sind, Datenverkehr zu definieren, oder wenn Sie einen Wert festlegen, der Ihren aktuellen Preistarif überschreitet.</dd>
<dt>`--storage SPEICHER`</dt>
<dd>(Optional) Ändert Ihr Speicherkontingent in den in Megabyte angegebenen Wert. Die Operation schlägt fehl, wenn Sie nicht berechtigt sind, Speicher zu definieren, oder wenn Sie einen Wert festlegen, der Ihren aktuellen Preistarif überschreitet.</dd>
</dl>

**Beispiel**

Mit dem folgenden Befehl wird Ihr Kontingentgrenzwert für Pull-Datenverkehr auf *7000* Megabyte und für Speicher auf *600* Megabyte festgelegt.

```
ibmcloud cr quota-set --traffic 7000 --storage 600
```
{: pre}

## `ibmcloud cr region`
{: #bx_cr_region}

Zeigt die Zielregion und die Registry an.

```
ibmcloud cr region
```
{: codeblock}

**Voraussetzungen**

Keine

Weitere Informationen finden Sie unter [Regionen](/docs/services/Registry?topic=registry-registry_overview#registry_regions).

## `ibmcloud cr region-set`
{: #bx_cr_region_set}

Legt eine Zielregion für die {{site.data.keyword.registrylong_notm}}-Befehle fest. Um die verfügbaren Regionen aufzulisten, führen Sie den Befehl ohne Parameter aus.

```
ibmcloud cr region-set [REGION]
```
{: codeblock}

**Voraussetzungen**

Keine

**Befehlsoptionen**
<dl>
<dt>`REGION`</dt>
<dd>(Optional) Der Name Ihrer Zielregion, z. B. `us-south`.

Weitere Informationen finden Sie unter [Regionen](/docs/services/Registry?topic=registry-registry_overview#registry_regions).

</dd>
</dl>

**Beispiel**

Mit dem folgenden Befehl wird "US South" als Zielregion festgelegt.

```
ibmcloud cr region-set us-south
```
{: pre}

## `ibmcloud cr token-add`
{: #bx_cr_token_add}

Fügt ein Token hinzu, mit dem Sie den Zugriff auf eine Registry steuern können.

```
ibmcloud cr token-add [--description DESCRIPTION] [--quiet | -q] [--non-expiring] [--readwrite]
```
{: codeblock}

**Voraussetzungen**

Informationen zu den erforderlichen Berechtigungen finden Sie im Abschnitt [Plattformmanagementrollen](/docs/services/Registry?topic=registry-iam#platform_management_roles).

**Befehlsoptionen**
<dl>
<dt>`--description BESCHREIBUNG`</dt>
<dd>(Optional) Gibt den Wert als Beschreibung für das Token an, die angezeigt wird, wenn Sie den Befehl `ibmcloud cr token-list` ausführen. Falls Ihr Token durch {{site.data.keyword.containerlong_notm}} automatisch erstellt wird, wird als Beschreibung der Name Ihres Kubernetes-Cluster festgelegt. In diesem Fall wird das Token beim Entfernen des Clusters automatisch entfernt.
  
<p> 
  <strong>Tipp</strong> Verwenden Sie in Ihrer Tokenbeschreibung keine persönlichen Daten.
</p>

</dd>
<dt>`--quiet`, `-q`</dt>
<dd>(Optional) Zeigt nur das Token ohne umgebenden Text an.</dd>
<dt>`--non-expiring`</dt>
<dd>(Optional) Erstellt ein Token mit nicht ablaufendem Zugriff. Ohne Angabe dieses Parameters läuft der Zugriff auf ein Token standardmäßig nach 24 Stunden ab.</dd>
<dt>`--readwrite`</dt>
<dd>(Optional) Erstellt ein Token, das Lese- und Schreibzugriff erteilt. Ohne Angabe dieser Option ist der Zugriff standardmäßig schreibgeschützt.</dd>
</dl>

**Beispiel**

Mit dem folgenden Befehl wird ein Token hinzugefügt, das die Beschreibung *Token for my account* besitzt, nicht abläuft und über Schreib-/Lesezugriff verfügt.

```
ibmcloud cr token-add --description "Token for my account" --non-expiring --readwrite
```
{: pre}

## `ibmcloud cr token-get`
{: #bx_cr_token_get}

Ruft das angegebene Token aus der Registry ab.

```
ibmcloud cr token-get TOKEN
```
{: codeblock}

**Voraussetzungen**

Informationen zu den erforderlichen Berechtigungen finden Sie im Abschnitt [Plattformmanagementrollen](/docs/services/Registry?topic=registry-iam#platform_management_roles).

**Befehlsoptionen**
<dl>
<dt>`TOKEN`</dt>
<dd>Die eindeutige Kennung des Token, das abgerufen werden soll. Mit dem Befehl `ibmcloud cr token-list` können Sie Ihre Tokens auflisten.</dd>
</dl>

**Beispiel**

Mit dem folgenden Befehl wird das Token *10101010-101x-1x10-x1xx-x10xx10xxx10* abgerufen.

```
ibmcloud cr token-get 10101010-101x-1x10-x1xx-x10xx10xxx10
```
{: pre}

## `ibmcloud cr token-list` (`ibmcloud cr tokens`)
{: #bx_cr_token_list}

Zeigt alle Token an, die für Ihr {{site.data.keyword.Bluemix_notm}}-Konto vorhanden sind.

```
ibmcloud cr token-list [--format FORMAT]
```
{: codeblock}

**Voraussetzungen**

Informationen zu den erforderlichen Berechtigungen finden Sie im Abschnitt [Plattformmanagementrollen](/docs/services/Registry?topic=registry-iam#platform_management_roles).

**Befehlsoptionen**
<dl>
<dt>`--format FORMAT`</dt>
<dd>(Optional) Formatiert die Ausgabeelemente unter Verwendung einer Go-Vorlage.

Weitere Informationen enthält der Abschnitt [CLI-Ausgabe für {{site.data.keyword.registrylong_notm}}-Befehle formatieren und filtern](/docs/services/Registry?topic=registry-registry_cli_reference#registry_cli_listing).

</dd>
</dl>

**Beispiel**

Mit dem folgenden Befehl werden alle schreibgeschützten Tokens unter Verwendung der Formatierungsanweisung *`"{{ if eq .ReadOnly true}}{{.ID}} - {{.Expiry}} - {{.ReadOnly}} - {{.Description}}{{ end }}"`* angezeigt.

```
ibmcloud cr token-list --format "{{ if eq .ReadOnly true}}{{.ID}} - {{.Expiry}} - {{.ReadOnly}} - {{.Description}}{{ end }}"
```
{: pre}

Dieses Beispiel erzeugt Ausgabe im folgenden Format:

```
10101010-101a-1a10-a1aa-a10aa10aaa10 - 1234567890 - true - demo
```
{: screen}

## `ibmcloud cr token-rm`
{: #bx_cr_token_rm}

Ein oder mehrere angegebene Registry-Tokens entfernen. 

```
ibmcloud cr token-rm TOKEN [TOKEN...] [--force | -f]
```
{: codeblock}

**Voraussetzungen**

Informationen zu den erforderlichen Berechtigungen finden Sie im Abschnitt [Plattformmanagementrollen](/docs/services/Registry?topic=registry-iam#platform_management_roles).

**Befehlsoptionen**
<dl>
<dt>`TOKEN`</dt>
<dd>Der Wert für TOKEN kann entweder das Token selbst oder die eindeutige Kennung des Tokens sein, die mit dem Befehl `ibmcloud cr token-list` ausgegeben wird. Sie können mehrere Tokens angeben; die Tokens müssen jeweils durch ein Leerzeichen voneinander getrennt werden.</dd>
<dt>`--force`, `-f`</dt>
<dd>(Optional) Ausführung des Befehls ohne Benutzereingabeaufforderungen erzwingen. </dd>
</dl>

**Beispiel**

Mit dem folgenden Befehl wird das Token *10101010-101x-1x10-x1xx-x10xx10xxx10* entfernt.

```
ibmcloud cr token-rm 10101010-101x-1x10-x1xx-x10xx10xxx10
```
{: pre}

## `ibmcloud cr vulnerability-assessment` (`ibmcloud cr va`)
{: #bx_cr_va}

Zeigt eine Schwachstellenanalyse für Ihre Images an.

```
ibmcloud cr vulnerability-assessment [--extended | -e] [--vulnerabilities | -v] [--configuration-issues | -c] [--output FORMAT | -o FORMAT] IMAGE [IMAGE...]
```
{: codeblock}

**Voraussetzungen**

Informationen zu den erforderlichen Berechtigungen finden Sie im Abschnitt [Zugriffsrollen für die Verwendung von {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-iam#access_roles_using).

**Befehlsoptionen**
<dl>
<dt>`IMAGE`</dt>
<dd>Der Name des Images, für das ein Bericht abgerufen werden soll. Der Bericht gibt Auskunft darüber, ob das Image bekannte Paketschwachstellen aufweist. Sie können für mehrere Images gleichzeitig Berichte anfordern, indem Sie alle Images im Befehl auflisten und hierbei zwischen den einzelnen Namen jeweils ein Leerzeichen angeben.

<p>Die Namen Ihrer Images können Sie mit dem Befehl `ibmcloud cr image-list` ermitteln. Kombinieren Sie den Inhalt der Spalten **Repository** und **Tag**, um den Imagenamen im Format `repository:tag` zu erstellen. Falls im Imagenamen kein Tag angegeben ist, analysiert der Bericht das Image mit dem Tag `latest`.</p>

<p>Die folgenden Betriebssysteme werden unterstützt:

<ul>
<li>Alpine</li>
<li>CentOS</li>
<li>Debian</li>
<li>Red Hat Enterprise Linux (RHEL)</li>
<li>Ubuntu</li>
</ul>
</p>

Weitere Informationen finden Sie unter [Imagesicherheit mit Vulnerability Advisor verwalten](/docs/services/va?topic=va-va_index).

</dd>
<dt>`--extended`, `-e`</dt>
<dd>(Optional) Die Befehlsausgabe zeigt zusätzliche Informationen zu Fixes für Pakete mit Schwachstellen an.</dd>
<dt>`--vulnerabilities`, `-v`</dt>
<dd>(Optional) Die Befehlsausgabe beschränkt sich auf Schwachstellen.</dd>
<dt>`--configuration-issues`, `-c`</dt>
<dd>(Optional) Die Befehlsausgabe beschränkt sich auf Konfigurationsprobleme.</dd>
<dt>`--output FORMAT`, `-o FORMAT`</dt>
<dd>(Optional) Die Befehlsausgabe wird in dem ausgewählten Format zurückgegeben. Das Standardformat lautet `text`. Die folgenden Formate werden unterstützt:

<ul>
<li>`text`</li>
<li>`json`</li>
</ul>

</dd>
</dl>

**Beispiele**

Mit dem folgenden Befehl wird ein Bericht mit einer Standardschwachstellenanalyse für Ihr Image angezeigt.

```
ibmcloud cr vulnerability-assessment registry.ng.bluemix.net/birds/bluebird:1
```
{: pre}

Mit dem folgenden Befehl wird ein Bericht mit der Schwachstellenanalyse für Ihr Image *`registry.ng.bluemix.net/birds/bluebird:1`* im JSON-Format angezeigt, der ausschließlich Schwachstellen enthält.

```
ibmcloud cr vulnerability-assessment --vulnerabilities  --output json registry.ng.bluemix.net/birds/bluebird:1
```
{: pre}
