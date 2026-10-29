---
title: "CLI Overview"
weight: 1
menu:
  cli:
    title: "Overview"
    parent: "getting_started"
    weight: 1
---

The Vector Charts CLI (`vc`) is a native binary for managing Cloud and OEM instances from the terminal: connection profiles, interactive login, API tokens, chart uploads, custom cells, and job status.

The same binary works for both Cloud and OEM.

## Install

### Convenience script

<pre>
curl -fsSL https://raw.githubusercontent.com/vector-charts/vector-charts-cli/main/scripts/install.sh | bash
</pre>

### Debian / Ubuntu

Download the `.deb` from [GitHub Releases](https://github.com/vector-charts/vector-charts-cli/releases) and install:

<pre>
sudo dpkg -i vc_*.deb
</pre>

### Nix

<pre>
nix profile install github:vector-charts/vector-charts-cli
# or
nix run github:vector-charts/vector-charts-cli -- version
</pre>

Unfree packages must be allowed (`NIXPKGS_ALLOW_UNFREE=1` with `--impure`, or set `allowUnfree` in your Nix config).

### From source

<pre>
go build -o vc ./cmd/vc
sudo install -m 755 vc /usr/local/bin/vc
</pre>

## Quick start

Profiles only need a portal URL. After login, the CLI reads `account.planInstance` from whoami to choose Cloud vs OEM and the tile API host (OEM uses the same origin).

<pre>
vc server add https://cloud.vectorcharts.com
vc server add local-oem http://localhost:9909

vc server login
</pre>

If `--profile` is omitted, the sole profile is used when only one exists; otherwise `current_profile`, otherwise `default`. URL may be positional on `vc server add`.

`vc server login` opens a browser device flow and mints or reuses a **Personal Token** bound to this machine. Alternatives:

<pre>
vc server login --token &lt;personal-token-id&gt;
vc server login --username you@example.com
</pre>

Discover OEM (or other) instances on the LAN via UDP multicast:

<pre>
vc server discover
</pre>

Check connectivity and identity:

<pre>
vc server list
vc server whoami
vc server status
</pre>

## Configuration

Config lives under `~/.vector-charts/` (override with `VECTOR_CHARTS_HOME`):

- `config.yml` — named profiles (`url`; `type` / `api_url` filled after login)
- `credentials.yml` — cached Personal Token / machine id (file mode `0600`)

Manage or revoke CLI devices in the portal under **Personal Tokens**. App **API Tokens** (Tokens tab) remain for integrations and are managed with `vc token`.

## Command groups

| Group | Purpose |
|-------|---------|
| `vc server` | Profiles, login/logout, discovery, connectivity |
| `vc token` | Portal API token CRUD (`list`, `create`, `update`, `delete`, `use`) |
| `vc charts` | Upload charts, manage uploads/cells, fetch S-63 permit |
| `vc jobs` | List jobs and status snapshot |

### Server

<pre>
vc server add [name] &lt;portal-url&gt;
vc server use &lt;name&gt;
vc server login
vc server logout
vc server list
vc server show
vc server status
vc server whoami
vc server discover
vc server remove &lt;name&gt;
</pre>

### Tokens

<pre>
vc token list
vc token create --name "automation"
vc token update &lt;token-id&gt; --name "renamed"
vc token use &lt;token-id&gt;
vc token delete &lt;token-id&gt;
</pre>

### Charts

<pre>
vc charts upload ./ENC_ROOT.zip
vc charts uploads list
vc charts uploads get &lt;id&gt;
vc charts uploads delete &lt;id&gt;
vc charts cells list
vc charts cells enable &lt;id&gt;
vc charts cells disable &lt;id&gt;
vc charts permit
</pre>

### Jobs

<pre>
vc jobs list
vc jobs status
</pre>

## Global flags

| Flag | Description |
|------|-------------|
| `--profile` | Profile name (default: sole profile, current profile, or `default`) |
| `-o table\|json` | Output format |
| `--url` | Override portal URL for this invocation |

## Connecting to OEM

OEM serves portal and tile APIs on one origin (default port `9909`). Add a profile with that URL only — type and API host are inferred after login:

<pre>
vc server add oem http://localhost:9909
vc server login
</pre>

`vc server list` probes portal health, API health (`mode: oem`), and authentication. LAN discovery (`vc server discover`) usually needs host networking when the OEM instance runs in a container.
