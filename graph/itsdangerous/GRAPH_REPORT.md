# Graph Report - external_projects\itsdangerous\src\itsdangerous  (2026-06-23)

## Corpus Check
- cluster-only mode — file stats not available

## Summary
- 135 nodes · 334 edges · 7 communities (6 shown, 1 thin omitted)
- Extraction: 89% EXTRACTED · 11% INFERRED · 0% AMBIGUOUS · INFERRED: 38 edges (avg confidence: 0.57)
- Token cost: 0 input · 0 output

## Graph Freshness
- Built from commit: `ab19ed17`
- Run `git rev-parse HEAD` and compare to check if the graph is stale.
- Run `graphify update .` after code changes (no API cost).

## Community Hubs (Navigation)
- [[_COMMUNITY_Community 0|Community 0]]
- [[_COMMUNITY_Community 1|Community 1]]
- [[_COMMUNITY_Community 2|Community 2]]
- [[_COMMUNITY_Community 3|Community 3]]
- [[_COMMUNITY_Community 4|Community 4]]
- [[_COMMUNITY_Community 5|Community 5]]
- [[_COMMUNITY_Community 6|Community 6]]

## God Nodes (most connected - your core abstractions)
1. `Serializer` - 26 edges
2. `want_bytes()` - 21 edges
3. `Signer` - 21 edges
4. `BadSignature` - 19 edges
5. `TimedSerializer` - 15 edges
6. `BadPayload` - 14 edges
7. `TimestampSigner` - 14 edges
8. `base64_decode()` - 11 edges
9. `base64_encode()` - 10 edges
10. `BadData` - 10 edges

## Surprising Connections (you probably didn't know these)
- `_PDataSerializer` --uses--> `BadSignature`  [INFERRED]
  serializer.py → exc.py
- `Serializer` --uses--> `BadSignature`  [INFERRED]
  serializer.py → exc.py
- `HMACAlgorithm` --uses--> `BadSignature`  [INFERRED]
  signer.py → exc.py
- `NoneAlgorithm` --uses--> `BadSignature`  [INFERRED]
  signer.py → exc.py
- `Signer` --uses--> `BadSignature`  [INFERRED]
  signer.py → exc.py

## Import Cycles
- None detected.

## Communities (7 total, 1 thin omitted)

### Community 0 - "Community 0"
Cohesion: 0.12
Nodes (16): Any, IO, is_text_serializer(), _PDataSerializer, Loads the encoded object. This function raises         :class:`.BadPayload` if, Dumps the encoded object. The return value is always bytes.         If the inte, Returns a signed string serialized with the internal         serializer. The re, Like :meth:`dumps` but dumps into a file. The file handle has         to be com (+8 more)

### Community 1 - "Community 1"
Cohesion: 0.16
Nodes (16): base64_decode(), bytes_to_int(), int_to_bytes(), Base64 decode a URL-safe string of bytes or text. The result is     bytes., BadData, BadHeader, BadSignature, BadTimeSignature (+8 more)

### Community 2 - "Community 2"
Cohesion: 0.12
Nodes (14): base64_encode(), Base64 encode a string of bytes or text. The resulting bytes are     safe to us, want_bytes(), Creates a new instance of the signer to be used. The default         implementa, Iterates over all signers to be tried for unsigning. Starts         with the co, The newest (last) entry in the :attr:`secret_keys` list. This         is for co, This method is called to derive the key. The default key         derivation cho, Returns the signature for the given value. (+6 more)

### Community 3 - "Community 3"
Cohesion: 0.18
Nodes (14): BadPayload, Raised if a payload is invalid. This could happen if the payload     is loaded, The newest (last) entry in the :attr:`secret_keys` list. This         is for co, A serializer wraps a :class:`~itsdangerous.signer.Signer` to     enable seriali, Serializer, Uses :class:`TimestampSigner` instead of the default     :class:`.Signer`., Reverse of :meth:`dumps`, raises :exc:`.BadSignature` if the         signature, TimedSerializer (+6 more)

### Community 4 - "Community 4"
Cohesion: 0.14
Nodes (11): HMACAlgorithm, _lazy_sha1(), _make_keys_list(), NoneAlgorithm, Subclasses must implement :meth:`get_signature` to provide     signature genera, Returns the signature for the given key and value., Verifies the given signature matches the expected         signature., Provides an algorithm that does not perform any signing and     returns an empt (+3 more)

### Community 5 - "Community 5"
Cohesion: 0.22
Nodes (8): datetime, Only validates the given signed value. Returns ``True`` if         the signatur, Works like the regular :class:`.Signer` but also records the time     of the si, Returns the current timestamp. The function must return an         integer., Convert the timestamp from :meth:`get_timestamp` into an         aware :class`d, Signs the given string and also attaches time information., Works like the regular :meth:`.Signer.unsign` but can also         validate the, TimestampSigner

## Knowledge Gaps
- **1 thin communities (<3 nodes) omitted from report** — run `graphify query` to explore isolated nodes.

## Suggested Questions
_Questions this graph is uniquely positioned to answer:_

- **Why does `Serializer` connect `Community 3` to `Community 0`, `Community 1`, `Community 2`, `Community 5`?**
  _High betweenness centrality (0.215) - this node is a cross-community bridge._
- **Why does `Signer` connect `Community 2` to `Community 0`, `Community 1`, `Community 3`, `Community 4`, `Community 5`?**
  _High betweenness centrality (0.156) - this node is a cross-community bridge._
- **Why does `BadSignature` connect `Community 1` to `Community 0`, `Community 2`, `Community 3`, `Community 4`, `Community 5`?**
  _High betweenness centrality (0.123) - this node is a cross-community bridge._
- **Are the 8 inferred relationships involving `Serializer` (e.g. with `BadPayload` and `BadSignature`) actually correct?**
  _`Serializer` has 8 INFERRED edges - model-reasoned connections that need verification._
- **Are the 6 inferred relationships involving `want_bytes()` (e.g. with `.derive_key()` and `.get_signature()`) actually correct?**
  _`want_bytes()` has 6 INFERRED edges - model-reasoned connections that need verification._
- **Are the 5 inferred relationships involving `Signer` (e.g. with `_PDataSerializer` and `Serializer`) actually correct?**
  _`Signer` has 5 INFERRED edges - model-reasoned connections that need verification._
- **Are the 9 inferred relationships involving `BadSignature` (e.g. with `_PDataSerializer` and `Serializer`) actually correct?**
  _`BadSignature` has 9 INFERRED edges - model-reasoned connections that need verification._