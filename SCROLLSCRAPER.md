# World ORT / ScrollScraper audio

Investigated 2026-10-06 using https://github.com/jae-63/scrollscraper
and its `cgi-bin/buildmp3.cgi` and `utilities/fetchMP3s.sh`.

## How it works
The builder enumerates verses inclusively across chapters. It loads individual
files from `ORT_MP3s.recoded/t{book}/{chapter:02}{verse:02}.mp3` (books 1–5).
Those recordings are downloaded as five book archives during ScrollScraper
setup. The former bible.ort.org host is no longer its live source.

FFmpeg concatenates the verse recordings into a reading, then adds a gTTS
spoken English introduction, a short spacer, and repeated reading copies with
long spacers. It caches a generated MP3 and returns its location. Building is
queued and rate limited; generated files can be removed later. They are not
permanent URLs suitable for an app catalog.

Verified the user's Genesis 1:3–2:4 request returned a downloadable generated
MP3; the direct Genesis 1:3 verse asset returned audio/mpeg with byte ranges.

## TorahTutor addition
The World ORT panel streams the currently selected verse directly from the
ScrollScraper host on an explicit Listen click. Native browser audio plays
cross-origin media without fetching it through JavaScript/CORS. Playback speed
preserves pitch, and starting either reference stops the other. Selecting a
new verse or recording yourself stops ORT playback.

External links open the selected verse or the entire selected aliyah in
ScrollScraper, where the user can request a generated MP3. TorahTutor does not
bulk-generate files, bypass rate limits, or bundle/rehost the ORT recordings.
No ScrollScraper source code was copied.

The ORT recordings have no word timestamp mapping here. PocketTorah remains
the source for synchronized highlighting and word/phrase slices. PocketTorah
word timings must not be applied to ORT recordings. The current text/assignment
coverage remains the 372 imported PocketTorah aliyot.

## Attribution and limits
World ORT recordings are marked copyright/all rights reserved by the source.
ScrollScraper's software license does not establish an open license for ORT
media. Attribution is displayed in the app. Obtain reuse permission before
bundling/rehosting recordings or shipping an offline ORT corpus.

The source FAQ states a limit of 8 new MP3s per IP per day, 30 MB per IP per day,
100 generated recordings and 300 MB total per day, and at most 72 verses times
repeat count. These limits may change. Large aliyot may exceed the builder
limit; users can choose a shorter excerpt on ScrollScraper.

The original recordings follow canonical full-kriyah sof-pasuk/sof-aliyah
melodies, which can differ from a custom excerpt's ending. The external source
can change or become unavailable.

Sources:
- https://scrollscraper.adatshalom.net/scrollscraperFAQ.html
- https://scrollscraper.adatshalom.net/scrollscraper-technical-FAQ.html
- https://github.com/jae-63/scrollscraper/blob/master/cgi-bin/buildmp3.cgi
- https://github.com/jae-63/scrollscraper/blob/master/utilities/fetchMP3s.sh
