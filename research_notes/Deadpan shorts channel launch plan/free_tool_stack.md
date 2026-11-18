# Free (or near-free) tool stack for faceless vertical 9:16 Shorts/TikToks (as of Nov 18, 2026)

Scope: a solo creator making deadpan "boring but useful" tips and odd facts for Gen Z, English, about 60 s or shorter, 1080x1920 at 30 fps. Style: slow, calm AI narration, simple vector, hand-drawn or whiteboard animation. Budget near zero. Work happens inside `/home/user/claude-code-video-toolkit`.

Method note (read first): from this cloud session, direct page fetches to remotion.dev, elevenlabs.io, modal.com and huggingface.co failed (the hosts are outside the session's allowed network domains). github.com fetches worked. So:
- GitHub-hosted facts (LICENSE files, READMEs) were read directly.
- Most pricing and terms figures come from search-engine summaries of official pages and of 2026 third-party guides.
- The confidence level is flagged on every finding. Anything that matters for money or legal risk should be checked once on the vendor page before launch.

---

## Q0. What the repo already has vs. what is missing (context for every section below)

### Takeaway
The toolkit already covers:
- TTS: ElevenLabs, and Qwen3-TTS on RunPod or Modal.
- Music: ACE-Step through the free acemusic.ai key.
- SFX: ElevenLabs.
- Images and video: FLUX.2 and LTX-2.
- FFmpeg, and timing sync from audio to config.
- Remotion 4.0.425 templates with `@remotion/paths` and `@remotion/shapes`.

It has **no vertical composition, no free local TTS (Kokoro/Piper), no caption or transcription pipeline (Whisper), and no hand-drawn rendering library (rough.js/Lottie)**.

### Cited Findings
- The registry's global default resolution is `{"width":1920,"height":1080}` at `defaultFps: 30`. The 3 templates are sprint-review, sprint-review-v2 and product-demo, and all are landscape. — [toolkit-registry.json](/home/user/claude-code-video-toolkit/_internal/toolkit-registry.json)
- In product-demo, size comes from config (`fps: 30, width: 1920, height: 1080` in `demo-config.ts`), which is passed to `<Composition width/height>` in `Root.tsx`. — [demo-config.ts](/home/user/claude-code-video-toolkit/templates/product-demo/src/config/demo-config.ts), [Root.tsx](/home/user/claude-code-video-toolkit/templates/product-demo/src/Root.tsx)
- Templates pin `remotion`, `@remotion/cli`, `@remotion/paths`, `@remotion/shapes` and `@remotion/transitions` at 4.0.425. One template also uses `@remotion/google-fonts`. There is no `@remotion/captions`, `@remotion/install-whisper-cpp`, `@remotion/lottie` or `roughjs` dependency. — [templates/*/package.json](/home/user/claude-code-video-toolkit/templates/)
- `tools/voiceover.py` supports only `--provider elevenlabs|qwen3`. The default is elevenlabs. — [voiceover.py](/home/user/claude-code-video-toolkit/tools/voiceover.py)
- `qwen3_tts`:
  - Status: "beta". Requires a RunPod account; a Modal endpoint also exists.
  - Speakers: Ryan, Aiden, Vivian, Serena, Uncle_Fu, Dylan, Eric, Ono_Anna, Sohee.
  - Supports `--tone`, `--instruct`, `--temperature`, and voice cloning.
  - Estimated cost: "$0.005-0.10 per generation". The Modal endpoint runs on an A10G GPU.
  - — [toolkit-registry.json](/home/user/claude-code-video-toolkit/_internal/toolkit-registry.json)
- `music_gen` (ACE-Step 1.5) defaults to the `acemusic` cloud API. It has 8 presets: corporate-bg, upbeat-tech, ambient, dramatic, tension, hopeful, cta, lofi. It also supports Modal and RunPod fallback. — [toolkit-registry.json](/home/user/claude-code-video-toolkit/_internal/toolkit-registry.json)
- The `sfx` and `music` tools use ElevenLabs, which is a paid route for commercial use (see Q1). `flux2` offers widths up to 1920 but heights only up to 1280, so it has no native 1920-tall option. `ltx2` tops out at 1024 px. — [toolkit-registry.json](/home/user/claude-code-video-toolkit/_internal/toolkit-registry.json)
- Shared components that could be reused vertically: AnimatedBackground, PointingHand, FilmGrain, Label, SlideTransition, Vignette, and others. — [lib/components](/home/user/claude-code-video-toolkit/lib/components/)
- A grep of tools/, lib/ and templates/ for "whisper" or "caption" finds no transcription or caption tool. The only hit is a music_gen flag about lyric captions. — [tools/music_gen.py](/home/user/claude-code-video-toolkit/tools/music_gen.py)
- CLAUDE.md guidance relevant here:
  - Narration pace is about 150 wpm standard and 120–130 wpm "slow".
  - Word budget is duration × 2.5.
  - `sync_timing.py` reconciles scene lengths with the real audio.
  - The "audio-anchored timeline" pattern is recommended for sub-30 s or tight spots.
  - — [CLAUDE.md](/home/user/claude-code-video-toolkit/CLAUDE.md)

### Inferences
- For a slow deadpan read at about 110–125 wpm, a 50–58 s Short holds roughly 90–115 words. That fits the "few words" brief.
- The missing pieces are small: a vertical template, a free local TTS provider, Whisper-based word captions, and a hand-drawn style layer.

### Gaps
- None for this section.

---

## Q1. Text-to-speech: free, calm/slow/deadpan English voices usable on monetized YouTube/TikTok

### Takeaway
**Kokoro-82M** is the best zero-cost default. It has Apache-2.0 weights, runs locally on CPU, has a `speed` parameter, and is clearly commercial-OK.

**Qwen3-TTS**, already in the repo, is the best "acting" option. It is Apache-2.0, and natural-language instructions can ask for slow, flat delivery. Running it on Modal is effectively free inside Modal's $30/month credit.

The others:
- **edge-tts** is a legal gray area for monetized use. Microsoft has not granted commercial rights.
- **ElevenLabs Free** is non-commercial and requires attribution.
- **Built-in TikTok and CapCut voices** have no clear commercial grant.
- **Azure F0** (0.5M neural characters a month) and **Google Cloud TTS** free tiers are legitimate free commercial routes with SSML rate and pause control. They need a cloud account with a card on file.
- **Piper** works, but each voice's license must be checked. The popular "lessac" voices exclude commercial use.

### Cited Findings

**Kokoro-82M (open weights)**
- The repo is Apache-2.0 and describes "Apache-licensed weights".
- The API is `KPipeline(lang_code='a')` (American) or `'b'` (British), called as `pipeline(text, voice='af_heart', speed=1, split_pattern=...)`. Output is 24 kHz.
- espeak-ng is used as a fallback grapheme-to-phoneme (G2P) step.
- — [GitHub hexgrad/kokoro](https://github.com/hexgrad/kokoro)
- v1.0 was released Jan 27, 2025, with 54 voices across 8 languages under Apache 2.0. This is from search summaries of the HF model card; huggingface.co could not be fetched directly. — [OpenSpeech](https://www.openspeech.dev/models/kokoro-82m); [aireiter guide](https://aireiter.com/blog/kokoro-82m-tts-local-guide)
- Conflict: one 2026 deployment guide has a fragment mentioning CC BY-NC-SA 4.0, but in unclear context. The same guide lists Kokoro as Apache 2.0. The official repo says Apache-2.0. — [Spheron guide](https://www.spheron.network/blog/deploy-open-source-tts-gpu-cloud-2026/) vs [hexgrad/kokoro](https://github.com/hexgrad/kokoro)
- A caveat from secondary sources: "Apache 2.0" for weights does not automatically settle every voice or dataset question. — [VisionStory review](https://www.visionstory.ai/open-source/kokoro-tts); [Kompozy review](https://kompozy.io/reviews/kokoro-tts)

**Piper**
- Active development moved to OHF-Voice/piper1-gpl, and the engine is GPL-3.0. — [GitHub OHF-Voice/piper1-gpl](https://github.com/OHF-Voice/piper1-gpl)
- Piper "makes no license grant of its own over voice models". Rights in a voice depend on its training data.
- **en_US-lessac**: the corpus license "excludes commercial use of the resulting synthesis", and many voices are fine-tuned from lessac.
- **en_US-hifi_tts_92**: CC BY 4.0, so attribution is required, and that requirement carries into fine-tunes.
- A separate "Commercial use" doc lists the permissive voices.
- — [piper1-gpl docs/LICENSING.md](https://github.com/OHF-Voice/piper1-gpl/blob/main/docs/LICENSING.md)

**Microsoft Edge voices via edge-tts**
- edge-tts supports `--rate=-50%`, `--volume` and `--pitch`, and `--write-subtitles` produces an SRT file.
- Custom SSML was removed: "Microsoft prevents the use of any SSML that could not be generated by Microsoft Edge itself". Only a single `<voice>` plus a single `<prosody>` is allowed, so no `<break>` tags.
- The repo appears to be GPL-3.0 (inferred from the LICENSE and gpl-3.0.txt file names).
- — [GitHub rany2/edge-tts](https://github.com/rany2/edge-tts)
- Microsoft Q&A moderators say no public documentation grants commercial rights for Read Aloud or edge-tts audio. They point users to Azure AI Speech for commercial use. One staff answer says commercial use without an Azure subscription "could be a violation of our terms of service". — [MS Q&A 5925556](https://learn.microsoft.com/en-au/answers/questions/5925556/commercial-use-of-edge-read-aloud-voices-via-edge); [MS Q&A 6007729](https://learn.microsoft.com/en-us/answers/questions/6007729/commercial-use-of-microsoft-edge-text-to-speech-vi?page=1#answer-12979213); [MS Q&A 2088770](https://learn.microsoft.com/en-us/answers/questions/2088770/are-opensource-edge-tts-free-for-commercial-use)
- Third-party sites conflict and are not authoritative:
  - edge-tts.com claims outputs are usable commercially, while also saying the voices are subject to Microsoft's terms. — [edge-tts.com terms](https://edge-tts.com/terms/)
  - A GitHub wrapper says "NOT for commercial use". — [ganapap1/TTS_NO_API](https://github.com/ganapap1/TTS_NO_API)

**Qwen3-TTS (open weights; already integrated)**
- Apache-2.0, released Jan 22, 2026, in 0.6B and 1.7B sizes.
- Native English speakers are Ryan ("dynamic male") and Aiden ("sunny American male").
- The models provide "adaptive control of tone, speaking rate, and emotional expression" from instructions.
- No VRAM figures are given.
- — [GitHub QwenLM/Qwen3-TTS](https://github.com/QwenLM/Qwen3-TTS)
- The repo's own cost estimate is $0.005–0.10 per generation, with Modal on an A10G. — [toolkit-registry.json](/home/user/claude-code-video-toolkit/_internal/toolkit-registry.json)

**Modal and RunPod costs**
- Modal Starter has no base fee and includes **$30/month compute credit** that does not roll over. Caps are 3 seats, 10 concurrent GPUs and 100 containers.
- GPU rates: T4 about $0.59/hr, L4 about $0.80/hr, A10 about $1.10/hr ($0.000306/s). One source gives A10G as $1.05/hr ($0.000292/s), which conflicts.
- — [MorphLLM Modal pricing](https://www.morphllm.com/modal-pricing); [Activepieces](https://www.activepieces.com/blog/modal-labs-pricing-2026-gpu-rates-plans-and-credits); [gpuhosted](https://gpuhosted.com/en/modal-pricing-guide/)
- RunPod serverless flex workers:
  - The 16 GB class starts at $0.58/hr; the 24 GB class (L4/A5000/3090) is $0.69/hr.
  - Billing is per second, from worker start to full stop. Workers scale to zero.
  - The idle timeout, about 5 s by default, is billable.
  - RunPod has no recurring free credit comparable to Modal's (none found in sources).
  - — [Flexprice RunPod guide](https://flexprice.io/blog/runprod-pricing-guide-with-gpu-costs); [RunPod serverless](https://www.runpod.io/serverless); [ModelsLab](https://modelslab.com/runpod-alternative)

**ElevenLabs Free**
- 10,000 credits a month (about 10 minutes of speech), with **no commercial license**. The help center reportedly says the free plan "cannot be used for any commercial purpose".
- Credits do not roll over.
- Starter is **$6/month** ($60/year) and is the cheapest tier with a commercial license.
- — [Dupple](https://dupple.com/learn/is-elevenlabs-free); [BIGVU](https://bigvu.tv/blog/elevenlabs-pricing-2026-plans-credits-commercial-rights-api-costs/); [ToolColumn](https://www.toolcolumn.com/learn/elevenlabs-free-vs-paid-plans)
- Attribution: free-tier content reportedly must credit ElevenLabs ("elevenlabs.io" or "11.ai" in the title). This is a secondary claim that could not be verified on elevenlabs.io. — [Kenerate](https://kenerateai.com/blogs/is-elevenlabs-free)
- One outlier source says 500 credits a month; treat it as unreliable. — [Stork](https://www.stork.ai/blog/is-elevenlabs-free-2026)

**Google Cloud TTS free tier (monthly, ongoing)**
- 4M characters Standard.
- About 1M characters each for Neural2 and Chirp 3: HD, and about 100K for Studio.
- WaveNet: sources conflict between 1M and 4M.
- Gemini-TTS is not in the free tier.
- — [texttolab](https://texttolab.com/blog/google-cloud-tts-pricing); [CostBench](https://costbench.com/software/ai-voice-tools/google-cloud-text-to-speech/); [Google pricing page](https://cloud.google.com/text-to-speech/pricing) (official page surfaced in search, but its free-tier numbers were not visible)

**Azure AI Speech F0**
- **0.5 million neural TTS characters/month free**, consistent across Microsoft's regional pricing pages. The China-region page was updated Jul 8, 2026. — [Azure Speech pricing](https://azure.microsoft.com/pricing/details/cognitive-services/speech-services); [Azure China pricing](https://www.azure.cn/en-us/pricing/details/cognitive-services/)

**CapCut TTS**
- Free accounts get basic, "robotic" TTS voices. Natural voices require Pro. One source says commercial asset licensing requires Pro. — [vidpros](https://vidpros.com/capcut-pro-vs-free/); [pexo](https://pexo.ai/blog/capcut-free-vs-paid-5843)

**TikTok built-in TTS**
- No official TikTok statement on commercial use was found.
- A creator lawyer warns the TTS "robot voice ... has not been licensed for commercial use". This is opinion, not TikTok policy. — [TikTok @legaldoer](https://www.tiktok.com/@legaldoer/video/7158620834335264046?lang=en)
- Vendor pages say TikTok voices are restricted on business accounts and mention the 2021 Bev Standing lawsuit against ByteDance. These are vendor sources. — [AnySpeech](https://anyspeech.io/blog/tiktok-text-to-speech)

### Inferences

**Comparison: deadpan suitability, rate control, commercial status, cost**

| Option | Calm/deadpan control | Rate / pause control | Commercial on monetized channels | Real cost |
|---|---|---|---|---|
| Kokoro-82M | Pick a low-affect voice; no emotion prompt | `speed` param (e.g. 0.85–0.9); pauses via line splits or stitching silence | Yes (Apache-2.0) | $0, local CPU |
| Qwen3-TTS | Best: `--instruct "slow, flat, deadpan, unimpressed"` plus low `--temperature` | Instruction-driven; pauses via per-sentence generation | Yes (Apache-2.0) | About $0.01–0.05/video on Modal A10G, inside $30 credit |
| Azure neural (F0) | Many calm voices | Full SSML: `<prosody rate>`, `<break time>` | Yes, under Azure terms | $0 up to 0.5M chars/mo |
| Google Neural2 / Chirp 3 HD | Good | SSML for Standard/WaveNet/Neural2; Chirp 3 HD SSML support unverified | Yes, under GCP terms (assumed) | $0 within about 1M chars/mo |
| edge-tts | Same Azure voices | `--rate` only; no `<break>` | **Gray / not granted** | $0 |
| Piper | Flat, robotic-ish | Rate param (see Gaps) | Per-voice; lessac = **no** | $0, CPU |
| ElevenLabs Free | Very good | Speed setting, tags | **No** on Free; Starter $6/mo = yes | $0 / $6 |
| CapCut / TikTok built-in | Recognizable "TikTok voice" | Minimal | **Unclear / not granted**; premium voices need Pro | $0 |

- The Qwen3-TTS cost per video is my arithmetic: 1–3 min of A10G time (cold start plus about 60 s of audio) at about $1.10/hr is $0.02–0.06. At that rate, $30 of credit covers hundreds of videos a month.
- A ~100-word Short is about 600 characters. That means about 800 Shorts a month on Azure F0 and about 1,600 on Google's 1M-character tiers.
- The "TikTok TTS voice" is also stylistically overused. A distinct calm voice (a Kokoro low-affect voice or Qwen3 Ryan with a flat instruction) helps the channel stand apart and avoids the licensing ambiguity.
- For a "not too perfect" deadpan feel, generate per sentence and insert explicit silences (0.4–0.8 s) with FFmpeg or Remotion `<Sequence>`. This avoids relying on SSML, which only Azure and Google fully support.

### Gaps
- Could not fetch elevenlabs.io directly. The exact free-plan attribution wording and whether the free tier still exists unchanged in Nov 2026 are unverified beyond secondary sources.
- Whether Kokoro's individual voice packs carry any extra restrictions was not checked on the HF card (blocked).
- Which Piper English voices are on the "Commercial use" list was not read.
- Piper's `length_scale` rate control was not confirmed by the fetched README; from prior knowledge it exists, but this is unverified here.
- Chirp 3: HD SSML/pause support and Google's explicit output-ownership terms were not verified.
- No official TikTok or CapCut page on TTS commercial rights was found.

---

## Q2. Animation: Remotion license, hand-drawn/whiteboard approaches in Remotion, no-code alternatives, free vector assets

### Takeaway
Remotion is **free for this creator**: individuals and for-profit companies with up to 3 employees qualify. The repo already includes `@remotion/paths` (`evolvePath` gives the "line being drawn" whiteboard effect).

Adding the MIT-licensed **rough.js** gives a sketchy, imperfect look, which is the cheapest route to "not too perfect" vector animation. Lottie works through `@remotion/lottie`.

Among no-code options:
- **Canva Free** and **Clipchamp Free** export 1080p without a watermark, as long as you avoid premium assets.
- **Kapwing Free** and **Jitter Free** watermark exports and cap them at 720p.
- **CapCut Free** is usable but has had shifting paywalls and terms.

For assets:
- No attribution needed: **unDraw, Open Peeps, Humaaans, Tabler (MIT), Lucide (ISC)**.
- **OpenMoji** requires CC BY-SA attribution.
- **Noto Emoji** fonts are OFL, and its images are Apache-2.0.

### Cited Findings

**Remotion license**
- The Free License covers "an individual", "a for-profit organization with up to 3 employees", "a non-profit or not-for-profit organization", and those "evaluating ... not yet using it in a commercial way". The license file also says: "In Remotion 5.0, the license will slightly change." — [Remotion LICENSE.md](https://github.com/remotion-dev/remotion/blob/main/LICENSE.md)
- Companies of 4+ need a Company License. Third-party 2026 guides list "Creators" at **$25/seat/month** and "Automators" at **$0.01/render with a $100/month minimum**. Sources differ on whether the threshold counts "employees" or "people". — [Remotion pricing](https://www.remotion.dev/pricing) (search snippet); [Wireflow](https://www.wireflow.ai/blog/remotion-pricing); [snapcn](https://snapcn.dev/remotion-license-pricing)

**Hand-drawn and whiteboard approaches in Remotion**
- `evolvePath()` (`@remotion/paths`) animates an SVG path "from being invisible to its full length". It returns `strokeDasharray`/`strokeDashoffset`, where progress 0 is invisible and 1 is fully drawn. `@remotion/paths` has no dependencies. — [Remotion evolvePath docs](https://remotion.dev/docs/paths/evolve-path)
- `interpolatePaths()` morphs between paths. — [Remotion interpolatePaths](https://www.remotion.dev/docs/paths/interpolate-paths)
- Rough.js:
  - MIT license.
  - "A compact graphics library that draws shapes, curves, and SVG paths with a sketchy, hand-drawn look".
  - Under 9 kB, works with Canvas and SVG.
  - — [GitHub rough-stuff/rough](https://github.com/rough-stuff/rough)

**No-code alternatives (free tiers, 2026; mostly secondary sources)**
- **Canva Free**: exports are watermark-free at 1080p if you use only free elements; premium assets add watermarks. One source cites a 30-minute length. — [dev.to: free editors no watermark 2026](https://dev.to/fredabila/free-video-editors-with-no-watermark-in-2026-what-you-actually-get-from-someone-who-builds-one-4663); [Lexidium](https://blog.lexidium.com/software/free-video-editors-no-watermark)
- **Clipchamp Free**: unlimited 1080p exports, no watermark. **Microsoft ended Clipchamp iOS support in June 2026** (recent change). — [dev.to](https://dev.to/fredabila/free-video-editors-with-no-watermark-in-2026-what-you-actually-get-from-someone-who-builds-one-4663); [Wikipedia: Microsoft Clipchamp](https://en.wikipedia.org/wiki/Microsoft_Clipchamp)
- **Kapwing Free**: watermark plus 720p cap. The free length cap conflicts across sources (1, 4 or 7 minutes). — [dev.to Kapwing alternatives](https://dev.to/fredabila/kapwing-alternatives-in-2026-an-honest-comparison-from-someone-who-builds-one-478j); [Lexidium](https://blog.lexidium.com/software/free-video-editors-no-watermark)
- **CapCut**
  - Plans and pricing:
    - Plans are now Free, Standard, Pro and Team.
    - **Pro is $19.99/mo or $179.99/yr (checked Nov 12, 2026)**, and the cheaper Standard plan is reportedly no longer listed.
    - Some sources still say about $10/mo.
    - — [SocialRails](https://socialrails.com/blog/capcut-pricing-guide); [pexo](https://pexo.ai/blog/capcut-free-vs-paid-5843)
  - Free-plan limits:
    - Pro-labeled templates, effects or AI segments watermark free exports.
    - Auto captions are reported as Pro-only or capped, for example 5 per 30 days. This is undocumented and varies by account.
    - — [vidpros](https://vidpros.com/capcut-pro-vs-free/); [fluxnote](https://fluxnote.io/guides/capcut-ai-review-2026); [reelvideocaptions](https://reelvideocaptions.com/blog/capcut-auto-captions-not-free-anymore.html)
  - Terms:
    - The June 2025 ToS update drew backlash over a perpetual, worldwide, sublicensable license on uploaded content. CapCut said the grant is "solely to the extent necessary to provide the Service". — [Digital Camera World](https://www.digitalcameraworld.com/tech/social-media/capcuts-new-terms-of-service-are-angering-the-internet-and-so-confusing-that-video-editors-are-asking-chatgpt-to-decipher-them); [TechRadar](https://www.techradar.com/pro/popular-video-editing-app-capcut-wants-to-use-any-content-you-produce-for-free-forever-heres-what-you-should-know)
    - The current general terms are reportedly dated **Apr 15, 2026**, with a separate US agreement. CapCut's materials license grants no rights in its built-in sound recordings or musical works. This came from a search summary, and the exact page was not confirmed. — [Studio L7 on CapCut ToS](https://studiol7.substack.com/p/who-really-owns-your-edits-what-capcuts); [capcutguide](https://capcutguide.com/who-owns-capcut/)
- **Jitter Free**: 3 workspace files, video/GIF/Lottie export at 720p/30fps, watermarked (secondary). — [SVG AI review](https://www.svgai.org/blog/svg-animation-generators); [femaleswitch Lottie alternatives](https://www.femaleswitch.com/directories/tpost/lottiefiles-alternatives)
- **Rive Free**: 3 collaborative files, 1 project, unlimited personal files, 10 MB asset limit. Free .riv exports play a Rive splash screen, which Cadet ($9/seat) removes. Rive is aimed at interactive runtime animation, not MP4 Shorts. — [vijaytalksai Rive pricing](https://vijaytalksai.com/rive-pricing-explained/)
- **LottieFiles Free**: free animations can be browsed and used commercially. Free workspaces are limited (sources say 5 files with 20 MB, or 10 animations; they conflict). — [exploreai](https://www.exploreai.directory/tools/lottiefiles); [getpulsesignal](https://getpulsesignal.com/pricing/lottiefiles)
- **Open-source desktop tools**:
  - Synfig is GPL-3.0. — [GitHub synfig](https://github.com/synfig/synfig)
  - OpenToonz is BSD-3 and "can be used free of charge for both commercial and non-commercial projects". — [Wikipedia: Toonz](https://en.wikipedia.org/wiki/Toonz); [opensource.com](https://opensource.com/article/17/2/opentoonz-2d-animation-software)
  - Blender (including Grease Pencil) is GPL, and your created work is yours. — [itechguides](https://www.itechguides.com/best-free-3d-animation-software-in-2026) (secondary)

**Free vector and icon assets**
- **unDraw**: free, even commercially, no attribution; colors customizable on site.
- **Open Peeps**: CC0.
- **Humaaans**: CC0 (single secondary source).
- — [Toolfolio](https://toolfolio.com/articles/free-open-source-illustrations-library)
- **OpenMoji**: **CC BY-SA 4.0**. Attribution is required and derivatives must be ShareAlike. Suggested credit: "All emojis designed by OpenMoji – the open-source emoji and icon project". — [OpenMoji FAQ](https://openmoji.org/faq/)
- **Noto Emoji**: fonts are SIL OFL 1.1; tools and most image resources are Apache-2.0. — [GitHub googlefonts/noto-emoji](https://github.com/googlefonts/noto-emoji)
- **Lucide**: ISC, "totally free for commercial use and personal use", 1,600–2,000+ icons. — [GitHub lucide-icons/lucide](https://github.com/lucide-icons/lucide)
- **Tabler Icons**: MIT, 6,545 icons (5,491 outline and 1,054 filled). — [GitHub tabler/tabler-icons](https://github.com/tabler/tabler-icons)

### Inferences
- **Best fit for "deadpan, not too perfect"**: Remotion plus rough.js shapes, `evolvePath` reveals of line-art SVGs (unDraw, Open Peeps, Tabler/Lucide icons), a paper-texture background, and the repo's existing `FilmGrain` and `PointingHand` components. All of it is code-driven and reusable, which suits a consistent series.
- Applying a tiny per-frame jitter (seeded noise) to rough.js output gives a "boiling line" hand-drawn feel. This is a known animation technique; there is no specific source for it here.
- Open Peeps (CC0, hand-drawn people) best matches the "hand-drawn" brief with zero attribution overhead. OpenMoji is attractive, but its ShareAlike terms make it a poor default.
- CapCut is the fastest no-code path, but its paywalls are moving (Pro price rose in 2026, and caption limits are unclear), so a Remotion pipeline avoids lock-in.
- Clipchamp is a stable free fallback editor on desktop and web, but no longer on iOS.

### Gaps
- Could not fetch the official remotion.dev/pricing page. The $25/seat and $0.01/render figures are from third-party summaries.
- What changes in the Remotion 5.0 license is unknown.
- `@remotion/lottie` usage and limits were not verified in this session.
- Excalidraw-style libraries beyond rough.js (Excalidraw itself uses rough.js; MIT per prior knowledge) were not verified.
- Canva Free's exact 2026 export specs and whether Canva allows its free elements in monetized videos were not verified on canva.com.
- Humaaans' license relies on a single secondary source.
- No official Jitter or Kapwing pricing pages were read.

---

## Q3. Captions/subtitles: free auto-caption options and word-by-word "karaoke" styling in Remotion

### Takeaway
Use **local Whisper** for zero cost and no account. The best fits are whisper.cpp through `@remotion/install-whisper-cpp`, or faster-whisper in Python; all are MIT-licensed.

Feed the result to `@remotion/captions` → `createTikTokStyleCaptions()` for paged, per-word highlight captions. Remotion's official **TikTok template** already implements this and can be adapted.

Because the creator generates the script, captions can even be aligned to known text. CapCut auto-captions are free only with unclear limits.

### Cited Findings
- `@remotion/install-whisper-cpp` flow: `transcribe()` runs Whisper.cpp, then `toCaptions()` converts the output into `Caption` objects for `@remotion/captions`.
  - It is Node.js-only (server side).
  - Its `--dtw` flag gives more accurate token timestamps (Whisper.cpp versions after 1.0.55).
  - `splitOnWord` gives word-level output.
  - — [Remotion toCaptions](https://www.remotion.dev/docs/install-whisper-cpp/to-captions); [Remotion transcribe](https://www.remotion.dev/docs/install-whisper-cpp/transcribe)
- `createTikTokStyleCaptions()` groups captions into pages, each with a `tokens` array of per-word timings. A `combineTokensWithinMilliseconds`-style setting controls how many words appear per page. — [Remotion docs](https://remotion.dev/docs/captions/create-tiktok-style-captions); [crepal tutorial](https://crepal.ai/blog/?p=5091)
- Remotion's official template "Generate TikTok-style captions with Whisper.cpp":
  - `node sub.mjs` captions every video in `public/`.
  - It downloads Whisper.cpp plus the `medium.en` model (1.5 GB), configured in `whisper-config.mjs`.
  - The README notes that "for some entities a company license is needed".
  - — [GitHub remotion-dev/template-tiktok](https://github.com/remotion-dev/template-tiktok); [remotion.dev/templates/tiktok](https://remotion.dev/templates/tiktok)
- whisper.cpp is MIT. — [GitHub ggml-org/whisper.cpp](https://github.com/ggml-org/whisper.cpp)
- faster-whisper is MIT, a CTranslate2 reimplementation "up to 4 times faster than openai/whisper for the same accuracy while using less memory". — [LinuxLinks faster-whisper](https://www.linuxlinks.com/faster-whisper-reimplementation-openai-whisper/); [Codersera 2026 comparison](https://codersera.com/blog/faster-whisper-vs-whisper-cpp-speech-to-text-2026/amp/)
- edge-tts can write an SRT directly during synthesis with `--write-subtitles`. — [GitHub rany2/edge-tts](https://github.com/rany2/edge-tts)
- CapCut auto captions are reported as Pro or limited (for example 5 per 30 days) in 2026, with inconsistent reports. — [reelvideocaptions](https://reelvideocaptions.com/blog/capcut-auto-captions-not-free-anymore.html); [vidpros](https://vidpros.com/capcut-pro-vs-free/)

### Inferences
- The minimal addition is a `tools/captions.py` built on faster-whisper (word timestamps), writing Remotion `Caption[]` JSON. It would sit next to `voiceover.py --scene-dir ... --json` and match the repo's Python-tool convention. The alternative is the Node `@remotion/install-whisper-cpp` route copied from template-tiktok.
- Since TTS audio is clean, `small.en` or `base.en` is likely accurate enough and much faster than `medium.en`. Exact script words can also replace Whisper's text while keeping its timings.
- Karaoke styling: render the active `tokens` page in large bold type (about 70–90 px at 1080 width). Highlight the current token with a color or scale spring, place it in the vertical middle-lower third, and keep it clear of platform UI.

### Gaps
- Exact Whisper model accuracy and speed on TTS audio were not benchmarked.
- The current option names in `createTikTokStyleCaptions` were not re-verified on the live docs (remotion.dev blocked).
- Platform "safe zones" (pixel margins hidden by TikTok/Shorts UI) were not researched.

---

## Q4. Music and sound effects safe for monetized Shorts/TikTok

### Takeaway
The safest zero-cost sources:
- **ACE-Step v1.5 output via acemusic.ai**: commercial use is allowed even on the Free plan, and it is already wired into the repo.
- **YouTube Audio Library** (for YouTube).
- **TikTok's Commercial Music Library** (CML) inside TikTok.
- **Freesound CC0** SFX.

**Pixabay** is free and commercial-OK, but carries real Content ID false-claim risk. Avoid Freesound **CC BY-NC / Sampling+**, CapCut's built-in music, and trending sounds on business accounts.

For a deadpan format, quiet ambient or lofi under the voice, or no music at all, is the norm.

### Cited Findings

**ACE-Step / acemusic.ai**
- ACE Music "continues the existing free-use and commercial-use policy for ACE-Step v1.5 outputs, including the v1.5 XL model".
- Users retain ownership of outputs "to the extent ownership rights exist under applicable law" and may use them commercially without a fee. Attribution is appreciated but not required.
- Outputs from **other models** on the Free plan are personal, non-commercial only.
- — [ACE Music Terms](https://acemusic.ai/terms/); [acemusic help: commercial use](https://acemusic.ai/help/articles/commercial-use-and-privacy/)
- A commercial license "does not guarantee a distributor will accept a release". — [acemusic use-case page](https://web.acemusic.ai/use-cases/prepare-an-ai-song-for-release/)
- The model's own license conflicts across secondary sources: MIT, versus Apache-2.0 code with a StepFun license on XL weights. — [dev.to ACE-Step guide](https://dev.to/czmilo/ace-step-15-the-complete-2026-guide-to-open-source-ai-music-generation-522e); [songcreator.pro](https://songcreator.pro/blog/what-is-ace-step-1-5)

**YouTube Audio Library**
- Tracks are reported as not Content-ID-claimed, and YouTube "vouches" for them. Some tracks are CC-licensed and need description credit, and the license type is shown in Studio. — [Foxi: Audio Library guide](https://www.foximusic.com/blog/copyright-free-music-youtube-audio-library-guide/); [Mubert comparison](https://mubert.com/blog/free-music-for-youtube-monetization-credit-content-id)
- The Shorts audio picker is different: secondary sources conflict on whether it creates a non-disputable "special" Content ID claim or no claim. Its license reportedly applies only when the music is added through YouTube's own tools. — [Foxi Shorts licensing](https://www.foximusic.com/blog/youtube-shorts-music-licensing-guide/); [PostLink](https://postlinkapp.com/blog/youtube-shorts-music-copyright)
- **A Short over 1 minute with an active Content ID claim is reportedly blocked globally**, rather than just claimed. This is secondary, and the details conflict. — [Foxi Shorts copyright guide](https://www.foximusic.com/blog/youtube-shorts-copyright-music-library-guide/)

**TikTok Commercial Music Library**
- On a **Business account**, "Add Sound" shows only CML sounds. Personal accounts see the full library and can switch to Commercial Sounds. — [TikTok Ads help: How to use the CML](https://ads.tiktok.com/help/article/how-to-use-the-commercial-music-library)
- TikTok tells businesses to use CML. Using the general library for business content risks infringement. — [TikTok Business blog](https://ads.tiktok.com/business/en-US/blog/audio-library-royalty-free-music)
- Secondary sources report a July 2025 tightening: business accounts using general-library or trending sounds may have videos muted or removed. — [Soundstripe](https://www.soundstripe.com/blogs/tiktok-music-licensing-rules); [Third Chair](https://usethirdchair.com/blog/tiktok-commercial-library-what-brands-can-really-use)

**Pixabay**
- Free for commercial and non-commercial use with no attribution. Music must be part of a larger work and not distributed standalone. The license is the custom Pixabay Content License, not CC0; pre-Jan 9, 2019 uploads are CC0. — [Pixabay FAQ](https://pixabay.com/service/faq/); [Wikipedia: Pixabay](https://en.wikipedia.org/wiki/Pixabay)
- Some contributors or their distributors register tracks in Content ID, which leads to claims on otherwise licensed use. — [Sonilo 2026 comparison](https://sonilo.com/blog/comparisons/pixabay-music-sound-effects-alternatives-2026)

**Freesound**
- CC0 needs no credit and allows commercial use. CC BY requires credit. **CC BY-NC bars monetized use**; forum consensus is that ad revenue counts as commercial. Sampling+ is retired and similar to BY-NC plus no ads. — [Freesound FAQ](https://www.freesound.org/help/faq); [Freesound forum](https://freesound.org/forum/legal-help-and-attribution-questions/39864); [Wikipedia: Freesound](https://en.wikipedia.org/wiki/Freesound)

**CapCut built-in audio**
- CapCut's materials license reportedly grants no rights in built-in sound recordings or musical works. — [Studio L7](https://studiol7.substack.com/p/who-really-owns-your-edits-what-capcuts) (via search summary)

### Inferences
- Generate one 60–90 s "channel theme" bed with ACE-Step (for example, the `lofi` or `ambient` preset, about 70–80 bpm, low volume around 0.08–0.12 under the voice) and reuse it as a sonic signature.
- **Do not register AI tracks in Content ID.** Ownership of AI output may be thin, and self-claims cause headaches when cross-posting.
- For SFX (pops, paper rustle, pen scratch), use Freesound filtered to CC0. Record a small personal SFX kit once, for example pen-on-paper with a phone; this costs nothing and is 100% owned.
- If the TikTok account stays Personal or Creator (not Business), trending sounds remain available inside the app. Mixing a trending sound over the voice usually works against a narration format, though.
- Keeping YouTube uploads at 60 s or under, or music-free, avoids the reported >1-minute blocking behavior for claimed music.

### Gaps
- Could not read YouTube's official Audio Library or Shorts audio Help pages. Claim behavior is from secondary sources that conflict.
- The exact text of TikTok's July 2025 business-account change is unverified.
- ElevenLabs SFX (already in the repo) needs a paid plan for commercial use (see Q1). The commercial terms of its SFX output on free accounts were not separately checked.
- Pixabay's official license-summary page was not read directly.

---

## Q5. Scheduling and publishing for free

### Takeaway
Both native schedulers are free and enough for a solo creator:
- **YouTube Studio** (desktop and mobile) schedules Shorts with the same Visibility → Schedule flow as long videos.
- **TikTok's native scheduler** is **web-only, from 15 minutes up to 10 days ahead**, and scheduled posts cannot be edited.

For one-stop cross-posting, **Buffer Free** (3 channels, 10 queued posts per channel) covers TikTok plus YouTube Shorts.

### Cited Findings
- **TikTok native scheduler**:
  - Schedules 15 min to 10 days ahead, from the web upload page only.
  - Scheduled posts cannot be edited; you re-upload instead.
  - Sources disagree on whether a Business account is required or whether Creator works too.
  - — [BulkPublish](https://www.bulkpublish.com/blog/can-you-schedule-tiktok-posts/); [Ignis](https://ignisapp.co/blog/tiktok-scheduling-limits-explained); [SocialBee](https://socialbee.com/blog/how-to-schedule-tiktok-posts/)
- **YouTube scheduling**:
  - Available in Studio desktop and the mobile app (Visibility → Schedule); some devices may require the YouTube Studio app.
  - A Community Guidelines strike keeps scheduled videos private during the penalty.
  - — [SocialBee: schedule Shorts](https://socialbee.com/blog/how-to-schedule-youtube-shorts/); [Quso](https://quso.ai/blog/how-to-schedule-youtube-shorts)
- **Buffer Free**:
  - Up to 3 channels, TikTok included, with 10 scheduled posts per channel at a time. This is a queue cap, not a monthly cap.
  - Supports YouTube Shorts.
  - Shorts published via Buffer reportedly can't use YouTube's built-in music library.
  - — [Buffer: schedule TikTok](https://buffer.com/resources/how-to-schedule-tiktok-posts/); [hashtagtools](https://hashtagtools.io/blog/buffer-free-plan-limits-pricing-2026); [use-apify](https://use-apify.com/blog/buffer-free-plan-guide); [Fulin Labs](https://fulinlabs.com/blog/schedulepost-vs-buffer-2026/)
- **Other free options**: Metricool Free (1 brand) and Multi Upload Tool (2 accounts). Native schedulers have no post caps. — [ShortSync](https://www.shortsync.app/best/free-social-media-scheduler); [multi-upload-tool](https://multi-upload-tool.com/blog/free-social-media-scheduler)

### Inferences
- **Batch workflow**: render 7–10 Shorts on one day. Schedule YouTube for 1–2 weeks out in Studio. Schedule TikTok up to 10 days out on the web, or let Buffer hold 10 queued per channel.
- Upload natively per platform rather than reposting files that carry another platform's watermark. Export a clean master from Remotion for each platform.
- For an audience aged 13–29, TikTok content for under-18 viewers has extra restrictions, but that was not researched here.

### Gaps
- Could not find YouTube's official maximum scheduling window. support.google.com did not surface in search.
- TikTok scheduler account-type requirements conflict across sources.
- Buffer's own pricing page was not opened.

---

## Q6. Minimal repo addition for vertical 1080x1920 Shorts, and render time for 60 s at 30 fps

### Takeaway
Minimal path: a new `templates/shorts-vertical/` Remotion project, cloned from product-demo's structure.

It needs:
- One `<Composition width={1080} height={1920} fps={30}>`, with duration computed from the narration audio.
- About 4–6 scene components (Hook, Fact/Steps, Visual gag, Payoff, Loop/CTA).
- `@remotion/captions` for word captions.
- Optionally `roughjs` and `@remotion/lottie`.

Supporting pieces are a `kokoro` provider in `voiceover.py` (or a `tools/kokoro_tts.py`), a `tools/captions.py` (faster-whisper), and registry entries.

A 60 s 1080x1920 30 fps render (1,800 frames) of simple SVG scenes should take **roughly 2–7 minutes** on a typical local machine. One published benchmark measured a median of 140 s for exactly that format on a cloud VM.

### Cited Findings
- The repo's product-demo template sizes compositions from config (`width: 1920, height: 1080, fps: 30`). The registry default is 1920x1080. — [demo-config.ts](/home/user/claude-code-video-toolkit/templates/product-demo/src/config/demo-config.ts); [toolkit-registry.json](/home/user/claude-code-video-toolkit/_internal/toolkit-registry.json)
- **Render benchmarks**:
  - A fixed **60 s 1080x1920 Remotion composition** on a cloud VM: median of 3 runs **139.6 s** (2.33 s per output second). — [GitHub PR benchmark](https://github.com/mahmoudemad68/Your_Editor/pull/12)
  - A 15 s 1080x1920 clip at concurrency 1 rendered in 1 min 43 s locally. Linear extrapolation gives about 7 min per 60 s; that is my extrapolation. — [lody-video-factory PR](https://github.com/ReC82/lody-video-factory/pull/133)
- **Performance tuning**:
  - `--concurrency` can raise or lower speed; `npx remotion benchmark` finds the optimum. — [Remotion performance docs](https://www.remotion.dev/docs/performance)
  - VP9 encoding left cores idle; `-row-mt 1` cut a 720-frame 1080x1920 render from 150.7 s to 62.4 s. H.264, the default MP4 codec, is the normal choice for Shorts. — [remotion issue #11676](https://github.com/remotion-dev/remotion/issues/11676)
  - Long renders can slow progressively, which is not relevant at 1,800 frames. — [remotion issue #11911](https://github.com/remotion-dev/remotion/issues/11911)
- Remotion's TikTok template is a reference for vertical, caption-centric compositions with whisper.cpp. — [GitHub remotion-dev/template-tiktok](https://github.com/remotion-dev/template-tiktok)

### Inferences

**Concrete minimal change set** (do not modify now; this is a proposal):
1. Create `templates/shorts-vertical/`.
   - `src/Root.tsx` registers `Short` at 1080x1920, 30 fps, with `calculateMetadata` reading the VO duration.
   - `src/config/short-config.ts` holds the script lines, per-line audio files, visual cue per line, and theme.
   - `src/scenes/*` holds the scenes.
   - `src/components/Captions.tsx` renders `createTikTokStyleCaptions` pages.
   - `src/components/Sketchy.tsx` wraps rough.js and `evolvePath`.
2. Add deps: `@remotion/captions@4.0.425` (pinned to the repo's Remotion version), `roughjs`, and optionally `@remotion/lottie` plus `lottie-web`.
3. Tools:
   - Add `--provider kokoro` to `tools/voiceover.py`, or a new `tools/kokoro_tts.py` (pip `kokoro`, `soundfile`; CPU).
   - Add `tools/captions.py` using faster-whisper with `word_timestamps`, outputting `public/captions.json`.
4. Registry: add the template, tools, and a `verticalResolution: {1080,1920}` config entry.
5. Reuse `lib/components` (FilmGrain, PointingHand, AnimatedBackground "subtle") by passing vertical dimensions. Some components may assume 16:9 and need a size prop; this is unverified.

**Layout and timing**:
- Keep the key action and captions in the central area, roughly 1080x1420 after trimming top and bottom UI. This is a common heuristic; see the Q3 gap on safe zones.
- Render with `--codec h264 --crf 18` and test concurrency with `npx remotion benchmark`.
- Expect simple flat-SVG scenes to render faster than the benchmarks above, which used video and image layers. Treat 2–7 min as the planning range.

### Gaps
- No first-party Remotion benchmark for 9:16 at 1,800 frames.
- The local machine spec of the creator is unknown.
- Whether repo components hard-code 1920x1080 was not audited file by file.

---

## Q7. Recommended zero-cost stack, low-cost upgrade path, and realistic time budget per video

### Takeaway
**Zero-cost stack (commercially clean)**

| Step | Tool |
|---|---|
| Script | LLM/Claude in this repo |
| Voice | Kokoro-82M locally (speed about 0.85–0.9), or Qwen3-TTS "Ryan, slow flat deadpan" on Modal inside the $30 free credit |
| Visuals | Remotion (free under 3 employees) plus rough.js, `evolvePath`, Open Peeps/unDraw/Tabler/Lucide |
| Captions | faster-whisper or whisper.cpp plus `@remotion/captions` |
| Music | ACE-Step v1.5 via free acemusic key (commercial OK) or the YouTube Audio Library |
| SFX | Freesound CC0 |
| Render | Local Remotion |
| Publish | YouTube Studio and TikTok web scheduler, or Buffer Free |

**Low-cost upgrades**, in order:
1. ElevenLabs Starter $6/mo for commercial license and premium calm voices.
2. Azure or Google TTS beyond the free tiers (pay-as-you-go).
3. CapCut Pro ($19.99/mo as of Nov 2026) only if a no-code editor is preferred.
4. Buffer or other paid schedulers if posting to more than 3 channels.

Remotion stays free unless the business grows past 3 people; after that it is $25/seat/mo per secondary sources.

### Cited Findings
- Remotion is free for individuals and companies of 3 or fewer employees. — [Remotion LICENSE.md](https://github.com/remotion-dev/remotion/blob/main/LICENSE.md)
- Kokoro: Apache-2.0, local, with a `speed` param. — [hexgrad/kokoro](https://github.com/hexgrad/kokoro)
- Qwen3-TTS: Apache-2.0, controls speaking rate and emotion by instruction. — [QwenLM/Qwen3-TTS](https://github.com/QwenLM/Qwen3-TTS)
- Modal: $30/month free credit. — [MorphLLM](https://www.morphllm.com/modal-pricing)
- ElevenLabs Starter is $6/mo and the cheapest commercial tier; Free is non-commercial. — [BIGVU](https://bigvu.tv/blog/elevenlabs-pricing-2026-plans-credits-commercial-rights-api-costs/)
- ACE-Step v1.5 outputs are commercial-OK on the free plan. — [acemusic help](https://acemusic.ai/help/articles/commercial-use-and-privacy/)
- CapCut Pro is $19.99/mo (checked Nov 12, 2026). — [pexo](https://pexo.ai/blog/capcut-free-vs-paid-5843)
- **Monetization policy risk for templated faceless channels**:
  - YouTube renamed "repetitious content" to **"inauthentic content"** on Jul 15, 2025, targeting mass-produced, templated or repetitive videos at the channel level.
  - AI voices and faceless formats are not banned per se, and realistic synthetic content must be disclosed.
  - Some sources claim further 2026 renames or guidance (Jul 2026) that could not be verified.
  - — [vidpal](https://www.vidpal.ai/blog/youtube-ai-content-monetization-policy-2026); [Mark Studios](https://www.markstudios.com/blog/faceless-youtube-channels-2026-what-works-what-gets-demonetized); [nofacetube](https://nofacetube.com/guides/youtube-inauthentic-content-policy/); [newmoneymatrix](https://newmoneymatrix.org/youtube-inauthentic-content-policy-explained/) (conflicting dates); [UpTube](https://www.uptube.io/blog/youtube-new-policies-2026)
- CLAUDE.md pacing: slow speech is 120–130 wpm; check timing after TTS with `sync_timing.py`; audio-anchored timelines are recommended for short spots. — [CLAUDE.md](/home/user/claude-code-video-toolkit/CLAUDE.md)

### Inferences

**Realistic time budget per video** (my estimate, no source; it assumes the vertical template and helper tools above already exist):

| Task | Early weeks | Steady state, batching 5–7 |
|---|---|---|
| Idea selection + fact check (odd facts need verification) | 15–20 min | 10 min |
| Script (90–115 words, deadpan beats, hook in first 1–2 s) | 15–20 min | 8–10 min |
| TTS per line + listen and redo a few lines (Kokoro or Qwen3) | 10 min | 5 min |
| Captions (automated Whisper) + spot fix | 5 min | 2–3 min |
| Visuals: pick and adjust SVG assets, set cue timings in config, preview in Studio | 40–60 min | 15–25 min |
| Music bed / SFX (reuse channel theme) | 10 min | 2 min |
| Render (2–7 min, unattended) + final watch | 10 min | 5–8 min |
| Title, description, hashtags, schedule on both platforms | 10 min | 5 min |
| **Total** | **about 2–2.5 h** | **about 50–70 min** |

- Building the template, Kokoro provider and captions tool is a one-time setup, probably 1–2 focused days with Claude Code assistance (estimate).
- To counter the "inauthentic/templated" risk while staying consistent, vary hooks, visuals and structure per episode. Keep the recurring deadpan voice and style as branding, not identical scaffolding. Add genuine value: accurate, sourced facts and useful tips.
- **Things to avoid** for a monetized channel: edge-tts, TikTok/CapCut built-in TTS, ElevenLabs Free, Piper lessac voices, Freesound BY-NC, CapCut built-in music, OpenMoji (unless attribution and ShareAlike are acceptable), and Kapwing/Jitter free exports (watermark, 720p).

### Gaps
- No primary source for per-video time budgets for this exact workflow; the table is an estimate.
- The official text of YouTube's current YPP policy page and any 2026 changes was not read (support.google.com not reachable or surfaced).
- Whether the platforms' AI-content labels (YouTube "altered or synthetic", TikTok AI-generated labels) apply to cartoon/vector explainers with AI voice was not verified. Sources mention only "realistic" content for YouTube.
