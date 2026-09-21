# One Life — coach media

Short looping clips of the One Life coaches demonstrating each movement, plus
a poster frame for each. Filmed for One Life and owned outright: no licence,
no attribution, nothing to expire.

Served straight to the apps over raw.githubusercontent.com, the same way the
exercise stills are served from free-exercise-db. Public because the apps
fetch them with no credentials.

## Naming

    coaches/ol-<exercise>-<coach>.mp4   the clip
    coaches/ol-<exercise>-<coach>.jpg   first frame, for list rows and any
                                        surface that renders a still

`<exercise>` matches the key used in the apps' exerciseMedia.js map, not the
catalogue id, so one clip can serve more than one catalogue entry.

## Encoding

H.264 (main profile), yuv420p, 24 fps, no audio track, `+faststart` so the
moov atom is at the front and playback can begin before the file is fully
fetched. Portrait clips are 448x672; the two lying-down movements are
landscape 672x378, which is the right framing for them -- players must not
assume one aspect ratio.

Sources were 23 MB total; these are 2.8 MB, 92-348 KB each, visually
indistinguishable at the size they render.

Re-encode with:

    ffmpeg -i SRC -an -vf "scale=448:-2,format=yuv420p" -c:v libx264 \
      -preset slow -crf 27 -profile:v main -level 4.0 -g 48 \
      -movflags +faststart -r 24 OUT.mp4
