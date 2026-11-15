ESP8266 Sound Visualizer
A compact real-time audio visualizer built on the ESP8266 (D1 Mini) and a Nokia 5510 LCD (84×48 monochrome, PCD8544). An MAX9814 electret microphone captures ambient sound, and the analog envelope is rendered as 8 animated bars with peak-hold dots and a sound-triggered LED — all in a pocket-sized form factor.

Features
8 independent bars driven by a single analog mic input, with per-bar scaling for a spectrum-analyzer look

Fast-attack / slow-decay envelope follower for natural bar movement

Peak-hold dots with adjustable hold time and fall rate

LED on D0 that lights up when sound exceeds a tunable threshold (with hold timer to avoid flicker)

Runs smoothly at ~30 FPS on a 4 MHz SPI bus

No FFT required — low CPU load, leaves headroom for WiFi and other tasks

Hardware
Component	Connection
Nokia 5510 LCD RST	D2
LCD CE/CS	D1
LCD DC	D6
LCD DIN/MOSI	D7
LCD CLK/SCK	D5
LCD VCC / BL	3.3V (BL via 330Ω)
LCD GND	GND
MAX9814 OUT	A0
MAX9814 VCC / GND	3.3V / GND
LED anode	D0 via 220Ω
LED cathode	GND
Software
Libraries: Adafruit_PCD8544, Adafruit_GFX

Tuning parameters: MAP_MAX_RAW (sensitivity), NOISE_FLOOR (silence cutoff), LED_THRESHOLD (LED trigger), DECAY_RATE / PEAK_DECAY_RATE (bar fall speed)

How it works
The MAX9814 outputs an analog envelope of the ambient audio. The ESP8266 samples it on A0, subtracts a noise floor, and maps the value to bar heights through a set of per-bar multipliers — giving the illusion of independent frequency bands without the cost of an FFT. Each bar uses a fast-attack/slow-decay follower plus a peak-hold dot for a classic VU-meter feel. A threshold on the raw signal drives an LED, with a short hold timer so it pulses cleanly on beats instead of flickering.

Possible extensions
Combine with a weather display and switch modes with a button

Add real FFT bars (I2S mic + arduinoFFT)

Segmented bar rendering for a true LED VU-meter look

Center-mirror mode to double perceived resolution

Status
✅ Working — bars animate with music, peak dots hold and fall correctly, LED pulses on sound.

