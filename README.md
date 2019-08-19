

# Komplexe Stylesheets strukturieren - das 5-1 Muster
5 Ordner, 1 Datei. Grundsätzlich hast du all deine partials in 5 verschiedenen Ordnern verteilt, und eine Datei auf dem Root-Level (normalerweise main.scss) importiert und kompiliert alles zu einem Stylesheet.

```
helpers/
base/
components/
layout/
vendors/
```

Und natürlich:

```
main.scss
```


## Vendors Ordner
Und zu guter Letzt, der vendors/ Ordner. Die meisten Projekte besitzen einen solchen oder ähnlichen Ordner indem alles CSS von externen Libraries und Frameworks wie z.B. Normalize, Bootstrap, jQueryUI, FancyCarouselSliderjQueryPowered und so weiter, gelistet sind. All diese in einem Ordner zu sammeln ist ein guter Weg zu sagen “Hey, das ist nicht von mir, nicht mein Code, nicht meine Verantwortung”.

```
_normalize.scss
_bootstrap.scss
_jquery-ui.scss
_select2.scss
```

Falls du irgendwann mal einen Bereich daraus überschreiben musst, rate ich einen achten Ordner namens vendors-extensions anzulegen. Dort kannst du die Dateien exakt danach benennen was sie überschreiben.

Zum Beispiel, vendors-extensions/_bootstrap.scss beinhaltet alle Regeln die einige von Bootstraps Default CSS überschreiben. Dadurch vermeide ich die Vendor-Dateien selbst zu bearbeiten, was generell keine gute Idee ist.

## Base Ordner
Der base/ Ordner beinhaltet etwas wie das Boilerplate des Projekts. Da wird eine Reset-Datei drin sein, ein paar Regeln für die Typografie und wahrscheinlich auch ein Stylesheet für allgemeinere HTML Elemente (welches ich _base.scss nenne):

```
_base.scss
_reset.scss
_typography.scss
```

## Layout Ordner
Im layout/ Ordner ist alles was für die Seite oder Applikation als Design definiert wird. Hier können Stylesheets für die Hauptbereiche der Seite (header, footer, navigation, sidebar, …), das Gridsystem oder Formulare drin sein.

```
_grid.scss
_header.scss
_footer.scss
_sidebar.scss
_forms.scss
_navigation.scss
```

## Components Ordner
Für kleinere Komponenten gibt es den components/ Ordner. Während der layout/ Ordner eher klein bleibt (hier wird das globale Wireframe definiert), beinhaltet components/ eher Widgets oder Module wie Slider, Loader und ähnliches. Durch den Ansatz eine Seite oder Applikation überwiegend aus kleinen Modulen zu entwickeln, sind hier tendenziell mehr Dateien vorhanden.

```
_media.scss
_carousel.scss
_thumbnails.scss
```

## Helpers Ordner
Der helpers/ Ordner umfasst alle Sass Tools und Helper die über das Projekt verteilt zum Einsatz kommen. Sei es globale Variablen, Funktionen, Mixins oder Platzhalter.

Die Grundregel hier ist, dass am Ende keine einzige Zeile CSS kompiliert werden soll, und die Dateien somit leer bleiben. Es sind reine Sass Helper.

```
_variables.scss
_mixins.scss
_functions.scss
_placeholders.scss
```

Bei einem sehr großen Projekt mit vielen abstrakten Utilities mag es interessant sein diese eher nach Typ oder Thema, wie zum Beispiel Typographie (_typography.scss), Theming (_theming.scss) etc., zu gruppieren. Jede Datei enthält alle zugehörigen Helper: Variablen, Funktionen, Mixins und Platzhalter. Das macht deinen Code einfacher zum durchsuchen und warten, besonders wenn die Dateien sehr groß werden.

## Main Datei
Die Main Datei (üblicherweise main.scss genannt) sollte die einzige Sass-Datei aus der Codebasis sein, welche nicht mit einem Unterstrich beginnt. Außer @import und Kommentaren steht dort nichts weiter drin.

Die Dateien sollten danach importiert werden, in welchem Ordner sie sich befinden. Eins nach dem anderen, nach folgender Reihenfolge:

```
abstracts/
vendors/
base/
layout/
components/
pages/
themes/
```

Um die Lesbarkeit einzuhalten, solltest du außerdem diese Richtlinien beachten:

eine Datei pro @import;
ein @import pro Zeile;
keine neue Zeile zwischen imports vom selben Ordner;
eine neue Zeile nach dem letzten import aus einem Ordner;
Dateiendungen und Unterstriche am Anfang weglassen.


```
sass/
|
|– helpers/
|   |– _variables.scss    # Sass Variablen
|   |– _functions.scss    # Sass Funktionen
|   |– _mixins.scss       # Sass Mixins
|   |– _placeholders.scss # Sass Platzhalter
|
|– base/
|   |– _reset.scss        # Reset/normalize
|   |– _typography.scss   # Regeln für Typographie
|   …                     # Etc.
|
|– components/
|   |– _buttons.scss      # Buttons
|   |– _carousel.scss     # Carousel
|   |– _cover.scss        # Cover
|   |– _dropdown.scss     # Dropdown
|   …                     # Etc.
|
|– layout/
|   |– _navigation.scss   # Navigation
|   |– _grid.scss         # Grid system
|   |– _header.scss       # Header
|   |– _footer.scss       # Footer
|   |– _sidebar.scss      # Sidebar
|   |– _forms.scss        # Forms
|   …                     # Etc.
|
|– vendors/
|   |– _bootstrap.scss    # Bootstrap
|   |– _jquery-ui.scss    # jQuery UI
|   …                     # Etc.
|
|
```
