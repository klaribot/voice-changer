## Tutorial Monitor Output

This section describes monitor output in server device mode, which was added in v.1.5.3.7.

## Configuration before v.1.5.3.6

In order to work with other applications such as Discord or Zoom, it is generally necessary to set this output to a virtual audio device such as Voicemeeter. This required a lot of overhead to go through the virtual audio device to check the converted audio (blue line).

! [image](https://github.com/w-okada/voice-changer/assets/48346627/faba8fdf-cfa5-468f-a56b-3fa986fb45a1)

## Configuration since v.1.5.3.7

In v.1.5.3.7, it is now possible to configure another output destination device in server device mode of the VC Client (red line). This allows direct output to the wasapi or asio device for monitoring without going through Voicemeeter, thus enabling monitoring with less delay.

! [image](https://github.com/w-okada/voice-changer/assets/48346627/1d5065eb-b042-4521-ade3-66828c87a712)

## Usage

Select server device mode in the device configuration area. You can set sampling rate (S.R.), input, output, and monitor.

! [image](https://github.com/w-okada/voice-changer/assets/48346627/c15e6800-75ec-410b-87f2-c96d0c697c91)

## Notes

Each of input, output, and monitor devices used in server device mode must have the same sampling rate. If they do not match, specify the sampling rate supported by each device from the GUI, as detailed information will appear on the console.

### Example

! [image](https://github.com/w-okada/voice-changer/assets/48346627/d621d356-5710-4766-932e-43b7d520df5f)

If the sampling rates do not match, the display will look like this.

(1) shows whether the device supports the sampling rate specified in the GUI or not.

(2) shows the sampling rates supported by each device, and the sampling rates for input, output, and monitor should all be specified. In this case, 48000 is specified.

## Tips

### Part 1

The delay may vary depending on your environment, but in our environment, we were able to minimize the delay by using Wasapi devices for Input and Monitor, and setting output as desired.
(using RTX4090)

### Part 2

The Wasapi sampling rate can only be set by the device. This setting can be changed from the Windows sound settings. (Win11)

! [image](https://github.com/w-okada/voice-changer/assets/48346627/300c8cf0-cb7d-4f24-8253-fa313caee5df)
