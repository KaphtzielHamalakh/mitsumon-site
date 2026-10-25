# PocketTorah integration

Source: https://github.com/rneiss/PocketTorah
Pinned commit: 8a23287221dd535966ee9914de9a03e71769a469.
Project creators: Russel Neiss and Charlie Schwartz.

## Rights and attribution

Russel Neiss's April 17, 2012 release announcement explicitly grants reuse of
recordings and metadata under Creative Commons Attribution-ShareAlike:
https://ejewishphilanthropy.com/torah-on-the-go/
Its license link resolves to **CC BY-SA 2.5 Generic**:
https://creativecommons.org/licenses/by-sa/2.5/
Legal text: https://creativecommons.org/licenses/by-sa/2.5/legalcode
Do not substitute an unsupported claim of CC BY-SA 4.0.

PocketTorah lists these readers: Etta Abramson, Joshua Foster, Eitan Konigsberg,
Eytan Kurshan, Ari Lucas, Rabbi Ita Paskind, Rebecca Russo, Joshua Schwartz,
Abigail Teller. We retain collective attribution because the repository does
not provide an individual reader mapping per recording. No endorsement implied.

Audio is unchanged and streamed from upstream. The optional standalone preview
embeds an unchanged Bereshit-1.mp3. Timing metadata in
`src/pockettorah/catalog.json` is adapted to JSON objects with word boundaries,
verse references, and reading identifiers. The adapted metadata is distributed
under CC BY-SA 2.5. Preserve attribution and that license when redistributing it
or derivative metadata. These notices also apply to embedded preview data.

Hebrew is the upstream Westminster Leningrad Codex edition. Slash morphology
separators are removed for display, while word order, vowels, accents and maqaf
are preserved. No translation is imported. See upstream data/torah/json headers
for transcription credits. PocketTorah's app-code release was announced as GPL3;
this integration is newly written and does not copy that React Native code.

## Mapping and validation

The importer reads aliyah start/end verses from data/aliyah.json; enumerates the
exact upstream w arrays in those verses; matches label and MP3 basenames after
case, space and apostrophe normalization; and validates finite, strictly
increasing times and a one-to-one word/timestamp mapping. N or N+1 timestamps
are accepted for N words. If the last end is absent, audio duration closes it.
Six readings fail validation and are explicitly excluded. Maftir reuse of aliyah
7 and Haftarah discontinuities are deliberately not inferred.

The UI derives short practice chunks at etnachta, zakef katon, revia or verse end.
These are learning boundaries, not a new interpretation of the recorded melody.
Upstream word timestamps supply slicing and highlighting. Small timing errors or
background sound in the recordings remain possible and need teacher review.

## Architecture and limitations

RecordedTransport owns one HTMLAudioElement and uses its audio clock for
highlighting and range playback. Revision checks cancel pending starts after
Stop or navigation. Browser preservesPitch separates playback speed from pitch.
Navigation is disabled during microphone capture; reference and self recordings
pause one another. A hidden document pauses reference playback. The original
WebAudio instrument and parser remain available in the analysis route.

All text/timings are bundled (about 6 MB uncompressed JS) so standalone previews
can select passages without fetching metadata. MP3s are fetched only when played.
This is convenient for initial review, but a larger deployment should split
metadata by portion and self-host credited audio instead of relying on raw GitHub
availability. No hosting deployment is made by this change.

