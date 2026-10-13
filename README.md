# Book Parser: Character Networks from Fiction

A Telegram bot ([@pyproj_icba_bot](https://t.me/pyproj_icba_bot)) that reads a novel, finds the characters, measures how often they interact and draws the result as an interactive HTML graph.

Team project by three students of Fundamental and Computational Linguistics at HSE University (2022). [Presentation with a demo run](https://docs.google.com/presentation/d/15j1VmueZI42IqV_gl9CYikQEbYUJbqJsgdmqB3cjqEM/edit?usp=sharing) (in Russian).

## How it works

The user sends a `.txt` file (UTF-8) and picks one of three modes.

1. **Given characters.** The user lists the characters of interest and chooses the paragraph separator (tab or new line) and how many interactions should go into the graph. The bot returns a CSV with the links and an HTML graph.
2. **Discovered characters.** The bot extracts candidate names that appear more often than a chosen threshold, the user picks the relevant ones, and the bot builds the graph. Two names joined with `_` are treated as one character (for example `Harry_Potter`).
3. **Characters by chapter.** The text is split by a custom separator (chapter, part, book) and the bot reports the most frequent characters in each piece. Optionally it tries to guess the main character.

Name candidates are proper nouns found with spaCy's part-of-speech tagger. The weight of a link between two characters is the number of times they co-occur in the same paragraph. Graphs are drawn with pyvis.

![Bot architecture](bot_scheme.png)

## Files

| File | What it does |
|---|---|
| `bot.py` | Telegram bot logic and dialogue flow |
| `modes.py` | Text processing and name extraction for the three modes |
| `ghandvis.py` | Graph construction and HTML visualisation (pyvis), upload of the HTML page |
| `requirements.txt` | Dependencies |

## How to run

```bash
pip install -r requirements.txt
# put your Telegram bot token into bot.py (TOKEN)
# and a GitHub token into ghandvis.py (used to publish the HTML graph)
python bot.py
```

## Team

- Text processing and parser logic: [Daria Kharlamova](https://github.com/harlamovads)
- Data visualisation and bot code: [Alisa Lyozina](https://github.com/WadjetEyeTheSpy)
- Bot architecture and bot code: [Alena Muravyeva](https://github.com/Alhassliebe)
