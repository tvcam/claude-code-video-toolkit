# First-hand teardown of sample short-form videos: hooks, narration pace, voice tone, editing, captions and sound (watched directly; as of 18 November 2026)

> **Read this first: what was watched, how, and what was blocked**
> - **YouTube: blocked on the first request.** yt-dlp's first metadata request (for Zack D. Films' "How Stitches Work", `ttuKeS5k4Uo`) got "Sign in to confirm you're not a bot". Under the access rules I stopped using YouTube at that point: no retries, cookies, alternate clients or workarounds. **No YouTube file was viewed first-hand.**
> - **TikTok: public videos were served without sign-in.** All 15 samples below were fetched from TikTok with yt-dlp, one at a time, at ≤720p (TikTok served 360p–1080p files), with TikTok's own English caption files and metadata. Roughly 30–40 requests were made in total.
>   - Two profiles answered "This user's account is private. Log into an account…": @kurzgesagt and @historymatters. I skipped both without retrying, so **the planned Kurzgesagt validation sample is missing**.
>   - Three profile listings failed with an extractor error and were not pursued: @zack.d.films, @minutephysicsofficial and @animated_life_tips. The active Zack D. Films account turned out to be @zackdfilms92.
> - **How each video was measured** (scripts in `/tmp/claude-0/-home-user-claude-code-video-toolkit/038151a7-743c-5519-a1db-477f514c766f/scratchpad/analysis_scripts_direct/`, all run with `python3 -I`):
>   - ffprobe for duration.
>   - ffmpeg `select='gt(scene,0.3)'` for **hard cuts**, plus a 0.15 threshold for **soft cuts** (fast camera moves and dissolves).
>   - `ebur128` for integrated LUFS, true peak and LRA.
>   - `silencedetect=-35dB:d=0.25` for silences.
>   - faster-whisper `base.en` for word timestamps, giving WPM, time to first word, words before 3 s, and every inter-word gap ≥0.25 s. These were cross-checked against TikTok's own caption cues, which match the hooks word for word.
>   - 50-ms RMS levels for a voice-vs-bed estimate.
>   - 10-fps frame differencing for the share of frozen frames, the longest static hold and the time of first motion.
>   - librosa pYIN for pitch.
> - **How I looked at the frames.** I viewed a contact sheet per video (frames at 0, 0.5, 1, 2, 3 s, then every 3 s) and a gridded "caption probe" with lines every 192 px of a 1920-px-high frame. Caption sizes and positions were read off that grid by eye, to about ±15 px.
> - **What I could not do: hear the audio.** "Narrator tone" below is inferred from measured pace, pauses, loudness range, pitch statistics (which mostly turned out inconclusive, see Q3) and the transcript wording. It is never a by-ear judgement. AI vs human voice is stated only where the speaker is visible or documented; elsewhere it is marked *inferred* or *not determinable*.
> - **Labels used throughout:**
>   - **[M]** a first-hand measurement from the file.
>   - **[E]** my estimate by eye from the frames, or an inference.
>   - **[D]** the earlier dataset-based pass (`sample_video_teardown.md`) or a third-party source.
>   - View counts are TikTok's rounded figures as returned on 18 Nov 2026.
> - **Clean-up.** All video files, audio, caption files, metadata JSON and page dumps were deleted after measurement. What remains in the scratchpad is contact sheets, caption probes and one metrics file: `/tmp/claude-0/-home-user-claude-code-video-toolkit/038151a7-743c-5519-a1db-477f514c766f/scratchpad/metrics_direct/metrics_direct_all.json`. No media was placed in the repository.

## Per-video teardown: 15 public TikTok videos measured first-hand (metrics, hooks, captions, art style, sound, tone, endings)

### Takeaway
I measured 15 public TikTok videos:
- **7 validation samples** from channels in the earlier table: Zack D. Films ×3, SimpliHow ×2 and Low Poly Shorts ×2, one of which is the same video as an earlier YouTube row.
- **6 in previously unmeasured styles:** Casually Explained ×3 (deadpan stick-figure), MinuteEarth (hand-drawn doodle), Useless Info (text-heavy "useless facts" with a TTS-like voice), and a wordless ZDF how-to.
- **2 TikTok-native TTS formats:** Useless Info and a Reddit-story/Subway Surfers video.
- **2 high-energy contrasts:** MrBeast and Alan Chikin Chow.

Every narrated video speaks its first word within the first 0.1 s. Narrated faceless pace ranges from **141 to 257 WPM (median 208)**. The calm 3D explainers sit at 141–192 WPM, and the deadpan stick-figure clips are among the *fastest* at 210–245 WPM. No successful narrated faceless sample has a pause longer than 0.96 s.

### Cited Findings

**Sample list** (all on TikTok; upload date; views as of 18 Nov 2026)

| # | Channel | Title (TikTok caption) | URL | Uploaded | Views | Len |
|---|---|---|---|---|---|---|
| 1 | Zack D. Films | Cutting A Watermelon With Dental Floss 😮 | [link](https://www.tiktok.com/@zackdfilms92/video/7708059129335598350) | 2026-11-14 | 1.9M (in ~4 days) | 35.6 s |
| 2 | Zack D. Films | The Surgery That Turns Legs Around 🔄🦵 | [link](https://www.tiktok.com/@zackdfilms92/video/7315249587311201582) | 2023-12-22 | 184.7K | 40.5 s |
| 3 | Zack D. Films | How To Air Layer A Plant 🤔 | [link](https://www.tiktok.com/@zackdfilms92/video/7706914296814521614) | 2026-11-11 | 371.7K (in ~1 week) | 31.5 s |
| 4 | SimpliHow (@simplihowww) | How To Relieve A Headache 😱 | [link](https://www.tiktok.com/@simplihowww/video/7445347531694837022) | 2024-12-06 | 12.4M | 22.2 s |
| 5 | SimpliHow | Wisdom Teeth Removal Hack 😨 | [link](https://www.tiktok.com/@simplihowww/video/7511853084750941470) | 2025-06-03 | 3.8M | 28.8 s |
| 6 | Low Poly Shorts | At a subatomic level, what we perceive as "touch"… (= YouTube "You've Never Touched Anything") | [link](https://www.tiktok.com/@lowpolyshorts/video/7606648171032317197) | 2026-02-14 | 86.6M | 38.8 s |
| 7 | Low Poly Shorts | Pointing a laser at an aircraft is a federal felony… | [link](https://www.tiktok.com/@lowpolyshorts/video/7612238436992322829) | 2026-03-01 | 12.6M | 36.5 s |
| 8 | Casually Explained | It's lit fam | [link](https://www.tiktok.com/@casuallyexplained/video/7583651459095465223) | 2025-12-14 | 2.4M | 21.0 s |
| 9 | Casually Explained | Function over form #interiordesign | [link](https://www.tiktok.com/@casuallyexplained/video/7576414392284237063) | 2025-11-24 | 516.5K | 40.3 s |
| 10 | Casually Explained | Canada is sideways Chile change my view | [link](https://www.tiktok.com/@casuallyexplained/video/7583207422945201415) | 2025-12-13 | 551.8K | 29.1 s |
| 11 | MinuteEarth | Sperm whales catch Giant Squid by 'suction feeding'… | [link](https://www.tiktok.com/@minuteearth/video/7636354677780614414) | 2026-05-05 | 186.9K | 63.9 s |
| 12 | Useless Info | Fun facts you should know!! 😂💀 | [link](https://www.tiktok.com/@uselessinfo_real/video/7407692115519524142) | 2024-08-27 | 1.1M | 6.3 s |
| 13 | Reddit.andy *(TTS "brainrot" format; low views)* | #subwaysurfersstorytime #reddit… | [link](https://www.tiktok.com/@reddit.andy/video/7175833788730133765) | 2022-12-11 | 27.8K | 239 s (first 60 s analysed) |
| 14 | MrBeast *(high-energy contrast)* | The last one was hard 😴 | [link](https://www.tiktok.com/@mrbeast/video/7670566355153833246) | 2026-08-05 | 90.2M | 23.0 s |
| 15 | Alan Chikin Chow *(high-energy contrast)* | who murdered my classmates!? | [link](https://www.tiktok.com/@alanchikinchow/video/7621178509800508703) | 2026-03-25 | 4.1M | 38.6 s |

**Table A: pace, pauses, cuts, motion, loudness** (all [M]; sources are the video URLs above)

Column notes:
- **WPM** is words ÷ full duration; the figure in brackets uses the speech span.
- **Pauses** are inter-word gaps ≥0.25 s.
- **Hard/soft cuts per 10 s** use ffmpeg scene thresholds 0.3 and 0.15.
- **Frozen share** is the share of 0.1-s steps with almost no picture change.
- **Voice-to-floor** is the median of the louder half of speech frames minus the 5th-percentile level inside the speech span. The number in brackets is the voice level minus the median level in Whisper gaps. A larger value means a quieter bed.

| # | WPM (span) | First word | Words <3 s | Pause mean / max (s) | Pauses /min | Hard / soft cuts /10 s | First cut, or first visual change | Frozen share / longest hold | LUFS / TP / LRA | Voice-to-floor (gap) dB |
|---|---|---|---|---|---|---|---|---|---|---|
| 1 ZDF Watermelon | 178 (183) | 0.0 s | 9 | 0.47 / 0.72 | 15.2 | 0 / 0 | No cut; knife already slicing at 0.0 s; motion from 0.1 s | 0% / 0 s | −10.4 / **+2.1** / 2.4 | 21.6 (5.8) |
| 2 ZDF Surgery | 141 (143) | 0.0 s | 10 | 0.51 / 0.76 | 13.3 | 0 / 0.25 | Tumour appears at 1.0 s; only cut at 34.3 s (to live-action stock) | 2% / 0.3 s | −9.2 / **+1.5** / 2.2 | 18.9 (5.8) |
| 3 ZDF Air Layer | **no narration** (Whisper found 6 words at 26.9 s, unverified) | — | 0 | — | — | 0 / 0.32 | Motion from 0.1 s; first soft cut 13.6 s | 0% / 0 s | −26.8 / −0.1 / 6.4 | — |
| 4 SimpliHow Headache | 192 (196) | 0.0 s | 11 | 0.46 / 0.76 | 16.2 | 0.9 / 1.35 | 2.03 s (mug and pills smash ≈2 s) | 18% / 0.9 s | −23.4 / −6.8 / 2.4 | 16.6 (1.3) |
| 5 SimpliHow Wisdom | 152 (159) | 0.0 s | 9 | 0.41 / 0.80 | 12.5 | 0.69 / 1.39 | Motion from 0.1 s; first cut 6.75 s | 1% / 0.1 s | −16.6 / 0.0 / 2.8 | 14.2 (6.7) |
| 6 Low Poly Touch | 206 (211) | 0.0 s | 12 | 0.34 / 0.48 | 9.3 | **4.64** / 6.45 | 1.2 s | 0% / 0 s | −15.8 / −1.5 / 1.7 | 13.8 (9.5) |
| 7 Low Poly Laser | 215 (217) | 0.0 s | 15 | 0.34 / 0.52 | 16.4 | 4.93 / 6.03 | Laser beam at 0.5 s; cut at 1.83 s | 4% / 0.9 s | −15.6 / −1.3 / 1.9 | 13.2 (4.2) |
| 8 CE Lit | **240 (244)** | 0.0 s | 11 | 0.45 / 0.78 | **31.4** | 0 / 0.95 | **First change 3.4 s** | **97% / 3.6 s** | −14.7 / −0.2 / 1.5 | **36.5** (18.7) |
| 9 CE Interior | **245 (248)** | 0.0 s | 16 | 0.50 / 0.84 | 17.9 | 0 / 0.25 | First change 1.4 s | **97% / 4.8 s** | −12.7 / −0.2 / 3.2 | **32.7** (31.0) |
| 10 CE Chile | 210 (215) | 0.0 s | 15 | 0.47 / 0.74 | 28.9 | 0 / 0 | First change 2.4 s | **97% / 4.4 s** | −13.1 / −0.2 / 2.1 | **30.8** (16.9) |
| 11 MinuteEarth | 207 (211) | 0.0 s (caption file says 0.10 s) | 7 | 0.52 / **0.96** | 17.8 | 0.31 / 1.1 | Caption at 0.5 s; first motion 1.6 s; soft cut 3.2 s | **94% / 4.5 s** | −22.3 / −6.4 / 3.7 | 16.7 (14.7) |
| 12 Useless Info | **257 (280)** | 0.0 s | **17** | none ≥0.25 s | 0 | 4.75 / 4.75 | 1.77 s | 2% / 0.1 s | −23.5 / −10.6 / 1.6 | 24.6 (—) |
| 13 Reddit story (0–60 s) | 218 (222) | 0.0 s | 6 | **0.82 / 1.22** | 20.0 | 0 / 1.0 | Gameplay starts ≈2 s; soft cut 1.37 s | 0% / 0 s | **−7.4** / +0.8 / 2.5 | 32.3 (21.8) |
| 14 MrBeast | 125 (126) | 0.0 s | 11 | 0.92 / **3.54** | 33.9 | 0 / 0 | No cut; animated card overlay moves from 0.1 s | 0% / 0 s | −16.0 / −0.1 / 5.1 | 24.7 (19.8) |
| 15 Alan Chikin Chow | not reliable (music-led; Whisper returned a repeated lyric) | — | — | — | — | **11.4 / 18.4** | **1.0 s** | 0% / 0 s | **−7.9 / +3.1** / 1.9 | 5.0 (0.7) |

**Table B: hooks, on-screen text, captions, style, sound, tone, ending**

Column notes:
- **Spoken hook** is verbatim; words after the 3-s mark are in brackets. Sources are the video URLs and TikTok caption files.
- **Caption spec** is [E], read from the 1920-px grid probe. "Height" is the height of the text block (ascender to descender) in pixels of a 1080×1920 frame. "y" is the vertical centre of the caption, measured from the top.

| # | Spoken hook [M] | On-screen text hook [E] | Hook type | Caption spec [E] | Art style [E] | Music / bed [M level; type E] | Narrator tone; AI or human | Ending (closing words [M]) |
|---|---|---|---|---|---|---|---|---|
| 1 | "Cut the watermelon like this. (Then pull a piece of dental floss tight…)" | Captions only ("Cut the" at 0.0 s) | **Imperative how-to**; the action is already happening | 1–2 words, sentence case. White heavy rounded sans with soft drop shadow, no outline. Height ≈65 px. Centred; **y ≈1,490–1,500 px (≈78%)**, ≈420 px clear of the bottom. New chunk every ~0.5–1 s | Glossy stylised 3D, top-down kitchen, hands only. A full character appears at ~21 s | Bed present; the quietest moments sit ≈22 dB under the voice | Steady, measured; calm-informative [E]. AI or human not determinable | **Absurd deadpan escalation**: "…kneel in the center, and spread your arms wide to summon the great water meloness, preparing to receive his blessing." Punchline; no loop |
| 2 | "If someone has bone cancer in their femur, a surgeon (will sometimes amputate…)" | Captions only | Conditional (third person) + medical shock | Same ZDF style; y ≈1,495 px | Flat-shaded 3D anatomy on a sky-blue gradient; cross-section cutaways. Switches to live-action stock at 34 s | Bed ≈19 dB under the voice | Calm-informative [E] | Resolution / benefit: "…gives more stability and mobility." |
| 3 | **None (wordless)** | No captions. An in-scene "ZACK D FILMS" sign at ~6 s | Pure visual process: cut → wrap moss → roots → pot | None | ZDF 3D, macro shots of hands | Music only; quiet (−26.8 LUFS) | — | Resolution: the grown plant, with the character admiring it |
| 4 | "If you have a headache, don't try to take pain relievers, (because this might make it even worse.)" | Captions. Mascot is sipping from a mug at 0.0 s; mug and pills shatter at ~2 s | Conditional + **contrarian warning** | 2–3 words, lowercase. White bold sans with thin dark outline. Height ≈65 px. **y ≈1,410 px (≈73%)** | 3D bald mascot; kitchen, then shower | Continuous bed or ambience (the shower scene) only ~1–17 dB under the voice | Calm, instructional [E]. Not determinable; pitch differs from #5, so a different voice | Resolution: "…massage the tragus of your ear to further ease the tension." |
| 5 | "If you're scared of getting your wisdom teeth removed, (drinking pineapple juice before might actually help.)" | 3D "SimpliHow" logo text in the scene at 0.0 s, plus captions | Conditional + reassurance hack | 1–2 words. White bold with thin outline. Height ≈50 px. y ≈1,460 px (≈76%) | 3D patient on a blue-grid set; macro shots of the mouth | Bed ≈14 dB under the voice | Calm [E]. Higher voice (median F0 ≈260 Hz) | Resolution: "…little to no swelling or pain." Branded end frame |
| 6 | "If you touch something and your atoms align in just the perfect (way…)" | Captions. "1 in 1,000,000,000…" number overlay at ~9 s | Conditional + impossible claim | 3–4-word lowercase fragments. **Yellow with black outline**, blocky bold. Height ≈42 px. **y ≈1,295 px (≈67%)** | Deliberately crude PS1-style low-poly 3D | **Loud bed**: ≈10–14 dB under the voice | Brisk, dry [E]. Not determinable | **Comic tag** ("…she technically didn't cheat on you"), then escalation ("…they would fuse together and trigger it") and a white-out |
| 7 | "If you point a laser at a plane, you might think you're just hitting it (with a tiny, harmless dot of light. But…)" | Captions. "Low Poly Shorts" logo at ~15 s | Conditional + misconception ("you might think… But") | Same as #6 | Low-poly 3D | Loud bed, ≈4–13 dB under the voice | Brisk, dry [E] | **Dry punchline**: "…making the plane look for a parking spot." |
| 8 | "A major difference between Canada and the US is our slang." | **Persistent series header**: YouTube logo + "Casually Explained: Canada" (y ≈450–590 px, ≈62 px tall, Comic-style font). No speech captions; hand-lettered speech labels ("Pop" / "Soda") | Deadpan topic statement | **None** | MS-Paint-style stick and blob characters on white. A 16:9 clip letterboxed into a band at y ≈720–1,330 px | **No music**: the floor is ≈36 dB under the voice, and pauses are near-silent (median pause level −48.5 dBFS) | **Deadpan, dry human voice**: the creator's own "monotonous stick figure" persona per [Shorty Awards](https://shortyawards.com/9th/casuallye) and [TV Tropes](https://www.tvtropes.org/pmwiki/pmwiki.php/WebAnimation/CasuallyExplained) | Punchline: "…that went from 0 to 100 real quick, while you say 32 to 212." |
| 9 | "So if you ever date or live with the opposite gender, you'll learn the stark differences (in thought process right away.)" | Header "Casually Explained: Interior Design" | Relatable conditional | None | Static stick figures | No music (floor ≈33 dB under the voice) | Deadpan, human | Punchline: "Which is really pretty ignorant. They clearly didn't see the gaming computer." |
| 10 | "Now, even though Canada is known as the Great White North, if you look at (the demographics of Vancouver, I'm in fact a minority.)" | Header; map labels | Contrarian statement. Starts mid-thought ("Now,"), a sign it was clipped from a long-form video | None | Stick figure + Wikipedia screenshot + a map filled in colour by colour | No music (floor ≈31 dB under the voice) | Deadpan, human | List-style punchline: "…All the other territories are climate change insurance." |
| 11 | "How do sperm whales catch giant squid?" | Same words as the caption at 0.5–2 s, with "WHALES" and "GIANT" boxed in red | Direct question | 3–5 words, **ALL CAPS condensed bold** (Bebas/Oswald-like), white with shadow. **A red rounded box highlights 1–2 key words.** Cap height ≈42 px. **Top: y ≈370 px (≈19%)** | **Hand-drawn doodle**: thick black outlines, textured flat fills; stick-figure scientist | Bed ≈15–17 dB under the voice | Calm, conversational [E]. Narrowest pitch spread among the human narrators (≈2 semitones SD) | Resolution with a dry line: "…so the whale almost always wins." |
| 12 | "Did you know that it's much safer to fight with pillows than it is to fight with (giant cinder blocks on top of a 58-story building?)" | **One word at a time** ("that", "much", "pillows", "fight") | "Did you know" + absurd non-fact | **Single word, very large** (≈135 px tall). White condensed bold with soft shadow. **Dead centre, y ≈975 px** | Stock footage: pillow fight, then a construction site | Floor ≈25 dB under the voice | **Flat and TTS-like**: no pause ≥0.25 s, 257–280 WPM, narrowest pitch spread (1.3 semitones SD). *Inferred TTS* | The joke lands at 6.3 s. At this length the video simply loops |
| 13 | "Overheard my 26M fiance 24F tell (her friend on the phone…)" | Reddit-post title in a white rounded box (y ≈360–560 px) for about the first 10 s | Story title read aloud | 1–2-line sentence subtitles. White regular-weight sans with thin shadow. ≈40 px. y ≈955 px | Full-frame Subway Surfers gameplay | Game audio ≈22–32 dB under the voice | TTS-like: very uniform ~1 s sentence gaps; tagged #capcut. *Inferred TTS* | (Only the first 60 s analysed; 239-s story) |
| 14 | "I'm guessing YouTubers' names, all right. Up first, I show speed." | None. An animated 3D card carousel from frame 0 | Challenge premise | None | Selfie talking head + 3D overlay | Low bed, ≈20–25 dB under the voice | Human, on camera; conversational with reaction pauses of 2.4–3.5 s | Self-deprecating punchline: "…I don't know why it made me do that voice." |
| 15 | Music-led; dialogue not reliably transcribed | None | In medias res horror skit | None | Cinematic live action, saturated pinks | Music ≈ voice level (0.7–5 dB) | Human, on camera; excited/screaming [E] | Cliffhanger scream [E] |

**SFX.** I did not measure sound effects separately, because I could not hear the audio and did not run onset detection. The only first-hand sound facts are the bed and floor levels above. In the Casually Explained clips, the median pause level of −44.0 to −48.5 dBFS shows nothing (music or SFX) plays under the pauses.

### Inferences
- **Two very different "calm" families both work.**
  - The *3D explainer* family (ZDF, SimpliHow) narrates at 141–192 WPM. It keeps a bed under the voice, moves from frame 0 and never freezes.
  - The *deadpan 2D* family (Casually Explained, and MinuteEarth's doodles) narrates *faster* (207–245 WPM) over 94–97% frozen frames. It relies on dry voice, a joke per sentence and a pop-on image every 2–5 s.
- **Casually Explained's TikToks are repurposed long-form clips.** Each is a 16:9 excerpt letterboxed on white with a "Casually Explained: <Topic>" header, and they still reach 0.5–2.4M views. A simple, consistent series header is a cheap on-screen hook for a static 2D style.
- **Zack D. Films is still posting 2026 Shorts with no hard cuts** (#1, #3). One of them, #3, is entirely wordless with no captions, so a "how-to" can work as a pure visual process.

### Gaps
- Kurzgesagt (TikTok "private / log in" message) and every YouTube-hosted original could not be viewed. I have no first-hand YouTube data, and YouTube Shorts loudness/encoding may differ from TikTok's.
- There is no true whiteboard (marker-on-white) sample. MinuteEarth (doodle) and Casually Explained (stick figure) are the nearest.
- No faceless channel *documented* as using an AI voice was found with ≥1M views. The two TTS-like samples are identified by inference only, and one of them (#13) has low views.
- Brainrot is represented by a low-view (27.8K), long (239 s) Reddit-story video. Better-performing short brainrot examples were not found in a few searches.
- Sample sizes per style are 1–3 videos. Views are not retention, and no retention data is public.

## Which earlier dataset-based findings are confirmed, corrected or contradicted first-hand?

### Takeaway
- **The method and the 3D-explainer numbers replicate almost exactly.** The same Low Poly video measured first-hand on TikTok gives 206 WPM, a first cut at 1.2 s and 4.64 hard cuts per 10 s. The earlier YouTube-based measurement gave 206 WPM, 1.2 s and 4.6.
- **Confirmed:** the instant first word, ~10–11 words in the first 3 s, ZDF's near-zero cut rate, lower-middle 1–3-word captions for the 3D family, and no spoken CTAs.
- **Corrected:**
  - "Calm ≈ 171 WPM" holds only for the 3D family. The deadpan and doodle samples run 207–245 WPM.
  - Loop endings are rare. Punchline or dry-tag endings dominate.
- **Contradicted for hand-drawn styles:** "always moving at frame 0" and "no silences ≥0.4 s".

### Cited Findings

| Earlier claim [D] | First-hand result [M] | Verdict |
|---|---|---|
| Median ≈171 WPM for faceless winners; ZDF 144–177 WPM ([earlier pass, json3 captions](https://github.com/Peiush/Yt-channel-folders/tree/main/yt-channel/edge-of-alive-research/work/competitors/raw/media)) | ZDF + SimpliHow (n=4): median 165 WPM, range 141–192 ([#1](https://www.tiktok.com/@zackdfilms92/video/7708059129335598350), [#2](https://www.tiktok.com/@zackdfilms92/video/7315249587311201582), [#4](https://www.tiktok.com/@simplihowww/video/7445347531694837022), [#5](https://www.tiktok.com/@simplihowww/video/7511853084750941470)). All 12 narrated faceless videos: median **208.5**, range 141–257. Casually Explained 210–245 ([#8](https://www.tiktok.com/@casuallyexplained/video/7583651459095465223), [#9](https://www.tiktok.com/@casuallyexplained/video/7576414392284237063), [#10](https://www.tiktok.com/@casuallyexplained/video/7583207422945201415)). MinuteEarth 207 ([#11](https://www.tiktok.com/@minuteearth/video/7636354677780614414)) | **Confirmed for 3D explainers; corrected for deadpan/doodle**, which run faster, not slower |
| Same Low Poly Short on YouTube: 206 WPM, first hard cut 1.2 s, 4.6 hard cuts/10 s ([earlier Table A row 9](https://www.youtube.com/shorts/0U6OcfxYZ7U)) | TikTok copy: 206 WPM, first cut 1.2 s, 4.64/10 s; 86.6M views on TikTok vs 53.1M on YouTube ([#6](https://www.tiktok.com/@lowpolyshorts/video/7606648171032317197)) | **Confirmed exactly.** This validates the earlier dataset method |
| First word at ≈0.08 s (max 0.16 s) | 12/12 narrated videos start at 0.0 s (Whisper); TikTok caption cues start at 0.00–0.10 s (all videos above) | **Confirmed** |
| Median 10 words in the first 3 s (range 7–14) | Median 11 (range 6–17); 3D family 9–11; Casually Explained 11–16; MinuteEarth 7 | **Confirmed** |
| ZDF mega-hits use almost no hard cuts | ZDF #1 and #2: 0 hard cuts (0 and 0.25 soft cuts per 10 s); zero frozen frames; a continuous camera does the work ([#1](https://www.tiktok.com/@zackdfilms92/video/7708059129335598350), [#2](https://www.tiktok.com/@zackdfilms92/video/7315249587311201582)) | **Confirmed**, including on a Nov-2026 upload |
| SimpliHow 0–0.7 hard cuts per 10 s, 162–178 WPM | 0.69–0.9 hard cuts per 10 s, 152–192 WPM ([#4](https://www.tiktok.com/@simplihowww/video/7445347531694837022), [#5](https://www.tiktok.com/@simplihowww/video/7511853084750941470)) | **Confirmed** |
| Something moves at frame 0 (6 of 8 ZDF) | 3D and live samples move by 0.1 s. Casually Explained is 97% frozen, with its first visual change at 1.4–3.4 s; MinuteEarth's first motion comes at 1.6 s, 94% frozen ([#8–#11](https://www.tiktok.com/@minuteearth/video/7636354677780614414)) | **Confirmed for 3D; contradicted for hand-drawn** |
| Captions are 1–3 white bold words, lower-middle (~75% height) ([frame_notes.md](https://github.com/Peiush/Yt-channel-folders/blob/main/yt-channel/edge-of-alive-research/work/competitors/raw/frame_notes.md)) | ZDF y ≈1,490–1,500 px (78%); SimpliHow y ≈1,410–1,460 px (73–76%); Low Poly y ≈1,295 px (67%, yellow). But 6 of 15 have no speech captions (Casually Explained ×3, ZDF #3, MrBeast, Alan). MinuteEarth puts captions at the top (≈370 px); Useless Info and the Reddit video put them dead centre (≈955–975 px) | **Confirmed for 3D explainers; not universal** |
| Word-by-word karaoke highlighting is common in some channels | Seen in 1 of 15 (MinuteEarth: a red box on key words). The 3D explainers swap 1–3-word chunks with no highlight | **Corrected**: highlighting is optional |
| No spoken CTA in ZDF (0/8) | 0 of the 12 fully transcribed closings contains a follow, subscribe or "watch more" CTA (closing words in Table B). Not counted: #3 is wordless, #13 was truncated at 60 s, #15's dialogue was unreliable | **Confirmed** |
| Loop endings recommended (only 2–3/26 loops in the earlier sample) ([06_video_breakdowns §7](https://github.com/Peiush/Yt-channel-folders/blob/main/yt-channel/edge-of-alive-research/06_video_breakdowns.md)) | 0/13 voiced videos end on a seamless spoken or visual loop. 8/13 end on a punchline or dry tag (Casually Explained ×3, Low Poly ×2, ZDF #1, MinuteEarth, MrBeast); 9/13 if Useless Info's one-joke reveal counts. 3/13 end on a plain resolution (ZDF #2, SimpliHow ×2); 1 is undetermined (#13, truncated) | **Corrected**: punchline/dry tag is the dominant ending; loops are rare |
| No silence gaps ≥0.4 s in 25/28 videos ([06_video_breakdowns](https://github.com/Peiush/Yt-channel-folders/blob/main/yt-channel/edge-of-alive-research/06_video_breakdowns.md)) | True for videos with a bed (0 silences below −35 dB in ZDF #1/#2, SimpliHow and Low Poly). Casually Explained has 1–4 true silences of 0.27–0.59 s per clip, and 16–17% of its speech span sits ≥20 dB under the voice | **Confirmed for bedded explainers; contradicted for the deadpan dry-voice style** |
| Master to about −14 LUFS; ZDF Stitches −12 LUFS; TikTok does not level files (median −21.2) ([delivery study](https://github.com/shortformkit/short-form-video-delivery-2026)) | TikTok-served files range −26.8 to −7.4 LUFS (median −15.6). ZDF −9.2/−10.4 with **true peaks over 0 dBTP** (+1.5/+2.1); Casually Explained −12.7 to −14.7; Low Poly −15.6/−15.8; SimpliHow 12.4M-view video at −23.4 | **Confirmed that TikTok does not normalise**: winners sit anywhere from −9 to −23 |
| "If/when you…" conditional is the most common opener (11/26) | 6/13 voiced open with "If…" (#2, #4–#7, #9). Others: imperative (#1), question (#11), "Did you know" (#12), statement (#8, #10), title read-out (#13), challenge (#14) | **Confirmed** as the most common single form |
| High-energy creators cut ~46/min; first cut ≈2.25 s ([hook study](https://github.com/shortformkit/short-form-video-hook-study-2026)) | Alan Chikin Chow: 11.4 hard cuts per 10 s (68/min), first cut 1.0 s, −7.9 LUFS. MrBeast's 90.2M Short is a single take with an animated overlay (0 cuts) | **Confirmed for skits**. Some high-energy hits are one take; energy comes from the delivery |

### Inferences
- The earlier dataset's ZDF/SimpliHow/Low Poly numbers can be trusted. Direct measurement adds the 2D/deadpan evidence it lacked, and that evidence changes the pace advice (see Q3).
- **True-peak overs on ZDF's TikTok files** (+1.5/+2.1 dBTP) suggest a hot master pushed into TikTok's AAC encode. Copying that loudness would risk audible clipping; the safer target stays at −14 LUFS / −1 dBTP.

### Gaps
- No YouTube files could be compared first-hand, so YouTube-specific delivery (normalisation, re-encode) is unverified here.
- Earlier rows 1–5 and 7–16, the YouTube mega-hits, were not re-measured directly. Only channel-level replication was possible.

## What do the calm, deadpan and hand-drawn examples do with pace and pauses? How slow can successful narration be, and where do the silences go?

### Takeaway
None of the successful narrated faceless videos is slow:
- The slowest is ZDF at 141 WPM (#2). SimpliHow's 3.8M-view video runs 152 WPM. The earlier YouTube data puts ZDF's 138M–255M hits at 144–149 WPM. **No successful narrated sample runs below ~140 WPM.**
- **Deadpan is fast speech plus frequent short beats.** Casually Explained talks at 210–245 WPM but pauses 18–31 times a minute, mean 0.45–0.50 s, max 0.74–0.84 s, on dry silence.
- **The longest pauses fall in three places, never mid-clause:** right after the hook question or claim, between how-to steps, and just before the punchline. They are 0.6–0.96 s long, and none is longer than 1.0 s.

### Cited Findings
- **Pause statistics [M].** The table gives pauses ≥0.25 s per video: mean / max, then rate per minute.

  | Style | Video | Mean / max (s) | Per min |
  |---|---|---|---|
  | Calm 3D | ZDF #1 | 0.47 / 0.72 | 15.2 |
  | Calm 3D | ZDF #2 | 0.51 / 0.76 | 13.3 |
  | Calm 3D | SimpliHow #4 | 0.46 / 0.76 | 16.2 |
  | Calm 3D | SimpliHow #5 | 0.41 / 0.80 | 12.5 |
  | Brisk | Low Poly #6 | 0.34 / 0.48 | 9.3 |
  | Brisk | Low Poly #7 | 0.34 / 0.52 | 16.4 |
  | Deadpan | Casually Explained #8 | 0.45 / 0.78 | 31.4 |
  | Deadpan | Casually Explained #9 | 0.50 / 0.84 | 17.9 |
  | Deadpan | Casually Explained #10 | 0.47 / 0.74 | 28.9 |
  | Doodle | MinuteEarth #11 | 0.52 / 0.96 | 17.8 |
  | TTS-like | Useless Info #12 | no pause ≥0.25 s | 0 |
  | TTS-like | Reddit #13 | 0.82 / 1.22 | 20.0 |

  Mean sentence-boundary gap: ZDF 0.42 s; SimpliHow 0.48–0.59 s; Low Poly 0.24–0.27 s; Casually Explained 0.35–0.55 s; MinuteEarth 0.60 s; Reddit TTS 0.93 s. — [#1](https://www.tiktok.com/@zackdfilms92/video/7708059129335598350), [#2](https://www.tiktok.com/@zackdfilms92/video/7315249587311201582), [#4](https://www.tiktok.com/@simplihowww/video/7445347531694837022), [#5](https://www.tiktok.com/@simplihowww/video/7511853084750941470), [#6](https://www.tiktok.com/@lowpolyshorts/video/7606648171032317197), [#7](https://www.tiktok.com/@lowpolyshorts/video/7612238436992322829), [#8](https://www.tiktok.com/@casuallyexplained/video/7583651459095465223), [#9](https://www.tiktok.com/@casuallyexplained/video/7576414392284237063), [#10](https://www.tiktok.com/@casuallyexplained/video/7583207422945201415), [#11](https://www.tiktok.com/@minuteearth/video/7636354677780614414), [#12](https://www.tiktok.com/@uselessinfo_real/video/7407692115519524142), [#13](https://www.tiktok.com/@reddit.andy/video/7175833788730133765)
- **Where the longest pauses fall (≥0.6 s) [M, from word timings].**
  - **After the hook question** (MinuteEarth): 0.96 s after "How do sperm whales catch giant squid?". — [#11](https://www.tiktok.com/@minuteearth/video/7636354677780614414)
  - **Before the climax** (MinuteEarth): 0.94 s before "Then, at the last second of approach…". — [#11](https://www.tiktok.com/@minuteearth/video/7636354677780614414)
  - **After the contrarian line** (SimpliHow): 0.76 s after "…might make it even worse." and before "Instead, get into a warm shower…". — [#4](https://www.tiktok.com/@simplihowww/video/7445347531694837022)
  - **Between how-to steps** (ZDF): 0.66 s after "…to make one slice." and 0.72 s after "…repeating this to make more." — [#1](https://www.tiktok.com/@zackdfilms92/video/7708059129335598350)
  - **Before the absurd turn** (ZDF): 0.62 s before "…kneel in the center…". — [#1](https://www.tiktok.com/@zackdfilms92/video/7708059129335598350)
  - **Around punchlines and tags** (Casually Explained):
    - 0.78 s before "We like to say, that went from 0 to 100…" — [#8](https://www.tiktok.com/@casuallyexplained/video/7583651459095465223)
    - 0.72 s after "…and say," and before "are you gonna get literally any furniture?" — [#9](https://www.tiktok.com/@casuallyexplained/video/7576414392284237063)
    - 0.84 s before the tag "Which is really pretty ignorant." — [#9](https://www.tiktok.com/@casuallyexplained/video/7576414392284237063)
    - 0.74 s inside a rapid deadpan list ("Earth is flat, ‖ definitely flat, milk in a bag…"). — [#10](https://www.tiktok.com/@casuallyexplained/video/7583207422945201415)
- **Speed of the slowest successful narration [M].** ZDF #2: 141 WPM (184.7K TikTok views). SimpliHow #5: 152 WPM (3.8M). — [#2](https://www.tiktok.com/@zackdfilms92/video/7315249587311201582), [#5](https://www.tiktok.com/@simplihowww/video/7511853084750941470) Earlier YouTube measurements [D]: ZDF "Blown Veins" 144 WPM (138M) and "How Stitches Work" 149 WPM (255M). — [earlier pass](https://github.com/Peiush/Yt-channel-folders/tree/main/yt-channel/edge-of-alive-research/work/competitors/raw/media)
- **What the picture does during pauses [M].**
  - 3D explainers keep moving through pauses. ZDF #1 has the same motion level in gaps as in speech (15.2 vs 15.6, mean frame difference) and 0% frozen frames; Low Poly has 0–4% frozen.
  - Casually Explained and MinuteEarth are frozen in 90–94% of their pause frames, with holds of up to 3.6–4.8 s. New drawings pop on every ~2–5 s, usually on the punchword (frames at 6/9/12/15 s in #8 show "Pop"/"Soda" → "Toque"/"Beanie" → "Washroom"/"Restroom" → "Ambulance").
  - MinuteEarth's captions keep changing every ~1 s while the drawing holds [E].
  - — [#1](https://www.tiktok.com/@zackdfilms92/video/7708059129335598350), [#6](https://www.tiktok.com/@lowpolyshorts/video/7606648171032317197), [#8](https://www.tiktok.com/@casuallyexplained/video/7583651459095465223), [#11](https://www.tiktok.com/@minuteearth/video/7636354677780614414)
- **Pauses are bedded or dry depending on style [M].**
  - Casually Explained pauses are near-silent: the median pause level is −44.0 to −48.5 dBFS, and voice-to-floor is 31–37 dB.
  - ZDF, SimpliHow, Low Poly and MinuteEarth pauses are filled by a bed (voice-to-floor 13–22 dB; no silencedetect hits at −35 dB).
  - — Table A rows 1–11
- **TTS signatures [M; attribution inferred].**
  - The "Useless Info" voice runs 257 WPM total and 280 WPM over the speech span, with **no** gap ≥0.25 s.
  - The CapCut-tagged Reddit video inserts near-uniform ~1.0 s gaps between sentences (12 of 16 sentence gaps fall between 0.94 and 1.22 s), unlike the human narrators' 0.35–0.6 s mean sentence gaps.
  - — [#12](https://www.tiktok.com/@uselessinfo_real/video/7407692115519524142), [#13](https://www.tiktok.com/@reddit.andy/video/7175833788730133765)
- **Pitch variability [M, low confidence].** pYIN was run with octave errors folded into ±6 semitones. Only two voices came out clearly narrow: the TTS-like "Useless Info" at 1.3 st SD and MinuteEarth at ≈2.1 st SD. The rest came out at 2.7–3.6 st SD, close to the ≈3.5 st SD that random noise produces under this folding, so they are inconclusive. Music beds and few voiced frames limit the method. **Pitch therefore cannot rank "deadpan vs calm" here.** — metrics JSON (scratchpad)
- **Deadpan persona (third-party).** Casually Explained's narrator is described as "the monotonous stick figure man", and its videos "seem like sincere takes" that turn into irony and self-deprecation. — [Shorty Awards](https://shortyawards.com/9th/casuallye); [TV Tropes](https://www.tvtropes.org/pmwiki/pmwiki.php/WebAnimation/CasuallyExplained)
- **High-energy contrast.** MrBeast talks at 125 WPM but with reaction pauses up to 2.4–3.5 s. Energy there comes from on-camera expression and a moving overlay, not pace. — [#14](https://www.tiktok.com/@mrbeast/video/7670566355153833246)

### Inferences
- **For a calm/deadpan AI narrator, "slow" is the wrong control.** Measured deadpan comes from four things:
  - (a) flat delivery;
  - (b) dry sentence construction, a sincere set-up followed by an ironic tag;
  - (c) many short beats of 0.4–0.6 s;
  - (d) one longer beat of 0.7–0.95 s before each punchline or turn.

  Overall pace stays at ≥150 WPM, and the calm 3D winners cluster at 165–190 WPM.
- **Silence vs bed is a stylistic switch:**
  - Dry voice with true silences reads as deadpan (Casually Explained).
  - A low bed under the pauses reads as calm-explainer (ZDF, MinuteEarth).
  - A loud bed with almost no pauses reads as brisk or energetic (Low Poly).
- **Static 2D needs either jokes or motion.** Casually Explained gets away with 97% frozen frames because nearly every sentence is a joke and the persona is established. A new channel with "boring but useful" content should add idle motion; this is an inference, not tested here.
- **Avoid the obvious TTS signatures:** zero pauses (#12) or perfectly uniform ~1 s inter-sentence gaps (#13). Vary the beats by function (0.4 / 0.65 / 0.9 s).

### Gaps
- Tone could not be judged by ear, and the pitch method was inconclusive for most voices. A human listen-through of 3–5 of these clips would confirm the "flat vs lively" labels.
- n=3 deadpan and n=1 doodle. I found no slow (<140 WPM) narrated faceless video with ≥100K views to test the lower bound, so the absence of slow successes is a sampling observation, not proof.

## Derived spec for this channel: narration, pauses, hook, visual rhythm, captions with pixel safe zones, music and SFX, loudness, ending, and a first-3-seconds checklist

### Takeaway
For a 25–40 s faceless, deadpan AI-narrated vector/hand-drawn tip Short, structured Hook → Why → What → How → Solution:
- **Narration:** 165–195 WPM overall, about 2.9 words per second. That is faster than the toolkit's default 2.5 words/s budget.
- **First line:** the first word at 0.0–0.1 s, and a 9–12-word hook clause finished by about 3 s.
- **Beats:** 0.4–0.6 s at sentence ends, 0.6–0.75 s between steps, 0.75–0.95 s before the punchline, and never more than 1.0 s.
- **Visuals:** motion from frame 0, a new drawn element every 2–4 s, and no hold longer than 4.5 s. Caption chunks change every 0.5–1 s.
- **Captions:** 1–3-word white rounded-bold captions centred at y ≈1,320–1,440 px.
- **Sound:** either no music (dry deadpan) or a bed whose quietest moments sit ~18–22 dB below the voice.
- **Loudness and ending:** −14 LUFS / −1 dBTP, ending on a dry tag with no spoken CTA.

Everything below is an **[E] inference** from the [M] measurements cited.

### Cited Findings (the evidence each spec item rests on)
- **Pace.** Calm 3D winners run 141–192 WPM (median 165). Deadpan stick-figure clips run 210–245. No successful narrated sample is below ~140. — Q3 sources; [#1](https://www.tiktok.com/@zackdfilms92/video/7708059129335598350), [#4](https://www.tiktok.com/@simplihowww/video/7445347531694837022), [#8](https://www.tiktok.com/@casuallyexplained/video/7583651459095465223)
- **Hook.** The first word comes at 0.0–0.1 s in 12/12 narrated videos, with a median of 11 words before 3 s. "If…" is the most common opener (6/13). A contrarian follow-up appears in #4 ("don't try to take pain relievers") and #7 ("you might think… But"). — [#4](https://www.tiktok.com/@simplihowww/video/7445347531694837022), [#7](https://www.tiktok.com/@lowpolyshorts/video/7612238436992322829)
- **Visual rhythm.**
  - The 3D group moves from 0.1 s, with a first visual event by 0.5–2.0 s: laser 0.5 s, tumour 1.0 s, smash 2.0 s, cut 1.2–1.8 s.
  - The 2D group is 94–97% frozen, with holds of ≤4.8 s.
  - — Table A
- **Caption placements measured on a 1920-px-high frame** (centre y):

  | Channel | Centre y | Text height | Colour / treatment |
  |---|---|---|---|
  | ZDF | ≈1,495 px | ≈65 px | — |
  | SimpliHow | ≈1,410–1,460 px | 50–65 px | — |
  | Low Poly | ≈1,295 px | ≈42 px | yellow |
  | MinuteEarth | ≈370 px | ≈42 px caps | red keyword box |
  | Useless Info | ≈975 px | ≈135 px | one word at a time |
  | Reddit | ≈955 px | ≈40 px | — |

  — Table B
- **Platform UI margins** are approximations from vendor tools, not official numbers.
  - TikTok: top 120–200 px, bottom 250–370 px, right 120–164 px, left 50–60 px, on a 1080×1920 canvas. — [AdMake](https://www.admakeai.com/blog/vertical-video-dimensions-2026); one vendor gives a central safe area of 900×1492 (bottom 320, right 120, top 108). — [TryMyPost](https://www.trymypost.com/blog/tiktok-ad-specs-2026-safe-zones)
  - YouTube Shorts: about right 120 px, bottom 380 px, top 180 px for organic posts. — [PostEverywhere](https://posteverywhere.ai/blog/youtube-shorts-aspect-ratio)
  - Google's ad-oriented figures are far stricter: top 288 px, bottom 672 px, right 192 px. — [Socialync](https://www.socialync.io/tools/safe-zones/youtube-shorts)
  - Platforms publish safe zones only for ads; organic overlays vary. — [Socialync](https://www.socialync.io/tools/safe-zones); [Reap](https://reap.video/blog/short-form-video-safe-zones)
- **Bed level.** Voice-to-floor is ZDF 19–22 dB, MinuteEarth 17, SimpliHow 14–17, Low Poly 13–14 and Casually Explained 31–37 (no music). — Table A
- **Loudness.** TikTok-served winners span −9.2 to −23.4 LUFS. LRA is 1.5–3.7 LU for the narrated faceless videos. ZDF has true-peak overs. — Table A
- **Endings.** 8/13 voiced videos end on a punchline or dry tag (9/13 counting #12), 3/13 on a plain resolution and 0/13 on a loop. None of the 12 fully transcribed closings has a spoken CTA. The tail after the last word is 0.33–1.36 s. — Table B; metrics JSON
- **Length.** Narrated faceless winners run 21–41 s (MinuteEarth 64 s, 187K views). — Table A

### Inferences (the spec)

**1. Runtime and word budget**
- Target 25–40 s.
- Budget **2.9 words per second** for the whole runtime: about 87 words for 30 s and about 116 for 40 s.
- Plan the TTS speaking rate so that speech within clauses runs at ~195–215 WPM, then add the beats below to land at 165–195 WPM overall.
- Do not plan for 150 WPM (2.5 w/s) with long pauses. No successful sample does that.

**2. Pause map for the AI voice** (insert explicit SSML or `[pause]` markers)
- Comma or within-sentence: 0.15–0.3 s.
- Sentence end: **0.45–0.6 s**.
- Between How-steps: **0.65–0.75 s**.
- After the Hook line (before "Why"), and just before the Solution or punchline: **0.8–0.95 s**.
- Never more than 1.0 s.
- Aim for 12–20 beats ≥0.25 s per minute; up to ~30 per minute is fine for list-style deadpan.
- Vary beat lengths by function. Uniform 1.0 s gaps sound like TTS.
- End the audio 0.4–0.9 s after the last word.

**3. Hook spec (first 1.5–3 s)**
- **Spoken:** the first word at 0.0–0.1 s, with 9–12 words by 3.0 s. Pick one of three templates:
  - (a) "If you [everyday situation], [contrarian instruction]." Modelled on #4.
  - (b) An imperative that is already doing the thing: "[Do X] like this." Modelled on #1.
  - (c) "If you [action], you might think [misconception]. But…" Modelled on #7.
- **On-screen:** the first caption chunk visible at 0.0 s. Optionally add a persistent small series header at the top, e.g. "Boring But Useful: <Topic>", at y ≈420–560 px. This is the Casually Explained pattern, and it gives the sound-off viewer the topic.
- **Visual:** the problem object is already in motion at frame 0, for example a hand mid-action or an object falling. The first distinct visual event (pop-on, smash, zoom accent) comes by 1.0–2.0 s.

**4. Visual-change rhythm (vector or hand-drawn)**
- One new drawn element, pose or label per sentence, i.e. every ~2–4 s.
- **No unchanged frame for more than 4.5 s.** That is the measured maximum for successful 2D.
- Keep low-level idle motion running underneath: blink, breathing bob, slow 2–5% camera push. This keeps frozen frames well under the 94–97% seen in Casually Explained and MinuteEarth.
- Hard cuts are optional: 0–1 per 10 s is in line with ZDF, SimpliHow, Casually Explained and MinuteEarth. Going above ~4 per 10 s reads as brisk (Low Poly).
- Time pop-ons to the punchword. Hold the picture still through the pre-punchline beat, then reveal on the punchline.

**5. Caption spec (1080×1920)**
- **Chunk and timing:** 1–3 words in sentence case, swapped at phrase boundaries every ~0.5–1.0 s. Cut on and off; no bounce.
- **Font and treatment:** white heavy rounded sans; soft drop shadow or a 3–4 px dark outline.
- **Size:** text block ≈60–70 px tall (font size ≈72–84 px), matching ZDF and SimpliHow.
- **Keyword accent:** optional, on one key word per caption, as a coloured box or text (MinuteEarth uses a red box).
- **Position:** centre y **≈1,320–1,440 px**, so the caption's bottom edge is no lower than ≈1,480 px, leaving ≥440 px clear at the bottom.
  - This sits a little above where ZDF and SimpliHow put theirs (1,410–1,500), so it stays clear of TikTok's ~250–370 px bottom UI and the ~380 px YouTube Shorts organic overlay.
  - Under the stricter 672-px ad figure, move it to centre y ≈1,180–1,240 px.
- **Horizontal:** keep text within x ≈90–930 px, clear of the right-side rail (≥150 px from the right edge). Keep anything at the top below y ≈220 px.
- Validate every template once against the live TikTok and Shorts apps, since the vendor margins are approximations.

**6. Music and SFX**
- **Option A, "dry deadpan" (the Casually Explained sound):** no music, a clean voice, and a room-tone floor at or below −45 dBFS, so the beats are true silence.
- **Option B, "calm explainer" (ZDF/MinuteEarth):** a soft, steady bed mixed so its quietest moments sit **~18–22 dB below the voice**. In practice that is music about −20 dB relative to dialogue loudness, e.g. voice at −14 LUFS and bed at about −34 LUFS short-term.
- **Avoid** Low Poly-style beds, which sit only ~13 dB under the voice and fill every gap. They signal energy, not calm.
- **SFX** were not measured first-hand. The suggestion of sparse, soft, diegetic sounds (pop, pencil scratch, snip) on pop-ons, with no meme SFX, is tone-matching inference only.

**7. Loudness**
- −14 LUFS integrated (±1), true peak ≤ −1.0 dBTP, LRA ≤ 4 LU.
- Rationale: winners on TikTok range from −9 to −23 LUFS because TikTok does not normalise, and ZDF's hot masters show over-0 true peaks after transcoding.

**8. Ending**
- End on a **dry one-line tag or deadpan escalation** right after the Solution, as in ZDF #1's "summon the great water meloness", Low Poly's "look for a parking spot" or MinuteEarth's "the whale almost always wins". The alternative is a clean resolution image.
- No spoken CTA.
- A loop line is optional and was not observed in this sample.
- Cut 0.4–0.9 s after the last word.

**9. First-3-seconds checklist**
1. The first spoken word starts at 0.0–0.1 s. No intro, logo or greeting.
2. 9–12 words are spoken by 3.0 s, ending the hook clause; it uses "you" or an imperative.
3. The hook contains a contrarian or "you might think…" turn, or an instruction already in progress.
4. Frame 0 shows the subject and something already moving. It is not a fade-in.
5. The first caption chunk is on screen at 0.0 s at centre y ≈1,320–1,440 px, white rounded bold, with a shadow or outline.
6. Optional: a series header at the top (y ≈420–560 px) names the topic for sound-off viewers.
7. One distinct visual event (pop-on, smash, zoom accent) lands by 1.0–2.0 s.
8. The bed (or dry room tone) and the voice start together at 0.0 s.
9. An 0.8–0.95 s beat is placed after the hook line, before "Why".
10. The final line is checked to work as a dry tag, and there is no CTA.

### Gaps
- No first-hand YouTube Shorts files, so YouTube delivery loudness and caption overlap with the live Shorts UI are unverified.
- The safe-zone pixel margins come from vendor tools that say they are approximations. Neither platform's official organic overlay template was retrieved.
- SFX use, narrator tone by ear, and retention effects were not measured. The spec should be A/B-tested on the channel's first 10–20 uploads (Option A dry vs Option B bedded; 170 vs 190 WPM) using retention curves.
