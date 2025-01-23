<p align="center">
  <img src=".github/scripts/thinkaloud/banner.webp" alt="ThinkAloud-Banner" width="600">
</p>
<h1 align="center">ThinkAloud.md 🔊</h1>
<p align="center">
  <em><strong>A Sonic Scratchpad with Superpowers ⚡️</strong></br></em>Use voice notes to kick-off CI/CD workflows.

</p>

<p align="center">
<a href="https://www.youtube.com/watch?v=E4WlUXrJgy4" target="_blank">
    <img src="https://img.shields.io/badge/Python-3776AB?logo=python&logoColor=fff)" alt="Python">
</a>
</p>

---


> [!Note] **WIP** 🚧 
>
> This project is a work in progress.
> Methods are prone to change as I think things out.

## What?

ThinkAloud is a tool for transcribing voice notes that kick off automations ⚡️ 🤖

Rather than being conversational, like a chatbot, ThinkAloud lets you capture long, raw, unfiltered "Thinking out loud" recordings that can then be processed and formatted for easy reading later, according to pre-made templates.

Using [Assembly AI's LeMUR](https://www.assemblyai.com/blog/lemur/), this workflow is capable of producing transcriptions, summaries, key points, sentiment analysis and more. Check out their [playground](https://www.assemblyai.com/playground).

## Rationale

For too long have I had my best ideas while driving. Try as I may, dictation is hit-and-miss, especially with road noise. As I'm not at my most coherent while focussing on the road, I often pause, causing my phone's speech detection to timeout in the silence.

Even if the transcription is accurate, I'll still have to read through my enormous notes full of "umms" and "ahhs". I'm not much for concise dictation, after all.

I know what AI speech-to-text models are capable of from working with Whisper in the past (see [Squawk](https://github.com/in03/squawk)) and I figured it would be easy enough to build what I needed.


`Question:`
> Wait... There are a *lot* of voice note apps hitched to the AI bandwagon. Why make another?

`Answer:`
> Good question!

There are definitely a lot. When I tried to come up with a name for the project, about twenty of them were already taken... by AI voice note apps:

- Voicey
- VoiceCraft
- VoiceFlow
- VoxFlow
- NoteFlow
- Notable
- Notably
- etc.

I actually found *more* voice note apps trying to come up with a project than I did when I was actually searching for a drop-in candidate.

Of those that I did try, many were simple frontends for Whisper-like transcription that produced GPT-style summaries. For someone familiar with OpenAI API pricing, they felt like half-baked AI cash-grabs.

The apps were poorly designed, too-limited and inconvenient. To get notes out after transcribing often felt like mailing yourself a physical letter.

On the flip-side, there are [enterprise-ready PaaS solutions](https://tana.inc) that aim to be a one-stop-shop that revolutionises everything you're doing. That's too much for me. I'm happy with Obsidian and I don't want to subject myself to vendor lock-in even if there is a generous free tier (with AI, there usually isn't, and fairly so). This might change for me someday, but now.


## Use Cases

Since the templates are processed by a GPT, you can get really creative 🎨 You can even chain further workflows to automate further:

- **Clean up ad-lib artefacts**: "umms" and "ahhs",
mistakes, stutters, silences.

- **Re-record**: Swap your noisy car voice-note with a professional studio-quality voice-over using [ElevenLabs](https://elevenlabs.io/).

- **Speaker diarisation**: Title each reader uniquely for conversational dialogue, like for a podcast.

- **Journal**: Summarise your whole day as a structured journal entry with time and place context, emotional analysis, key points, etc.

- **Populate Dataviews**: Populate Obsidian dataview fields, autofill tables, queries and kick-off Javascript tasks.

- **Integrate with Workflow**: [n8n](https://n8n.io/) workflows.

- **Blogging**: Create draft posts that match the structure and tone of your personal blog, or even publish directly to GitHub pages afterwards.

- **Social Cross-Posting**: Publish to multiple social media platforms at once, respecting their various algorithms.

- **BYD**: Generate and publish proof-of-concept apps from spur-of-the-moment app ideas.


## Elevator Pitch

✨ **Picture this...**

You're stuck in your morning commute and you're in the zone for some great technical ideas for your blog. Thankfully you've set up ThinkAloud on your vault and you've created a `my-tech-blog.md` template. You start audio recording with Obsidian and, for twenty minutes, dictate your brand new industry-disrupting block-chain idea.  When you get to the office, your voice note now contains a full draft blog post, along with your original recording.

## How it Works
ThinkAloud relies on a GitHub Actions workflow to run a Python script when changes are made to your markdown notes.

The workflow searches for unhandled voice recordings embedded in the notes, calls Assembly AI for transcription and uses LeMUR to format, summarise or analyse the note, using user-made templates for structure, format and prompting.

## Prerequisites

To use ThinkAloud as intended right out-of-the-box, you'll require:

1. Obsidian
2. `Fit` sync plugin
3. GitHub account
4. AssemblyAI API key
5. ElevenLabs API key (optional)

## Setup

1. **Start tracking your notes with git:** While you can technically do manual commits and pushes, it won't be very fun. If you're using Obsidian, I recommend the [fit](https://github.com/joshuakto/fit) or [git](https://github.com/Vinzent03/obsidian-git) plugins. Both work on mobile with some caveats. **Fit works with GitHub only.**

2. **Add Thinkaloud**: Clone it to the base of your repo as a git submodule or download and merge manually if updates or git submodules aren't your thing.

3. **Configure**: Check the Github Actions workflow and make sure you're happy with the setup. Check paths, filenames, etc.

4. **Create templates**: Create templates to guide LeMUR to follow your desired structure, format and prompts.

5. **Try it**: Make sure you enable the built-in audio recording plugin if using Obsidian.

### Templates

There are a couple of templates already setup as examples. You can disable or delete them, use them for inspiration. Do as you will.
They serve as a reference for expected syntax and required fields, but here's a brief explainer.

These are placeholders
```jsx
{{ I am a placeholder }}
// I am a comment
I am a static string
```

```jsx
// Path: Templates/Journal-Entry.md

author: {{ Author }}
date: {{ Date}} 
tags: journal, diary, log

// A unique phrase used to match the voice note to the template. If not present, template filenames and content context are compared for a best guess match.
match_phrase: captains log

// Track state of transcription (ready, fail or success). Remove to disable.
ProcessSTT: ready

// Track state of ElevenLabs TTS (ready, fail or success). Remove to disable.
ProcessTTS: ready 

---

# {{ Title }}

{{ Tone/Emotion, 3 lines }}

{[ Context (when, where) , 2 lines }}

{{ TL;DR, paragraph }}

{{  Key points, 3 - 5 }}

```


## Compatibility

Beyond the Python script, ThinkAloud really consists of a CI/CD workflow. This should make it pretty easy to modify as needed by users. 

Official support for non-Obsidian and non-Github setups will be considered based on demand.

### Alternative Note Apps

Adaptation to other git-ready Markdown note apps should be pretty simple. 

Note apps that embed their audio files in the markdown file with a tag like,
```
[!audio](/user/me/notes/audio.mp3)
```
should work out of the box. 

If the audio is not embedded or is embedded in a different way, changes to the workflow file and Python script will be required.

### Alternative CI/CD

Converting the GH actions workflow to work on other CI/CD tools (GitLab, WoodPecker, CodeBerg, etc.) should be fairly straightforward.

### Alternative APIs

With access to the right models and powerful hardware, you could technically do this all self-hosted, albeit with varied results.

I've chosen to use paid APIs from two leading voice AI companies for ease of use. Other paid services may work as well, but it's a trail you'll have to blaze yourself.

### Alternative Everything

If you're looking for something else, you're welcome to try what I did and guess cool names for AI voice note projects and see what you find. Beyond that...

***[Audiopen](https://audiopen.ai/prime)*** is a "notable" 🤭 standout.

Of all the personal-use-tailored apps, AudioPen was the only one I liked and used consistently. The summaries are decent, the pricing is reasonable and the solo developer adds new features frequently. 

Conveniently, it's available as a PWA app and native mobile app for both Android and IOS. You can get simple summaries with voice notes up to 3 minutes long or pay for prime and get access to a slew of extra features. 

For the paid version, the Zapier integration and webhooks features could allow you to kick off other workflows and achieve some similar functionality to ThinkAloud, though I don't believe you can create templates.

## Contributing

This project is still pretty green, but if you reach out, I'm happy to chat 😊💬
