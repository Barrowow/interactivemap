# interactivemap

**Build Interactive Map — Usage**

- **Purpose:**: Generate an interactive Leaflet HTML map that shows cities with emoji markers and a simple red/yellow/green status based on conversion rates.
- **Script:**: `build_interactive_map_emotes_heatmap.py`

**Requirements**

- **Python:**: 3.8+ (tested on 3.11)
- **Libraries:**: standard library only (uses `csv`, `json`, `pathlib`, `datetime`). No extra pip packages required.

**Usage**

- **Run:**: Execute the script from the folder containing the CSV exports:

  ```powershell
  python build_interactive_map_emotes_heatmap.py
  ```

- **Output:**: The script writes a timestamped HTML file like `interactive_map_emotes_YYYYMMDD_HHMMSS.html` in the same folder.

**What the script does**

- Aggregates rows from CSV files in the current directory (ignores files starting with `interactive_map`).
- Optionally loads city performance metrics from `Kursantritte für Heat Mappe Angebote + Conversion.csv` if present.
- Calculates a conversion rate (`kurs / deals * 100`) when metrics exist and assigns one of three colours:
  - red (`#ff0000`) = clearly below the 3.2% reference (below 3.04%)
  - yellow (`#ffff00`) = within ±5% of 3.2% (≈3.04–3.36%)
  - green (`#00ff00`) = clearly above 3.36%
- Produces an HTML map with emoji markers, solid coloured circles and a legend. No heat/blur effects.

**Customization**

- Change the reference or tolerance: edit `conversion_color()` in `build_interactive_map_emotes_heatmap.py`.
- Show different reasons or emojis: update `VISIBLE_REASONS` and `EMOTE_REASONS` at the top of the script.

**Troubleshooting**

- White page in browser: open the newest `interactive_map_emotes_*.html` (check timestamp). If the file is truncated, re-run the script. Clear browser cache if necessary.
- Missing colours: ensure the script had access to the metrics CSV so conversion rates are calculated; cities without metrics are shown grey.

**Notes**

- The script intentionally limits printed/populated reasons and emojis for visual clarity.
- If you want a continuous gradient instead of three discrete colours, I can change the `conversion_color()` mapping back to a smooth interpolation.

**Contact / Next steps**

- Tell me if you want a legend with explicit numeric thresholds, different thresholds, or a gradient instead of discrete colours.
