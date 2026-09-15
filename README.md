# BARCODE storage probe

A single static page that measures whether a browser keeps IndexedDB data, and
for how long.

It exists to answer one question for a private project: Apple caps script-writable
storage — IndexedDB included — at seven days of Safari use without interaction
with the site. An app that keeps the user's only copy in IndexedDB therefore needs
to know what actually happens, on a real phone, rather than what the 2020
write-ups say.

**What it does**

- Reports `navigator.storage.persisted()`, `estimate()` and whether it is running
  as a home-screen app or a browser tab.
- Writes ~400 small records to IndexedDB, plus a dated marker, on request.
- On every later visit, says whether those records are still there and how long
  it has been.

**Why it is its own repository.** Browser storage is partitioned by origin, so a
multi-day test needs a hostname that does not change. An ephemeral tunnel gets a
new one every restart, which voids the test.

It collects nothing and sends nothing anywhere. Everything stays in the browser
it runs in.
