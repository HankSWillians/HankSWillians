name: Update README stats

on:
  schedule:
    - cron: "0 5 * * *"   # every day
  workflow_dispatch:       # lets you run it manually from the Actions tab

jobs:
  build:
    runs-on: ubuntu-latest
    permissions:
      contents: write
    steps:
      - uses: actions/checkout@v4

      - name: Generate stats card
        uses: stats-organization/github-readme-stats-action@v2
        with:
          card: stats
          options: username=${{ github.repository_owner }}&show_icons=true&include_all_commits=true&theme=tokyonight&hide_border=true&bg_color=0D1117&title_color=3B9EFF&icon_color=FF4D6D
          path: profile/stats.svg
          token: ${{ secrets.GITHUB_TOKEN }}
          fail_on_error: true

      - name: Generate top languages card
        uses: stats-organization/github-readme-stats-action@v2
        with:
          card: top-langs
          options: username=${{ github.repository_owner }}&layout=compact&langs_count=6&theme=tokyonight&hide_border=true&bg_color=0D1117&title_color=3B9EFF
          path: profile/top-langs.svg
          token: ${{ secrets.GITHUB_TOKEN }}
          fail_on_error: true

      - name: Commit cards
        run: |
          git config user.name "github-actions[bot]"
          git config user.email "41898283+github-actions[bot]@users.noreply.github.com"
          git add profile/*.svg
          git diff --staged --quiet || git commit -m "chore: update README stats cards"
          git push
