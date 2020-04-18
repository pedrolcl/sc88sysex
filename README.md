#sc88sysex 
sc88sysex is a Roland SC-88 System Exclusive Librarian, written as a Bash script for Linux.

Edit and run the provided script install.sh to install it. This script needs bash, amidi (from the ALSA utilities) and a few other command line utilities.

##Usage:
       sc88sysex [-v] [-h] [-p PORT] [-d DEVICEID] [-t TIMEOUT] {-a ADDRESS -z SIZE | -c COMMAND} [-r|-s FILENAME]

##OPTIONS
       -h     Prints a help message.

       -v     Prints more verbose messages.

       -p PORT
              Sets the raw MIDI port to which receive and send SYSEX messages.

       -d DEVICEID
              Sets the device number assigned to the SC-88 in the MIDI network.

       -t TIMEOUT
              Sets the number of seconds to wait for data before closing the receiving session.

       -a ADDRESS
              Sets the address of the system exclusive data to be transferred.  It can be a symbolic name or three hex constants. List of the predefined symbolic addresses: 
                    BULKDUMP INTDRINST INTDRMLST INTSNDLST

       -z SIZE
              Sets  the  size  of  the  system exclusive transfer. It can be a symbolic name or three hex constants. List of the predefined symbolic sizes:
                    ALL ALL1 ALL2 DRUMSET64 DRUMSET65 DRUMSETS GS1 GS2 SC55 SC88 
                    TONEBANK64 TONEBANK65 TONEBANKS

       -c COMMAND
              Sets a command to be sent to the SC-88 as a system exclusive message.  It can be a symbolic name or three hex constants. List  of  the predefined commands:
                    GMRESET GSRESET MODE1 MODE2

       -r FILE
              Save the receive data under this file name (optional).  If not specified, the file name is built upon the given address and size arguments.

       -s FILE
              Sends the contents of this file name.
            
##FILES
        ~/.sc88sysexrc 
            personal configuration

        /etc/sc88sysexrc 
            system wide configuration

        You  can  set  your preferred default options in a config file either in your home directory or as a global configuration file in /etc. The format is simply a set of lines
        having a expression of VARIABLE=value type. You can add more symbolic addresses, sizes and commands here.

        If you don't provide one, the following default options take effect:
            
        MIDIPORT="hw:0"    (MIDI Port: hw:0)
        DEVICEID=10        (Device ID: 10)
        TIMEOUT=3          (Timeout: 3 seconds)
        LIBDIR=~/SC88LIB   (Library directory: $HOME/SC88LIB)

##Examples:
        sc88sysex -a BULKDUMP -z ALL
            Sends a bulk dump request using the default  MIDI  port  to  the 
            SC-88,  and stores the received data in a file named 
            "sc88_bulkdump_all.syx"

        sc88sysex -c GSRESET
            Sends a GS reset command to the SC-88

        sc88sysex -s dump.syx
            Sends a data file "dump.syx" to the SC-88.

        sc88sysex -a '40 00 00' -z '00 00 04' -r deftune.syx
            Gets the master tune parameter from the SC-88  saving  it  on  a
            file named "deftune.syx"
