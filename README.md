# Nexus Per Saecula

> *Latin: "The Connection Through the Ages"*

A historical connection game that links any two famous people through a chain of **real, documented physical meetings** — from ancient Greece to the modern era.

---

## What Is It?

**Nexus Per Saecula** is a browser-based game built around one question:

> *How many real meetings does it take to connect Socrates to Barack Obama?*

Unlike the traditional "Six Degrees of Kevin Bacon" which uses pop culture associations, every link in Nexus Per Saecula is a **genuine historical encounter** — two people in the same room, at the same event, on the same battlefield. No letters. No "influenced by." No century-skipping.

The game uses **Breadth-First Search** on a hand-curated graph of ~200 historical figures and ~400 documented meetings, building a chronological spine from 400 BC to the present day where each edge spans at most ~40 years. This means two people separated by 2,000 years genuinely require 50+ steps to connect — the path length reflects the real time gap.

---

## Demo

Open `index.html` directly in any browser. No installation, no server, no internet connection required (except for Google Fonts).

---

## Features

- 🔗 **BFS pathfinding** — always finds the shortest valid chain
- 📜 **Historical accuracy** — every link is ✓ documented or ~ historically plausible
- ⏳ **Time-honest** — no lazy century jumps; Alexander → Hitler takes 55+ real steps
- 🔍 **Autocomplete** — type any partial name to find people in the database
- 👤 **Browse all people** — expandable grid showing all ~200 figures with birth eras
- 🌐 **Zero dependencies** — single self-contained HTML file, runs offline

---

## How It Works

### The Data

All connections are stored as a flat edge list:

```js
["Julius Caesar", "Cleopatra VII", "Caesar arrived in Alexandria 48 BC; Cleopatra was smuggled to meet him", "✓"],
["Charlemagne", "Alcuin of York", "Charlemagne invited Alcuin to lead the Palace School at Aachen in 782 AD", "✓"],
["Beethoven", "Franz Liszt", "The 11-year-old Liszt performed for Beethoven in Vienna in 1823", "✓"],
```

Each entry is `[Person A, Person B, description, confidence]` where:
- `✓` = well-documented historical meeting
- `~` = historically plausible encounter

### The Graph

At startup, the edge list is compiled into a bidirectional adjacency list. Every person becomes a node; every documented meeting becomes an edge in both directions.

### The Search

Typing two names triggers **Breadth-First Search**, which explores the graph level by level and guarantees the shortest possible path. A `prev` map tracks how each person was reached, allowing the full chain to be reconstructed from destination back to source.

### The Spine

The core of the database is a **historical spine** — a single connected chain running from ~400 BC to 1945 AD where each consecutive pair actually met and each link spans at most ~40 years:

```
Socrates → Plato → Aristotle → Alexander the Great → Ptolemy I → Euclid
→ ... → Julius Caesar → Augustus → Tiberius → Caligula → Claudius → Nero
→ ... → Constantine I → Ambrose → Augustine → Pope Leo I → Attila the Hun
→ Theodoric → Boethius → Pope Gregory I → Charlemagne → Alcuin
→ ... → Saladin → Marco Polo → Dante → Boccaccio → Chaucer
→ ... → Galileo → Newton → Voltaire → Franklin → Napoleon → Goethe
→ Beethoven → Liszt → Wagner → Nietzsche → Freud → Einstein → Chaplin
→ Gandhi → Churchill → FDR → Stalin → Mao → Nixon → Elvis → The Beatles
→ Bob Dylan → Martin Luther King Jr. → JFK → ... → Obama → Mandela
```

Famous people not on the spine are connected to their nearest spine node via documented meetings.

---

## People in the Database

The database covers figures from across history including:

| Era | Examples |
|-----|---------|
| Ancient Greece | Socrates, Plato, Aristotle, Alexander the Great, Cleopatra |
| Roman Empire | Julius Caesar, Augustus, Nero, Marcus Aurelius, Galen |
| Early Church | Augustine, Ambrose, Pope Gregory I, Charlemagne |
| Medieval | Saladin, Richard I, Genghis Khan, Marco Polo, Joan of Arc |
| Renaissance | Leonardo da Vinci, Machiavelli, Michelangelo, Galileo |
| Enlightenment | Newton, Voltaire, Franklin, Goethe, Beethoven |
| 19th Century | Darwin, Lincoln, Nietzsche, Freud, Tolstoy, Edison |
| 20th Century | Einstein, Churchill, Gandhi, MLK, JFK, Elvis, The Beatles, Obama |

---

## Project Structure

```
nexus-per-saecula/
│
├── index.html     # The entire game — open this in a browser
└── README.md            # This file
```

All game logic, data, and styling are contained in a single HTML file:

- **EDGES** — the raw connection data (~400 entries)
- **ERA** — approximate birth years for display
- **GRAPH / DISPLAY** — built at runtime from EDGES
- **resolve()** — fuzzy name matching (handles partial names and typos)
- **bfs()** — Breadth-First Search pathfinder
- **renderChain()** — DOM rendering with staggered animations

---

## Known Limitations

- Some links are plausible but not perfectly documented — historical records from ancient and medieval eras are incomplete
- The database is not exhaustive; many famous people are not yet included

---

## Contributing

Pull requests welcome. To add a connection:

1. Find a documented physical meeting between two historical figures
2. Add it to the `EDGES` array in `index.html`:
   ```js
   ["Person A", "Person B", "Description of how/where/when they met", "✓"],
   ```
3. Add a birth year to the `ERA` object if the person is new:
   ```js
   "Person A": "123 BC",
   ```
4. Ensure the new person connects to at least one existing node in the graph

Please only add `✓` (documented) links for meetings with a verifiable historical source. Use `~` for plausible encounters that lack direct documentation.

---

## Etymology

**Nexus** — Latin for *bond*, *connection*, or *link*

**Per Saecula** — Latin for *through the ages* or *across the centuries*

Together: *"The Bond Across the Centuries"*

---

## License

MIT — do whatever you like with it.

---

*Built with vanilla HTML, CSS, and JavaScript. No frameworks. No build step. No nonsense.*
