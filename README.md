# Nimply - Make (Integromat) App

Make apps are authored in Make's web-based **Custom Apps builder** (they are not deployable from a repo). This directory holds the JSON definitions to paste into the builder, so the app is version-controlled here and reproducible.

## Setup order

1. **Register the OAuth client** (once per Make zone). Make's OAuth redirect URL is
   `https://www.integromat.com/oauth/cb/app` (shown in the builder under the connection).
   ```bash
   curl -X POST https://api.nimply.io/oauth/register \
     -H "Content-Type: application/json" \
     -d '{"client_name":"Make","redirect_uris":["https://www.integromat.com/oauth/cb/app"]}'
   ```
   Save the returned `client_id`.
2. In Make: **Custom apps → Create a new app** — name `Nimply`, theme color `#F0530F`.
3. Paste each JSON file from this directory into the matching builder tab (Base, Connection, Modules).
4. In the connection's **Common data**, set `clientId` to the value from step 1.
5. Test each module against a real workspace, then request app review/publication from the builder.

## Files

| File | Builder location |
|---|---|
| `base.json` | App → Base |
| `connection.oauth2.json` | Connections → nimply-oauth (type: OAuth 2 authorization code) |
| `rpc.list-channels.json` | Remote Procedures → listChannelsRpc (powers the channel dropdown — create BEFORE the modules) |
| `rpc.platform-channels.json` | Remote Procedures → listYouTubeChannelsRpc / listTikTokChannelsRpc / listPinterestChannelsRpc / listLinkedInChannelsRpc (one file, four RPCs — register each separately, BEFORE the platform modules) |
| `rpc.pinterest-boards.json` | Remote Procedures → listPinterestBoardsRpc (board dropdown; reads the module's `channelId` parameter) |
| `rpc.tiktok-privacy-levels.json` | Remote Procedures → listTikTokPrivacyLevelsRpc (privacy dropdown; reads the module's `channelId` parameter) |
| `module.create-post.json` | Modules → Create a Post (action) |
| `module.create-youtube-video.json` | Modules → Create a YouTube Video (action) |
| `module.create-tiktok-post.json` | Modules → Create a TikTok Post (action) |
| `module.create-pinterest-pin.json` | Modules → Create a Pinterest Pin (action) |
| `module.create-linkedin-post.json` | Modules → Create a LinkedIn Post (action) |
| `module.update-post.json` | Modules → Update a Post (action) |
| `module.schedule-post.json` | Modules → Schedule a Post (action) |
| `module.unschedule-post.json` | Modules → Unschedule a Post (action) |
| `module.upload-media.json` | Modules → Upload Media from URL (action) |
| `module.upload-media-binary.json` | Modules → Upload Media (Binary) (action) — 3-request presigned chain; test after import, the binary PUT (request 2, `type: "binary"`) is the part most sensitive to builder-version quirks |
| `module.list-channels.json` | Modules → List Channels (search) |
| `module.watch-events.json` | Modules → Watch Events (instant trigger / webhook) |
| `webhook.events.json` | Webhooks → nimply-events (paired with Watch Events) |
| `APP_README.md` | App → Readme tab (user-facing, GitHub-Flavored Markdown) |

## Notes

- The connection uses **PKCE** (`code_challenge`/`code_verifier`) as required by Nimply's OAuth 2.1 server; Make's OAuth2 connection supports this via the `oauth2CodeChallenge` / IML `codeChallenge` helpers configured in `connection.oauth2.json`.
- The **Watch Events** trigger registers a Nimply webhook (`POST /v1/webhooks`) on attach and deletes it on detach; the event payload envelope is `{id, type, createdAt, workspaceId, data}` and the module outputs `data` merged with `type`/`createdAt`.
- Scopes requested: all (workspace/channels/posts/media/analytics read+write, webhooks:manage) — Make users pick one connection for all modules.
