# gpui-pre-windows

crates.io's `gpui-pre-windows` 0.3.8, Zed's `gpui_windows` at `279fe07`, with four changes for ELYTerminal, which takes it through `[patch.crates-io]`.

DirectWrite shapes a fallback run with a face of its own choosing. gpui rebuilt that face from its family, weight and style and looked it up again, and the lookup can return another face: for Maple Mono NF CN's italic, its Regular file with an oblique simulation. The Italic file's glyph ids then drew from the Regular file, so CJK text in italic showed other characters (ELYTerminal issue #30). A fallback run now draws with the face DirectWrite served, which the text system keeps.

gpui's `ClipboardItem` holds text, an image and files together, and the clipboard wrote the text and the image but never the files. kitty's clipboard protocol, OSC 5522, writes all three. Files now go as `CF_HDROP`, a `DROPFILES` header and wide names, as Explorer copies them.

Mica and Mica Alt set DWM's system backdrop beside the acrylic accent gpui left in place, and the accents left the backdrop, so a switch kept the last effect (ELYTerminal issue #38). Mica now clears the accent, and every accent sets the backdrop back to none. The backdrop draws behind the clear client area as it is: extending the frame there would make DWM draw its own caption buttons behind a window's own.

Windows sends a move when a window repaints under a still pointer, and gpui showed the pointer it had hidden for typing at every move, so the pointer blinked at each key (ELYTerminal issue #67). A move with no button at the last client point, in device pixels, now passes by before the pointer comes back, logged at trace; the point clears on leave and on a non-client move.

Remove this fork once a gpui-pre release draws a fallback run with its served face, writes files to the clipboard, keeps the pointer hidden through a move that moved nothing, and switches between Mica and the accents cleanly without extending the frame.
