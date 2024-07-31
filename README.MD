# DANSK-datorn
### This repository is for the DANSK-datorn - a FLEX 6809 computer designed in Denmark.

Sadly the designer Hans Dalgaard passed away this year.  
If you have any information about this computer, please contact me.

From MPU-laren #3 - 1985  

        ******   PRESS-STOPP   ********  
        *                             *  
        *   NY FLEX 6809 - DATOR      *  
        *                             *  
        ******   PRESS-STOPP   ********  

## NY FLEX DATOR

Alla kanske inte har råd att gå över till ett nytt datorsystem eler kanske inte vill kasta alla sina gamla FLEX-program som man lagt ned mycket möda och tid på att skriva eller kopiera.
För alla dessa har det ju inte hänt så mycket sedan RT-datorns tid.
NU har det dock lossnat !!!!!
PD68 har härmed nöjet att presentera den s.k. DANSK-datorn.
Systemet som jag själv f.ö. själv använder sedan en tid tillbaka har en rad fördelar jämfört med RT-datorn, elle vad sägs om:

* Kör med 2 MHz (dubbelt så snabbt som RT-datorn)
* 256 kbyte minneskort (går att bygga ut till 1 Mbyte)
* RAM-disk s.k. V-disk som standard
* Kör FLEX09 operativsystem
* Hanterar direkt 4 st 1 Mbyte floppydrivar
* Promkort med plats för 428 kbyte EPROM
* Inbyggd CRT-kontroller MC68B45 (ingen yttre dyr terminal krävs utan endast videomonitor och tankgentbord)
* Endast 3 kort i enkelt europaformat krävs för at få en komplett dator
* Krestkorten säljs lösa utan komponenter för att alla skall kunna köpa komponenter billigt på egen hand
* Centronics- eller V24- utgång till printer.

## ** SPECIFICATION FOR DC1 CPU BOARD **
![CPU-board](/Images/DC1-CPU.jpg)
* 2 MHz 68B09E CPU
* All CPU address, data and control lines are fully buffered
* Page select registers alow memory expansion to 1 Mbyte RAM for virtual disk or printer buffer. Fully SWTPC compatible
* 4k system monitor contains bootstrap loader and video drivers
* 2k on-board static RAM
* Buffered TTL serial port for keyboard with software baudrate
* Buffered Centronics parallel printer interface
* Real Time Clock with on-board battery backup timer and alarm
* One 16 but timer with interrupt
* Runs TSC FLEX09 operating system

## ** Specification for DC2 CRT-FLOPPY BOARD **

* CRT Video:
* 2 MHz 68B45 CRT Controller displays 80 * 24 line via 2k om memory mapped RAM at location $E000 - $EFFF
* Video drivers in DANBUG Monitor V.1.x emulate most functions of the SWTPC CT-82 terminal except graphic
* 4k EPROM character generator supports the full ASCII character set, enlarged ans semi-graphic characters
* Composite Video output

* Floppy:
* Double Density floppy disk controller for either 5" or 8" drives uses WD 2797
* Single and double side, single and double density, up to four drives total
* Fully buffered output and Schmitt trigger input buffers for the disk drive signals.

## ** Specification for DC3 256k Dynamic RAM board

* Full 2 MHz operation with transparent on board refresh, runs continuously without cycle stretching or stealing.
* Extended addressing. SWTPC compatible
* Use AM2764B Dyn-RAM controller

## ** Specification for DC4 428k EPZROM board **

* Use EPROMS 2664, 27128 or 27256
* The board occupies only four bytes I/O at address $E030 - $E033
* Move 64k to RAM in 0,5 seconds
* Driver routines in DANBUG monitor V.1.0

## ** Specification for DC5 I/O board **

* Two serial ports
  - 1 RS232C with handshaking - RTS, CTS, DTR, DCD, DSR and RxC
  - 1 RS232C with handshaking - RTS and CTS
  - Program-selectable baudrates between 50 - 19200 baud
* One parallel port
  - Centronics parallel printer interface
  - Two 16-bit timer
* EPROM programmer
  - Programs 2732A, 2764, 27128 and 27256
* Sounder for system bell
