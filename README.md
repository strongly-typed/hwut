# hwut
Hardware Unit Testing: Confirming peripheral configuration and conformance to waveform


## Getting Started with sigrok and its Protocol Decoders

Download or compile sigrok

Get a sample trace:

	wget 'http://sigrok.org/gitweb/?p=sigrok-dumps.git;a=blob_plain;f=uart/v_and_a_va18b_cable/v_and_a_va18b_cable_ir_serial_usb.sr;hb=HEAD'
	
It was recoreded (accoring to the README) at 16 MHz sample rate and shows a UART communication at 2400 baud.

	sigrok-cli -i v_and_a_va18b_cable%2Fv_and_a_va18b_cable_ir_serial_usb.sr -P uart:baudrate=2400:rx=RX -B uart=rx | hexdump

This takes a while and some decoded binary data appears

	0000000 1b 27 3d 4f 5d 67 7d 80 95 a0 b0 c0 d4 e0 1b 27
	0000010 3d 4f 5d 67 7d 80 95 a0 b0 c0 d4 e0 1b 27 3d 4f
	0000020 5d 67 7d 80 95 a0 b0 c0 d4 e0 1b 27 3d 4f 5d 67
	0000030 7d 80 95 a0 b0 c0 d4 e0 1b 27 3d 4f 5d 67 7d 80
	0000040 95 a0 b0 c0 d4 e0 1b 27 3d 4f 5d 67 7d 80 95 a0
	0000050 b0 c0 d4 e0 1b 27 3d 4f 5d 67 7d 80 95 a0 b0 c0
	0000060 d4 e0 1b 27 3d 4f 5d 67 7d 80 95 a0 b0 c0 d4 e0
	0000070 1b 27 3d 4f 5d 67 7d 80 95 a0 b0 c0 d4 e0 1b 27
	0000080 3d 4f 5d 67 7d 80 95 a0 b0 c0 d4 e0 1b 27 3d 4f
	0000090 5d 67 7d 80 95 a0 b0 c0 d4 e0 1b 27 3d 4f 5d 67
	00000a0 7d 80 95 a0 b0 c0 d4 e0 1b 27 3d 4f 5d 67 7d 80
	00000b0 95 a0 b0 c0 d4 e0 1b 27 3d 4f 5d 67 7d 80 95 a0
	00000c0 b0 c0 d4 e0 1b 27 3d 4f 5d 67 7d 80 95 a0 b0 c0
	00000d0 d4 e0 1b 27 3d 4f 5d 67 7d 80 95 a0 b0 c0 d4 e0
	00000e0 1b 27 3d 4f 5d 67 7d 80 95 a0 b0 c0 d4 e0 1b 27
	00000f0 3d 4f 5d 67 7d 80 95 a0 b0 c0 d4 e0 1b 27 3d 4f
	0000100 5d 67 7d 80 95 a0 b0 c0 d4 e0 1b 27 3d 4f 5d 67
	0000110 7d 80 95 a0 b0 c0 d4 e0 1b 27 3d 4f 5d 67 7d 80
	0000120 95 a0 b0 c0 d4 e0 1b 27 3d 4f 5d 67 7d 80 95 a0
	0000130 b0 c0 d4 e0 1b 27 3d 4f 5d 67 7d 80 95 a0 b0 c0
	0000140 d4 e0 1b 27 3d 4f 5d 67 7d 80 95 a0 b0 c0 d4 e0
	0000150 1b 27 3d 4f 5d 67 7d 80 95 a0 b0 c0 d4 e0 1b 27
	0000160 3d 4f 5d 67 7d 80 95 a0 b0 c0 d4 e0 1b 27 3d 4f
	0000170 5d 67 7d 80 95 a0 b0 c0 d4 e0 1b 27 3d 4f 5d 67
	0000180 7d 80 95 a0 b0 c0 d4 e0

The repeating pattern `27 3d 4f 5d ...` suggest that the data was interpreted correctly.
