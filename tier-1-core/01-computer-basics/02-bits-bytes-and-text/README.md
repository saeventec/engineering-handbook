# 1.01.02 Bits, bytes and text

> **Tier:** 1 · Core  **Area:** Computer basics  **Status:** ✅ Done

## TL;DR
Everything in a computer is stored as **bits** (0 or 1), grouped into **bytes** (8 bits each).
Numbers are stored as binary. Text is stored in two steps: each character gets a number (its **Unicode code point**), and an **encoding** (almost always **UTF-8**) turns those numbers into bytes.
In Python, `str` is text and `bytes` is raw bytes. You convert between them with `.encode()` and `.decode()`, and you must use the same encoding both ways.

## Before you start
- [1.01.01 How a computer runs a program](../01-how-a-computer-runs-a-program/): memory, storage and the CPU.

## Why it matters
Garbled text like `CafÃ©` instead of `Café`, `UnicodeDecodeError` crashes, emoji breaking a database column, `0.1 + 0.2` not being `0.3`: all of these are bytes problems.
They show up when reading files, calling APIs and saving to databases, which is most of what software does.
Once you know how data becomes bytes, these bugs go from "magic" to a 2-minute fix.

## The idea

### Bits and bytes
A **bit** is the smallest piece of data: `0` or `1`. Hardware stores it as something with two states, like a high or low voltage.

A **byte** is 8 bits, like `01000001`. 8 bits can make 2⁸ = **256** different patterns, so one byte can hold a number from 0 to 255.
Bytes are the unit everything is measured in:

| Unit | Size | Feels like |
|---|---|---|
| 1 byte | 8 bits | one English letter |
| 1 KB (kilobyte) | 1,000 bytes | a short email |
| 1 MB (megabyte) | 1,000 KB | a photo |
| 1 GB (gigabyte) | 1,000 MB | a movie |

(You'll also see **KiB, MiB, GiB**, which use 1,024 instead of 1,000. The memory table in [1.01.01](../01-how-a-computer-runs-a-program/) uses them. The difference is small; just know both exist.)

### Binary: counting with 0 and 1
We count in **decimal** (base 10): each position is worth 10× the one to its right.
Computers use **binary** (base 2): each position is worth 2× the one to its right.

```
binary  1  0  1  0  1  0
worth  32 16  8  4  2  1   → 32 + 8 + 2 = 42
```

So `101010` in binary is 42. Python writes binary with a `0b` prefix: `0b101010`.

### Hexadecimal: a short way to write bytes
Binary is long and hard to read. **Hexadecimal** ("hex", base 16) is a shorter way to write the same thing.
It uses the digits `0–9` and then `a–f` for 10–15. One hex digit = 4 bits, so **one byte = exactly two hex digits**, from `00` to `ff` (0 to 255).
Python writes hex with a `0x` prefix: `0xff` is 255.

You'll see hex all the time: colors (`#ff5733`), memory addresses, error messages, hashes and IDs.

### Integers
An integer is stored as binary in a fixed number of bytes. Common sizes:

| Size | Range (signed: can be negative) |
|---|---|
| 8-bit (1 byte) | −128 to 127 |
| 32-bit (4 bytes) | about −2.1 billion to 2.1 billion |
| 64-bit (8 bytes) | about ±9.2 × 10¹⁸ |

If a value doesn't fit, you get an **overflow**: an error, or a number that wraps around to a wrong value.
This happens in real systems, for example when a database `INTEGER` ID column (often 32-bit) passes 2,147,483,647.

**Python is different:** its `int` has unlimited precision. It just uses more bytes as the number grows, so `2 ** 100` works fine.
But the moment you save to a database or send to another system, their size limits apply again.

### Decimals (floats)
Numbers with a decimal point, like `0.1`, are usually stored as **floats**: binary fractions with about 15–17 significant digits (the IEEE 754 standard, used by almost every machine).
Some simple decimals, like 0.1, can't be written exactly in binary, just like 1/3 can't be written exactly in decimal (0.333…).
So tiny errors appear: `0.1 + 0.1 + 0.1` is `0.30000000000000004`, not `0.3`.
Never use floats for money. That's covered in [2.20.02 Money and numbers](../../../tier-2-growth/20-cross-cutting-concerns/02-money-and-numbers/) (not written yet).

### Text, step 1: characters become numbers (Unicode)
A computer can't store "A". It can only store numbers. So we need a big agreed table: "A is 65, é is 233, € is 8364, 😀 is 128512…".
That table is **Unicode**. It covers almost every writing system, plus symbols and emoji.

- Each character's number is its **code point**, written like `U+0041` (hex for 65).
- Code points go from `U+0000` to `U+10FFFF`: about 1.1 million possible values. Only part of them are used so far.
- The first 128 code points are the same as **ASCII**, an old table that only covers English letters, digits and basic symbols.

### Text, step 2: numbers become bytes (encoding)
Code points can be big (128512 doesn't fit in one byte). So we need rules for turning code points into bytes. Those rules are called an **encoding**.
**Decoding** is the reverse: bytes back to text.

The encoding used almost everywhere today is **UTF-8**. It uses 1 to 4 bytes per character:

| Code points | Bytes | Examples |
|---|---|---|
| U+0000 – U+007F | 1 | `A`, `7`, `?` (all of ASCII) |
| U+0080 – U+07FF | 2 | `é`, `ñ`, Arabic, Hebrew |
| U+0800 – U+FFFF | 3 | `€`, Chinese, Japanese, most other scripts |
| U+10000 – U+10FFFF | 4 | 😀 and most other emoji |

Why UTF-8 won:
- **Plain English text is the same in ASCII and UTF-8**, byte for byte. Old files and tools keep working.
- Common text stays small, and it can still store every Unicode character.

Other encodings exist, mostly in older systems: **Latin-1** (also called ISO-8859-1), **Windows-1252**, **UTF-16** (used inside Windows and JavaScript).

### The golden rule: bytes don't know their encoding
A file or network message is just bytes. Nothing inside says "I'm UTF-8".
If you decode with a **different** encoding than the one used to encode, you get either:
- an **error** (`UnicodeDecodeError`), or worse,
- **mojibake**: wrong characters without any error, like `CafÃ©` for `Café`.

That's why file formats and protocols state the encoding: HTTP headers like `Content-Type: text/html; charset=utf-8`, or JSON, which must be UTF-8 when sent between systems (more in [1.09.02 JSON and serialization](../../09-apis/02-json-and-serialization/), not written yet).

### Text in Python: `str` vs `bytes`
- `str` is **text**: a sequence of Unicode code points. `"Café"`
- `bytes` is **raw bytes**: numbers 0–255. Written with a `b` prefix: `b"Caf\xc3\xa9"` (`\xc3` means "the byte with hex value c3").
- `.encode("utf-8")` turns `str` → `bytes`. `.decode("utf-8")` turns `bytes` → `str`.
- Python never mixes them silently: `"Café" + b"..."` raises a `TypeError`.

**Decode early, encode late.** The Python docs advise working with `str` inside your program: decode bytes as soon as they come in (file, network), and encode only when sending them out.

**Python 3.15 change:** Python now uses UTF-8 by default for files and terminal input/output, whatever the computer's settings.
Before 3.15, the default depended on the computer's language settings (its "locale"), so the same code could read a file fine on Linux and garble it on Windows.

## Example
Numbers as bits and bytes:

```python
import math

order_count = 42
print(bin(order_count))                      # → 0b101010
print(hex(255))                              # → 0xff
print(order_count.bit_length())              # → 6   (bits needed to store 42)
print(2 ** 8)                                # → 256 (values one byte can hold)
print((1000).to_bytes(2, "big"))             # → b'\x03\xe8'  (1000 as 2 bytes)
print((1000).to_bytes(2, "big").hex())       # → 03e8
print(2 ** 100)                              # → 1267650600228229401496703205376
print(0.1 + 0.1 + 0.1)                       # → 0.30000000000000004
print(0.1 + 0.1 + 0.1 == 0.3)                # → False
print(math.isclose(0.1 + 0.1 + 0.1, 0.3))    # → True  (compare floats like this)
```

Text as code points and bytes:

```python
for char in ["A", "é", "€", "😀"]:
    encoded = char.encode("utf-8")
    print(char, ord(char), hex(ord(char)), encoded, len(encoded))
# → A 65 0x41 b'A' 1
# → é 233 0xe9 b'\xc3\xa9' 2
# → € 8364 0x20ac b'\xe2\x82\xac' 3
# → 😀 128512 0x1f600 b'\xf0\x9f\x98\x80' 4

city = "Café"
data = city.encode("utf-8")
print(len(city), len(data))     # → 4 5   (4 characters, 5 bytes)
print(data)                     # → b'Caf\xc3\xa9'
print(data.decode("utf-8"))     # → Café
print(data.decode("latin-1"))   # → CafÃ©   (wrong encoding: mojibake, no error!)

"Café".encode("latin-1").decode("utf-8")
# → UnicodeDecodeError: 'utf-8' codec can't decode byte 0xe9 in position 3: unexpected end of data

"Café" + data
# → TypeError: can only concatenate str (not "bytes") to str
```

`ord()` gives a character's code point. `chr()` does the reverse: `chr(233)` → `'é'`.

Reading a file: always name the encoding.

```python
from pathlib import Path

customers_file = Path("customers.csv")
print(customers_file.read_text(encoding="utf-8"))
# → name,city
# → Zoë,Café
print(customers_file.read_bytes())
# → b'name,city\nZo\xc3\xab,Caf\xc3\xa9\n'
```

Same file, two views: `read_text` decodes it into `str`, and `read_bytes` shows the raw bytes on disk. Files are covered properly in [1.03.10](../../03-python/10-files-and-data-formats/) (not written yet).

## In real work
- **Use UTF-8 everywhere**: files, databases, APIs, HTML. If someone gives you data in another encoding, convert it to UTF-8 at the edge (when it comes in).
- **Write `encoding="utf-8"` explicitly** when opening files, even on Python 3.15. Your code may run on older Python versions, and it tells readers what to expect.
- **"Characters" ≠ "bytes".** A `VARCHAR(10)` column or a "max 280" limit may count bytes, code points or something else. Check what the system counts, especially for emoji and non-English names.
- **Seeing `Ã©`, `â€™` or `�`?** That's an encoding mismatch. Usually UTF-8 bytes were decoded as Latin-1/Windows-1252, or invalid bytes were replaced with `�`. Find where the bytes were decoded with the wrong encoding.
- **CSV files from spreadsheets and Windows tools** are a classic source of trouble: some are in an old encoding like Windows-1252, and some UTF-8 files start with an invisible marker called a **BOM** (byte order mark, bytes `ef bb bf`). Plain `"utf-8"` keeps it as a strange `\ufeff` character at the start of the text; `"utf-8-sig"` skips it.
- **Read hex calmly.** Error messages, hashes and network dumps show bytes in hex. Two hex digits = one byte.

## Common mistakes
- **Assuming 1 character = 1 byte.** True only for ASCII. `"Café"` is 4 characters but 5 bytes in UTF-8. Use `len(text.encode("utf-8"))` when you need the byte size.
- **Opening files without an encoding.** It worked on your machine, then breaks elsewhere. Pass `encoding="utf-8"`.
- **Fixing mojibake by encoding/decoding again and again until it looks right.** Find the one place where the wrong encoding was used and fix it there.
- **Comparing floats with `==`.** Use `math.isclose()`, and never use floats for money.
- **Mixing `str` and `bytes`.** Decode bytes to `str` as soon as they enter your program; encode only when sending them out.

## Check yourself
1. How many different values can one byte hold, and why?
   <details><summary>Answer</summary>256 (0 to 255), because a byte is 8 bits, and 2⁸ = 256.</details>
2. What's the difference between a code point and an encoding?
   <details><summary>Answer</summary>A code point is the number Unicode gives a character (é is U+00E9 = 233). An encoding is the rule for turning code points into bytes (UTF-8 turns é into the 2 bytes c3 a9).</details>
3. A customer's name shows up on your website as `JosÃ©`. What happened?
   <details><summary>Answer</summary>The name was stored as UTF-8 bytes, but somewhere they were decoded with a different encoding (likely Latin-1 or Windows-1252). Find that spot and decode as UTF-8.</details>
4. How many bytes does `"😀"` take in UTF-8? And `"hello"`?
   <details><summary>Answer</summary>4 bytes for the emoji; 5 bytes for "hello" (1 byte per ASCII character).</details>
5. Why can Python handle `2 ** 100`, but a database column might fail on a much smaller number?
   <details><summary>Answer</summary>Python's `int` grows to any size. Database columns have a fixed size (like 32 or 64 bits), so big values overflow.</details>

## Q&A
_No questions yet._

## Key takeaways
- A **bit** is 0 or 1; a **byte** is 8 bits (256 values, 0–255). **Hex** writes one byte as two digits (`00`–`ff`).
- Integers in most systems have a **fixed size** and can overflow; Python's `int` can't, but databases and other systems still can.
- **Floats** are binary fractions with tiny errors: compare with `math.isclose()`, and never use them for money.
- Text = **code points** (Unicode's number for each character) turned into bytes by an **encoding**. Use **UTF-8** (1–4 bytes per character).
- Bytes don't say their encoding. Decoding with the wrong one gives **mojibake** or `UnicodeDecodeError`.
- In Python, `str` is text and `bytes` is raw data: decode early, encode late, and always pass `encoding="utf-8"`.

## Sources
- [Python docs: Unicode HOWTO](https://docs.python.org/3/howto/unicode.html) (checked 2026-11-13)
- [RFC 3629: UTF-8, a transformation format of ISO 10646](https://www.rfc-editor.org/rfc/rfc3629) (checked 2026-11-13)
- [PEP 686: Make UTF-8 mode default](https://peps.python.org/pep-0686/) (checked 2026-11-13)
- [What's New in Python 3.15](https://docs.python.org/3.15/whatsnew/3.15.html) (checked 2026-11-13)
- [Python tutorial: Floating-point arithmetic, issues and limitations](https://docs.python.org/3/tutorial/floatingpoint.html) (checked 2026-11-13)
- [Python docs: Built-in types (int, bytes)](https://docs.python.org/3/library/stdtypes.html) (checked 2026-11-13)
- [Python docs: `codecs` (standard encodings, utf-8-sig, BOM)](https://docs.python.org/3/library/codecs.html) (checked 2026-11-13)
- [RFC 8259: The JSON data interchange format, section 8.1](https://www.rfc-editor.org/rfc/rfc8259#section-8.1) (checked 2026-11-13)
- [MDN: JavaScript `String` (UTF-16 code units)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String) (checked 2026-11-13)
- Example output: run locally on Python 3.15.2 (2026-11-13)
