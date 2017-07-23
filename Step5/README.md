# Demo


```
BUNDLE_PATH=<absolute path of .mag file>
CONFIG=<one of 'basic_rnn', 'lookback_rnn', or 'attention_rnn', matching the bundle>

melody_rnn_generate \
--config=${CONFIG} \
--bundle_file=${BUNDLE_PATH} \
--output_dir=/tmp/melody_rnn/generated \
--num_outputs=10 \
--num_steps=128 \
--primer_melody="[60]"
```

This will generate a melody starting with a middle C. If you'd like, you can also supply
a priming melody using a string representation of a Python list. The values in the list
should be ints that follow the melodies_lib.Melody format (-2 = no event, -1 = note-off
event, values 0 through 127 = note-on event for that MIDI pitch). For example
--primer_melody="[60, -2, 60, -2, 67, -2, 67, -2]" would prime the model with the first
four notes of Twinkle Twinkle Little Star. Instead of using --primer_melody, we can use
--primer_midi to prime our model with a melody stored in a MIDI file. For example,
--primer_midi=<absolute path to magenta/models/melody_rnn/primer.mid> will prime the
model with the melody in that MIDI file.


