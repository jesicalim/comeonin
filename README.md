# Comeonin [![Build Status](https://travis-ci.org/elixircnx/comeonin.svg?branch=master "Build Status")](https://travis-ci.org/elixircnx/comeonin) [![Hex.pm Version](http://img.shields.io/hexpm/v/comeonin.svg)](https://hex.pm/packages/comeonin)

Password hashing (bcrypt, pbkdf2_sha512) library for Elixir.

This library is intended to make it very straightforward for developers
to check users' passwords in as secure a manner as possible.

Comeonin supports `bcrypt` and `pbkdf2_sha512`.

## Features

* Comeonin uses the most secure, up-to-date hashing schemes.
* It uses the latest version of bcrypt, supporting the $2b$ prefix.
* It is easy to use.
    * There are several convenience functions to make checking passwords easier.
    * Salts are generated by default.
    * Each function has sensible, secure defaults.
* It provides excellent documentation.
    * Clear instructions are given on how to use Comeonin.
    * Several recommendations are also given to help developers keep their apps secure.

## Requirements

Elixir version 1.0 or later and Erlang/OTP version 17.0 or later.

You also need to have a C compiler, such as `gcc`, installed.

Ubuntu and Debian-based systems can get `gcc` and `make` by installing `build-essential` package. Also `erlang-dev` may be needed if not included in your Erlang/OTP version.

For users of Ubuntu, or any other Debian-based distro, we recommend downloading
erlang from [erlang solutions](https://www.erlang-solutions.com/downloads/download-erlang-otp),
as the version of erlang in the Ubuntu repositories is usually quite old.

## Installation

1. Add comeonin to your `mix.exs` dependencies

  ```elixir
  defp deps do
    [ {:comeonin, "~> 1.2"} ]
  end
  ```

2. List `:comeonin` as an application dependency

  ```elixir
  def application do
    [applications: [:logger, :comeonin]]
  end
  ```

3. Run `mix do deps.get, compile`

## Usage

Either import or alias the algorithm you want to use -- either `Comeonin.Bcrypt`
or `Comeonin.Pbkdf2`.

Both algorithms use similar naming conventions so as to make it easy to switch
between them. Both have the `hashpwsalt` function, which is a convenience
function that automatically generates a salt and then hashes the password.

To hash a password with the default options:

    hash = hashpwsalt("difficult2guess")

See each module's documentation for more information about
all the available options.

To check a password against the stored hash, use the `checkpw`
function. This takes two arguments: the plaintext password and
the stored hash:

    checkpw(password, stored_hash)

There is also a `dummy_checkpw` function, which takes no arguments
and is to be used when the username cannot be found. It performs a hash,
but then returns false. This can be used to make user enumeration more
difficult.

### Generating passwords and checking password strength

In the Comeonin.Password module, there are functions to generate random
passwords and to check passwords for password strength.

There is also a `create_hash` function in the main Comeonin module which
can be used to check a password for password strength before hashing it.

The password strength check consists of two options: a minimum length and
a check for punctuation characters and digits.

### Interacting with a database

The `create_user` function in the Comeonin module takes a map, removes the
"password" entry, checks the password for password strength (see the section
above for details), and then hashes the password and adds a "password_hash"
entry to the map. If there are no errors, it returns the new map.

## Documentation

http://hexdocs.pm/comeonin

## License

BSD. For full details, please read the LICENSE file.
