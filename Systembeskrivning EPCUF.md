EPCUF - Enhanced Personal Computer Using FLEX
1. Systembeskrivning
1.1 Bussbeskrivning
EPCUF använder sig av en 6809E-processor. Det är en 9-bitars processor från Motorola. 6809E har inte någon inbyggd oscillator för systemklockan. Systemklockan är en yttre oscillator som används både för processor och bildskärm. Den yttre oscillatorn gör det möjligt att synkronisera läs- och skrivoperationerna mot bildminnet och på sätt undvika flimmer på skärmen.
EPCUF är en vidareutveckling av den traditionella "FLEX-datorn". Genom att lägga till funktioner som t.ex. ramdisk, Printerbuffert och Promdisk har systemet förbättrats avsevärt.
Processorbussen i EPCUF är inte någon standardkonstruktion.

Bussen betår av 4 delar; adressbuss, databuss, kontrollbuss och kraftbuss. Bussens utseende och konstruktion bestäms av 6809E-processorn. EPCUF har en utökad minnesadressering. Adressbussen har därför utökats med 4 adressledningar (A16 - A19). Systemklockans placering på DC2-kortet och valet av 6809E ökar antalet signaler i bakplanet.

Adressbuss		A0 - A19	fyra extra bitar A16 - A19
Databuss		D0 - D7
Kontrollbuss	R/W			R/W från processor
				/R 			/R konstruerad signal PALDC1
				E 			E klocka till processor
				/E 			inverterad E klocka
				Q			Q klocka
				S-OFF		buffrad PB4 (ej använd)
				/BELL		Ljudsignal från DC2-kort
				/NMI 		NMI avbrott
				/IRQ		IRQ avbrott
				/FIRQ		FIRQ avbrott
				/RES 		Resetsignal
				/ME 		Enable för minne		$0000 - $DFFF
				/IO 		Enable för IO			$E000 - $E0FF
				/CRT		Enable för bildminne	$E800 - $EFFF
Kraftbuss		+5V			Matning +5V
				+12V		Matning +12V
				-12V		Matning -12V
				0V			GND


1. Systembeskrivning

Buss för DCx-kort
						A		C
				GND		+	01	+	GND
				/NMI	+	02	+	/ME	$0000 - $DFFF
				/IRQ	+	03	+	/IO	$E000 - $E0FF
				/FIRQ	+	04	+
				/RES	+	05	+
						+	06	+
						+ 	07	+	E
						+	08	0	Q
$E800 - $EFFF /CRTRAM	+	09	+	CRT Q
				A19		+	10	+	/E
				A18		+	11	+	S-OFF
				A17		+	12	+	/BELL
				A16		+	13	+
						+	14	+	D0
						+	15	+	D1
						+	16	+	D2
						+	17	+	D3
						+	18	+	D4
						+	19	+	D5
						+	20	+	D6
						+	21	+	D7
				R/W		+	22	+	/R
				+12V	+	23	+	-12V
				A15		+	24	+	A0
				A14		+	25	+	A1
				A10		+	26	+	A2
				A13		+	27	+	A3
				A11		+	28	+	A4
				A9		+	29	+	A5
				A8		+	30	+	A6
				A12		+	31	+	A7
						+	32	+	+5V

1.2 Kontaktbeskrivning
Till EPCUF kan följande periferiutrustning anslutas. Vissa enheterbehövs för att systemet ska fungera.
1. Floppydisk
2. Bildskärm (monitor med composit video)
3. Tangentbord seriellt 1200 baud
4. Centronics interface för printer

## DC1-CPU kort
S2 - ACIA (MC 6850)
	PB3		10	9
	BOOT	8	7
	5V		6	5	TXD
	GND		4	4	RXD
	/MNI	2	1

S3 - Printer (Centronics)
	ACK		20	19	PB6
	D7		18	17	PB0
	D6		16	15	GND
	D5		14	13	GND
	D4		12	11	GND
	D3		10	9	GND
	D2		8	7	GND
	D1		6	5	GND
	D0		4	3	GND
	STROBE	2	1	GND

## dc2 - fLOPPY/CRT kort
S3 - Floppy
	READY	34	33	GND
	SS		32	31	GND
	READ	30	29	GND
	WPROT	28	27	GND
	TR00	26	25	GND
	WG		24	23	GND
	WD		22	21	GND
	STEP	20	19	GND
	DIR		18	17	GND
	MON		16	15	GND
	DS3		14	13	GND
	DS2		12	11	GND
	DS1		10	9	GND
	INDEX	8	7	GND
	DS0		6	5	GND
	TG43	4	3	GND
	SPARE	2	1	GND

S2 - VIDEO
	VIDEO	1
	GND		2
	GND		3
	LIGHTP	4

DC5-I/O kort (Prombrännare)
S4 - VIA
	CA1		26	25		PB6
			24	23		PB0
			22	21		GND
			20	19		GND
	PA7		18	17		GND
	PA6		16	15		GND
	PA5		14	13		GND
	PA4		12	11		GND
	PA3		10	 9		GND
	PA2		 8	 7		GND
	PA1		 6	 5		GND
	PA0		 4	 3		GND
	CA2		 2	 1		GND

S2 - ACIA (6551)
	+12V	10	 9	DCD
	RTS		 8	 7	GND
	CTS		 6	 5	TXD
	DSR		 4	 3	RXD
	RXC		 2	 1	DTR

S3 - ACIA (6551)
	-12V	10	 9	
	CTS		 8	 7	GND
	RTS		 6	 5	TXD
			 4	 3	RXD
			 2	 1

Ansluts ett DC5-kort till bussen så ökas antalet tillgängliga interface. DC5-kortet är utrustat med 2 st serieportar och en paralellport.

1.3 Minneskarta över datorn
	EPCUF's 6809E-processor kan direktadressera 65536 minnespositioner. Denna adresseringsrymd delas av primärminne (RAM), I/O-organ samt systemprogram (ROM). I EPCUF är primärminner utökat till 1MB. Det utökade minnet adresseras över ett DATRAM (Dynamic Address Translation RAM). Den minnesarea som styrs av DATRAM kan inte direktadresseras av processorn. Systemet utnyttjar denna minnesarea för printerbuffert, ramdisk och temporär datalagring. Den ordinarie minnesdispositionen framgår av figuren nedan.

	$FFFF	._______________.	$FFF0 - $FFFF 	DATRAM DC1-KORT
			.				.					WOM (Write Only Memory)
			. DC4-BUG       .
	$F000	._______________.
			.               .
			. VIDEO RAM     .
	$E800	._______________.
			.				.
			. 2K STAT RAM	.
	$E100	._______________.
	$E0FF	.				.
			.				.
			.				.	$E070 - $E07F	VIA		DC1-KORT
			.				.	$E030 - $E03F	VIA		DC5-KORT
			.				.	$E02C - $E02F	ACIA	DC5-KORT
			.				.	$E028 - $E02B	ACIA	DC5-KORT
			.  I / O  -		.	$E024 - $E027	ACIA	DC5-KORT
			.				.
			.				.	$E023	EPROM DATA		DC4-KORT
			.				.	$E022	EPROM NR		DC4-KORT
			.				.	$E021	EPROM ADR. LOW	DC4-KORT
			.				.	$E020	EPROM ADR. HI	DC4-KORT
			.  A D R E S -	.
			.				.	$E014 - $E01B FLPY-CONT	DC2-KORT
			.				.	$E010 - $E013 CRT-CONTR	DC2-KORT
			.				.
			.  S E R .		.	$E004 - $E005	ACIA	DC1-KORT
			.				.	$E002 - $E003	RTC		DC1-KORT
	$E000	._______________.
	$DFFF	.				.
			.				.
			. FLEX OPERATING.
			.				.
			. SYSTEM		.
	$C000	._______________.
	$BFFF	.				.
			.   U S E R 	.
			.				.
			.				.
			.    R A M 		.
	$0000	._______________.

1.3.1 Minnesadressering över 64kb
	I punkt 1.3 visades minneskartan över systemet. 6809E-processorn kan adressera 65536 minnesceller. Adressen från processorn (logisk adress) övesätts via DATRAM (Dynamic Address Translation RAM) till en fysisk adress mot det dynamiska minnt (1MB). Det innebär att systemet arbetar med 2 st adressbussar, en logisk och en fysisk adressbuss. Införandet av DATRAM (Dynamic Address Translation RAM) gör att processorn kan växla mellan olika minneskartor eller sidor. Den logiska adressen har området $0000 - $DFFF (64k) och den fysiska $00000 - $FFFFF (1Mb). Det ska påpekas att den logiska adressen är begränsad till $DFFF (56kb). Det beror att I/O, 1k RAM, bildminne ocg DC4BUG delar utrymme på denna buss. Ovanstående begränsning får i praktiken ingen större nackdel. Det betyder att den sida man kan "mappa" åt gången inte får vara större än 56k. Det blir dock fortfarande möjligt att nå hela minnet (1Mb).
	Den fysiska adressbussen byggs enligt figur nedadn.

	DATRAM (Dynamic Address Translation RAM)
## Fixa bild
Den fysiska adressen består av 5 st 4-bitars grupper(eng. nibbles). Adressledningarna A0 - A11 kommer direkt från processorn och placerar endast buffertar ut till bussen. Dessa adressledningar från processorn bildar ett 4 kbyte block. Resterade adressledningar (A12 - A19) kommer från ett DATRAM. DATRAM består fysiskt (på DC1-kortet) av 2 st bipolära RAM som kan lagra 16 nibble. Dessa båda minnen adresseras paralellt för att man ska få en byte. Den fysiska adressen blir avhängigt av informationen som finns lagrad i detta minne.

DATRAM's 16 minnesceller adresseras med 4 adressledningar (A0 - A3). Dessa adressledningra är kopplade till utgången av en 4-bitars multiplexor. Funktionen är följande:
Normalt när processorn arbetar och inte skriver mot DATRAM så är DATRAM's adresstrådar kopplade mot processorns mest sigifikativa adressledningar A12 - A15. Informationen lagrad i DATRAM kommer att avläsas och skickas ut mot systembussen i takt med processorns adressering. A12 - A15 kan anta värden från $0 - $F hexadecimalt. Antag att den logiska adressen har värdet 0000 0000 0000 0000 binärt. Det innebär att DATRAM's adress 0 utpekas. Innehållet i adress 0 kommer att skickas ut på adressledningarna A12 - A19. Antag också att innehållet i adress 0 (DATRAM) är $01. Den fysiska adressen mot dynamiska minnet på systembussen får då värdet:
0000 0001 0000 0000 0000 (20 bitar)
OBS! Den logiska adressen har värdet:
0000 0000 0000 0000 (16 bitar)

Den fysiska adressen kan generellt skrivas:
DD XXX

DD  = block från DATRAM
xxx = 4k block i dynamiska minnet.

Byten DD från DATRAM kan anta 256 kombinationer. Det är möjligt att adressera 256 st 4k block. 256 x 4kbyte blir 1MB.

16 st minnespositioner i DATRAM kan utpeka 16 st 4k block i systemminnet. I praktiken kan bara 14 st block (56 kbyte) utnyttjas.
DATRAM's innehåll har ovan beskrivits att vara på varandra följande, dvs, blocken tillsammans bildar en kontinuerlig area. Det är inget krav. Ordningen mellan blocken kan vara helt godtycklig. Ett 4k blockkan bytas ut i den vanliga minneskartan genom att manipulera innehållet i DATRAM. Det är möjligt att t.ex. temporärt spara undan ett 4k block och sedan ta tillbaka det. Växlingen mellan de olika minnesareorna blir också mycket snabb.
Hur adresseras DATRAM?
Man måste kunna byta ut innehållet i DATRAM oberoende av den temporära minneskartans utseende. Dvs. DATRAM får inte ha en adress som kan mappas bort. Detta har lösts genom att begränsa den logiska adressens värde. Signalen /ME som kopplar in minnet kommer från PALDC1. Minnet blir anropat inom området $0000 - $DFFF dvs. 56 kb. Området över 56k är reserverat för systemets I/O och DC4BUG.

PAL-kretsen (PALDC1) avkodar I/O-adresser. Det finns en signal benämd /EX som styr accessen mot DATRAM. När processorn skriver mot en adress i området $FFF0 - $FFFF så avkodas adressen i PALDC1. Ut från denna PAL kommer signalen /EX. /EX går till miltiplexorns selectingång. Multiplexorn växlar läge och adressledningarna A0 - A3 når DATRAM i stället för A12 - A15 samtidigt förses DATRAM med data från databussen. Det betyder att DATRAM kan programmeras med godtyckligt data.

Det går att skriva mot DATRAM med ovan beskrivna konstruktion. Operativsystemet i EPCUF för därför tabell som speglar innehållet i DATRAM. Tabellen har en fast placering i minnet ($DFD0 - $DFDF). förändras innehållet i DATRAM ska tabellen uppdateras.

$DFD0 motsvarar innehållet i DATRAM adress $FFF0, $DFD1 -> $FFF1 osv.

Vid upstart av systemet så måste DATRAM förses med vissa grundvärden, som framgår av nedanstående tabell:

DATRAM
$FFF0 - $00
$FFF1 - $01
$FFF2 - $02
$FFF3 - $03
$FFF4 - $04
$FFF5 - $05
$FFF6 - $06
$FFF7 - $07
$FFF8 - $08
$FFF9 - $09
$FFFA - $0A
$FFFB - $0B
$FFFC - $0C
$FFFD - $0D
$FFFE - $0E
$FFFF - $0F

Ovan uppräknade värden är alltså utgångsvärdena. Med dessa värden nås det normala adressområdet $0000 - $FFFF

Ett exempel kan vara på sin plats.
Antag att innehållet i $FFF0 ändras från $00 till $10. Antag också att processorn skriver mot adressen $0100 i ett 4k block. Den totala adressen mot bussen ser nu ut så här:
$10100

1.3.2 RAMDISK
Ramdisk är ett sekundärminne där man har emulerat (efterliknat) funktionen av en floppydisk i RAM. Det innebär att den måste formateras. Disken måste ha ett systemspår där FLEX kan finna SIR (System Information Record) och filkatalogen. Bootsektorn kan däremot utelämnas inte heller behöver disken innehålla någon formateringsbakgrund. RAMDISKEN är fysiskt placerad i det dynamiska minnekortet. Minnet är uppdelat i minnesbanker, Minnesområdet från 0 upp till 64k används av FLEX. Området därutöver delas mellan RAMDISK och PRINTERBUFFERT, Formateringen av ramdisken görs med VDISK.CMD. Kommandot vdisk kommer att beskrivas mer ingående i SYSTEMBESKRIVNING - MJUKVARA.

1.3.3 PROMDISK
Det är den här funktionen som verklugen lyfter konstruktionen och faktiskt förändrar FLEXsystemet till ett mycket attraktivt system. Operativsystemet FLEX gör på följande sätt när det tolkar ett kommando som användaren har skrivit efter prompten +++.
1. Datorn tolkar kommandor och hämtar detsamma från SYSTEMDRIVE, placerar programmet i ram och startar upp programmet.
2. Datorn fortsätter sedan att läsa in ev arbetsfil från WORKDRIVE

Alla dessa läsningar mot floppydisken tar tid och det gör maskinen långsam även om processorn arbetar med en klockfrekvens på 2MHz. Det är här som PROMDISKEN, eller rättare sagt, prommade kommandon kommer in i bilden. Operativsystemet FLEX är omskrivet (patchat) så att datorn i första hand försöker att finna efterfrågat kommado i PROMDISKEN. Finns kommandot i prom läser datorn in kommandot från detta.

1.4 AVVIKELSE FRÅN TSC FLEX 09
EPCUF har en del nya egenskaper som inte finns i originalversionen av TSC FLEX. De flesta av oss som har varit med om att bygga en RT-dator eller dator av liknande konstruktion har väl sneglat åt datorer med finesser som printerbuffert, realtidsklocka, ramdisk och kanske kommandokatalog härbärgerad i ROM. Nu är det dags att sluta drömma och bara njuta av verkligheten.

FLEX kan i EPCUF botas på två olika sätt. Det vanliga sättet är att läsa bootsektorn från floppyskivan och sedan läsa ned hela FLEX i RAM. I EPCUF är det möjligt att läsa ned en prommad FLEX. Prom nr 13 på promkortet DC4 är helt reserverat för operativsystemet FLEX. Datorn läser via VIA'an på CPU-kortet (DC1) för att avgöra var ifrån bootning ska ske, skivan eller promkortet.

Själva kärnan av FLEX (FLEX.COR) är på vissa ställen rejält omstuvad så här går det inte att känna igen sig längre. De nya funktionerna som är införda har ställt krav på hård- och mjukvara. Nedan följer en uppräkning på de nya funktionerna och hur det har påverkat FLEX systemet.

Realtidsklocka
Läsning vid start av systemet. Det är inte längre nödvändigt att svara med dagens datum innan systemet bootar. Rätt tid och datum läses från den batteriuppbackade klockan.

Printerspooler
Det utökade minnet användes också som printerbuffert. Utilities för att skriva mot printern är som förut. När kommando P,LIST,TEST matas in till datorn sker följande:
1. P - dirigerar utskriften till printerbufferten (reserverad del av minnet)
2. LIST - läser filen TEST.

Utmatning från minnet (bufferten) till printerporten sker sedan med jämna intervall m.h.a. avbrott (interrupt). Avbrotten genereras av timern i VIA'n på CPU-kortet. I praktiken upplevs utmatning och fortsatt jobb mot datorn att ske samtidigt. Enda tillfället man märker att datorn utför två uppgifter är vid arbete mot floppydisken. Floppy har företräde framför printer utskriften.

Kommandokatalog i PROM
Användarens kommando tolkas annorlunda sätt i EPCUF. FLEX undersöker först om det finns ett DC4-kort anslutet i systemet. Om det så är fallt försöker operativsystemet att i första hand hitta det efterfrågade kommandot i promdiskens kommandotabell. Finner FLEXinte kommandot så söker systemet vidare på SYSTEMDRIVE. Misslyckas sökningen här så rapporteras fel i vanlig ordning. DC4-kortet har plats för 12 st 28-pin promkapslar. Kortet kan bestyckas med olika typer av prom. Det är i första hand 2764, 27128 och 27256 som kommer ifråga. Bestyckas kortet med 13 st 27256 och 1 st 2764 fås minneskapacitet på 424 kb, Den 14:e kåpan måste vara av typen 2764. Operativsystemet självt är placerat i detta minne. Med 424 kb som tillgängligt lagrinsgytrymme blir det möjligt att lägga FLEX utilities, assembler, editor mm i prom.

I/0
Inmatningsrutinerna mot FLEX är förändrade. Det går inte längre att ansluta en terminal. Terminalen är redan inbyggd i systemet. Datorn tar in data från tangentbordet via en ACIA placerad på CPU-kortet. Tecken som matas in i datorn passerar rutiner i DC4BUG och hamnar sedan hos FLEX. Till EPCUF ansluts ett tangentbord med seriellt snitt. Tangentbordet ska lämna ASCII-tecken med 1200 Baud överföringshastighet. Det kan i detta sammanhang nämnas att det går alldeles utmärkt att använda ett PC-tangentbord. Man måste dock sätta en processor mellan tangentbordet och danskdatorn som översätter PC-tangentbordets scankoder till ASCII-tecken.
Utmatningsrutinerna mot blidskärmen är förändrade. FLEX skriver inte längre mot en ACIA utan mot DC4BUG. I DC4BUG finns en driver för bildskärmen i systemet. MC6845 används som bildprocessor. Programmet för bildskärmen emulerar en CT-82 terminal. CRT-kortet lämnar composite videosignal. Till EPCUF ansluts en monitor med composite videoingång.
