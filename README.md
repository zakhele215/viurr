https://www.viu.com/ott/za/en/vod/2433300/Relative-Justice-S1?utm_medium=social_share_sender_android&utm_uuid=bull


Download programmes from Viu

## Prerequisite
- [FFmpeg](https://ffmpeg.org/)

## Usage

### Command Line Interface

Install globally

```bash
# npm
npm install -g viurr
# pnpm
pnpm install -g viurr
```

#### Inspect

```bash
# Inspect the details of an episode
viurr inspect episode <productId>
```

```bash
# Inspect details of a series
viurr inspect series <productId>
```

| Option   | Description                     |
| -------- | ------------------------------- |
| `--json` | Print the result in JSON format |

#### Download

```bash
# Download files of an episode
viurr download episode <type> <productId>
```

```bash
# Download files of a series
viurr download series <type> <productId>
```

---

#### Options

`type`

`cover` | `subtitle` | `video`

Specify `--help` to see the available options of each `type`, for example:

```bash
$ viurr download episode video --help
viurr download episode video <productId>

Download video of an episode

Options:
  --help     Show help                                                 [boolean]
  --version  Show version number                                       [boolean]
  --quality  Video quality
          [string] [choices: "1080p", "720p", "480p", "240p"] [default: "1080p"]
```

---

`productId`

The ID that can be found in the URL on viu.com, for example,

```
https://www.viu.com/ott/hk/zh-hk/vod/6979/男兒當入樽
                                     ----
```
The `productId` of this episode is `6979`.

---

#### Examples

Cover image

```bash
$ viurr download episode cover 6979
Downloading cover image of 「男兒當入樽」 EP.1 【天才籃球員誕生】
Downloaded: /path/to/your/directory/男兒當入樽 EP.1 【天才籃球員誕生】.jpeg
```

Subtitle

```bash
$ viurr download episode subtitle 6979
Downloading subtitle of 「男兒當入樽」 EP.1 【天才籃球員誕生】 (Language: 繁體中文)
Downloaded: /path/to/your/directory/男兒當入樽 EP.1 【天才籃球員誕生】.chi.srt
```

Video

```bash
$ viurr download episode video 6979
Downloading video of 「男兒當入樽」 EP.1 【天才籃球員誕生】 (Quality: 1080p)

# encode in progress
Downloading video of 「男兒當入樽」 EP.1 【天才籃球員誕生】 (Quality: 1080p)
Encoding [872.93/fps] [1843.7 Kb/s] [23.5 MB] [00:01:46]

# after finished
Downloading video of 「男兒當入樽」 EP.1 【天才籃球員誕生】 (Quality: 1080p)
Downloaded: /path/to/your/directory/男兒當入樽 EP.1 【天才籃球員誕生】.mkv
```

This program uses FFmpeg to encode the HLS playlist file and output the video with the original codecs. (i.e. `-c copy`).

If you already have FFmpeg available in your `PATH`, then you are good to go, otherwise, you need to set the environment variable `FFMPEG_PATH` as the path to the executable FFmpeg.

Example:

```bash
FFMPEG_PATH=/path/to/ffmpeg viurr download episode video 6979
```

#### Note

- `download series` is a shortcut to `download episode` to handle all available episodes in a series.
- It is recommended to use `inspect` to see the available subtitles and video qualities before attempting to download the files.

### Programmatic

Install as local module

```bash
# npm
npm install viurr --save
# pnpm
pnpm install viurr
```

#### Types

Learn more [here](https://github.com/LibelDev/viurr/blob/master/src/types/types.ts)

#### Inspect

```js
import { inspect } from "viurr";
```

Inspect the details of an episode

`inspect.episode(productId: string): Promise<IEpisode>`

Inspect the details of a series

`inspect.series(productId: string): Promise<ISeries>`

#### Download

```js
import { download } from "viurr";
```

Download the video in specific quality

`download.video(productId: string, quality: QualityOption = '1080p'): Promise<[ISeries, IEpisode, string, IEncoder]>`

Download the cover image

`download.cover(productId: string): Promise<[ISeries, IEpisode, string]>`

Download the subtitle in specific language in SRT format

`download.subtitle(productId: string, languageId: LanguageFlag, temporary = false): Promise<[ISeries, IEpisode, string]>`

## TODO

- [x] Combine second subtitle
- [ ] Interactive CLI
- [ ] GUI

## Build

```bash
pnpm build
```

## Development

```bash
pnpm build:watch
pnpm cli
```

## Test

Not available

## License

MIT License

## Disclaimer

This project is for technical testing and educational purposes only. The owner and contributors do not assume any legal responsibilities caused by the users. Users should be aware of and take the risks.
