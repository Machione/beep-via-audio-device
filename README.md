# Beep via Audio Device

Replicate the [Unix beep command](https://www.unix.com/man-page/linux/1/beep/), but use the audio output device instead of the builtin speaker. This allows devices that may not have a internal speaker (e.g. a Raspberry Pi) to play the beep tones via a connected speaker (e.g. through the 3.5mm jack) instead.

All the functionality of the original Unix beep is preserved meaning that this can be used as a drop-in replacement. Additionally, for help documentation, consult the original `man beep`.

## Installation

1. Ensure that [Python 3](https://www.python.org/downloads/) is installed.
2. Install [PyAudio](https://pypi.org/project/PyAudio/) and [NumPy](https://pypi.org/project/numpy/).
3. Clone this repository or download the [beep code](./beep). For the sake of these instructions, I assume that you've downloaded the code to ~/beep-via-audio-device/beep.
4. Add the location of the beep code to the beginning of your PATH environment variable. For the example location given above;
```bash
echo 'export PATH="~/beep-via-audio-device/beep:$PATH"' >> ~/.bashrc
source ~/.bashrc
```

## A note to Raspberry Pi users

Ensure that the audio device is enabled in the Raspberry Pi otherwise this will not work. In my case (running a model 4B), this means ensuring the command `modprobe snd_bcm2835` is executed every time the Pi reboots. Your mileage may vary. Do some googling for your specific Pi model.
