# Air-Control Web Flasher

Browser-based manual Intel HEX flasher for the Air-Control ESP32 devices.

## Open locally / GitHub Pages

Open `index.html` from a static HTTPS host. Web Serial requires a secure context and a Chromium-based desktop browser such as Google Chrome or Microsoft Edge.

Once GitHub Pages is enabled for this repository, the page will be available at:

`https://1filth1.github.io/air-control/webflasher/`

## Usage

1. Connect the target board to the computer with a USB data cable.
2. Open the flasher in Chrome or Edge.
3. Select the target device and choose its matching `.hex` file.
4. Click **Подключить устройство** and select the board's serial port.
5. Wait for automatic chip detection.
6. Click **Начать прошивку** and keep the USB connection stable until completion.

If automatic connection fails, put the board into download mode (usually hold BOOT while tapping RESET), then reconnect.

## Intel HEX handling

The flasher uses Espressif's `esptool-js` 0.7.1 and its Intel HEX parser. Absolute addresses and sparse segments are preserved. Flash is not globally erased (`eraseAll: false`), so sectors absent from the HEX file are not intentionally wiped.

Flash mode is DIO, frequency is 40 MHz, and flash size defaults to auto-detection. The file's address records are authoritative; no manual offset is added.

## Supported browser

- Google Chrome / Microsoft Edge on desktop: supported (Web Serial API).
- Firefox / Safari: not supported.

## Safety

- Use only the HEX built for the selected board.
- Do not disconnect USB or close the page during flashing.
- Before programming, disconnect or safely disable the compressor and valve power stage. Test the controller on the bench before reconnecting pneumatic loads.
- Keep a known-good firmware copy so the board can be recovered if a wrong image is selected.

## Implementation

The HEX file is parsed and flashed locally in the browser. Firmware contents are not uploaded to a server. The flasher does not fetch releases or automatically choose firmware files.
