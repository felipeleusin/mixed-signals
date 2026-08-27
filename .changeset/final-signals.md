---
'mixed-signals': minor
---

Add `rpc.markFinal(...signals)` to promise clients a signal will never change
again. Final signals serialize as `{"@S": id, "v": value, "f": 1}`: the client
still gets a `Signal`, but observing it sends no `@W` and the server never
subscribes to it. A signal that becomes final while clients watch it is
announced with a debounced `N:@S:id,null,0` seal update, which forwarding
relays. Signal update modes are now numeric: seal `0`, append `1`, merge `2`,
and splice `3`.
