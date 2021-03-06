miku.js
=======

JavaScript library for using NSX-39 with Web MIDI.

[DEMO](demo.html)

## How to use

```JavaScript
// get instance
Miku.init()
  .then(miku => {
    // set lyrics
    miku.lyrics('こ', 'ん', 'に', 'ち', 'わ');

    // play
    miku.noteOn(69, 127, 0);

    // stop
    miku.noteOff(69, 0, 0);
  });
```

## API

### Set lyrics

Send MIDI message to set lyrics.

```JavaScript
// Array of String
miku.lyrics(['あ', 'い', 'う', 'え', 'お']);

// Separated by space
miku.lyrics('あ い う え お');

// Separated by comma
miku.lyrics('こ,ん,に,ち,わ');

// unknown character is ignored
miku.lyrics('み t ddd く'); // Same as miku.lyrics('み く')
```

### Play note

```JavaScript
let noteNumber = 60;
let velocity   = 64;

miku.noteOn(noteNumber, velocity, 0);

...
// Some seconds after

miku.noteOff(noteNumber, velocity, 0);
```

### Send other MIDI message

```JavaScript
// bend value is 0 to 16384. Default value is 8192.
miku.pitchBend(4096);

// Modulation
miku.controlChange(1, 127);
```

### Event listening

These events are also emitted from MIDI Input.

```JavaScript
miku.on('noteOn', (noteNum, velocity) => {
  console.log('Note on', noteNum, velocity);
});

miku.on('noteOff', (noteNum, velocity) => {
  console.log('Note off', noteNum, velocity);
});

miku.on('pitchBend', (value) => {
  console.log('Pitch bend', value);
});

miku.on('sysEx', (dataArray) => {
  console.log('sys ex', dataArray);
});
```
