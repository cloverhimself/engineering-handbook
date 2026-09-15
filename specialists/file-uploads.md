# File Uploads and Media

Treat uploaded files as untrusted input.

Define allowed file types, maximum sizes, ownership rules, retention, visibility, malware/content scanning requirements where appropriate, and deletion behavior before implementation.

Do not trust client-provided MIME type or filename alone. Generate storage keys/filenames server-side. Keep executable user content away from application execution paths.

Prefer object storage or a managed media service for production user uploads rather than the application server filesystem.

Store file metadata separately from the binary object when useful: owner, storage key, original name, content type, size, checksum, visibility, timestamps.

Use signed or controlled access for private media. Never expose private storage credentials to clients.

Delete/replace flows must handle orphaned objects and database records deliberately. Large media processing should happen asynchronously when appropriate.
