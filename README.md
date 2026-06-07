# Jumpseat ACARS Drama API

A small API for exploring ACARS Drama data in personal dashboards, notebooks, home lab projects, and experiments.

> **Tip:** Keep archive windows narrow and use pagination or limits where possible.

## Base URL

```text
https://api.jumpseat.acarsdrama.com
```

## Available Endpoints

| Method | Endpoint                       | Description                                                     |
| ------ | ------------------------------ | --------------------------------------------------------------- |
| `GET`  | `/v1/messages/search`          | Search messages using the same filters as Message Search.       |
| `GET`  | `/v1/flight-playback/options`  | List available flight and registration combinations for a date. |
| `GET`  | `/v1/flight-playback/messages` | Replay messages for a selected flight / registration combo.     |
| `GET`  | `/v1/stations/report`          | Generate station reports using redacted Station Identifiers.    |
| `GET`  | `/v1/insights`                 | Recover ACARS Drama insight posts.                              |

## Example Requests

### Search Recent Messages

Search recent messages containing a keyword.

```text
GET /v1/messages/search?source=messages&q=smell&limit=10
```

Example:

```text
https://api.jumpseat.acarsdrama.com/v1/messages/search?source=messages&q=smell&limit=10
```

### Search Archive by Category

Search archived messages by category within a narrow time window.

```text
GET /v1/messages/search?source=messages_archive&category=medical&from=2026-06-01T00:00:00&to=2026-06-02T00:00:00&limit=25
```

Example:

```text
https://api.jumpseat.acarsdrama.com/v1/messages/search?source=messages_archive&category=medical&from=2026-06-01T00:00:00&to=2026-06-02T00:00:00&limit=25
```

### List Flight Playback Options

List available flight / registration combinations for a given date.

```text
GET /v1/flight-playback/options?date=2026-06-01&q=UA
```

Example:

```text
https://api.jumpseat.acarsdrama.com/v1/flight-playback/options?date=2026-06-01&q=UA
```

### Replay Selected Flight Playback Combo

Replay ACARS messages for a selected flight playback combination.

```text
GET /v1/flight-playback/messages?date=2026-06-01&comboKey=UA123%7CN123AB
```

Example:

```text
https://api.jumpseat.acarsdrama.com/v1/flight-playback/messages?date=2026-06-01&comboKey=UA123%7CN123AB
```

> The `comboKey` value should be URL-encoded. For example, `UA123|N123AB` becomes `UA123%7CN123AB`.

### Build a Station Report

Generate a station report from one or more redacted Station Identifiers.

```text
GET /v1/stations/report?stations=%23sabc123,%23sdef456&source=all&from=2026-06-01T00:00:00&to=2026-06-02T00:00:00
```

Example:

```text
https://api.jumpseat.acarsdrama.com/v1/stations/report?stations=%23sabc123,%23sdef456&source=all&from=2026-06-01T00:00:00&to=2026-06-02T00:00:00
```

> Station identifiers should be URL-encoded. For example, `#sabc123` becomes `%23sabc123`.

### Fetch ACARS Drama Insights

Fetch recent ACARS Drama insight posts.

```text
GET /v1/insights?limit=10
```

Example:

```text
https://api.jumpseat.acarsdrama.com/v1/insights?limit=10
```

## Query Parameters

Common parameters vary by endpoint, but may include:

| Parameter  | Description                                                             |
| ---------- | ----------------------------------------------------------------------- |
| `source`   | Data source to query, such as `messages`, `messages_archive`, or `all`. |
| `q`        | Search keyword, flight prefix, or filter text.                          |
| `category` | Message category filter, such as `medical`.                             |
| `from`     | Start timestamp for archive/report windows.                             |
| `to`       | End timestamp for archive/report windows.                               |
| `limit`    | Maximum number of results to return.                                    |
| `date`     | Date used for flight playback options or replay.                        |
| `comboKey` | Selected flight / registration combo key.                               |
| `stations` | Comma-separated list of redacted Station Identifiers.                   |

## Usage Notes

* Keep archive windows narrow for faster, more reliable queries.
* Use `limit` when exploring large result sets.
* Paginate where supported.
* URL-encode special characters in query parameters, especially `#`, `|`, and commas when necessary.
* This API is intended for personal dashboards, notebooks, home lab projects, and experiments.
