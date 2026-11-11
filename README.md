# Telephony

The common telephony vocabulary -- calls and the recordings and transcriptions they leave, the voicemails people miss and the conferences that join many callers -- distilled from the APIs that already exist. Phone numbers belong to the messaging context, which owns them for voice and SMS alike. Part of [Schema Commons](https://github.com/api-commons/schema-commons),
published by the [API Commons](https://apicommons.org).

Built from the providers tagged Telephony, VoIP, Cloud Telephony, IVR, SIP, Calling, Voice, Business Phone in [APIs.io](https://apis.io) that
publish their own OpenAPI. Only harvested contracts count -- nothing API Evangelist
generated. Every number below is a count of providers.

## What the market already agrees on

<!-- commons:summary -->
| Concept | Expose it | Readable schema | Core properties (share) | Collection named |
| --- | ---: | ---: | --- | --- |
| call | 49 | 47 | status 72%, created_at 66%, id 66%, direction 57%, from 53% | calls 40, call 11, call-logs 2, call_logs 1 |
| recording | 21 | 14 | id 86%, created_at 71%, duration 71%, status 64% | recordings 12, recording 10, call-recordings 1 |
| transcription | 18 | 13 | id 62%, created_at 54%, status 54% | transcriptions 9, transcription 6, transcript 5, transcripts 2 |
| conference | 8 | 8 | id 75%, status 62%, created_at 50%, name 50% | conferences 6, conference 2 |

Cohort: 146 providers with harvested OpenAPI, 49 crosswalks. Of the providers exposing a call: 76% create, 86% list, 76% fetch, 18% update, 31% delete. Generated 2026-11-10 by build.py.
<!-- /commons:summary -->

Shares are of the providers with a readable resource schema for that concept. The
extended tier and the long tail of every concept are in [profile.yml](profile.yml).

## What the measurement shows

- A call agrees on status, direction, the caller and created_at across CPaaS platforms, business phone systems and voice-AI agents -- the call-detail record is shared.
- A recording agrees on id, duration, status and created_at; a conference on id, name, status and created_at.
- Transcriptions span call transcripts and general speech-to-text jobs: they agree only on id, status and created_at, because the transcript itself is text, utterances or segments.

## Artifacts

- [openapi.yml](openapi.yml) -- OpenAPI 3.1 of the shared operations. No one serves it; it
  is the shape to map to. Lints clean against the
  [naming ruleset](https://github.com/api-commons/schema-commons/blob/main/ruleset/schema-commons-naming.yaml).
- [schema/](schema) -- JSON Schema 2020-12 per concept; each property carries
  `x-commons-tier`, `x-commons-share`, `x-commons-providers` and the spellings seen.
- [crosswalk/](crosswalk) -- one per provider, common name -> their name, with the harvested
  spec and operations each mapping was read from.
- [adopters.yml](adopters.yml) -- who exposes which concept, linked to their APIs.io page.
- [concepts.yml](concepts.yml) -- the only hand-written input: concepts, path segments and
  their qualifiers, aliases, reviewed exclusions, merged duplicates, and the decisions below.
- [census/](census) -- the cohort and the raw census the profile is built from.

## Decisions

These are calls, not measurements, recorded so they can be revisited as the method matures.

- Phone numbers are the messaging context's: one number serves voice and SMS, and the concept is not duplicated.
- A call covers call logs, call records and CDRs.
- Voice is in the cohort, so voice-AI agents' calls count; every concept but the call `requires: [call]`.
- Voicemail was measured and dropped: the resources found were settings.
- Duplicates merged: OpenPhone into Quo, Wispr.

## Rebuild

```bash
../schema-commons/scripts/run.sh .
```

## License

Artifacts CC BY-NC-SA 4.0 ([LICENSE](LICENSE)); code Apache 2.0 ([LICENSE-CODE](LICENSE-CODE)).
