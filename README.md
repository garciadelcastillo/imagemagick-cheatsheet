# imagemagick-cheatsheet

Common operations and examples with [ImageMagick](https://imagemagick.org/index.php). For the love of me, I can never remember them off the top of my head... :sweat_smile:

Unless otherwise noted, these commands assume `Windows` + `Powershell`.

Check [this guide](https://nono.ma/ffmpeg-and-imagemagick-guide) by [@nonoesp](https://github.com/nonoesp) for other cool tricks. 

Many of these operations are possible with `ffmpeg` as well, check my other [cheatsheet](https://github.com/garciadelcastillo/ffmpeg-cheatsheet).

### Batch resize+crop

Use `mogrify` for batch processes **in place** (originals will be overwritten). This example resizes to 256x256, fitting to the smallest simension (`^`). Then crops, keeping image centered:

  magick mogrify -resize 256x256^ -gravity center -extent 256x256^ *.png
