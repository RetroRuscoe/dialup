# Dial Up

A functional home dial-up network.

## Hardware Used

* Palm III
* Palm modem
* Genius 56k modem
* Cisco SPA112
* Lenovo laptop running Xubuntu Linux

## Set Up Diagram

```
                         ┌─────────────────────────┐
                         │   Xubuntu Laptop        │
                         │-------------------------│
                         │ Asterisk SIP Server     │
                         │ PPP / pppd              │
                         │ Wi-Fi → Internet        │
                         └──────────┬──────────────┘
                                    │
                         Ethernet   │ 192.168.50.x
                                    │
                     ┌──────────────▼──────────────┐
                     │     Cisco SPA112 ATA        │
                     │-----------------------------│
                     │ Line 1              Line 2  │
                     └──────┬────────────────┬─────┘
                            │                │
                        RJ11│                │RJ11
                            │                │
             ┌──────────────▼───┐     ┌──────▼────────────┐
             │ Palm III +       │     │ Genius 56K Modem  │
             │ Palm Modem       │     │-------------------│
             │------------------│     │ Auto-answer modem │
             │ MultiMail Pro    │     └─────────┬─────────┘
             │ PPP Dial-up      │               │ RS232
             └──────────────────┘               │
                                                │
                                   USB-to-Serial│Adapter
                                                │
                                     ┌──────────▼─────────┐
                                     │   Xubuntu Laptop   │
                                     │   /dev/ttyUSB0     │
                                     └────────────────────┘
```

## Modem Setup via minicom

Add the following configuration by running `sudo minicom -s`

| AT&D0 | Ignore DTR signal changes. Prevents disconnects when Linux software opens/closes the serial port. |
| AT&K0 | Disable modem compression/flow-control features that interfere with PPP over ATA links. |
| ATE0 | Disable command echo. Prevents PPP loopback/echo problems. |
| ATQ0 | Enable modem result codes (CONNECT, RING, etc.). |
| ATV1 | Use verbose text responses instead of numeric codes. |
| AT%C0 | Disable data compression. Important for stable modem-over-VoIP operation. |
| ATS0=1 | Auto-answer after one ring. |
| AT&W | Save the configuration permanently in modem memory. |
