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

