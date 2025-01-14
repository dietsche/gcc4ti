
           GCC4TI Cross Compiler for the TI-89 and TI-92 Plus v0.96 Beta 10
          ================================================================

Xavier Vassor       Xavier@tigcc.ticalc.org    (original linker and tigcc)
Zeljko Juric        Zeljko@tigcc.ticalc.org    (library and documentation)
Kevin Kofler        Kevin@tigcc.ticalc.org     (linker, fixes for A68k, GCC,
                                                GAS, library, ...)
Sebastian Reichelt  Sebastian@tigcc.ticalc.org (linker, IDE, GCC fixes)
Niklas Brunlid      Niklas@tigcc.ticalc.org    (bugfixes and additions)
Jean Canazzi        Jean@tigcc.ticalc.org      (first modification of GCC)
Philipp Winkler     p.winkler@atn.nu           (library help file conversion)

Lionel Debroux      lionel_debroux@yahoo.fr  
Patrick Pelissier   patrick.pelissier@gmail.com
Manoel Trapier      godzil@godzil.net

Email us at:        tigccpp@box.godzil.net


                      +-------------------------------+
                      |        README CONTENTS        |
                      |===============================|
                      |  1. Disclaimer                |
                      |  2. About GCC4TI              |
                      |  3. Installation              |
                      |  4. The Library               |
                      |  5. The Command Line Compiler |
                      |  6. The IDE                   |
                      |  7. Examples                  |
                      |  8. Bug Reports               |
                      |  9. History                   |
                      +-------------------------------+

1. Disclaimer
-------------

Original files Copyright (C) 1999-2005 Xavier Vassor, Niklas Brunlid,
                                       and Jean Canazzi
ld-tigcc Copyright (C) 2002-2009 Sebastian Reichelt and Kevin Kofler
Library & Documentation Copyright (C) 2000-2009 Zeljko Juric and contributors
IDE Copyright (C) 2000-2009 Sebastian Reichelt and contributors
TIGCC Tools Suite Copyright (C) 2000-2009 Thomas Nussbaumer
                                          (http://tict.ticalc.org/)

Included programs with different licenses:
A68k Copyright (C) 1987-2009 Charlie Gibbs, David Ellsworth, Kevin Kofler,
                             Julien Muchembled, and Paul Froissart

Setup executable created using NSIS (http://nsis.sourceforge.net) and
compressed using LZMA (http://www.7-zip.org/sdk.html) for the data and UPX
(http://upx.sourceforge.net/) for the stub.

This program is free software; you can redistribute it and/or modify it under
the terms of the GNU General Public License as published by the Free Software
Foundation; either version 2 of the License, or (at your option) any later
version.

This program is distributed in the hope that it will be useful, but WITHOUT
ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS
FOR A PARTICULAR PURPOSE. See the GNU General Public License for more
details.

You should have received a copy of the GNU General Public License along with
this program; if not, write to the Free Software Foundation, Inc.,
59 Temple Place - Suite 330, Boston, MA 02111-1307, USA.

Some components (TIGCCLIB, ttpack, pstarter) have additional permissions
beyond the GPL.

A different license applies to A68k.


2. About GCC4TI
--------------

GCC4TI is a fork ( http://en.wikipedia.org/wiki/Fork_(software_development) )
of TIGCC, with different goals and different planning.

Please check out http://trac.godzil.net/gcc4ti/ , the official GCC4TI site,
for more information on the todo/wish list.

3. Installation
---------------

In the ZIP file containing GCC4TI, you will find a program called
'setup-gcc4ti.exe'. Run this program and follow the instructions of the setup
program. It will add a few new items to your start menu, so you should not
use a program group that already exists.

If you want to uninstall GCC4TI, you can do this at any time from either the
start menu or the control panel. Please be aware that this will remove the
whole folder in which the program was installed, not only the files which
were installed by the setup program.

If you experience any problems installing GCC4TI, or running it after it has
been installed, please use the GCC4TI mailing list, tigccpp@box.godzil.net .

4. The Library
--------------

The library included in this release of GCC4TI is a collection of over 750
functions. With this library, it is possible to create kernel-free (so-called
"nostub") programs as well as programs that make use of kernel features. A
very detailed documentation in HTML Help format is included, in which more
than 600 TIOS entries are described in detail. This documentation may be very
valuable for assembly programmers too. To read the documentation, open
'tigcc.chm', located in the 'Doc' folder, or click on the appropriate item in
the start menu.

5. The Command Line Compiler
----------------------------

The following paragraphs apply only to the command line compiler. If you want
to use the IDE instead, you do not need to worry about these topics.

The command line compiler (tigcc.exe) works almost the same way that the
standard gcc.exe does. Aside from accepting .asm files as parameters and
calling the a68k assembler to compile them, it also supports a few
non-standard options:

-pack <varname>
  Compress the file generated during compilation. 'varname' is the name of
  the on-calc packed variable. Although 'varname' cannot have an extension,
  the variable on the calculator will always have the extension 'ppg'.
  'varname' cannot be the same as the on-calc name of the program itself.
  When you use this switch, two variables will be created; one with the
  extension '.89y' or '.9xy', and one '.89z' or '.9xz' variable.
  This option comes from Thomas Nussbaumer's (thomas.nussbaumer@gmx.net)
  excellent TIGCC Tools Suite, where this feature is called "ExePack
  Technology." You can read about it on the official TI-Chess Team site
  (tict.ticalc.org).

-q
  Keep as quiet as possible while assembling and linking. This option is not
  needed by the compiler because it is always quiet, but the linker and
  especially the assembler output some information.

-v0
  This switch is an addition to the '-v' switch. It tells tigcc.exe to output
  only the commands that are run directly. This was the default in some
  previous releases.

-g
  The '-g' switch in GCC turns on debugging information in the preferred
  format for the target. In GCC4TI, this is DWARF 2, which can be used with a
  GDB-enabled TiEmu.

-standalone
  Do not link against tigcc.a. All of GCC's internal functions are
  implemented in this library, as well as all non-TIOS functions. Using one
  of these will result in an error from the linker.

-ar
  Create an archive (a static library) instead of a program. The resulting
  file will have a '.a' ending.

-bsr
  This option is ignored for compatibility.

For more info about standard options that are recognized by the compiler,
have a look at the GCC4TI Documentation, or visit
http://gcc.gnu.org/onlinedocs/gcc_3.html.

In addition, you can use '-WA,...' instead of '-Wa,...' to pass options to
the A68k assembler.

We suggest that you use the '-O2' or '-Os' switch in all your compilations;
it increases speed and decreases the program size at the cost of compilation
time.

There is an important difference to the standard gcc.exe: tigcc.exe always
overwrites assembly or object files. For example, if a file 'test.c' is
compiled, the files 'test.s' and 'test.o' will be created and overwritten if
necessary, but they will automatically be deleted again if neither '-c' or
'-S' nor '-g' are specified.

6. The IDE
----------

Documentation of the IDE is included in the manual and will be installed by
the setup program. You can access it from the start menu or from the IDE
itself.

7. Examples
-----------

There are some examples made by Zeljko Juric in the folder "Examples". You
can compile and modify them to learn how to use GCC4TI. Most of them can also
be found at some place in the documentation, with explanations and in some
sort of context.

8. Bug Reports
--------------

There may still be some bugs in the linker, in tigcc.exe, and in the IDE. If
you encounter a bug, please use the GCC4TI mailing list, tigccpp@box.godzil.net

9. History
-----------

See http://tigcc.ticalc.org/doc/info.html#history for the TIGCC history.
