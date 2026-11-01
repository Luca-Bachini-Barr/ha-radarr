# Radarr for Home Assistant (fork with upcoming releases)

A copy of Home Assistant core's `radarr` integration (2026.10.4) with one addition. It installs as a custom integration with the same `radarr` domain, so it overrides the built-in one and keeps existing entities.

## Added
`sensor.radarr_upcoming`: the number of movies with a cinema, digital or physical release in the next 92 days (about three months). Its `movies` attribute lists each movie, sorted by next release:

| Key | Meaning |
|---|---|
| `title`, `year` | Movie |
| `next_release`, `next_release_type` | Earliest release date in the window and its type (`cinema`, `digital`, `physical`) |
| `releases` | All release dates in the window: list of `{type, date}` |
| `has_file` | Already downloaded |
| `certification`, `runtime` | From Radarr |
| `poster`, `fanart` | Public TMDB image URLs (Radarr's own `/MediaCover` URLs need the API key) |

Data comes straight from Radarr's `/api/v3/calendar`, because aiopyarr's calendar model drops the image URLs. It refreshes hourly. Attributes are not recorded.

## Install / rollback
Install via HACS (custom repository, type Integration) or copy `custom_components/radarr` to `/config/custom_components/radarr` and restart. To go back to the built-in integration, delete that folder and restart.

Core fixes to Radarr don't reach this copy: re-copy core's files when updating Home Assistant if Radarr changes.
