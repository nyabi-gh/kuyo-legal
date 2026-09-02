# Kuyo Privacy Policy

Effective: September 2, 2026

Kuyo is a Discord bot that reads selected text messages aloud. It also contains an optional character-reply feature for explicit mentions, which the service operator may enable or disable. This policy explains what information Kuyo uses and how it is handled.

## Information we use

Kuyo uses only the information needed to provide its features:

- Discord server, channel, and user IDs
- Server settings, voice preferences, custom join greetings, and custom pronunciation entries
- Messages posted in the text channel selected by a server administrator
- When the optional character-reply feature is enabled, non-empty messages that explicitly mention Kuyo
- Display names and the names of mentioned users, roles, or channels when needed to read a message naturally

Kuyo does not collect passwords, payment information, contacts, or direct messages. With the character-reply feature disabled, messages outside the selected TTS channel are ignored. If the feature is enabled, Kuyo processes an outside-channel message only when it explicitly mentions Kuyo and contains other text.

## How information is used

Message text is prepared for speech. The default voice is a Microsoft Edge Read Aloud voice, so unless a member selects one of the local voices, the prepared text is sent to Microsoft. Supertonic, VOICEVOX, and the optional XTTS backend run locally in the service operator's deployment; Edge also receives the prepared text when a selected local backend fails before returning any audio. The generated audio is played in the connected Discord voice channel.

When the service operator enables the character-reply feature, a non-empty message that explicitly mentions Kuyo is reduced to remove Discord identifiers, links, code blocks, and spoiler-hidden text, and limited in length. The current message and up to three recent exchanges with that member from the previous 30 minutes are sent to the OpenAI Responses API. GPT-5.6 Luna writes Kuyo's short reply in the language of the message. Application code then checks that reply against a fixed grammar — a length limit, letters and simple punctuation, with at most four digits in a simple answer, no long number sequences, no digits next to words such as phone number or password, and no links, mentions, or markup — and replaces it with a curated character line if it does not fit. The application does not reject an otherwise valid message or reply solely because it contains sexually explicit wording. Questions about Kuyo's own instructions and knowledge questions are answered from a curated set rather than in the model's words. API response storage is disabled, and the only account information sent with a request is a one-way identifier derived from the Discord user ID with a secret key, used by OpenAI for abuse prevention; the ID itself is not sent. Messages without an explicit Kuyo mention and mentions with no other text are not sent to OpenAI.

Kuyo does not sell personal information, show advertising, create user profiles, or use message content for tracking.

## Storage and retention

Kuyo does not persist raw message text, generated audio, or conversation history to its database or disk. Completed speech may be held in a size-limited process-memory cache for up to 15 minutes to avoid synthesizing an identical line again. Cache keys are one-way hashes rather than readable message text, and cached audio is removed on expiry, eviction, or restart. When character replies are enabled, up to three recent exchanges per member are held in process memory for 30 minutes so a short conversation can continue. Each server keeps its own memory: what a member says in one server is never sent along with their conversation in another. This short-term memory is also cleared when the bot restarts or the member deletes all personal data.

Server settings and pronunciation entries are kept while the bot remains in the server. They are deleted when the bot is removed. Voice preferences and custom join greetings are shared across servers that use Kuyo and remain until the user deletes them or the service is discontinued.

Limited service logs may contain server IDs, Discord user IDs, timing information, and error messages. Message text is not written to these logs. Logs are automatically rotated and used only to keep the service reliable.

## Service providers

Kuyo relies on the following providers:

- [Discord](https://discord.com/privacy) for messages, commands, and voice connections
- [Microsoft](https://privacy.microsoft.com/privacystatement) for selected Edge voices and local-backend fallback speech
- [OpenAI](https://openai.com/policies/privacy-policy/) for writing Kuyo's short character reply only when the optional feature is enabled

Kuyo also runs Supertonic and [VOICEVOX](https://github.com/VOICEVOX/voicevox_engine) inside the service operator's own deployment. The operator may enable a similarly local XTTS-v2 service after installing compatible hardware. Text processed by these local engines is not sent to their providers as a speech-generation request, although first-time model installation may download model files from their distributors.

These providers may process information in countries outside your own and apply their own privacy terms.

## Your choices and rights

Use `/kuyo`, then open `My settings`, to see or delete the voice settings and custom join greeting linked to your Discord account. Deleting all personal data also clears the short-term conversation memory, in every server at once.

Server administrators can view or remove custom pronunciation entries from `/kuyo` → `Server settings` → `Pronunciation`. Removing Kuyo from a server deletes that server's settings and pronunciation entries.

For any other privacy request, contact the administrator who added Kuyo to your Discord server. Do not post personal information in a public issue or channel.

## Age requirements

Kuyo's character-reply feature is intended for adults. Server administrators should restrict access to suitable members and channels. Kuyo is not directed to children.

## Changes

This policy may be updated when Kuyo changes. The effective date at the top will be revised when material changes are made.
