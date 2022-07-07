# Serial Peripheral Interface(SPI)
Another [[Communication Protocol]] that enables a [[Duplex Communication|full-duplex]] communication umlike [[Two Wire Interface]] with only a [[Duplex Communication|half-duplex]] communication

It uses 4 pins to function. 
- MISO: Master in Slave out
- MOSI: Master out Slave in
- SCK: Clock
- SS: Slave Select

Using this 4 pins, it could turn on or turn off some components. ![[Drawing 2022-06-25 04.21.17.excalidraw.png]]

SS, SCK and MOSI share the same wire but not MISO. MISO switch on and off the components. To enable a component:
- Input low voltage in MISO, component turn off
- Input high voltage in MISO, component turn on