# imagemagick-cheatsheet

Common operations and examples with [ImageMagick](https://imagemagick.org/index.php). For the love of me, I can never remember them off the top of my head... :sweat_smile:

Unless otherwise noted, these commands assume `Windows` + `Powershell`.

Check [this guide](https://nono.ma/ffmpeg-and-imagemagick-guide) by [@nonoesp](https://github.com/nonoesp) for other cool tricks. 

Many of these operations are possible with `ffmpeg` as well, check my other [cheatsheet](https://github.com/garciadelcastillo/ffmpeg-cheatsheet).

### Batch convert
Use `mogrify` for batch convert a bunch of images to a new format:

    magick mogrify -format jpg *.heic

### Batch resize+crop

Use `mogrify` for batch processes **in place** (originals will be overwritten). This example resizes to 256x256, fitting to the smallest simension (`^`). Then crops, keeping image centered:

    magick mogrify -resize 256x256^ -gravity center -extent 256x256^ *.png

### Image pairs

Creates an image stitching two next to each other (or a 2x1 `montage`). This example crops two input images to `256x256` and stitches them together (useful for example for `Pix2Pix` dataset creation):

    magick montage a.png b.png \
        -resize 256x256^ \
        -gravity center \
        -extent 256x256 \
        -geometry 256x256^ \
        -tile 2x1 \
        -depth 8 \
        -define png:color-type=2 \
        ab.png
    
The above also forces 8-bit color depth (if you are using 16-bit imagemagick) and color image (if inputs are BW).


### Creating a mosaic/montage/collage of images

Using:

    magick montage *.png -geometry 224x224 -tile 27x14 montage.png

Creates a 27x14 collage with the stills. Margins can be added to the `geometry` parameter, as well as background and borders:

    magick montage *.png -geometry 256x128>+10+5 -tile 12x10 -background white -border 1 -bordercolor lightgray montage.png

The `>` operator reduces images only bigger than `256x128`.
