# wirelesspowertransmission
This project has been part of my educational learning during my diploma engineering.
Software objective
The objectives of the software that was to be developed were many. The following are a few of them
The software developed for this project was designed to meet several key goals:
- Generate the required frequency to enable effective wireless power coupling between the transmitter and receiver.
- Allow dynamic frequency adjustment using push buttons connected to the microcontroller, enabling user-controlled tuning.
- Display a welcome or introductory message when the system is powered on, signaling successful initialization.
- Show the institution name and project supervisor’s name on the display as part of the startup interface.
- Maintain a consistent frequency output to support stable and uninterrupted wireless power transmission.
  
🧠 Key Components
- AT89S52 Microcontroller
- TX & RX coils
- Capacitor tuning for resonance
- Oscillator circuit

Pin Description
VCC :Supply voltage.
GND:Ground
Port 0:
Port 0 functions as an 8-bit, bidirectional I/O port with open-drain configuration. When used for output, each pin is capable of sinking current from up to eight TTL logic inputs. Writing logic high (1s) to the pins allows them to act as high-impedance inputs.
This port can also serve as a multiplexed low-order address and data bus during access to external memory for both programs and data. In this mode, Port 0 utilizes internal pull-up resistors.
During Flash memory programming, Port 0 receives code bytes, and during program verification, it outputs them. External pull-up resistors are necessary for the verification phase.
Port 1:
Port 1 is another 8-bit, bidirectional I/O port, but with internal pull-up resistors. The output drivers of this port can both sink and source current for up to four TTL logic inputs. When logic high (1s) is written to Port 1 pins, the internal pull-ups pull them high, allowing them to be used as inputs. When used this way, pins that are externally pulled low will source current due to the internal pull-ups.
Additionally, the pins P1.0 and P1.1 can be configured for timer/counter 2 functions: P1.0 can act as the external count input (T2), and P1.1 can serve as the trigger input (T2EX), as detailed in the related configuration table.
Port 1 is also used to receive the lower address bytes during both Flash programming and verification.

Port 2 (P2):
Port 2 is an 8-bit bidirectional port with built-in pull-up resistors. It can both send and receive signals. The output pins of Port 2 can handle up to four TTL devices. When you write 1s to Port 2, the internal pull-ups pull the pins high, making them act as inputs. If an external device pulls them low, they will still send some current due to the pull-ups.
Port 2 sends out the high-order address byte when the microcontroller reads from external program memory or when using 16-bit addresses to access external data memory (like with MOVX @DPTR). In this case, Port 2 uses strong pull-ups to send 1s.
When using 8-bit addressing (like with MOVX @RI), Port 2 outputs the data stored in its special function register (SFR).
During Flash memory programming and verification, Port 2 also receives the upper address bits and certain control signals.

Port 3 (P3):
Port 3 is another 8-bit bidirectional I/O port, also equipped with internal pull-ups. Its output pins can both source and sink current for up to four TTL inputs. If you write 1s to the pins, the internal pull-ups make them high, so they can be used as inputs. If an external device pulls them low, the port still sources some current due to the pull-ups.
Besides basic I/O use, Port 3 supports several special functions of the AT89S52 microcontroller (these are listed in a related table).
Port 3 is also involved in handling control signals during Flash programming and verification

RST

Reset input. A high on this pin for two machine cycles while the oscillator is running resets the device. This pin drives High for 96 oscillator periods after the Watchdog times out. The DISRTO bit in SFR AUXR (address 8EH) can be used to disable this feature. In the default state of bit DISRTO, the RESET HIGH out feature is enabled.

ALE/PROG

Address Latch Enable (ALE) is an output pulse for latching the low byte of the address during accesses to external memory. This pin is also the program pulse input (PROG) during Flash programming.
In normal operation, ALE is emitted at a constant rate of 1/6 the oscillator frequency and may be used for external timing or clocking purposes. Note, however, that one ALE pulse is skipped during each access to external data memory. If desired, ALE operation can be disabled by setting bit 0 of SFR location &EH. With the bit set, ALE is active only during a MOVX or MOVC instruction. Otherwise, the pin is weakly pulled high. Setting the ALE-disable bit has no effect if the microcontroller is in external execution mode.

PSEN
Program Store Enable (PSEN) is the read strobe to external program memory.
When the AT89S52 is executing code from external program memory, PSEN is activated twice each machine cycle, except that two PSEN activations are skipped during each access to external data memory.

EA/VPP
External Access Enable. EA must be strapped to GND in order to enable the device to fetch code from external pro-gram memory locations staring at 0000H up to FFFFH
Note, however, that if lock bit 1 is programmed, EA will be internally latched on reset. EA should be strapped to Vee for internal program executions. This pin also receives the 12-volt programming enable voltage (Vy) during Flash programming.

XTAL1
Input to the inverting oscillator amplifier and input to the internal clock operating circuit.

XTAL2
Ouput from the inverting oscillator amplifier.

RST (Reset Pin)
The RST pin is used to reset the microcontroller. When this pin stays high for two machine cycles while the oscillator is running, the device resets.
If the Watchdog timer times out, this pin automatically goes high for 96 oscillator periods. This automatic reset behavior can be turned off by setting the DISRTO bit in the AUXR special function register (SFR) at address 8EH. By default, this auto-reset function is turned on.
ALE/PROG (Address Latch Enable / Programming Input)
ALE is a control signal that sends out a pulse to lock the lower byte of the address when accessing external memory.
During Flash programming, this pin also serves as the PROG input to receive the programming pulse.
Normally, ALE pulses are generated at a regular rate — one pulse every six oscillator cycles. This pulse can also be used as a timing signal for external circuits. However, when accessing external data memory, one ALE pulse is skipped. If needed, ALE can be disabled by setting bit 0 in the SFR at address 8EH. When disabled, ALE only works during MOVX and MOVC instructions. Otherwise, the pin stays weakly high. This setting doesn’t apply when the system runs code from external memory.

PSEN (Program Store Enable)
PSEN is the read signal used when the microcontroller accesses external program memory.
When running code from external memory, the PSEN pin is activated twice per machine cycle — except during data memory access, where two activations are skipped.

EA/VPP (External Access / Programming Voltage)
EA controls whether the microcontroller uses external or internal program memory.
If EA is connected to GND, the microcontroller fetches code from external memory starting at address 0000H to FFFFH.
If EA is connected to Vcc, it uses the internal program memory instead.
If Lock Bit 1 is set, the EA pin’s state is locked internally during reset.
 During Flash programming, this pin also takes in the 12V programming voltage (VPP).
 
XTAL1
This is the input pin to the internal oscillator circuit and inverting amplifier. It connects to an external crystal or clock signal to drive the microcontroller.

XTAL2
This is the output pin from the internal inverting amplifier, typically connected to one end of a crystal oscillator.
