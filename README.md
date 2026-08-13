# MIDI to header file in c

This program parses lighting contorl information encoded in a MIDI file and converts it into a
C header file for later use by the MCU.

## Usage

Run the program with:

```bash
gcc main.c new_midi2array.c -o convertMIDI
./convertMIDI (YOUR_MIDI_FILE)
```

## NOTES

The input MIDI file must follow the convensions below.

1. Only 6 notes are used for lighting control: E4, G4, B4, D5, F5, and A5.
2. For E4 through F5, comments are used to specify the corresponding part and its RGB color. Each comment follows this format: `X:RRGGBB`,
where `X` represents the lighting part (`A` for E4 through `E` for F5), and `RRGGBB` is a six-digit hexadecimal RGB value.
3. A5 corresponds to part F, which supports additional lighting effects. Its comment follows this format:
`F:RRGGBBS`, where `S` is a single-digit special-effect index.

## Input and Output Representation

The duration of each MIDI note determines how long the corresponding WS2812 lighting event remains active.
For parts A through E, each event contains:

- timestamp
- RGB color

Part F additionally contains:

- special-effect index
- special-effect duration

The generated data follows the structures defined in structure_of_ws2812.h and can be included directly
in the MCU firmware.

## Credits

The initial project structure was inherited from code developed by previous members of the engineering
team. The MIDI parsing, lighting-effect processing, and related extensions in this version were
developedas part of the continued development of the project.
