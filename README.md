# teensy ADAT toslink output
ADAT Toslink output for Teensy 3.1/3.2 

What I've created here is a Teensy ADAT Toslink optical output encoder.
The ADAT signal can carry 8 channels of 24bits audio at 44.1kHz or 48kHz. The Teensy audio library defaults to 16 bit 44.1kHz audio which is stuffed in the 24bits. Internally is uses a I2S masterclock which can be changed in the sourcecode to support 48kHz. SMUX is not yet implemented, but should be doable.

The encoding is done using NZRI encoding in packets of 8 bit for which 4 lookup tables are made, so that the memory needed for the lookup for NZRI encoding is 4KB. In the encoding of a frame (containing 8ch 16 bit audio) a frame contains 256 bits, which is twice the datarate of the SPDIF output in the Teensy audio library. In order to support that I used multipliers at a samplerate speed twice as high as compared to the SPDIF example. There is a lot bitshifting and XORring involved, so the ADAT output object is relatively CPU-expensive to use (I guess). I am relatively new to C++ and the Teensy, so if anyone has some optimalisations or improvements, please let me know!

Happy audio programming for the Teensy!
