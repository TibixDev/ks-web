# KSWeb
This repository holds the Vue remake of the original katawa-shoujo.com website, currently hosted at:
- [katawa-shoujo.com](https://katawa-shoujo.com/)
- [katawa-shoujo.online](https://katawa-shoujo.online/)
- [katawa-shoujo.ru](https://katawa-shoujo.ru/)


## Prerequisites
- [bun](https://bun.sh/)

## Running the project
```sh
bun install # installs dependencies
bun run dev # starts the dev server
```

## Building the project
```sh
bun install # installs dependencies
bun run build # builds the project
```

## Contributing
We welcome contributions to the project! If you have a change, translation or improvement to make, please open a pull request and we will review it as soon as possible.

## Note for CJK website translators (not the game)

You might notice that we use a couple of CJK fonts that are *impossibly* small (< ~50KB). That's because I (Bridget, @bridgetsystems on Discord and Codeberg) have taken the liberty to remove everything but the characters actually used in the translation. This is a terrible hack, but saves Vercel bandwidth and us money in the long run. 
Thus, if you want to modify the translation, you WILL need to modify the fonts too, otherwise some fallback font will be (hopefully) used (depending on your device) and it's just going to look ugly and mis-matched. Doing that is easy: You will need to modify `mikachan_trimmed.woff2` for JP, and `zh_combo_trimmed.woff2` for ZH (both under `ks-web/public/fonts`). The full fonts are `mikachan_o-PB.otf` for JP and`zh_combo.ttf` for ZH (both under `ks-web/public/fonts`). (We still haven't been able to find a better KR font). Download it (or use `git`), then get a font editor (I have personally used [FontForge](https://fontforge.org/en-US/), but it's a dreadful experience, the only good thing it has going for is that it's free.) You will need to compare the strings: look up what characters you ***fully*** removed from your translation and remove them from the trimmed font, then look up what characters you added in your translation in the full font and put them in the trimmed font. Or ping me, I don't mind.