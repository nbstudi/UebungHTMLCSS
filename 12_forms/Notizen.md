To Do:
- tel Feld beim Smartphone testen bzgl Nummernfeldes

- RegEx zuende behandeln:
📘 Was noch fehlt – aber du brauchst nicht alles

Hier die restlichen Hauptthemen, die es gibt, aber viele davon sind optional oder nur in Spezialfällen relevant:

Thema	                            Wichtig für Praxis?             Kommentar
\d, \w, \s usw.                     ✅ Ja	                       Häufig genutzt, einfach zu merken
Quantifizierer ?, +, *, {n,}	    ✅ Ja	                       Häufig in Eingabevalidierungen
Gruppierung (...)	                🔶 Mittel	                    Wichtiger bei komplexeren Mustern, z. B. in Replace-Szenarien
Alternativen `	                    `	                            🔶 Mittel
Lookahead / Lookbehind	            🔴 Selten	                    Fortgeschrittene Themen
Flags (z. B. (?i) für Case-Ins.)	🔴 Selten	                    Sprache-/Tool-spezifisch
Start- und Endanker ^, $	        ✅ Ja	                       Oft übersehen, aber wichtig z. B. für "muss mit ... beginnen"
Negationen [^a-z]               	✅ Ja	                       Sehr nützlich für "alles außer"

🔁 Empfehlung: So kannst du das Thema strukturieren und abschließen

Wenn du wirklich ein gutes Grundverständnis aufbauen willst (was bei dir fast schon erreicht ist!), dann reicht es, wenn du diese Reihenfolge noch in Ruhe durcharbeitest:

✅ \d, \w, \s, \D, \W, \S
✅ +, *, ?, {min,max}
✅ ^, $
🔶 (...) (Gruppierung und Backreferences)
🔶 | (Alternative)
🔶 [^...] (Negierte Zeichenklassen)
Und dann kannst du sagen: “Ich kann reguläre Ausdrücke.”

- name Attribut bei den restlichen Feldern ergänzen?
-----------------------------------------------------------------------------------------------------------------------------

Exkurs zu enctype:
Wenn nichts weiteres angegeben, wird das Standardformat (application/x-www-form-urlencoded) verwendet.
Hier werden dann alle Felder zu einer einzigen Zeichenkette zusammengefügt.
Mal angenommen wir haben die Felder username und age und der Werte sind "Max Mustermann" und "30":
  <input name="username" value="Max Mustermann">
  <input name="age" value=30>
  <input name="initials" value="m&m">
  <input name="nickname" value="Mäxle">

Das wird dann folgendermaßen kodiert:
username=Max+Mustermann&age=30&initials=m%26m&nickname=M%C3%A4xle

Erklärung:
- vor dem Gleichheitszeichen steht das Feld, danach dessen Wert
- Leerzeichen werden in ein Pluszeichen umgewandelt
- weitere Felder werden mit einem &-Zeichen davor getrennt
->diese und ein paar andere Sonderzeichen sind reservierte Sonderzeichen und gehören zu den unsicheren Zeichen
- wenn man Sonderzeichen literal nutzen will, dann müssen diese durch percent-encoding (auch URL-Encoding) escaped werden, zb %26 für das &-Zeichen,
sonst wird es fälschlicherweise als Trennzeichen zwischen den Feldern interpretiert. (weitere: %2B für Pluszeichen, %3D für Gleichheitszeichen, usw usw)
- Nicht-ASCII Zeichen (ebenso unsichere Zeichen) zb Umlaute wie ä, werden in UTF-8 kodiert und dann pro Byte percent-encodiert.
  Also ä in UTF-8 hex wäre C3 A4, und diese wären dann %C3%A4.
- der Rest sind sichere Zeichen, diese werden ganz normal literal übernommen
(- es gibt noch Steuerzeichen wie zb 0x00 dem sogenannten Nullbyte und andere Steuerzeichen, das sind unsichtbare Zeichen,
die spielen hier aber keine Rolle, daher gehe ich nicht näher darauf ein)

Jetzt zum Problem bei Binärdaten. Hier ein paar Bytes die zb von einer Bilddatei stammen könnten:
0xFF 0xD8 0xFF 0x00 0xC8 0x26 0x41 0x42
(oder halt FF D8 FF 00 C8 26 41 42, also die eigentlichen Hex Ziffern, die "0x" signalisiert nur dass es sich um eine Hex Ziffer handelt)
- Jetzt ist es so, dass der ASCII Bereich von 0x00 bis 0x7F (dezimal 0 bis 127) geht.
Das erste Byte ist nicht im gültigen Bereich, also wird es percent encoded also FF zu %FF, sowie D8 zu %D8, FF zu %FF, 00 zu %00 und 26 zu %26. 41 und 41 sind im gültigen Bereich,
diese entsprechen dem A und dem B. (Achtung es handelt sich hier immer noch um Hex Ziffern, daher ist Hex 41 in ASCII ein A usw.)
Daraus ergibt sich folgender String: %FF%D8%FF%00%C8%26AB

Beim Decodieren passiert nun folgendes, das %26 entspricht nämlich dem escapeten &-Zeichen. Bzw. sieht der Parser hier ein & Zeichen und demnach ein Feldtrenner.
Dh dieser Byte ist nun kein Byte mehr und wurde zu einem reservierten Zeichen, bzw dem &-Zeichen. Das Bild kann somit nicht mehr richtig dargestellt werden und ist fehlerhaft. 

Daher kommt enctype=multipart/form-data ins Spiel. Ganz kurz gefasst, wird jedes Feld separat übertragen. Die einzelnen Parts werden durch einen sogenannten
Boundary, quasi eine Trennlinie getrennt. Jeder Part hat einen Header der Name, Content-Type usw enthält und bei Dateien die Binärdaten.
Hier werden die Bytes 1 zu 1 übernommen und werden nicht als Text geparsed und nicht escaped, somit entsteht keine Fehlinterpretation oder Verfälschung der Bytes.