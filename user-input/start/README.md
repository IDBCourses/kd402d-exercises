# User input

This morning's programs stop waiting for us. Until now, every program ran from top to bottom and stopped. Today the program waits for you to press a key, and answers the moment you do: your computer keyboard becomes an instrument.

We build `instrument.js` together in the lecture, one step at a time. The steps in the file match the slides. If you fall behind, or want to see where we're heading, `user-input/reference/instrument.js` is the finished version.

## Run it

1. Sync your fork and pull (see the main README), so this `user-input/` folder is on your laptop.
2. Open `user-input/start/index.html`, then run **Live Preview: Show Preview (External Browser)** from the Command Palette (`Ctrl+Shift+P` / `Cmd+Shift+P`).
3. Open the browser's developer tools (`F12`, or `Cmd+Option+I` on a Mac) and click the **Console** tab.
4. Click **Switch the sound on**. Then click anywhere on the page, so the page has the keyboard, and press keys.

The instruments are made in `setup.js`; you don't need to change it. When you save, the page reloads on its own; click **Switch the sound on** again after each reload.

## The steps

After each step: save, press keys, check the console, and commit.

| Step | What you do                                                     | A commit message could be           |
| ---- | --------------------------------------------------------------- | ----------------------------------- |
| 1    | Listen for `keydown` and log `event.key`                        | `Log every key press`               |
| 2    | Play a note when `a` goes down, and another for `s`             | `Play a note on a key press`        |
| 3    | Write `noteFor(key)`, and play the note it gives back           | `Look up the note for each key`     |
| 4    | Start the note on `keydown`, stop it on `keyup`, skip repeats   | `Hold and release notes`            |
| 5    | `z` and `x` change the octave, space switches the sound          | `Change octave and sound with keys` |
| 6    | Make it your own                                                | your choice                         |

## Make it your own

Some ideas:

- Add the black keys: `w e t y u` play `C#` `D#` `F#` `G#` `A#`.
- Map the keys by letter instead: `c` plays C, `d` plays D … `b` plays B. Which is easier to play? Which is easier to remember?
- Only the notes C, D, E, G and A (a pentatonic scale): nothing you play sounds wrong.
- A different sound: change a `new Tone.PolySynth()` in `setup.js` to `new Tone.PolySynth(Tone.FMSynth)`. (This is the one time you may change `setup.js`.)
- A key that changes how long every note is, or how loud.

## If something goes wrong

- **Nothing happens when you press keys, and there's no error:** check the spelling of the event name. It's `"keydown"`, all lowercase. `"keyDown"` isn't an error: the browser waits for an event called that, and it never comes.
- **One note plays when the page loads, then nothing:** there are brackets after the function name in `addEventListener("keydown", playNote())`. That calls `playNote` straight away and hands over what it gives back. Take the brackets off: `addEventListener("keydown", playNote)`.
- **Key presses show up in the console instead of the page:** the console has the keyboard. Click on the page itself first.
- **No sound, but the console logs the key:** click **Switch the sound on** again (every reload switches it off), and check the volume and your headphones.
- **`TypeError: Cannot read properties of undefined (reading 'key')`:** the function has no `event` parameter, or you called it yourself. Write `function startNote(event)`, and let the browser call it.
- **A note keeps playing after you let go:** the `keyup` listener is missing, or `stopNote` asks `noteFor` for a different note than `startNote` did. Did the octave change while the key was down? Press the key again to release it.
- **A held note stutters:** the `if (event.repeat)` check is missing at the top of `startNote`.
- **`SyntaxError: Identifier 'synth' has already been declared`:** `synth` is made in `setup.js`. Don't make it again in `instrument.js`.
- **`noteFor` always gives back `""`:** log `key` at the top of `noteFor`. Is it the key you expected? Capitals count: with Shift or Caps Lock on, `a` is `"A"`.
