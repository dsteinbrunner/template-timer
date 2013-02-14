# Template::Timer

Template::Timer provides inline timings of the time Template Toolkit
spends in template processing througout your code.  It's an overridden
version of Template::Context that wraps the process() and include()
methods.

Using Template::Timer is simple.

    my %config = ( # Whatever your config is
        INCLUDE_PATH    => "/my/template/path",
        COMPILE_EXT     => ".ttc",
        COMPILE_DIR     => "/tmp/tt",
    );

    if ( $development_mode ) {
        $config{ CONTEXT } = Template::Timer->new( %config );
    }

    my $template = Template->new( \%config );

Now when you process templates, HTML comments will get embedded in your
output, which you can easily grep for.

    <!-- TIMER START: process mainmenu/mainmenu.ttml -->
    <!-- TIMER START: include mainmenu/cssindex.tt -->
    <!-- TIMER START: process mainmenu/cssindex.tt -->
    <!-- TIMER END: process mainmenu/cssindex.tt (0.017279 seconds) -->
    <!-- TIMER END: include mainmenu/cssindex.tt (0.017401 seconds) -->

....

    <!-- TIMER END: process mainmenu/footer.tt (0.003016 seconds) -->
    <!-- TIMER END: include mainmenu/footer.tt (0.003104 seconds) -->
    <!-- TIMER END: process mainmenu/mainmenu.ttml (0.400409 seconds) -->

# INSTALLATION

To install this module, run the following commands:

    perl Makefile.PL
    make
    make test
    make install


# COPYRIGHT AND LICENSE

Copyright 2005-2013 Andy Lester.

This program is free software; you can redistribute it and/or modify
it under the terms of the Artistic License v2.0.

See http://www.perlfoundation.org/artistic_license_2_0 or the LICENSE.md
file that comes with the ack distribution.