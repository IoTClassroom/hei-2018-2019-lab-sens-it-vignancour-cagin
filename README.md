# Lab Sensit

## Prerequesite

### Sigfox Cloud

1.  Head over to the [activate](https://buy.sigfox.com/activate).

2. Select your country, enter the device ID & PAC and finish creating your account.

3. Once done, log on the [backend](https://backend.sigfox.com/).

4. Try sending a message by double pressing the button.

5. Click on your device ID and select the **"Messages"** tab. You should now see a Sigfox message.

### Sens'it development environment

#### Linux / Mac OS

1. Download and install [GNU Arm Embedded Toolchain version 7.2.1](https://developer.arm.com/open-source/gnu-toolchain/gnu-rm/downloads).

2. Download and install [dfu-util 0.9](http://dfu-util.sourceforge.net/).

3. Run `/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"``

4. Run ```brew install dfu-util```

5. Edit `./sensit-sdk-v2.0.0/sdk/Makefile`:

    * Make sure your `CC`, `BIN_TOOL`, `SIZE_TOOL` paths links to the right folder.
    * Example:
        ```
        CC = /Users/antoine/Documents/gcc-arm-none-eabi-7-2018-q2-update/bin/arm-none-eabi-gcc
        BIN_TOOL  = /Users/antoine/Documents/gcc-arm-none-eabi-7-2018-q2-update/bin/arm-none-eabi-objcopy
        SIZE_TOOL = /Users/antoine/Documents/gcc-arm-none-eabi-7-2018-q2-update/bin/arm-none-eabi-size
        ```
        
6. In `./sensit-sdk-v2.0.0/sdk/`, run `make temperature`.

7. If there are no warnings, run `make prog`.

**Hourray, you just flashed the `main_TEMPERATURE.c` firmware.**

Now check on the Sigfox Backend if you received some messages.

### Windows

1. Download and install [GNU Arm Embedded Toolchain version 7.2.1](https://developer.arm.com/open-source/gnu-toolchain/gnu-rm/downloads). Make sur to tick the "Add path variables" at the end of installation.

2. Download and unzip [dfu-util-0.9-win64.zip](http://dfu-util.sourceforge.net/releases/).

3. Download [Make for Windows](http://gnuwin32.sourceforge.net/downlinks/make.php)

4. Edit `./sensit-sdk-v2.0.0/sdk/Makefile`:

    * Set `LIB_PATH`, `BIN_PATH`, `OBJ_PATH` paths links to the right folder.
    * Example:
        ```
        LIB_PATH = C:/Users/antoine/Documents/sensit-sdk-v2.0.0/sdk/lib
        BIN_PATH = C:/Users/antoine/Documents/sensit-sdk-v2.0.0/sdk/bin
        OBJ_PATH = C:/Users/antoine/Documents/sensit-sdk-v2.0.0/sdk/obj
        ```

5. In `./sensit-sdk-v2.0.0/sdk/`, run `make temperature`.

6. If there are no warnings, run `make prog`.

**Hourray, you just flashed the `main_TEMPERATURE.c` firmware.**

Now check on the Sigfox Backend if you received some messages.

## Program your Sens'it

To program your Sens'it you will need to put it in bootloader:
1. Connect your device to your computer.
2. Reset your device. With one of the provided firmwares you can do this with 4 short presses on the button.
3. When the secondary LED starts blinking, do a long press on the button.
4. If both LEDs become white, your device is in bootloader.

Then, use the `make prog` command to program your Sens'it.

### Hint

If you want to return to the original firmware of the Sens'it 3, use the following command to program it:
```
dfu-util -a 0 -s 0x08000000:leave -D bin/sensit_discovery_vX.X.X.bin
```
Replace `X.X.X` with the current version of the Discovery firmware available in the `bin` folder.

### Don't forget to:

1. Create a new `README.md` file in your repo.
2. Insert:
```
My Sens'it ID: <YOUR_SENSIT_ID>
```