# Data Representation and Error Control

Reference file for the `computer-engineering` skill, covering NCEES knowledge
area 1 (data representation: number and character representation,
encoding/decoding, error detection and correction, compression)
[REF-NCEES-004]. Floating point is cited to IEEE 754-2019 [REF-IEEE-006];
error-correcting codes to Hamming (1950) [REF-PAPER-003], whose full text was
not read here — see the caution in §4.

## 1. Integer representation

**State radix, width, and signedness before every operation** (`SKILL.md`
rule 2). For an $n$-bit field:

| Representation | Range | Notes |
| --- | --- | --- |
| Unsigned | $0$ to $2^n - 1$ | Wraps modulo $2^n$ on overflow |
| Two's complement | $-2^{n-1}$ to $2^{n-1} - 1$ | Single zero; negate = invert and add 1; the dominant machine format |
| Sign-magnitude | $-(2^{n-1}-1)$ to $2^{n-1}-1$ | Two zeros; rare outside legacy formats |
| One's complement | $-(2^{n-1}-1)$ to $2^{n-1}-1$ | Two zeros; end-around carry; survives in the Internet checksum |
| Excess-$k$ (biased) | $-k$ to $2^n - 1 - k$ | Used for floating-point exponents |

**Overflow detection (two's complement addition):** overflow occurred if and
only if both operands have the same sign and the result's sign differs —
equivalently, carry-in to the sign bit ≠ carry-out of it. Unsigned overflow
is simply carry-out. Report which one the hardware flags: many ISAs expose
both a carry flag and an overflow flag, and confusing them is a classic
defect in hand-written arithmetic.

**Fixed point:** a $Qm.n$ value has $m$ integer bits and $n$ fraction bits
(conventions differ on whether the sign bit counts in $m$ — **state the
convention**). Resolution is $2^{-n}$; multiplication of two $Qm.n$ values
yields $Q2m.2n$ and must be re-scaled, with the rounding mode stated.

**Endianness:** state byte order for every multi-byte field that crosses a
bus, a network, or a file boundary. Network byte order in IETF protocols is
big-endian [REF-IETF-001]; most current microcontrollers are little-endian.
A struct copied straight from memory to a wire has the wrong byte order
unless the two happen to match.

## 2. Floating point — IEEE 754-2019

IEEE 754-2019 [REF-IEEE-006] "specifies interchange and arithmetic formats
and methods for binary and decimal floating-point arithmetic" and "exception
conditions and their default handling." Binary interchange formats consist
of a sign bit, a biased exponent field, and a trailing significand field;
the leading significand bit is implicit (1 for normal numbers, 0 for
subnormals). The widths below are the standard's basic binary formats:

| Format | Total bits | Exponent bits | Trailing significand bits |
| --- | --- | --- | --- |
| binary32 | 32 | 8 | 23 |
| binary64 | 64 | 11 | 52 |

**Practice points**, all consequences of the format rather than numbers to
memorise:

* **Precision is relative, not absolute.** Adjacent representable values
  are spaced by one unit in the last place (ulp), which scales with the
  magnitude. Adding a small value to a large one may change nothing.
* **Equality comparison of computed floats is a defect** unless the values
  are exactly representable and produced by identical operation sequences.
  Compare against a tolerance stated in the design.
* **Subnormals, infinities, and NaN** are part of the format. A pipeline
  that never checks for NaN propagates it silently into an actuator command.
* **Exceptions** (invalid, division by zero, overflow, underflow, inexact)
  have default results under the standard; an embedded target may trap
  instead. State which behaviour the toolchain configures.
* **Decimal formats exist** in the standard; do not assume "IEEE 754" means
  binary only when reading a datasheet or a spec.

Where a design needs guaranteed accuracy, do the error analysis in ulps of
the chosen format at the magnitudes actually encountered — do not quote a
"7 significant digits" rule of thumb as a guarantee.

## 3. Character representation and encoding

* **ASCII** is a 7-bit code; the 8th bit of a byte is either zero, parity,
  or a vendor extension — state which.
* **Unicode** assigns code points; **UTF-8, UTF-16, UTF-32** are encodings
  of them. UTF-8 is byte-oriented (no endianness), variable length (1–4
  bytes per code point), and ASCII-compatible in its single-byte range.
  UTF-16 and UTF-32 have endianness and may carry a byte-order mark.
* **A field sized in "characters" is under-specified.** Size buffers in
  bytes with the encoding stated; a 64-character name in UTF-8 can occupy
  256 bytes.
* **Line codes and serial framing** (NRZ, NRZI, Manchester, 8b/10b and
  similar DC-balanced codes) are chosen for clock recovery and DC balance
  on the physical link. State the code, its overhead (8b/10b costs 25 %),
  and its run-length limit when quoting a link's payload rate.

## 4. Error detection and correction

**Choose the code from the fault model** (`SKILL.md` rule 6) — single random
bit errors, burst errors of length $b$, or erasures — then report both the
guarantee and the blind spot.

### Parity

A single parity bit detects any odd number of bit errors and **no even
number**. It corrects nothing. Adequate only where the channel's error
model is dominated by single-bit events and a retry exists.

### Checksums

Additive checksums (including the one's-complement Internet checksum used
by IP [REF-IETF-001]) detect all single-bit errors and many multi-bit
errors, but are blind to some error patterns — for example, two errors that
cancel in the sum, or reordering of whole words. Their virtue is cheap
software computation, not detection strength.

### Cyclic redundancy check (CRC)

A CRC treats the message as a polynomial over GF(2) and appends the
remainder after division by a generator polynomial of degree $r$. Properties
that follow from the mathematics, independent of which polynomial is chosen:

* All burst errors of length $\leq r$ are detected.
* Any error pattern that is itself a multiple of the generator polynomial
  is **undetected** — that is the blind spot, and it always exists.
* Detection of specific classes (all odd-weight errors, all double-bit
  errors up to a given length) depends on the polynomial's factors and the
  message length. **Do not quote a "Hamming distance of the CRC" without
  citing the polynomial, the message length, and the source of the
  distance table** — the same polynomial's guarantees change with length.

Report the polynomial by its full hex representation *and* the convention
used (normal, reversed, or Koopman notation), the initial value, whether
input/output are reflected, and the final XOR. Two implementations that
agree on the "CRC-32" name but differ on any of these produce different
results.

### Hamming and block codes

Hamming (1950) [REF-PAPER-003] introduced systematic codes that correct
single errors, and the concept of minimum distance between codewords. The
general results attributed to that work — that a code with minimum distance
$d$ detects up to $d-1$ errors and corrects up to
$\lfloor (d-1)/2 \rfloor$, and that a single-error-correcting Hamming code
needs $r$ check bits for up to $2^r - r - 1$ data bits — are standard
coding-theory statements. **The paper's full text is paywall-blocked and
was not read for this repository; the attribution of these specific
statements to the paper is marked `REQUIRES VERIFICATION` (`TODO.md` §0.9).**
The statements themselves are consistent with every coding-theory
treatment, but cite them as "standard coding theory" rather than to a page
of Hamming until the item is closed.

**SECDED** (single-error-correct, double-error-detect) adds one overall
parity bit to a Hamming code and is the common choice for ECC memory. State
what happens on a detected-uncorrectable error: the hardware's response
(machine check, interrupt, silent flag) is a system-safety decision, not an
implementation detail.

### Choosing

| Fault model | Reasonable starting point | Report |
| --- | --- | --- |
| Rare single-bit, retry available | Parity or checksum | Blind to even-weight / cancelling errors |
| Bursts on a serial link or storage | CRC of degree $\geq$ burst length | Polynomial, conventions, length assumed |
| Random bit flips in memory, no retry | SECDED ECC | Response to uncorrectable error |
| Erasures or long bursts (storage, RF) | Interleaving plus a block code | Interleave depth, code parameters, source |

## 5. Compression

* **Lossless** (run-length, dictionary, entropy coding): the decompressed
  data is bit-identical. Required for code, configuration, and any
  measurement whose exact value matters. Compression ratio is
  data-dependent and can be **less than 1** on incompressible or
  already-compressed input — a buffer sized for "compressed" output must
  handle expansion.
* **Lossy** (transform-based audio/image/video coding): the decompressed
  data is an approximation. Never applied to telemetry, logs, or safety
  data without an explicit, reviewed statement of the acceptable error.
* **Entropy bound:** no lossless scheme can, on average, encode a source
  below its entropy in bits per symbol. A claimed ratio that beats the
  entropy of the source is a measurement error or a lossy scheme in
  disguise.
* Compression before encryption is the correct order for size; encryption
  before compression yields incompressible output. Compression of
  attacker-influenced data alongside secrets can leak the secret through
  the compressed length — a known class of side channel; flag it in any
  threat model (`SKILL.md` rule 7).
