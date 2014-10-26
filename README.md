Music JSON (proposal)

A proposal for a standard way of creating music sequence data in JSON

## Background

This document aims to describe a way to describe musical information in JSON.
The JSON should be minimal, easy to extract information from, easily readable by
software, and easy to convert to other formats such as MIDI or OSC. It is bourne
out of a need to standardise a way of exchanging music between emerging apps and
web apps, and was discussed at Mozilla Festival London 2014.

This spec is intended as a discussion starter. Please comment, propose ideas and
make pull requests.

## Example document

    {
        "author": "author"

        "settings": {},

        "sequence": [
            [2,   0.5, "note", 76, 0.8],
            [2.5, 0.5, "note", 77, 0.6],
            [3,   0.5, "note", 79, 1],
            [3.5, 3.5, "note", 74, 1],
            [10,  0.5, "note", 76, 1],

            [0,   4,   "chord", "C∆"],
            [4,   4,   "chord", "G-"]
        ]
    }



## Sequence

A sequence is simply an array of events.

    [event1, event2, ... ]

## Event

An event is an array describing the timing, duration and type of a event.

    [time, duration, type, data ...]

An event has a start time, a duration and a type. An event also contains extra
data that is dependent on the type.

#### time

<code>time</code> is a float describing a point in time from the time from the
sequence start time (which is <code>0</code>).

<code>time</code> values are arbitrary. The actual tiem an event is played is
dependent upon the <code>time</code> value of the event AND the rate at which
the sequence is played. <code>time</code> values do not directly describe
seconds or beats – although they could if the sequence were played back at the
correct rate.

#### duration

<code>duration</code> is the length of time the event is to be played for. As
with <code>time</code>, the resulting duration of an event depends on the speed
the sequence is played at.

#### type

<code>type</code> describes the type of event. Possible values are:

- <code>"note"</code> A musical note. A note event has the data values <code>note number</code> and <code>note velocity</code>:

    [time, duration, "note", number, velocity]

- <code>"chord"</code> A musical symbol describing the current key centre and
mode of the music, represented as a string.

    [time, duration, "chord", symbol]

- <code>"sequence"</code> A sequence event carries the data for a sequence array, enabling the playback of nested sequences.

    [time, duration, "sequence", array]


## Implementations

- <a href="http://labs.cruncher.ch/scribe/">Scribe</a> is a music notation
interpreter and renderer that consumes Music JSON.

## References

- OSC spec: <a href="http://opensoundcontrol.org/spec-1_0">http://opensoundcontrol.org/spec-1_0</a>
- OSC example messages: <a href="http://opensoundcontrol.org/files/OSC-Demo.pdf">http://opensoundcontrol.org/files/OSC-Demo.pdf</a>
- Music XML: <a href="http://www.musicxml.com/for-developers/">http://www.musicxml.com/for-developers/</a>
- VexFlow: <a href="http://www.vexflow.com/">http://www.vexflow.com/</a>

