# AP-Index: Abschnitte

Die wesentlichen inhaltlichen Daten finden sich in der Datenstruktur `assessmentPart`. Die großen Studien des IQB “Bidungstrend” und “VERA” sind beispielsweise in Fächer aufgeteilt, deren Daten in separaten Teams entwickelt werden. Aber auch in kleineren Studien kann es sinnvoll sein, für den besseren Überblick die Studie in Abschnitte aufzuteilen.

Auf dieser Seite finden Sie die allgemeinen Parameter eines Abschnittes sowie Angaben für Zusatzdokumente. Folgende Abschnittsparameter sind auf separaten Seiten beschrieben:

- `bookletModules`, `instruments` und `units` auf der Seite [Instrumente](../content-package/instruments.llms.md),
- `baseScales`, `derivedScales` und `aggregatedScales` auf der Seite [Skalen](../content-package/scales.llms.md)

# `id`, `name`, `description`

Aus welchem Grund das Inhaltspaket ACP in Abschnitte aufgeteilt wird, kann variieren. Üblicherweise folgt dies Testdomänen – also Mathematik, Sprache usw. – oder zeitlichen Phasen bei Testungen, die über mehrere Testzeitpunkte durchgeführt werden. Bei StarS trifft letzteres zu, d. h. für jeden Messzeitpunkt gibt es einen Abschnitt.

Im Datenmanagement müssen dann natürlich ein verlässlicher Bezug zu einem Abschnitt `id` sowie Erläuterungen über die Datenfelder `name` und `description` hinterlegt sein. In Auswahllisten oder Protokollen kann dann der Abschnitt gut identifiziert werden.

`name` und `description` sind Felder mit expliziter Sprachmarkierung. Das bedeutet, dass man Informationen in mehreren Sprachen hinterlegen kann, je nach Zielgruppen.

``` json
{
 "id": "fr",
 "name": [
    {
      "lang": "de",
      "value": "Französisch Sek I"
    }
  ],
  "description": [
    {
      "lang": "de",
      "value": "Testaufgaben für Hörverstehen und Leseverstehen in zwei Testheften (Basisniveau, erweitertes Niveau) zu jeweils 60 min"
    }
  ]
}
```

# `metadata`

Das IQB nutzt seit einigen Jahren konsequent ein eigenes Metadatensystem, das auf internationalen Standards beruht. Kern sind Vokabulare, in denen Wertelisten für spezifische Merkmale veröffentlicht sind. Verschiedene Metadaten werden dann Objekten über sog. Metadatenprofile zugewiesen. Es handelt sich um ein sehr flexibles und universelles Verfahren, digitalen Objekten Zusatzinformationen zuzuweisen, ohne jedes Mal die Spezifikation ändern zu müssen.

Weitere Informationen und Literatur finden Sie [hier](https://iqb-vocabs.github.io). Die Metadatenprofile, die im AP-Index verwendet werden, finden Sie [hier](https://iqb-vocabs.github.io/p44/)

Beispiel Objekt-Metadaten JSON

``` json
{
  "metadata": {
    "profileId": "https://raw.githubusercontent.com/iqb-vocabs/p44/master/index.json",
    "entries": [
      {
        "id": "e1",
        "label": [
          {
            "lang": "de",
            "value": "Art der Erhebung"
          }
        ],
        "value": [
          {
            "id": "https://w3id.org/iqb/v85/dt/1"
          }
        ],
        "valueAsText": [
          {
            "lang": "de",
            "value": "Kompetenz- und Leistungsdaten"
          }
        ]
      },
      {
        "id": "kim_type_school",
        "label": [
          {
            "lang": "de",
            "value": "Schulform"
          }
        ],
        "value": [
          {
            "id": "https://w3id.org/kim/schularten/s02"
          }
        ],
        "valueAsText": [
          {
            "lang": "de",
            "value": "Grundschule"
          }
        ]
      }
    ]
  }
}
```

Beispiele: Klassenstufe, Für SPF geeignet, Erhebungseinheit

# `additionalDocuments`

An dieser Stelle werden Dokumente gelistet, die Teil des Inhaltspaketes für diesen Abschnitt sind, aber keinen direkten Bezug zur Testdurchführung haben. Eine Erhebung benötigt üblicherweise zahlreiche Handreichungen für die Beteiligten, um die Prozesse zu erläutern, zu schulen oder Möglichkeiten aufzuzeigen, mit den Ergebnissen den Unterricht zu verbessern. Die Metadaten helfen Fachanwendungen, das Material an der richtigen Stelle anzubieten bzw. in die Prozesse einzubeziehen.

Die Datenstruktur ist ein Array, und jeder Eintrag hat folgende Eigenschaften:

- `contentType`: Art des Materials. Im Laufe der Weiterentwicklung dieser Spezifikation werden weitere Typen hinzukommen.
  - `CODING_INSTRUCTIONS` sind Anweisungen in Textform, wie Antworten zu kodieren sind (sog. Codebook). Diese können ausgedruckt werden und unterstützen den manuellen Kodierprozess.
  - `STUDY_BACKGROUND` markiert Texte, die man zur allgemeinen Einführung an Interessierte geben kann, um für Verständnis zu werben.
- `targeting`: In dieser Eigenschaft sind die Zielgruppen aufgezählt (Array), für die das Material gedacht ist.
  - `PROCTOR`: Testaufsicht während der Durchführung vor Ort
  - `TEST_TAKER`: Testpersonen
  - `TEACHER`: Lehrkraft als Zielgruppe für die Umsetzung von Erkenntnissen im Unterricht
  - `TEST_ADMINISTRATION`: Verantwortliche für das Management bzw. Koordinierung der Erhebung(en)
  - `GOVERNANCE`: Zielgruppe für Ergebnisrückmeldungen auf den verschiedenen Ebenen der Bildungsadministration (Schulleitung, Schulamt usw.)
  - `CODER`: Personenkreis, der mit der manuellen Kodierung beauftragt ist
- `file`: Pro Material gibt es genau eine Material-Datei, aber diese kann in verschiedenen Sprachvarianten auftreten. Daher ist diese Eigenschaft wieder ein sprachspezifisches Array, jeweils mit `id` (Pfad zum Material), `lang` für die Sprachangabe, `label` und `description` für die UI

Zurück nach oben
