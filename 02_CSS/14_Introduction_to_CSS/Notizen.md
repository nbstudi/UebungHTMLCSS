nth-child erklären? evtl kommt das in nachfolgenden Übungen.
--------------------------------------------------------------------------------------------------
Spoiler:

1️⃣ Grundsyntax
element:nth-child(an+b) { /* Styles */ }
element → das HTML-Element, das du ansprechen willst (z. B. p, li, div …)
n → ein Zähler, der bei 0 startet und bei jedem Kind erhöht wird
a und b → Zahlen, mit denen du bestimmen kannst, welche Kinder ausgewählt werden

2️⃣ Spezielle Kurzformen
odd → entspricht 2n+1 → alle ungeraden Kinder (1., 3., 5., …)
even → entspricht 2n → alle geraden Kinder (2., 4., 6., …)
Beispiele:
p:nth-child(odd) { color: blue; }  /* 1., 3., 5. ... */
p:nth-child(even) { color: pink; } /* 2., 4., 6. ... */

3️⃣ Allgemeine Formel an+b
n = 0,1,2,3,…
a = Schrittweite (z. B. jede zweite, dritte, vierte …)
b = Startpunkt (ab welchem Kind beginnt es)

Beispiel 1: Jede dritte Zeile ab dem ersten:
p:nth-child(3n+1) { color: red; } /* 1., 4., 7., 10. ... */

Beispiel 2: Jede dritte Zeile ab dem zweiten:
p:nth-child(3n+2) { color: green; } /* 2., 5., 8., 11. ... */

Beispiel 3: Jedes fünfte Kind ab dem dritten:
p:nth-child(5n+3) { color: orange; } /* 3., 8., 13., ... */

4️⃣ Weitere Möglichkeiten
Man kann negative Startpunkte benutzen: z. B. 3n-1 → ab Kind -1, dann jede dritte → Browser ignoriert negative Startpunkte und zählt ab dem ersten Kind.
Man kann :nth-child() auch mit anderen Pseudoklassen kombinieren, z. B. :nth-last-child() (zählt von hinten) oder :not().


💡 Merke: odd/even sind nur bequeme Kurzformen für die Formel. Mit an+b kannst du praktisch jede beliebige Reihenfolge von Kindern gezielt stylen.