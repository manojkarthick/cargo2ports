# cargo2ports

Simple Python utility to generate a `cargo.crates` stanza for a MacPorts
Portfile from a Rust project's lockfile.

For example, taking in a `Cargo.lock` file that looks like this:

```
# This file is automatically @generated by Cargo.
# It is not intended for manual editing.
[[package]]
name = "ahash"
version = "0.3.4"
source = "registry+https://github.com/rust-lang/crates.io-index"
checksum = "9c251dce3391a07b43218ca070203ecb8f9f520d35ab71312296a59dbceab154"
dependencies = [
 "const-random",
]

[[package]]
name = "aho-corasick"
version = "0.7.10"
source = "registry+https://github.com/rust-lang/crates.io-index"
checksum = "8716408b8bc624ed7f65d223ddb9ac2d044c0547b6fa4b0d554f3a9540496ada"
dependencies = [
 "memchr",
]
...
```

...this utility will generate this:

```
cargo.crates \
    ahash                            0.3.4  9c251dce3391a07b43218ca070203ecb8f9f520d35ab71312296a59dbceab154 \
    aho-corasick                    0.7.10  8716408b8bc624ed7f65d223ddb9ac2d044c0547b6fa4b0d554f3a9540496ada \
    ansi_term                       0.11.0  ee49baf6cb617b853aa8d93bf420db2383fab46d314482ca2803b40d5fde979b \
    arrayref                         0.3.6  a4c527152e37cf757a3f78aae5a06fbeefdb07ccc535c980a3208ee3060dd544 \
    arrayvec                         0.5.1  cff77d8686867eceff3105329d4698d96c2391c176d5d03adc90c7389162b5b8 \
    atty                            0.2.14  d9b39be18770d11421cdb1b9947a45dd3f37e93092cbf377614828a319d5fee8 \
    autocfg                          1.0.0  f8aac770f1885fd7e387acedd76065302551364496e46b3dd00860b2f8359b9d \
    base64                          0.11.0  b41b7ea54a0c9d92199de89e20e58d49f02f8e699814ef3fdf266f6f748d15c7 \
    bitflags                         1.2.1  cf1de2fe8c75bc145a2f577add951f8134889b4795d47466a54a5c846d691693 \
    blake2b_simd                    0.5.10  d8fb2d74254a3a0b5cac33ac9f8ed0e44aa50378d9dbb2e5d83bd21ed1dc2c8a \
...
```

### Installation

Follow these steps to install `pipx` from MacPorts and install `cargo2ports` globally

```
sudo port install pipx
pipx install git+https://github.com/manojkarthick/cargo2ports.git
```

Note: Update your `$PATH` to add the pipx bin directory or update the `PIPX_BIN_DIR` environment variable.

### Usage

`cargo2ports ./Cargo.lock`

If you are already in a directory containing a `Cargo.lock` file, you run just the command with no parameters:

`cargo2ports`

If you would like to change the number of spaces each stanza line is indented by, use `-i`:

`cargo2ports -i 2 ./Cargo.lock`

You can also change the width of the field containing the name and version usin `-w`:

`cargo2ports -w 25 ./Cargo.lock`
