# C33 Infrared Receiver Module and Controller

Based on [BrickHackers IR-VS1838](https://github.com/BrickHackers/pxt-IR-VS1838) by [BrickHackers](https://github.com/BrickHackers)

MakeCode extension for C33 IR receiver module (VS1838) and Mini Slim controller.

## C33 Infrared Receiver / VS1838

| ![C33 Infrared Receiver](https://raw.githubusercontent.com/thireyes/pxt-c33-ir-recv/master/icon.png "C33 Infrared Receiver") | 
| :-------------------------------------------------------------------------------------------------------------------------------------: | 
|                                                         _C33 Infrared Receiver Module_                                                  |  

IR receiver chip is focused to use with Arduino and Raspberry Pi, however, works with micor:bit and calliope too.
According to VS1838B datasheet, it features:
* **[ frequency ]**  38 kHz
* **[ working voltage ]**  2.7 – 5.5 V DC
* **[ Receiver Distance ]** 22 – 25 m
* **[ Size ]** 7.4 mm x 6.2 mm x 5.3 mm


| ![IR Controller](https://github.com/thireyes/pxt-c33-ir-recv/blob/master/irCotnroller.png "IR controller") |
| :---------------------------------------------------------------------------------------------------------: |
|                             _Mini Slim infrared remote controller_                                          |

Some sellers could print their logo on controller, but functionality should be same. 
* **[ buttons ]** 20 function keys; the effective life of 20,000 pressings
* **[ frequency ]** 38 kHz
* **[ effective angle ]** 60°
* **[ transmission distance ]** cca 8 m (specific and surroundings, the receiver sensitivity and other factors)

# Documentation
> Open this page at [https://github.com/thireyes/pxt-c33-ir-recv](https://github.com/thireyes/pxt-c33-ir-recv)

## Use as Extension
This repository can be added as an extension in MakeCode.
* open https://makecode.microbit.org/
* click on **New Project**
* click on **Extensions** under the gearwheel menu
* search for **https://github.com/thireyes/pxt-c33-ir-recv** and import the C33-IR-Recv  extension


## irVS1838.connectIrReceiver

Connects to the IR receiver module at the specified pin.

```sig
irVS1838.connectIrReceiver(DigitalPin.P0)
```

### Parameters

- `pin` - digital pin with an attached IR receiver

## irVS1838.onIrButton

Do something when a specific button is pressed or released on the remote control.

```sig
irVS1838.onIrButton(IrButton.Ok, IrButtonAction.Pressed, () => {})
```

### Parameters

- `button` - the button to be checked
- `action`- the trigger action
- `handler` - body code to run when the event is raised

## irVS1838.irButton

Returns the code of the IR button that was pressed last. Returns -1 (IrButton.Any) if no button has been pressed yet.

```sig
irVS1838.irButton()
```

## irVS1838.onIrDatagram

Do something when a specific button is pressed or released on the remote control.

```sig
irVS1838.onIrDatagram(() => {})
```

### Parameters

- `handler` - body code to run when the event is raised

## irVS1838.irDatagram

Returns the IR datagram as 32-bit hexadecimal string. The last received datagram is returned or "0x00000000" if no data has been received yet.

```sig
irVS1838.irDatagram()
```

## irVS1838.wasIrDataReceived

Returns true if any IR data was received since the last call of this function. False otherwise.

```sig
irVS1838.wasIrDataReceived();
```

## irVS1838.irButtonCode

Returns the command code of a specific IR button.

```sig
irVS1838.irButtonCode(IrButton.Num9)
```

### Parameters

- `button` - the button

## MakeCode Example

```blocks

irVS1838.connectIrReceiver(DigitalPin.P0)

basic.forever(function () {
    if (irVS1838.wasAnyIrButtonPressed()) {
        basic.showNumber(irVS1838.irButton())
    }
})

irVS1838.onIrButton(IrButton.OK, IrButtonAction.Pressed, function () {
    basic.showIcon(IconNames.Heart)
})

irVS1838.onIrButton(IrButton.OK, IrButtonAction.Released, function () {
    basic.showIcon(IconNames.SmallHeart)
})

```

## License

Licensed under the MIT License (MIT). See LICENSE file for more details.

## Supported targets

- for PXT/microbit
- for PXT/calliope
