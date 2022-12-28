#!/usr/bin/env python3
import sys
import time
import pyaudio
import numpy as np


def seperate_beep_data(raw_data):
    all_beep_data = []
    this_beep_data = []
    for arg in raw_data:
        if arg == "-n":
            all_beep_data.append(this_beep_data)
            this_beep_data = []
        else:
            this_beep_data.append(arg)

    all_beep_data.append(this_beep_data)
    return all_beep_data


def build_beep(args):
    beep_args = {
        "f": 440,
        "l": 200,
        "r": 1,
        "d": 100,
        "D": None
    }

    for i in range(0, len(args), 2):
        arg = args[i].replace("-", "")
        value = int(args[i+1])
        beep_args[arg] = value

    return beep_args


def beep(f=400, l=200, r=1, d=100, D=None, **kwargs):
    samples = (np.sin(2*np.pi*np.arange(rate*(l/1000))*f/rate)).astype(np.float32).tobytes()

    if D is not None:
        d = D
    else:
        D = 0

    first_beep = True
    for _ in range(r):
        if first_beep == False:
            time.sleep(d/1000)
        else:
            first_beep = False

        s.write(samples)

    time.sleep(D/1000)
    return


if __name__ == "__main__":
    p = pyaudio.PyAudio()
    rate = 48000
    s = p.open(format=pyaudio.paFloat32, channels=1, rate=rate, output=True)

    if len(sys.argv) == 1:
        beep()
        exit(0)

    all_beep_data = seperate_beep_data(sys.argv[1:])
    all_beep_args = [build_beep(data) for data in all_beep_data]
    for beep_args in all_beep_args:
        beep(**beep_args)

    s.stop_stream()
    s.close()
    p.terminate()
