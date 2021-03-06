# RAOP-Player
RAOP player and library (AirPlay)

This is a RAOP (airplay) player and library for the v2 protocol (with synchro). It works for Windows, OSX, Linux x86 and ARM. 
There is a small player can can play raw pcm form any file or stdin (useful for use pipes with a decoder like lame, flac or ffmpeg)

The player is just and example how to use the library, but it has a few interesting options:

raop_play <options> <server_ip> <filename ('-' for stdin)>"

	[-ntp <file>] write current NTP in <file> and exit
	
	[-p <port number>]
	
	[-v <volume> (0-100)]
	
	[-l <latency> (frames] [-q <queue>(frames)]
	
	[-w <wait>]  (start after <wait> milliseconds)
	
	[-n <start>] (start at NTP <start> + <wait>)
	
	[-nf <start>] (start at NTP in <file> + <wait>)
	
	[-e (encrypt)]
	
	[-d <debug level>] (0 = silent)
	
	[-i (interactive)] (commands: 'p'=pause, 'r'=(re)start, 's'=stop, 'q'=exit)
	
It's possible to send synchronous audio to multiple players by using the NTP options (optionally combined with the wait option).
Either get the NTP of the master machine from any application and then fork multiple instances of raop_play with that NTP and
the same audio file, or use the -ntp option to get NTP to be written to a file and re-use that file when calling the instances of 
raop_play

Makesfiles are provided for OSX, Linux (x86 and ARM). Under Windows, I use Embarcadero C++, so I don't use makefile

You need pthread for Windows to recompile the player / use the library here: https://www.sourceware.org/pthreads-win32
ALAC codec is also needed from here: https://github.com/macosforge/alac

It's largely inspired from https://github.com/chevil/raop2_play but limit the playback to pcm as it focuses on creating a library and optimizing AirPlay synchronization 
