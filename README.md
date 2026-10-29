# Glim

**A location-based social discovery app that helps people meet in real life, at the same events, cafés and venues.**

Most social apps keep you on your phone. Glim works the other way round: you check in where you actually are, see who else is there, and connect in person. Profiles only become visible to people at the same place, at the same time.

> Built with React Native (Expo), TypeScript and Supabase. Android & iOS.

<!-- Add screenshots here: drag images into this README on GitHub, e.g.
<p>
  <img src="docs/home.png" width="230" /> <img src="docs/moments.png" width="230" /> <img src="docs/chat.png" width="230" />
</p>
-->

---

## Features

**Discover**
- Live events and places, with "this week" listings, search and saved favourites
- Location-verified check-in: you can only check in when you're actually there
- Anyone can browse events and places; only people who are there can see who's there

**Meet**
- **Who's here:** people checked in at the same place, visible only while you're both there
- **Glim** (like) someone; when it's mutual, a chat opens
- Invite your matches to an event with one tap

**Moments**
- Short photo and video stories from events and places, gone after 24 hours
- In-app camera: tap for a photo, hold to record, with live colour and "glow" filters
- Likes, threaded comments with replies, and a full-screen vertical feed

**Chat**
- Real-time messaging with reactions, replies, edit and unsend
- Voice notes, photos and videos (blurred until tapped), plus disappearing snaps
- Event invite cards and "Find each other" at the venue

**Safety & privacy**
- Automated image moderation before anything is shown
- Report and block everywhere, an 18+ age check and selfie verification
- Privacy controls: read receipts, hiding when you leave, who can invite you
- Media links are short-lived and signed; files are deleted when they expire or when people unmatch

---

## Tech stack

| Layer | Tools |
|---|---|
| App | React Native, Expo (SDK 57), Expo Router, TypeScript |
| State & data | TanStack Query, an offline outbox for messages and likes |
| UI & motion | Reanimated, Gesture Handler, VisionCamera, expo-video, expo-audio |
| Backend | Supabase: PostgreSQL + PostGIS, row-level security, RPC functions, Realtime |
| Server logic | Supabase Edge Functions (Deno): uploads, moderation, push notifications, cleanup |
| Storage | Supabase Storage or Cloudflare R2 (S3-compatible), signed URLs |
| Builds | EAS Build, Google Play Console |

## Architecture highlights

- **Security in the database.** Every table uses row-level security. Sensitive actions (likes, matches, comments, check-ins) go through server functions that enforce the rules, such as "only people at the same event can see each other".
- **Location done carefully.** Check-ins are verified with PostGIS distance checks on the server, not just in the app.
- **Media pipeline.** The app compresses photos and videos, uploads them straight to storage with a signed link, and a server function screens and publishes them. A scheduled job deletes expired files.
- **Works on bad networks.** Messages and likes queue offline and send automatically when the connection returns.
- **Tested rules.** 40+ SQL migrations, with database tests that check access and privacy rules (for example, that two likes at the same instant create exactly one match), plus app unit tests with Jest.

## Code

The source code is in a private repository. **I'm happy to give access, or walk through the code on a call, for hiring purposes.** Just get in touch.

## About

Designed and built by **Yonas Habte**. Development was AI-assisted (Claude); product direction, architecture decisions, testing and releases are my own.

**Contact:** yonashabte023@gmail.com
