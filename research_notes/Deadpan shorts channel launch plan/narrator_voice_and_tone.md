# Narrator Voice and Tone for a Faceless, Deadpan, "Boring but Useful" Shorts Channel (state of knowledge, Nov 2026)

Research notes for the report writer. Evidence grades used throughout: **STRONG** = replicated or a line of studies, plus meta-analyses; **MODERATE** = a solid peer-reviewed study or two, or consistent findings from one lab group; **WEAK** = a single study known only from secondary reports, vendor or industry surveys, creator heuristics, or opinion. Note on method: live fetching of elevenlabs.io was blocked by this session's network policy, so all ElevenLabs details come from search snippets of official doc pages plus the toolkit's own ElevenLabs skill files. Most academic findings were checked through abstracts, indexes or press summaries, not full texts.

---

## 1. Speech rate: what rate helps comprehension, recall, credibility and likeability, and what WPM fits "slow but not sleepy"?

### Takeaway
People can understand speech far faster than any narrator talks. Comprehension holds up to about 270 wpm and drops sharply near 315 wpm, so slow narration is a **style and comedy choice, not something comprehension needs**. Persuasion research gives a mild warning: very slow speakers (about 100 wpm) were rated less credible than moderately fast ones (about 195 wpm), and a moderately brisk rate did best in a field study. The target is therefore "unhurried": an average of roughly 125–145 wpm including pauses, slowing further only on punchlines.

### Cited Findings
- **Comprehension ceiling (MODERATE–STRONG):** Kuperman et al. (2021) found listening comprehension "was not hindered at the speech rate of 270 wpm but showed a steep decline at the rate of 315 wpm". Listening and reading appear to share the same time limits. — [McMaster Experts record](https://experts.mcmaster.ca/scholarly-works/2127220)
- **Speed-up tolerance (MODERATE, secondary summary):** Speech can be sped up by about 25% "without too much impact" on understanding. Near a 50% speed-up, comprehension "typically" drops significantly. — [Psychology Today, 2023](https://psychologytoday.com/au/blog/small-talk-and-big-questions/202307/is-speed-listening-right-for-you)
- **Video lectures at 2x (MODERATE; several experiments, 2021/2022):** In Murphy et al., *Applied Cognitive Psychology* 36(1):69–82, playback up to 2x caused little loss in immediate or one-week-delayed comprehension, with declines only above 2x. Students *believed* slower playback helped them, but their scores did not show it. The authors note the results may differ with different speech rates or content difficulty. — [ScienceDaily, 2022](https://sciencedaily.com/releases/2022/01/220111153637.htm); [Times Higher Education](https://www.timeshighereducation.com/news/no-major-harm-learning-double-speed-lecture-viewing); [UMPI CTL summary](https://www.umpi.edu/ctl/?p=5084)
- **Slow speech and credibility (WEAK–MODERATE; classic single study, Miller et al., JPSP, 1976, known here only secondhand):** A moderately fast talker (~195 wpm) was rated more credible and persuasive. Slow talkers (≤ ~100 wpm) were rated less credible. — [Speed of speech and persuasion (PDF via typeset.io)](https://typeset.io/pdf/speed-of-speech-and-persuasion-48bx24hl8s.pdf)
- **Moderators (MODERATE; Smith & Shaffer, *PSPB*, 1995):** At 180 vs 220 wpm, fast speech raised persuasion only for moderately involved listeners, through perceived credibility. Fast speech also *reduced* listeners' ability to tell strong arguments from weak ones, which is consistent with the Elaboration Likelihood Model. — [Speed of Speech and Persuasion: Evidence for Multiple Effects (index record)](https://scholarhub.vn/publication/Speed-of-Speech-and-Persuasion-Evidence-for-Multiple-Effects/d70dd17b-51bb-4d0d-a6ce-d40067433c42)
- **Field optimum (WEAK–MODERATE; Conrad et al., 2012, 1,380 recorded survey-invitation calls, secondary summary):** About 3.5 words/second (~210 wpm) was the most successful rate, and very fast or very slow interviewers did worse. Interviewers who used frequent short pauses beat perfectly fluent ones. — [PsyBlog summary](https://www.spring.org.uk/?p=92794)
- **Gaze × rate (WEAK; single study, *Psychological Reports*, 2012):** With little gaze, slow speech *decreased* trustworthiness compared with fast speech. Slow speech alone still increased perceived persuasiveness. — [Psychological Reports 110(2):663–676](https://https-sage-cnpereading-com-443.webvpn1.xju.edu.cn/doi/10.2466/07.11.21.28.PR0.110.2.663-676)
- **Ad/audio norms (WEAK–MODERATE):** A *Journal of Advertising Research* study put the optimal rate for audio ads at about 180 wpm. — [WARC news summary](https://cdn.warc.com/newsandopinion/news/how-speech-delivery-speed-impacts-audio-ads/43304)
- **Industry convention (WEAK):** 150–160 wpm is the usual audiobook benchmark. It is an industry convention, not a research-derived optimum. — [Audiobook narration speed explainer](https://sites.google.com/view/snowdaycaculators/audiobook-narration-speed-explained-what-150-160-wpm-really-means)
- **Toolkit's own house rule:** standard narration is ~150 wpm, with "Slow 120–130 wpm" for technical or complex material and "Fast 160–180" for intros and CTAs. TTS engines drift, often compressing pauses, so durations must be re-measured after generation. — [/home/user/claude-code-video-toolkit/CLAUDE.md](file:///home/user/claude-code-video-toolkit/CLAUDE.md)

### Inferences
- Slow narration does not buy comprehension, because viewers can handle 2x. What it buys is (a) the deadpan comic register, (b) a calm contrast with high-arousal feeds, and (c) perhaps better scrutiny of good advice (Smith & Shaffer: faster speech blurs strong vs weak arguments, so a slower, clear delivery should let *genuinely useful* tips land as strong). The cost is fewer words: at 130 wpm a 50-second Short holds about 108 words, versus about 133 at 160 wpm.
- Avoid the "sleepy" zone. The only direct credibility penalty in the literature is at about 100 wpm or below, so don't let the average fall below roughly 120 wpm. Build "slow" mostly from **pauses between sentences**, not from stretched syllables, which make TTS sound slurred or robotic.
- Recommended target: **125–145 wpm effective** (words ÷ total narration time, pauses included). The articulation rate *inside* phrases should be near normal (~145–160 wpm), with the slowness carried by gaps. Make the hook line slightly faster or denser, and the punchline the slowest line.
- Is slow speech penalised on Shorts/TikTok? No study tests this directly. The swipe decision happens in the first second or two (section 2), so the risk falls on the *opening*, not on overall pace. Front-load meaning, with no slow intro.

### Gaps
- I found no peer-reviewed study of narration rate vs retention or swipe-away on short-form vertical video platforms specifically.
- A widely repeated finding that radio news is remembered best at 170–190 wpm (attributed to Rodero) came up only in a search summary. The primary paper was not verified, so it is not used here.
- The Miller 1976 and Conrad 2012 numbers come from secondary summaries. Exact effect sizes are unverified.

---

## 2. Pauses and timing: comprehension, comedic timing (the pause before a punchline), and how long a pause can last before viewers swipe

### Takeaway
Pauses placed at **meaningful boundaries** measurably help memory for the word that follows (MODERATE). Random pauses do not help. The folk rule that a punchline needs "a pause before it" is **not well supported** by acoustic studies of real joke-telling. What reliably marks punchlines is **lower pitch and slower rate**. A 2026 preprint reopens the pause question for high-surprise punchlines. No research says how long dead air can last before a viewer swipes, so the safe rule is no silence at the start and short beats elsewhere, with something always moving on screen.

### Cited Findings
- **Silent pauses aid recognition memory (MODERATE; MacGregor, Corley & Donaldson, *Neuropsychologia*, 2010, ERP study):** In a surprise memory test, listeners were more likely to recognise words that came right after a silent pause. — [Univ. of St Andrews research portal](https://research-portal.st-andrews.ac.uk/en/publications/listening-to-the-sound-of-silence-disfluent-silent-pauses-in-spee/)
- **"Er" hesitations have a similar but double-edged effect (MODERATE; Corley et al., *Cognition*, 2007, n=12):** Hesitations improved later memory for the next word. The authors warn that sparing use may help recall but can make the speaker seem less knowledgeable. — [BPS Research Digest](https://www.bps.org.uk/research-digest/effect-er-hesitations-speech)
- **Placement matters (MODERATE):** Pauses help only at meaningful points. Pauses inserted at random spots give little or no recall benefit. — [PMC10637151](https://pmc.ncbi.nlm.nih.gov/articles/PMC10637151)
- **Lab vs real lectures (WEAK; single study, ICPhS 2023):** A study of university lectures did not replicate the recall benefit of pause-like particles seen in single-sentence lab tests. — [ICPhS 2023 paper](https://guarant.cz/icphs2023/85.pdf)
- **Punchline prosody (MODERATE; Pickering, Attardo et al., 2009):** Punchlines were *not* louder than the setup. They were delivered at **significantly lower pitch and slower speech rate**, often but not necessarily with a "smiling/laughing voice", and were **not preceded by significant pauses**. — [Penn State: Prosodic markers of saliency in humorous narratives](https://pure.psu.edu/en/publications/prosodic-markers-of-saliency-in-humorous-narratives/)
- **Joke timing (MODERATE; Attardo & Pickering, *Humor*, 2011; 20 joke performances):** No evidence that punchlines are reliably preceded by pauses, and no significant change in speech rate at the punchline. The authors say timing theory "is in serious need of further research". A 2013 conversational follow-up also found no volume or rate differences between humorous and non-humorous pause units. Later work reported that the punchline-pitch result did not replicate. — [De Gruyter, Timing in the performance of jokes](https://www.degruyterbrill.com/document/doi/10.1515/HUMR.2011.015/pdf?lang=en); [Benjamins chapter](https://benjamins.com/catalog/bct.55.03att)
- **Counterpoint (WEAK; 2026 preprint, peer-review status unconfirmed):** Speakers reportedly *lengthen* pauses before high-surprise punchlines, and this timing matters for the audience. The search summary mentions a ~1.5 s extended pause, but I could not verify that number. — [eScholarship preprint](https://escholarship.org/content/qt58t1w6r7/qt58t1w6r7.pdf)
- **Short pauses aid persuasion (WEAK–MODERATE):** Telephone interviewers who used frequent short pauses were more successful than perfectly fluent ones (Conrad et al. 2012). — [PsyBlog summary](https://www.spring.org.uk/?p=92794)
- **Swipe metric:** YouTube Studio reports "Viewed vs. swiped away", also labelled "Stayed to watch", meaning the share of viewers who chose to watch rather than swipe. — [Creator Essentials glossary](https://www.creatoressentials.com/glossary/viewed-vs-swiped-away/); [YouTube Help: content performance](https://support.google.com/youtube/answer/12220281)
- **No official benchmark (WEAK; vendor/creator heuristics):** YouTube publishes no benchmarks. Creator tools commonly cite ≥70% "viewed" as a good hook and ≥80% as strong, and advise comparing against your own channel. — [Subscribr](https://subscribr.ai/p/youtube-shorts-analytics-metrics-viral); [ContentStudio guide](https://contentstudio.io/blog/youtube-shorts-analytics-guide)

### Inferences
- Use pauses as **signposts before the key payload word** (the tip, the number, the punchline noun). This matches the MacGregor/Corley mechanism: a pause raises attention to the next word. Place them only at clause or idea boundaries.
- For the comic beat, the evidence suggests carrying it with **pitch drop + slowdown on the punchline itself**, plus a short beat *after* it so the joke can land while a visual reaction plays. A long pre-punchline pause is optional. Test 0.4 s vs 0.9 s pre-punchline beats rather than assuming the longer one wins.
- For the **first ~1 s** of a Short there should be no silence at all. Narration or a sound should start at frame 0–9 (≤0.3 s). This is a cautious inference: swipe decisions are made at the hook, and no study gives a tolerable dead-air length.
- Inside the video, deliberate silences of **0.6–1.2 s** are probably safe *if the visuals change during them* (a blink, a slow zoom, an on-screen text punchline). One "long" silence (~1.5 s) per video can be the signature comedic beat. Treat that as an A/B variable, not a rule.

### Gaps
- No study found that measures how long a pause in short-form video can last before viewers swipe away. Platform-side data is proprietary.
- No experimental study of pause length in *synthetic* comedic narration was found.

---

## 3. Prosody: when does flat/monotone delivery read as funny (deadpan, dry wit) and when as boring or robotic?

### Takeaway
There is **no controlled experiment showing that flat delivery makes a line funnier**. The evidence is indirect. Irony and humour are recognised mainly from *context and incongruity*, not from one "tone of voice". Real punchlines naturally drop in pitch and slow down. Learners clearly detect a *bored* narrator from voice alone and are less motivated by one. So deadpan works when the **content or visuals carry the absurdity and the voice stays calm, competent and committed**. It fails when the voice signals disinterest or when the content is itself dull.

### Cited Findings
- **No single "ironic tone" (MODERATE; Bryant & Fox Tree, *Language and Speech*, 2005):** Listeners combine several cues, including context. In their 2002 study, context was a stronger cue to irony than prosody. — [BibBase record](https://bibbase.org/network/publication/bryant-foxtree-isthereanironictoneofvoice-2005); [Typeset PDF](https://typeset.io/pdf/is-there-an-ironic-tone-of-voice-2o7dhxq5ue.pdf)
- **Sarcastic speech acoustics (MODERATE; Cheang & Pell, 2008):** The most common feature of sarcastic speech is a slower speaking rate, often with more varied pitch and stress. — [Cheang & Pell 2008 (PDF)](https://www.cs.columbia.edu/~julia/papers/cheangDell08.pdf)
- **Punchlines: lower pitch, slower (MODERATE):** see section 2. — [Penn State](https://pure.psu.edu/en/publications/prosodic-markers-of-saliency-in-humorous-narratives/)
- **Deadpan as aesthetic (scholarly, theoretical):** Deadpan is described as an aesthetic that dampens comic affect and sets form against content. — [SAGE article (mirror link), doi 10.1177/14614448211054011](https://https-sage-cnpereading-com-443.webvpn1.xju.edu.cn/doi/10.1177/14614448211054011)
- **Mechanism, from practitioner/film-school sources (WEAK):** Deadpan works by expectation violation and withheld emotional cues: viewers expect comedic delivery and get a straight face. — [Vancouver Film School: Deadpan – How "Serious" Humour Works](https://vfs.edu/node/8659)
- **Limits (WEAK, practitioner):** "Weak material cannot be rescued merely by speaking quietly", and "restrained delivery without context may sound sincere." — [Brainbound: deadpan wit](https://www.brainbound.blog/deadpan-wit-mastery)
- **Content and speaker over delivery (WEAK–MODERATE; single study of 531 scientific talks):** Joke type and delivery method showed no significant effect on whether a joke succeeded. Speaker identity mattered more. — [SciCommBites summary](https://scicommbites.org/?p=3218)
- **Bored vs happy narrator (MODERATE; Lawson, Mayer et al., 2021, several experiments):** Learners recognised whether an instructor was happy, content, frustrated or bored about as accurately from **voice alone** as from voice plus an on-screen agent. Students were happier and more motivated with happy than with bored instructors. Positive instructors drew more self-reported attention, but learning-outcome results were mixed. — [Lawson et al. 2021, Educational Technology R&D (PDF)](https://www.cs.purdue.edu/homes/bbenes/papers/Lawson2021EdTechResDev.pdf); [NSF PAR: positivity principle](https://par.nsf.gov/biblio/10474990-positivity-principle-do-positive-instructors-improve-learning-from-video-lectures); [IJAIED 2021](https://link.springer.com/article/10.1007/s40593-021-00282-y)
- **Platform precedent:** TikTok's "Jessie" TTS voice (actually a recorded human, Canadian radio host Kat Callaghan, though widely assumed to be a robot) became "almost the voice of TikTok". Creators use it **ironically**, pairing its bright, peppy delivery with dreary content such as lockdown footage. In other words, a mismatch between voice affect and content is already a native comedic device on the platform. — [Globe and Mail](https://arc-dev.theglobeandmail.com/canada/article-tiktok-talk-voice-tiktalk); [Good Morning America](https://www.goodmorningamerica.com/living/story/meet-woman-tiktoks-famous-jessie-voice-92990300); [Global News](https://globalnews.ca/news/9888850/what-happened-to-tiktok-text-to-speech-voice)

### Inferences
- **Flat reads as funny when:** (1) the *words* are absurd, overly literal, understated or bureaucratically formal about something trivial ("Step one. Stop. Doing that."), (2) visuals show something the voice under-reacts to, and (3) delivery stays *committed and polite*, as if the narrator fully believes this is normal. The incongruity is the joke, the voice is the straight man, and context carries the irony (Bryant & Fox Tree).
- **Flat reads as boring or robotic when:** (1) pitch is flat on *every* syllable with no lexical stress, which is a TTS failure, (2) the narrator sounds *bored or disinterested*, which Lawson et al. show listeners detect and dislike, (3) there are no rhythmic contrasts (all sentences the same length and the same pause), or (4) the content has no incongruity.
- Practical prosody target: a **narrow but not zero pitch range**, lower average pitch, falling (declarative) intonation even on absurd lines, normal word stress, no "smiling voice", and the **slowest, lowest line at the punchline** (consistent with Pickering 2009).
- Commonly cited deadpan archetypes to *describe* (not imitate) in briefs: the flat one-liner comic who delivers surreal observations in a slow monotone; the "unflappable straight man" reacting to chaos with polite understatement; the corporate/airline-announcement register applied to trivial life problems; nature-documentary gravitas applied to mundane objects. Examples often named for deadpan include silent-film "stone face" comedy and laconic stand-up one-liner styles. These examples were not verified in this session, and the voice must remain an original or stock TTS voice.

### Gaps
- No controlled experiment found that compares the same joke in flat vs expressive delivery for perceived funniness.
- No research found on whether TTS-generated deadpan is perceived differently from human deadpan.

---

## 4. Calm voices: calm/soothing narration, ASMR-adjacent content, low-arousal "slow" content, and why Gen Z seeks calm

### Takeaway
The physiology evidence for calming audio is **real but narrow**. ASMR lowers heart rate only in people who experience ASMR (MODERATE, from a single well-cited study). The "Gen Z wants calm" claim rests on **trend reports and surveys from agencies and brands (WEAK–MODERATE)**. These consistently describe a backlash against overstimulating "sludge" feeds, intentional boredom trends, and screen-time reduction. Calm delivery is plausibly a *differentiator*, but no study shows it increases retention on short-form platforms.

### Cited Findings
- **ASMR physiology (MODERATE; Poerio et al., PLOS ONE, 2018):** In a lab study, ASMR experiencers' heart rates dropped by about 3.14 bpm more than non-experiencers' while watching ASMR videos, comparable to stress-reduction techniques such as music and mindfulness. Skin conductance *rose*, which was unexpected. Pleasant-affect gains appeared only in ASMR experiencers. The authors call the findings preliminary. — [University of Sheffield news](https://www.sheffield.ac.uk/psychology/news/brain-tingles-first-study-its-kind-reveals-physiological-benefits-asmr); [ScienceDaily](https://www.sciencedaily.com/releases/2018/06/180621101334.htm); [DOAJ record](https://doaj.org/article/91d993963fe84ace8e7ac1fccc699275)
- **Backlash against overstimulation (WEAK–MODERATE; agency trend report, 2024):** We Are Social's Think Forward 2024 describes a shift away from hyper-stimulating "sludge" (split-screen) feeds toward content that minimises sensory overload, such as lo-fi looping animations. — [We Are Social Think Forward 2024: Attention Layering](https://thinkforward.wearesocial.com/01-attention-layering.html)
- **Intentional disconnection (WEAK–MODERATE; brand survey):** 63% of Gen Z report intentionally reducing screen time for wellbeing, and 39% of Gen Z smartphone owners would consider a flip phone. — [Later blog: Gen Z offline era](https://later.com/blog/the-yearn-for-more-how-brands-can-reach-gen-z-in-their-offline-era/)
- **Boredom and silence trends (WEAK; journalism, Oct 2025):** "Rawdogging", meaning sitting with no phone, music or distraction, and viral silence challenges are framed as attention resets amid concern that constant short-form exposure hurts attention. — [AOL: Gen Z sitting in silence](https://www.aol.com/articles/members-gen-z-sitting-silence-184548786.html); [KQ98: binging on boredom](https://www.kq98.com/2025/10/09/binging-on-boredom-becomes-popular-way-to-unplug)
- **"83% of Gen Z watch soothing content" (WEAK, source untraceable):** This statistic circulates but I could not trace it to a primary survey. — [Comfort-content blog](https://pineapple-pepper-wmfy.squarespace.com/lately/comfort-creators)

### Inferences
- A calm, low-arousal voice fits a real counter-trend, but the channel is still *on* a high-intensity feed. The calm is the **contrast that makes the hook noticeable**, not a reason to slow the first second. Treat "calm" as the persona's emotional baseline, and keep information density high.
- ASMR-style whispering or close-mic sound is **not** recommended. Its effects are limited to ASMR-responsive people, it would push the channel toward "sleep content", and the brief is comedic-useful, not sleep. A warm, close, low-reverb mic sound is enough.

### Gaps
- No peer-reviewed study found on "slow TV" or low-arousal *short-form* video performance with Gen Z.
- No primary data found on what share of Gen Z prefers calm narration on Shorts/TikTok.

---

## 5. Synthetic voices: trust, credibility, learning, the voice uncanny valley, backlash against "AI voice" channels, and how to make TTS feel intentional

### Takeaway
The old "voice principle" (human beats machine voice) was built on **dated TTS**. Studies with modern engines find **no learning penalty** and similar credibility (MODERATE–STRONG for the narrow claim that modern TTS ≈ human for learning). Listeners now often **cannot tell** AI from human voices (MODERATE). The real risk is **perceived AI-ness**: when audiences *suspect* AI, trust drops sharply (WEAK–MODERATE, industry surveys), and "unnatural voice" is one of the top tells. YouTube's 2025 "inauthentic content" policy targets mass-produced, repetitive output, not AI voices as such. The defence is to make the voice an obviously *designed character* with original scripting.

### Cited Findings
- **Original voice principle (STRONG historically, but dated technology; Mayer, Sobko & Mautone, *J. Educ. Psych.*, 2003):** Students did better on transfer and rated the speaker more positively with a standard-accented voice than a foreign-accented one (Exp. 1), and with a human voice than a machine voice (Exp. 2). — [Gunadarma library record](https://library.gunadarma.ac.id/journal/social-cues-in-multimedia-learning-role-of-speakers-voice); [Cambridge Handbook chapter](https://www.cambridge.org/core/books/abs/cambridge-handbook-of-multimedia-learning/principles-based-on-social-cues-in-multimedia-learning/093C1CDE75CF486DACD4CABC325ABE47)
- **Critique of the 2003 design:** It compared only two voices, which may have differed on more than one dimension, and it measured no cognitive load. — [Redalyc review PDF](https://www.redalyc.org/pdf/2931/293123547018.pdf)
- **Modern TTS ≈ human (MODERATE; Craig & Schroeder, *Computers & Education*, 2017):** The human voice and a modern TTS engine both beat an older TTS engine on credibility and learning. — [ASU Elsevier Pure (Chiou et al. record citing it)](https://asu.elsevierpure.com/en/publications/how-we-trust-perceive-and-learn-from-virtual-humans-the-influence/). A vendor summary adds that the modern voice gave more transfer and training efficiency than the old engine and was rated on par with the human voice. — [ReadSpeaker blog (vendor)](https://www.readspeaker.com/blog/elearning-voice)
- **Replication (MODERATE; Craig & Schroeder, 2018/2019, "Text-to-Speech Software and Learning: Investigating the Relevancy of the Voice Effect"):** No significant differences in learner perceptions, learning outcomes or efficiency between modern TTS and human voice. This is known only via a vendor summary. — [ReadSpeaker blog (vendor)](https://www.readspeaker.com/blog/elearning-voice)
- **Voice quality affects trust, not learning (MODERATE; Chiou, Schroeder & Craig, *Computers & Education* 146:103756, 2020):** Voice quality did not significantly affect learning but did affect trust and other perceptions. — [ASU Elsevier Pure](https://asu.elsevierpure.com/en/publications/how-we-trust-perceive-and-learn-from-virtual-humans-the-influence/)
- **Newer studies (WEAK; secondhand via a 2025 preprint):** Deng et al. found no effect of human vs synthetic narration on motivation or retention, and Zhang & Wu (2024) report high-quality synthesized voices are as effective as human voices for learning, retention and cognitive load. — [arXiv 2511.20660](https://arxiv.org/abs/2511.20660v1)
- **Quality over origin (WEAK, vendor study):** TechSmith varied only the narration (high/low-quality human vs AI). Clarity and polish mattered more than human vs AI, and quiz scores rose with voice quality. — [TechSmith blog](https://techsmith.com/blog/ai-voices-avatars-in-training-videos)
- **Detection (MODERATE; Barrington, Cooper & Farid, *Scientific Reports* 15:11004, 2025):** Listeners labelled AI voices correctly as AI only about 60% of the time, and judged ElevenLabs clones to match the real speaker's identity about 80% of the time (220 speakers). — [UC Berkeley I School](https://www.ischool.berkeley.edu/research/publications/2025/people-are-poorly-equipped-detect-ai-powered-voice-clones); [PMC11958761](https://pmc.ncbi.nlm.nih.gov/articles/PMC11958761/)
- **Detection, second lab (MODERATE; Lavan et al., PLOS One, 2025):** 58% of voice clones were judged human. Fully synthetic, non-cloned voices were judged human 41% of the time. — [Live Science](https://www.livescience.com/technology/artificial-intelligence/ai-voices-are-now-indistinguishable-from-real-human-voices); [The Register](https://www.theregister.com/2025/10/09/voice_clone_detection_study/)
- **Voice uncanny valley (MODERATE, mixed):** Kühne, Fischer & Zhou (2020, n=95) found the human voice rated higher on all dimensions except eeriness, and "no evidence for an auditory uncanny valley". Baird et al. (2018) found likability rises *monotonically* with voice human-likeness. — [Frontiers in Neurorobotics 2020](https://www.frontiersin.org/journals/neurorobotics/articles/10.3389/fnbot.2020.593732/text). Higgins et al. (2022) found a synthetic voice on a *photorealistic* virtual human supported **mismatch** theories of the uncanny valley. — [Trinity College Dublin repository](https://www.tara.tcd.ie/bitstreams/3afb8626-9296-4838-832a-9230d94d4c44/download). A voice-assistant study found the most realistic voice was rated most pleasant and least eerie. — [PMC9136288](https://pmc.ncbi.nlm.nih.gov/articles/PMC9136288)
- **Suspected-AI penalty (WEAK–MODERATE; Raptive survey of 3,000 US adults, July 2025):** Trust fell by nearly half when people *believed* content was AI-made, and purchase consideration dropped 14%. — [PPC Land](https://ppc.land/raptive-study-shows-ai-content-cuts-reader-trust-by-half/); [ContentGrip](https://www.contentgrip.com/raptive-study-ai-stink/)
- **Voice as a tell (WEAK–MODERATE; Animoto report, Sept 2025 survey, published Jan 2026):** About 83% had watched a video they suspected was AI. Top giveaways were robotic gestures (67%) and **unnatural voices (55%)**, and 36% said AI video lowers brand trust. — [Business Wire](https://www.businesswire.com/news/home/20260121875037/en); [Adweek](https://www.adweek.com/adweek-wire/83-of-consumers-can-spot-ai-videos-36-say-it-hurts-brand-trust-new-animoto-report/)
- **Blind-test parity (WEAK–MODERATE; Studio Resonate/SiriusXM, 1,326 weekly radio listeners):** AI and human voiceover scored within a few points on trust, energy and likability for promo reads when listeners didn't know the source. — [ContentGrip](https://www.contentgrip.com/studio-resonate-ai-voice-study/)
- **YouTube policy (July 15, 2025):** "Repetitious content" was renamed "inauthentic content" to cover mass-produced, repetitive material. TeamYouTube called it "a minor update", and YouTube clarified that it is not a crackdown on "faceless" channels as such. — [AOL/TechCrunch syndication](https://www.aol.com/youtube-monetization-policies-battles-ai-154324339.html); [AlternativeTo](https://alternativeto.net/news/2025/7/youtube-updates-its-policy-to-demonetize-inauthentic-mass-produced-ai-generated-content). Third-party reading (WEAK): an AI voiceover reading *original* scripts generally doesn't trigger it unless it impersonates a real person. — [Fliki blog](https://fliki.ai/blog/youtube-monetization-policy-2025). Reports of a January 2026 wave of channel terminations exist but come from secondary sources (WEAK). — [WebProNews](https://www.webpronews.com/youtubes-war-on-ai-slop-collides-with-faceless-creators-who-built-the-platform-first/)

### Inferences
- The learning risk of TTS is now small. The main risks are **perceived low effort** (the "AI slop" heuristic) and the **default-voice tell** (the same stock voice and default settings heard on thousands of channels).
- Ways to make TTS feel intentional, built from the evidence above:
  1. **Character over realism.** Give the narrator a stated persona (e.g., "an extremely polite, slightly tired help-desk narrator") and keep it in *writing* style, catchphrases and sign-offs. Deadpan makes residual TTS flatness *fit the character* instead of exposing it.
  2. **Deliberate, visible timing.** Pauses that land on visual beats read as authored. Default TTS pauses read as accidental.
  3. **Avoid the most-used stock voices and default settings.** Pick a less common voice, or tune speed and pitch slightly away from default (unnatural or generic voices are a top "AI tell" per Animoto).
  4. **Originality signals for YouTube's policy:** original scripts, a recurring visual character, varied formats, no templated mass output.
  5. **Optional transparency.** A light, self-aware nod in the bio ("narrated by a very calm robot") turns the AI fact into part of the bit. The Raptive data suggests *suspicion* hurts. Whether owning it helps or hurts is untested, so A/B it in the bio or pinned comments, not in the videos themselves.
- Platform labelling (TikTok/YouTube "altered or synthetic" disclosures) applies mainly to realistic depictions of people or events. Stock TTS narration over drawn animation is generally outside that scope. I did not verify current label rules this session, so the report writer should flag it.

### Gaps
- No study found on Gen Z or teen reactions to AI narration specifically.
- I could not access the full texts of Craig & Schroeder 2017/2019. Details come from abstracts and a vendor blog.
- Current (Nov 2026) TikTok and YouTube AI-disclosure rules were not verified.

---

## 6. Voice character: does a consistent narrator persona improve recognisability and follow rate, and how do faceless channels build a "voice brand"?

### Takeaway
I found **no independent research** linking narrator-voice consistency to follow rate. The advice that voice is a faceless channel's main brand signal comes from **vendor and creator guides (WEAK)**. Indirect evidence is suggestive: the TikTok "Jessie" voice became a recognisable platform signature, and listeners reliably infer narrator emotion and character from voice alone. Recommend one locked voice plus a consistent persona, and vary content and formats so the channel doesn't look templated.

### Cited Findings
- **Voice as brand signal (WEAK, vendor guides):** The narrator voice is called "the single most powerful brand signal for a faceless channel", and switching voices between uploads confuses returning viewers. — [Fluxnote: faceless channel branding guide](https://fluxnote.io/guides/faceless-channel-branding-guide); [EasyViral](https://easyviral.ai/blog/build-brand-identity-faceless-youtube-channel-2026); [Narration Box (vendor)](https://narrationbox.com/blog/secret-to-faceless-youtube-growth-voice-cloning)
- **Niche fit (WEAK, opinion):** In credibility niches (health, finance, tech) an authoritative voice reportedly beats a warm one. — [Fluxnote](https://fluxnote.io/guides/best-ai-voice-faceless-youtube-channel-2026)
- **Consistency vs sameness:** Channels whose output looks too similar risk being treated as mass-produced or inauthentic. — [AOL/TechCrunch on YouTube policy](https://www.aol.com/youtube-monetization-policies-battles-ai-154324339.html); [Fluxnote](https://fluxnote.io/guides/faceless-channel-branding-guide)
- **A recurring synthetic-sounding voice can become iconic:** TikTok's "Jessie" voice is described as "almost the voice of TikTok", "similar to how Siri has become the voice of Apple". — [Globe and Mail](https://arc-dev.theglobeandmail.com/canada/article-tiktok-talk-voice-tiktalk)
- **Voice carries persona and emotion:** Learners identify narrator emotional states from voice alone about as well as with a visible agent. — [Lawson et al. 2021 (PDF)](https://www.cs.purdue.edu/homes/bbenes/papers/Lawson2021EdTechResDev.pdf)

### Inferences
- Build the brand as **voice + script voice + visual character + sonic tag**: the same TTS voice and settings, a stable persona bible (what the narrator calls the viewer, the sign-off, signature understatements), and a recurring 0.5–1 s sound or visual sting.
- The persona should be **calm-competent-polite**, not bored (section 3). A "tired but helpful" persona works when the tiredness is aimed at the *problem* ("You did the thing again. Fine.") and the helpfulness at the *viewer*.
- Lock the voice after the A/B phase (section 9) and do not change it for at least 30–50 uploads. A voice change effectively restarts recognition. This is an inference with no data.

### Gaps
- No empirical data found on follow or subscribe rates vs voice consistency for faceless channels.
- No academic study found on "voice brand" or sonic identity for creator channels (sonic-branding research for ads exists but was not reviewed this session).

---

## 7. Practical TTS direction: getting slow, deadpan delivery from Kokoro, Piper, Qwen3-TTS, edge-tts and ElevenLabs

### Takeaway
Each engine has one global speed control, and only some honour in-text pause markup. **ElevenLabs** (non-v3 models) supports `<break time="x.xs"/>` up to ~3 s plus a speed setting. **Azure SSML** supports `<break>` and `<prosody rate>`, but **edge-tts blocks custom SSML** and offers only global `--rate/--pitch/--volume`. **Piper** has `length_scale` and `sentence_silence`. **Kokoro** has a `speed` multiplier. **Qwen3-TTS** takes natural-language `instruct` on the 1.7B CustomVoice model only. For engines without break tags, the reliable approach is **generate per sentence, then insert exact silences in post** (ffmpeg or the timeline).

### Cited Findings
- **ElevenLabs speed:** 1.0 is the default, below 1.0 slows and above speeds up. — [ElevenLabs API: get default voice settings](https://elevenlabs.io/docs/api-reference/voices/get-default-settings). On ElevenLabs' Agents platform the documented supported range is **0.7–1.2**, and values outside it are not supported. — [ElevenLabs: speed control](https://elevenlabs.io/docs/agents-platform/customization/voice/speed-control). Conflict: a community SDK page lists 0.25–4.0, and the toolkit's own reference lists 0.5–2.0. — [Mintlify ElevenLabs Python reference](https://www.mintlify.com/elevenlabs/elevenlabs-python/api-reference/voices/settings); `/home/user/claude-code-video-toolkit/.claude/skills/elevenlabs/reference.md`. **Treat 0.7–1.2 as the safe range.**
- **ElevenLabs break tags:** `<break time="1.5s" />`, max ~3 s per break. "Excessive breaks can cause speed artifacts." — `/home/user/claude-code-video-toolkit/.claude/skills/elevenlabs/SKILL.md` (toolkit skill derived from ElevenLabs docs; live docs could not be fetched this session). **Eleven v3 reportedly does NOT support SSML break tags**; use audio tags and punctuation instead (WEAK, third-party). — [skills.lc ElevenLabs TTS skill](https://skills.lc/openclaw/skills/openclaw-skills-skills-shaharsha-elevenlabs-tts-skill-md)
- **ElevenLabs v3 stability:** The official v3 prompting guide calls stability "the most important setting in v3", with Creative/Natural/Robust modes. Creative is most expressive but "prone to hallucinations", and Robust "reduces responsiveness to directional prompts". — [ElevenLabs prompting guide](https://elevenlabs.io/docs/best-practices/prompting); [mirror](https://cdntest.elevenlabs.io/docs/best-practices/prompting). Third-party guides suggest lowering stability to 0.3–0.5 when tags sound muted (WEAK). — [Runware: directing with audio tags](https://runware.ai/docs/models/elevenlabs-v3/guides/directing-with-audio-tags)
- **Toolkit defaults:** `tools/voiceover.py` defaults to ElevenLabs stability 0.85 ("higher = more consistent"), style 0.0 ("lower = more neutral") and speed 1.0, all exposed as CLI flags (`--stability`, `--style`, `--speed`). — `/home/user/claude-code-video-toolkit/tools/voiceover.py`
- **Azure SSML:** `<break time>` accepts 0–5000 ms in Microsoft's English docs (other Microsoft pages state a 20000 ms cap, so verify), and `<prosody rate>` accepts relative percentages (e.g., `-20%`) or keywords such as `slow`. — [Microsoft Learn: SSML document structure](https://learn.microsoft.com/en-us/azure/ai-services/speech-service/speech-synthesis-markup-structure)
- **edge-tts:** Custom SSML support was **removed since v5.0.0** because Microsoft blocks SSML that Edge itself wouldn't generate. `--rate`, `--volume` and `--pitch` still work (pitch in Hz, e.g., `--pitch=-50Hz`), and negative values need `=` (e.g., `--rate=-50%`). Only a single `<speak>`/`<voice>` is allowed, so there is no per-phrase prosody. — [rany2/edge-tts GitHub](https://github.com/rany2/edge-tts); [PyPI edge-tts](https://pypi.org/project/edge-tts/); [commit "drop custom SSML support"](https://git.vicicode.com/mirrors/edge-tts/commit/68a9e191d7b00c424fe137390254a7a5c8e41db7)
- **Kokoro-82M:** `speed` is a multiplier, default 1.0, with <1 slower. Allowed ranges differ by wrapper (0.5–2.0 in one HF Space, 0.25–4.0 in Featherless). — [Chutes Kokoro docs](https://chutes.ai/docs/models/chutes-kokoro); [Featherless Kokoro docs](https://featherless.ai/docs/audio-speech-model-kokoro); [HF Space wrapper](https://huggingface.co/spaces/vyles/Tools/blob/cbe02121522865ddf7ab8b559dc7343a76554a19/Modules/Generate_Speech.py)
- **Piper:** `length_scale` sets speed (higher = slower, default 1.0). `noise_scale` (default 0.667) adds variation and `noise_w` (default 0.8) sets phoneme-width variation. `sentence_silence` (seconds, default 0.0) appends silence after each sentence. Example: `piper -m foo.onnx --length_scale 0.5 --sentence_silence 2`. — [Piper voice.py (HF mirror)](https://huggingface.co/spaces/DLI-SLQ/piper-tts/blob/main/piper/voice.py); [en_US-amy voice config](https://huggingface.co/rhasspy/piper-voices/blob/v1.0.0/en/en_US/amy/medium/en_US-amy-medium.onnx.json); [linuxcommandlibrary: piper](https://linuxcommandlibrary.com/man/piper)
- **Qwen3-TTS:** Instruction control comes with the CustomVoice models, which have 9 premium speakers. The **0.6B CustomVoice ignores `instruct`**, so use the **1.7B CustomVoice**. Doc examples include "Speak very slowly and calmly". — [Qwen3-TTS docs: custom voice](https://www.mintlify.com/QwenLM/Qwen3-TTS/guides/custom-voice); [Qwen3-TTS FAQ](https://www.mintlify.com/QwenLM/Qwen3-TTS/resources/faq). Alibaba's hosted instruct model documents natural-language control of pitch, speaking rate, emotion and "character personality". — [Alibaba Cloud Model Studio TTS](https://www.alibabacloud.com/help/en/model-studio/tts-model/)
- **Toolkit Qwen3 presets:** `calm` = "Speak slowly and calmly, with a soothing, relaxed delivery." and `professional` = "Speak in a clear, professional tone with measured pacing." Unknown `--tone` strings are passed through as raw instruct text, and **instruct is ignored for cloned voices** (`--ref-audio`). — `/home/user/claude-code-video-toolkit/tools/qwen3_tts.py` (lines 83–95, 977–988)

### Inferences (settings to try; all need ear-testing)
- **Universal method:** write one sentence per line, generate **per sentence** (or per beat), then assemble with exact silences in Remotion/moviepy/ffmpeg. This works on every engine, avoids TTS drift and pause compression, and makes pause length an editable variable for A/B tests (it matches the toolkit's "audio-anchored timeline" pattern in CLAUDE.md).
- **ElevenLabs (Multilingual v2 / Turbo-class models, which support `<break>`):** stability 0.75–0.9 (flatter, consistent), similarity ~0.75, style 0.0, speed 0.88–0.95, `<break time="0.4s"/>` between clauses, `<break time="0.8s"/>` before a punchline, and none longer than 1.5 s in-line (longer gaps go in post). **v3:** use only if you need tags such as calm or flat delivery cues. Use Natural stability, no `<break>`, and test whether tags help or hurt the deadpan.
- **edge-tts:** `--rate=-10%` to `--rate=-20%`, `--pitch=-2Hz` to `--pitch=-6Hz`. Get pauses from sentence-per-clip generation plus inserted silence, since in-text breaks aren't possible. Periods and line-final punctuation give natural short pauses. Ellipses vary by voice, so test them.
- **Kokoro:** `speed` 0.85–0.92. Separate sentences with periods. Generate per sentence and pad silence in post.
- **Piper:** `length_scale` 1.1–1.25 (slower), `sentence_silence` 0.35–0.5, and try `noise_scale` ~0.5 and `noise_w` ~0.6 for a flatter, steadier read (inference from the parameter definitions; untested).
- **Qwen3-TTS (1.7B CustomVoice), example instruct (original persona, no real-person reference):** "Speak slowly and evenly in a calm, flat, matter-of-fact tone, like a very polite narrator who has explained this many times before. Keep pitch low and steady. No excitement, no smiling. Pause briefly after each sentence. Say the last line slightly slower and lower." Also try `--temperature` 0.4–0.6 for consistency (the toolkit notes lower temperature = more consistent).
- **Punctuation tricks (engine-dependent, test):** a full stop instead of a comma gives a longer, falling cadence. A single-word sentence ("Anyway.") creates a deadpan beat. A line break or a new clip is the most reliable pause. Spell out numbers and abbreviations to avoid odd stress.

### Gaps
- The live ElevenLabs docs (exact break-tag limit, v3 tag list, current speed range for the TTS endpoint) could not be fetched. Values come from search snippets and toolkit files.
- No official documentation found on how Kokoro or edge-tts voices handle ellipses or em-dashes.
- The current official Qwen3-TTS Hugging Face model card was not retrieved directly. Details come from mirrored docs.

---

## 8. Gender, accent and age of voice: effects on trust or retention for young audiences

### Takeaway
The only robust voice-identity finding is that **standard-accented** narration beat a foreign accent for learning and speaker ratings (Mayer et al. 2003, MODERATE, and critiqued for confounds). I found **no reliable evidence** that narrator gender or perceived age affects trust or retention for 13–29-year-olds on short-form video. **Test, don't assume.**

### Cited Findings
- **Accent:** Learners did better on transfer, and rated the speaker more positively, with a standard accent than a foreign accent. — [Gunadarma record of Mayer, Sobko & Mautone 2003](https://library.gunadarma.ac.id/journal/social-cues-in-multimedia-learning-role-of-speakers-voice). Mayer's handbook later states the voice principle as learning better from "a standard-accented human voice". — [Cambridge Handbook chapter](https://www.cambridge.org/core/books/abs/cambridge-handbook-of-multimedia-learning/principles-of-multimedia-learning-based-on-social-cues-personalization-voice-and-image-principles/19309D764FD015A556334531A463DE03)
- **Confound critique:** The 2003 study compared only two voices, which may have differed on other dimensions. — [Redalyc review](https://www.redalyc.org/pdf/2931/293123547018.pdf)
- **Gender:** A study on voice gender in multimedia (García Rodicio, *Electronic Journal of Research in Educational Psychology*) exists, but its findings could not be confirmed from the available abstract. — [Redalyc PDF](https://www.redalyc.org/pdf/2931/293123547018.pdf)
- **Quality dominates:** Vendor research found voice quality and clarity mattered more than human vs AI origin (WEAK). — [TechSmith](https://techsmith.com/blog/ai-voices-avatars-in-training-videos)

### Inferences
- For a US/global English audience, a voice heard as **"standard" North American or neutral international English** is the low-risk default for clarity. A distinctive accent could become part of the persona but adds risk and needs testing.
- Gender and perceived age: no evidence base, so include at least one male-presenting, one female-presenting and one androgynous or low-affect voice in the A/B test (section 9).
- For deadpan specifically, **lower-pitched and steady** voices of any gender are likely easier to make sound "dry" in TTS. This is an inference from the punchline-pitch findings in section 2, not tested.

### Gaps
- No peer-reviewed evidence found on narrator gender, accent or age effects for teen/young-adult viewers on TikTok or Shorts.
- García Rodicio's voice-gender findings are unverified.

---

## 9. Synthesis: voice style guide and A/B test plan (derived from sections 1–8)

### Takeaway
Use a calm, polite, slightly tired but **competent** narrator. Average about 130–140 wpm including pauses, with near-normal speed inside phrases and the slowness carried by deliberate gaps. Use a low, steady pitch with falling endings, and make the punchline the slowest, lowest line, followed by a short silent beat over a visual reaction. Start talking at frame 0. Choose the voice with a two-stage test: a blind listener panel, then on-platform metrics.

### Cited Findings (evidence anchors for the guide)
- Comprehension is fine up to ~270 wpm, so slowness is stylistic. — [McMaster](https://experts.mcmaster.ca/scholarly-works/2127220)
- Very slow speech (≤ ~100 wpm) was rated less credible. — [Typeset PDF](https://typeset.io/pdf/speed-of-speech-and-persuasion-48bx24hl8s.pdf)
- Pauses at meaningful boundaries aid memory for the next word. — [St Andrews](https://research-portal.st-andrews.ac.uk/en/publications/listening-to-the-sound-of-silence-disfluent-silent-pauses-in-spee/)
- Punchlines are naturally lower in pitch and slower, not reliably preceded by pauses. — [Penn State](https://pure.psu.edu/en/publications/prosodic-markers-of-saliency-in-humorous-narratives/)
- A bored-sounding narrator lowers learner motivation. — [Lawson et al. 2021](https://www.cs.purdue.edu/homes/bbenes/papers/Lawson2021EdTechResDev.pdf)
- "Unnatural voice" is a top AI tell, and suspected AI halves trust. — [Business Wire/Animoto](https://www.businesswire.com/news/home/20260121875037/en); [PPC Land/Raptive](https://ppc.land/raptive-study-shows-ai-content-cuts-reader-trust-by-half/)
- "Viewed vs swiped away" is the key Shorts hook metric, with ~70–80% as a creator heuristic. — [Creator Essentials](https://www.creatoressentials.com/glossary/viewed-vs-swiped-away/); [Subscribr](https://subscribr.ai/p/youtube-shorts-analytics-metrics-viral)

### Inferences: VOICE STYLE GUIDE (v1, to be tuned by testing)

**Persona.** "The Very Calm Narrator": polite, unhurried, mildly weary about the *problem*, never about the *viewer*; fully committed to every word, never winks. It is an original stock or designed TTS voice and imitates no real person.

**Rate.**
- Effective rate (pauses included): **130–140 wpm**, never below ~120.
- Articulation inside phrases: ~145–160 wpm (TTS speed ≈ 0.88–0.95 on ElevenLabs/Kokoro, `length_scale` ≈ 1.1–1.2 on Piper, `--rate=-10…-15%` on edge-tts).
- Word budget: 45 s ≈ 100 words; 55 s ≈ 120 words (fewer if the script has many beats).
- By section: **Hook** (0–3 s) is the densest and slightly faster, with no lead-in silence. **Why/What** at baseline. **How** at baseline with one pause before each step. **Solution/punchline** is the slowest line, about 10–15% slower than baseline.

**Pauses (edit in post where the engine can't).**
- Lead silence: **0 s** (audio starts ≤0.3 s).
- Between clauses: 0.2–0.3 s. Between sentences: 0.4–0.6 s.
- Before a key term or step number: 0.4–0.5 s (signpost pause).
- Comedic beat: **0.6–1.0 s *after*** the deadpan line, with a visual reaction (blink, slow zoom, freeze). Optional 0.3–0.6 s *before* it. Test longer pre-punchline beats (section 2 counterpoint).
- One signature "awkward silence" of up to ~1.5 s per video, max, and only while something on screen changes.
- End: a 0.3–0.5 s tail, then a hard cut or loop point (loops help Shorts replays; this is a creator heuristic and was not researched here).

**Pitch and energy.**
- Low-to-mid pitch, narrow range, steady loudness, no "smiling voice", no rising question intonation on statements.
- Declarative falling endings, *especially* on absurd lines (deadpan = treating the absurd as routine).
- Energy: calm, not sleepy. If listeners describe it as "bored", raise the warmth, not the speed (Lawson et al.).

**Emphasis rules.**
- At most one emphasised word per sentence. Create emphasis by **isolation** (a short sentence or a pause before the word), not by pitch spikes.
- Put the punchline's key word *last* in the sentence (end-weight).
- One-word sentences as beats ("Correct." "Anyway." "No.").
- Never stack several jokes in one breath. Give each joke its own sentence and beat.

**Where to place silence for comedic timing (Hook → Why → What → How → Solution).**
- Hook: no silence. Exception: a 0.3 s beat right after a deadpan opener if the visual is already funny.
- Why: one beat after the understated consequence ("This is bad. [0.6 s] For you.").
- How: signpost pauses before each step. The deadpan aside goes *after* a step, followed by a beat.
- Solution: slowest line, then a 0.6–1.0 s beat, then the sign-off or loop.

**Engine starting presets.**
- ElevenLabs (v2-class models): stability 0.8, similarity 0.75, style 0.0, speed 0.92, `<break>` ≤1.5 s, longer gaps in post.
- edge-tts: `--rate=-12% --pitch=-4Hz`, sentence-per-clip, silences in post.
- Kokoro: `speed=0.9`, sentence-per-clip.
- Piper: `--length_scale 1.15 --sentence_silence 0.45`, optionally `noise_scale 0.5`, `noise_w 0.6`.
- Qwen3-TTS 1.7B CustomVoice: the instruct text from section 7, temperature 0.5, with 2–3 speakers tested.

### Inferences: A/B TEST PLAN FOR CHOOSING THE VOICE
1. **Shortlist (day 1–2):** 4–6 candidate voices across engines and genders (e.g., 1–2 ElevenLabs, 1 Qwen3 speaker with the deadpan instruct, 1 Kokoro, 1 edge-tts neural voice). Render **the same 45 s script**, which contains a hook, one tip and two deadpan jokes, using identical animation and the pause map above.
2. **Blind panel (day 2–4):** recruit 15–30 people aged 13–29 (friends, Discord/Reddit communities; follow parental-consent norms for minors). Present the clips in random order with no voice names. Ask for 1–7 ratings of: "funny/dry", "clear", "trustworthy/useful", "sounds annoying-AI", "would keep watching", "bored-sounding". Also ask which one they would follow. Drop any voice rated high on "annoying-AI" or "bored". Keep the top 2.
3. **Pause-length micro-test (same panel or a second round):** take the winning voice and compare the punchline beat at 0.4 s vs 1.0 s, and effective rate at 125 vs 145 wpm (a 2×2 design). Pick the funniest combination that isn't rated "slow/boring".
4. **On-platform test (weeks 1–3):** alternate the top 2 voices across *different* topics in a balanced ABAB… order (≥6 Shorts per voice), posting at the same times. Don't post identical duplicate videos, given the inauthentic/repetitive-content risk. Compare medians of **viewed-vs-swiped (stayed to watch)**, average % viewed, likes and subscribers per 1k views, and comment sentiment (count "AI voice" complaints vs "this voice 😭" love).
5. **Decision rule:** choose the voice that wins stayed-to-watch *and* subs per 1k views by a clear margin (e.g., ≥5 points on stayed-to-watch, consistent across most pairs). If it's a tie, choose the one the panel rated funnier. Then **lock voice and settings** (save them as a brand `voice.json` profile in the toolkit) for at least 30–50 videos, and only re-test pause and rate parameters after that.

### Gaps
- All numeric targets in this style guide are **inferences** built on general speech, humour and learning research plus creator heuristics. None has been validated on short-form vertical video with Gen Z audiences, so the A/B plan is how they get validated.
