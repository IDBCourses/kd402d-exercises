# User input: a finished version

The instrument from the lecture with every step done, plus the black keys. Comments in `instrument.js` explain each part. This is also the version played at the start of the lecture.

Yours can look different and still be right: other notes, other keys, other names. What matters is that you can point at each `addEventListener` and say which function the browser calls and when, and at `noteFor` and say which note a key gives back.

Run it the same way as `user-input/start`: open `index.html` with Live Preview, open the console, click **Switch the sound on**, then click the page and play.

| Keys        | What they do                                     |
| ----------- | ------------------------------------------------ |
| `a` … `k`   | white keys, from C to the next C                 |
| `w e t y u` | black keys                                       |
| `z` / `x`   | one octave down / up                             |
| space       | switch between the clean sound and the buzzy one |

Don't change these files. Read them, copy from them, run them, but make your own changes in `user-input/start`.

## How it fits together

- **Three listeners, three jobs.** `changeSettings` and `startNote` both listen for `keydown`; `stopNote` listens for `keyup`. When a key goes down, the browser calls every function listening for `keydown`, in the order they were added.
- **One question, asked in one place.** `noteFor` is the only place that knows which key plays which note. To change the layout, you change `noteFor` and nothing else.
- **Remembering between presses.** `octave` and `isBuzzy` live outside the functions, so they keep their values from one key press to the next. Each press is a new call; the variables are what carry over.
- **Early `return`.** `startNote` stops straight away for repeated keydowns and for keys that aren't notes. Everything below the `return` only runs for a real, new note.
