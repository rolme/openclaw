# OpenClaw Vesicle Channel

Vesicle is an OpenClaw channel plugin for sending and receiving iMessage traffic through the Vesicle native macOS bridge.

## Install

From a local checkout:

```sh
openclaw plugins install -l ./extensions/vesicle
```

From a packed tarball:

```sh
openclaw plugins install ./openclaw-vesicle-2026.4.25.tgz
```

For a fast local install smoke from the OpenClaw checkout:

```sh
pnpm test:plugins:vesicle-install
```

Configure the channel under `channels.vesicle`:

```json5
{
  messages: {
    groupChat: {
      visibleReplies: "automatic",
    },
  },
  channels: {
    vesicle: {
      enabled: true,
      serverUrl: "http://127.0.0.1:1234",
      authToken: "vesicle-auth-token",
      webhookSecret: "shared-webhook-secret",
      dmPolicy: "allowlist",
      allowFrom: ["+15551234567"],
      groupPolicy: "allowlist",
      groupAllowFrom: ["any;+;messages-group-guid"],
    },
  },
}
```

The default webhook path is `/vesicle-webhook`.

Group chats follow OpenClaw's shared visible-reply policy. Set
`messages.groupChat.visibleReplies` to `"automatic"` when normal assistant replies
should be posted back into the iMessage group. Without that setting, OpenClaw still
processes group turns, but visible group output requires the message tool.
