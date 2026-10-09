# Overlap

A minimal single-file web app for checking the current time across a country's cities. Search for a country, click it, and see the live local time in each of its timezones.

## Features

- Top bar with a light / dark theme toggle. The choice is remembered.
- Centered country search with keyboard-navigable suggestions (↑ ↓ Enter Esc). It also understands names like "USA" and "UK".
- Selecting a country lists its cities, ordered west to east, with live local time, date and UTC offset.
- Updates every second, with no refresh needed.

## How It Works

1. The page embeds a small table of IANA timezone identifiers per country, taken from the tz database's `zone.tab`. It holds identifiers only, no offsets.
2. Country names come from `Intl.DisplayNames`.
3. For each city, the time and date come from `Intl.DateTimeFormat` with that city's IANA zone.
4. The UTC offset is derived with `formatToParts()`: the zone's wall-clock fields are read as UTC and the real instant is subtracted. This handles daylight saving and zones like +5:30, +5:45 and +8:45 automatically.

## Tech Stack

- HTML5
- Tailwind CSS (CDN)
- Vanilla JavaScript
- Intl API
- IANA timezone database through browser timezone support

## Running Locally

Open `index.html` in a modern browser (internet needed once for the Tailwind CDN), or serve the folder:

```bash
python3 -m http.server 8000
```

## Usage

Type a country in the search box, pick it from the list (or press Enter), and read the city times below. Use the sun/moon button in the top bar to switch theme.

## Timezone Accuracy

There are no UTC offset tables and no hand-written DST rules. Every time and offset is computed by the browser's `Intl` APIs from IANA identifiers, so results follow your browser's timezone data. Country-to-zone membership is the only static data, and it changes rarely.

## Project Structure

```text
overlap/
└── index.html
```

## License

MIT License. Copyright (c) 2026 Overlap contributors.

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
