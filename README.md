# NAME

Data::Object::Role::Buildable

# ABSTRACT

Buildable Role for Perl 5

# SYNOPSIS

    package Vehicle;

    use Moo;

    with 'Data::Object::Role::Buildable';

    has name => (
      is => 'rw'
    );

    1;

# DESCRIPTION

This package provides methods for hooking into object construction of the
consuming class, e.g. handling single-arg object construction.

# SCENARIOS

This package supports the following scenarios:

## buildarg

    package Car;

    use Moo;

    extends 'Vehicle';

    sub build_arg {
      my ($class, $name) = @_;

      # do something with $name or $class ...

      return { name => $name };
    }

    package main;

    my $car = Car->new('tesla');

This package supports handling a `build_arg` method, as a hook into object
construction, which is called and passed a single argument if a single argument
is passed to the constructor.

## buildargs

    package Sedan;

    use Moo;

    extends 'Car';

    sub build_args {
      my ($class, $args) = @_;

      # do something with $args or $class ...

      $args->{name} = ucfirst $args->{name};

      return $args;
    }

    package main;

    my $sedan = Sedan->new('tesla');

This package supports handling a `build_args` method, as a hook into object
construction, which is called and passed a `hashref` during object
construction.

## buildself

    package Taxicab;

    use Moo;

    extends 'Sedan';

    sub build_self {
      my ($self, $args) = @_;

      # do something with $self or $args ...

      $args->{name} = 'Toyota';

      return;
    }

    package main;

    my $taxicab = Taxicab->new('tesla');

This package supports handling a `build_self` method, as a hook into object
construction, which is called and passed a `hashref` during object
construction. Note: Manipulating the arguments doesn't effect object's
construction or properties.

# AUTHOR

Al Newkirk, `awncorp@cpan.org`

# LICENSE

Copyright (C) 2011-2019, Al Newkirk, et al.

This is free software; you can redistribute it and/or modify it under the terms
of the The Apache License, Version 2.0, as elucidated in the ["license
file"](https://github.com/iamalnewkirk/data-object-role-buildable/blob/master/LICENSE).

# PROJECT

[Wiki](https://github.com/iamalnewkirk/data-object-role-buildable/wiki)

[Project](https://github.com/iamalnewkirk/data-object-role-buildable)

[Initiatives](https://github.com/iamalnewkirk/data-object-role-buildable/projects)

[Milestones](https://github.com/iamalnewkirk/data-object-role-buildable/milestones)

[Contributing](https://github.com/iamalnewkirk/data-object-role-buildable/blob/master/CONTRIBUTE.md)

[Issues](https://github.com/iamalnewkirk/data-object-role-buildable/issues)
