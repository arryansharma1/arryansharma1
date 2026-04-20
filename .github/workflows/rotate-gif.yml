name: 🎬 Rotate Daily GIF

on:
  schedule:
    - cron: '0 0 * * *'   # Midnight UTC every day
  workflow_dispatch:       # Also lets you trigger it manually to test

jobs:
  update-gif:
    runs-on: ubuntu-latest
    permissions:
      contents: write

    steps:
      - name: Checkout repo
        uses: actions/checkout@v4

      - name: Pick today's GIF and update README
        run: |
          # ── 15 funny + technical GIFs ──────────────────────────────────────
          GIFS=(
            "https://media.giphy.com/media/13HgwGsXF0aiGY/giphy.gif"          # 00 - fast typing
            "https://media.giphy.com/media/zOvBKUUEERdNm/giphy.gif"           # 01 - l33t hacker
            "https://media.giphy.com/media/LmNwrBhejkK9EFP8ZpN/giphy.gif"    # 02 - it works!
            "https://media.giphy.com/media/077i6AULCXc0FKTj9s/giphy.gif"     # 03 - coffee + laptop
            "https://media.giphy.com/media/du3J3cXyzhj75IOgvA/giphy.gif"     # 04 - this is fine 🔥
            "https://media.giphy.com/media/xT0xeJpnrWC4XWblEk/giphy.gif"    # 05 - mind blown
            "https://media.giphy.com/media/3oKIPtjElfqwMOTbH2/giphy.gif"    # 06 - thinking hard
            "https://media.giphy.com/media/RbDKaczl7HPoU0paTH/giphy.gif"    # 07 - one does not simply debug
            "https://media.giphy.com/media/UrkHf5bYMjBJkVDEpe/giphy.gif"   # 08 - error error error
            "https://media.giphy.com/media/Wn74RUT0vjnoU98Zdv/giphy.gif"   # 09 - loading forever
            "https://media.giphy.com/media/qgQUggAC3Pfv684Cnr/giphy.gif"   # 10 - working at 3am
            "https://media.giphy.com/media/f3iwJFOVOwuy7K6FFw/giphy.gif"   # 11 - cat on keyboard
            "https://media.giphy.com/media/26tn33aiTi1jkl6H6/giphy.gif"    # 12 - it's alive!
            "https://media.giphy.com/media/yYSSBtDgbbRzq/giphy.gif"        # 13 - nerd glasses on
            "https://media.giphy.com/media/l3q2K5jinAlChoCLS/giphy.gif"   # 14 - matrix rain
          )

          # Day of year (001–366) → pick index 0–14
          DAY=$(date +%j)
          INDEX=$(( (10#$DAY - 1) % ${#GIFS[@]} ))
          GIF="${GIFS[$INDEX]}"

          echo "Day $DAY → GIF index $INDEX → $GIF"

          # Replace ONLY the daily-gif img tag (keyed on alt="daily gif")
          sed -i 's|<img align="right" width="300" alt="daily gif" src="[^"]*"|<img align="right" width="300" alt="daily gif" src="'"$GIF"'"|' README.md

      - name: Commit & push if README changed
        run: |
          git config user.name  "github-actions[bot]"
          git config user.email "github-actions[bot]@users.noreply.github.com"
          git diff --quiet README.md || (
            git add README.md
            git commit -m "🎬 chore: rotate daily GIF [skip ci]"
            git push
          )
