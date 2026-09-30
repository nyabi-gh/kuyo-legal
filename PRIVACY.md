# Kuyo Privacy Policy

Effective: September 30, 2026

Kuyo is a Discord bot that reads selected text messages aloud and provides optional social-link previews, enabled by default per server. It also contains an optional character-reply feature for explicit mentions, which the service operator may enable or disable, and mini-games any member can open with the `/game` command. This policy explains what information Kuyo uses and how it is handled.

## Information we use

Kuyo uses only the information needed to provide its features:

- Discord server, channel, user, and original/preview message IDs
- Server settings, voice preferences, custom join greetings and leave farewells, and custom pronunciation entries
- Messages posted in the TTS channels selected by a server administrator; in a voice channel's built-in chat, only messages from members in that voice channel are read
- Supported public-post URLs in accessible server channels when link previews are enabled
- When the optional character-reply feature is enabled, text and supported image attachments, including spoiler-marked images, in messages that explicitly mention Kuyo
- Display names and the names of mentioned users, roles, or channels when needed to read a message naturally
- While a word-chain game is running, messages posted in that channel, so that a word played into the game can be judged
- When the service operator runs the optional settings website and you sign in to it, your Discord user ID and the IDs of the servers you belong to

Kuyo does not collect passwords, payment information, contacts, or direct messages. Outside the selected TTS channels, Kuyo checks supported URLs when link previews are enabled and processes explicit mentions when character replies are enabled. It ignores messages from other bots and webhooks for link previews.

## How information is used

Message text is prepared for speech. The default voice is a Microsoft Edge Read Aloud voice, so unless a member selects one of the local voices, the prepared text is sent to Microsoft. Supertonic, VOICEVOX, and the optional XTTS backend run locally in the service operator's deployment; Edge also receives the prepared text when a selected local backend fails before returning any audio. The generated audio is played in the connected Discord voice channel.

When the service operator enables the character-reply feature, the text of a message that explicitly mentions Kuyo is reduced to remove Discord identifiers, links, code blocks, and spoiler-hidden text, and limited in length. For model-generated replies, the current message and up to eight recent exchanges with that member in the same channel or thread from the previous 30 minutes are sent to the OpenAI Responses API. Recognized technical text-decoding requests, and immediate requests to reformat that encoded text, receive a local character reply without a model call. For these requests, only a generic topic marker and the local reply are retained in conversation memory; the encoded payload is not retained. The configured model writes Kuyo's short reply in the language of the message. A quoted message is also included, reduced in the same way and limited to 500 characters, only when it is already cached in the same channel and was authored by that member or Kuyo. Other members' messages and full channel histories are not fetched for character replies. Application code checks the reply length (100 characters by default), limits number sequences to four digits per run and eight in total, and rejects sensitive numbers, links, or mentions. Harmless emoji and presentation marks are removed while retaining the words. Invalid output receives a localized format-error notice; unavailable generation and daily budget exhaustion have separate notices. These failure notices are not stored as conversation exchanges. The application does not reject an otherwise valid message or reply solely because it contains sexually explicit wording. Questions about Kuyo's own instructions use curated lines; unfamiliar topics and uncertain knowledge retain the model's contextual response. API response storage is disabled, and a one-way identifier derived from the Discord user ID with a secret key is sent for abuse prevention; the user ID itself is not sent. The same model response may also pick one of two fixed emoji reactions, which Kuyo adds to the member's message; no additional information is sent for this. Messages without an explicit Kuyo mention and bare mentions without eligible attachments are not sent to OpenAI. Unsupported image attachments may trigger a text-only request to explain that they could not be included.

When a member attaches images to a message mentioning Kuyo, up to four PNG, JPEG, or WebP images, including spoiler-marked attachments, of up to 8 MiB each are passed to OpenAI as signed Discord CDN URLs for visual understanding. Text is optional for these mentions. These URLs can contain channel and attachment IDs, filenames, and temporary access signatures. Text or personal information visible inside image pixels is not automatically redacted before transmission. Unsupported formats, pasted image links, embeds, and attachments on quoted messages are not passed as image inputs. Kuyo does not download or persist image files for this feature. Image URLs are used only for the current request and are not retained in the short-term conversation memory or application logs. The text question, generated answer, and a marker that an image was attached may remain in short-term memory under the same retention rules as other exchanges.

For link previews, Kuyo sends the author’s server display name, Discord avatar URL, and accompanying text to Discord through an application-owned webhook, with rewritten public-post URLs for Discord to render through the services in [the provider list](UNFURL_PROVIDERS.md). Nicknames and avatars identify the original sender; the message remains an application message. When it has Manage Messages permission, Kuyo removes the original after sending and recording its replacement and rechecking the original. Messages containing attachments or other context that cannot be preserved, oversized copies, and originals changed during copying are retained. The post identifier and any supported image selection are visible to Discord and the preview provider; Kuyo does not send the surrounding message text or Discord author ID to those providers. Their services may retrieve and cache the referenced public content.

The mini-games opened with `/game` use the Discord user IDs of the people playing, the titles, results, and candidate names an organizer types for a ladder or winner draw, and, for a word chain, the words they type. A message in a channel with a running word chain is examined only for a Korean word; anything else is left alone and is neither judged nor answered. When the service operator has configured a dictionary key, a single word played into the game, or the single syllable the next answer must begin with, is sent to the National Institute of the Korean Language's 표준국어대사전 open API to check that it is a noun and to find Kuyo an answer. No Discord server, channel, user identifier, or surrounding message text is sent with those lookups. Rock-paper-scissors, the ladder game, and winner draws send nothing outside Discord.

The optional settings website uses Discord sign-in with the `identify` and `guilds` permissions. At sign-in it reads your Discord user ID and the IDs of the servers you belong to, then revokes the Discord access token; the token is not kept. Your name and avatar are looked up through the bot when a page needs them and are not stored. Each time you open or change a server's settings, Kuyo asks Discord whether you are still a member and still have Manage Server. Settings changed on the website are stored exactly like the same settings changed with `/kuyo`. A voice preview on the website speaks one fixed sample sentence, never text you wrote; for a Microsoft Edge voice, only that sentence is sent to Microsoft, and the audio is not stored.

Kuyo does not sell personal information, show advertising, create user profiles, or use message content for tracking.

## Storage and retention

Kuyo does not persist raw message text, generated audio, or conversation history to its database or disk. Completed speech may be held in a size-limited process-memory cache for up to 15 minutes to avoid synthesizing an identical line again. Cache keys are one-way hashes rather than readable message text, and cached audio is removed on expiry, eviction, or restart. When character replies are enabled, up to eight recent exchanges per member are held in process memory so a short conversation can continue. Each channel and thread keeps its own memory: what a member says in one channel, such as a private one, is never sent along with their conversation in another channel or server. An exchange stops being used 30 minutes after it happened, and a member's conversation in a channel is removed from memory within about a minute once 30 minutes pass without them addressing Kuyo there. This short-term memory is also cleared when Kuyo leaves the server, when the bot restarts, or when the member deletes all personal data; a reply still being written when the member deletes their data is stopped and not posted.

Mini-games are held in process memory only. A game keeps the participants' user IDs, the words already played, the hands chosen, and any titles, results, and candidate names entered for it, and it is discarded when the game ends, when it is left alone (three minutes for a word chain, ten for the others), or when the bot restarts. Dictionary lookups are cached in memory for up to one hour. Nothing from a game is written to the database, and game results stay in the channel message like any other message.

Server settings and pronunciation entries are kept while the bot remains in the server. They are deleted when the bot is removed. Voice preferences and custom join greetings and leave farewells are shared across servers that use Kuyo and remain until the user deletes them or the service is discontinued.

Link-preview records contain original/preview message IDs, server/channel/author IDs, dismissal/replacement flags, and a SHA-256 fingerprint of the message text and normalized links. Raw URLs, media, avatar URLs, and webhook tokens are not stored in the database. Dismissal records prevent a removed preview from reappearing after edits or restarts. When Kuyo has replaced and removed an original, its tracking record remains until the replacement is deleted, the channel is deleted, or Kuyo leaves the server. For originals that remain, records are removed when Kuyo processes deletion of the original message or channel, or leaves the server; removing only the preview keeps a dismissal record. Events missed while offline are not replayed. For removal of remaining tracking records, contact the server administrator.

A website sign-in is kept as a random session cookie. The database stores only a one-way hash of that cookie, your user ID, the server IDs read at sign-in, and an expiry time. Sessions end after seven days, when you sign out, or when you delete all personal data, and expired sessions are removed automatically.

The service operator keeps copies of the database as backups, readable only by the server administrator, for up to 30 days; website sign-ins are left out of them. Settings you delete remain in backups made before the deletion until those backups expire. So that restoring a backup cannot bring deleted settings back, a deletion is also recorded with your user ID and time in a separate file for 35 days, and deletions made after a restored backup are applied again when the service starts.

Limited service logs may contain server IDs, Discord user IDs, timing information, and error messages. Message text is not written to these logs. Logs are automatically rotated and used only to keep the service reliable.

## Service providers

Kuyo relies on the following providers:

- [Discord](https://discord.com/privacy) for messages, commands, voice connections, and link previews
- The external services in [the preview provider list](UNFURL_PROVIDERS.md) for supported social-link previews
- [Microsoft](https://privacy.microsoft.com/privacystatement) for selected Edge voices and local-backend fallback speech
- [OpenAI](https://openai.com/policies/privacy-policy/) for writing Kuyo's short character reply only when the optional feature is enabled
- The National Institute of the Korean Language's [표준국어대사전 open API](https://stdict.korean.go.kr/openapi/openApiInfo.do) for checking a word in the word-chain game, only when the service operator has configured a key

Kuyo also runs Supertonic and [VOICEVOX](https://github.com/VOICEVOX/voicevox_engine) inside the service operator's own deployment. The operator may enable a similarly local XTTS-v2 service after installing compatible hardware. Text processed by these local engines is not sent to their providers as a speech-generation request, although first-time model installation may download model files from their distributors.

These providers may process information in countries outside your own and apply their own privacy terms.

## Your choices and rights

Use `/kuyo`, then open `My settings`, or the settings website when it is available, to see or delete the voice settings, custom join greeting, and custom leave farewell linked to your Discord account. Deleting all personal data also clears the short-term conversation memory, in every channel and server at once, and ends every website sign-in.

Server administrators can view or remove custom pronunciation entries from `/kuyo` → `Server settings` → `Pronunciation`. Removing Kuyo from a server deletes that server's settings and pronunciation entries.

Server administrators can disable link previews in `/kuyo` → `Server settings`. The original author or a member with Manage Messages can delete the entire replacement, including text, links, and embeds, using the Delete message button. An older Hide preview button first updates to the new label and explains the change; pressing the new button deletes the message. Tracking and dismissal state remain until the applicable message/channel/server cleanup described above. Prefix a link with `!`, surround it with angle brackets, or use code/spoiler formatting to prevent automatic conversion.

For any other privacy request, contact the administrator who added Kuyo to your Discord server. Do not post personal information in a public issue or channel.

## Age requirements

Kuyo's character-reply feature is intended for adults. Server administrators should restrict access to suitable members and channels. Kuyo is not directed to children.

## Changes

This policy may be updated when Kuyo changes. The effective date at the top will be revised when material changes are made.
