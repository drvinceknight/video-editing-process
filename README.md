# video-editing-process
How I edit teaching videos

## Recording

I use two commercial pieces of software for recording videos:

- [Microsoft whiteboard](https://app.whiteboard.microsoft.com) for any writing.
- [CleanShot](https://cleanshot.cloud/) for the actual recording.

I record my computer screen with a small video of me being shown in the corner
(a feature of Cleanshot). If I am doing any writing then I have a browser
window pointed at the same microsoft whiteboard that I am using on my tablet.

If I have written anything on the whiteboard I also export that to a png (`thumb.png`).

This creates: `raw.mp4` and possibly `thumb.png`.


## Initial edit

I use iMovie for quick cuts, crops and trims of the video.

This creates: `cut.mp4`

## Generating subtitles

I use [`whisper`](https://github.com/openai/whisper) to generate subtitles in `.srt` format:

    $ whisper cut.mp4 --model small --language English

This creates: `cut.mp4.srt`.

## Quality assurance

I watch the video `cut.mp4` and read the subtitles file at the same time
`main.srt` to confirm it is accurate. Possibly making manual edits at this
stage.

## Adding hard subtitles

I use [`ffmpeg`](https://github.com/FFmpeg/FFmpeg) to add subtitles to the
video.

    $ ffmpeg -i cut.mp4 -vf subtitles=cut.mp4.srt main.mp4

Note that this requires `ffmpeg` to have `libass` enabled. Run `ffmpeg
-version` and confirm that `—-enable-libass` is present in the output.

**These are "hard" as opposed to "soft" to make inclusiveness the
default.**
