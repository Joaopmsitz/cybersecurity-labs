# Activity 4.2 — Solving Simple Cryptography Challenges with CyberChef

## Objective

Use CyberChef to automate the decoding of a long Morse-code message. The activity demonstrates how a sequence of text transformations can normalize encoded data before decoding it into a readable representation.

## Tool

- [CyberChef — GCHQ](https://gchq.github.io/CyberChef/)

The exercise provides a Morse-like input in which the elements are represented by the strings `di`, `dit`, and `dah`. These elements must first be normalized into the conventional dot-and-dash representation.

## Procedure

The original encoded block was copied from the course material into CyberChef's Input panel. The following operations were added to the recipe in sequence.

### 1. Remove the separators

Add **Find / Replace**.

Configuration:

| Parameter | Value |
|---|---|
| Find | `-` |
| Find type | REGEX |
| Replace | Empty |
| Global match | Enabled |
| Multiline matching | Enabled |

This removes the hyphen characters used as separators in the original representation.

### 2. Convert `di` and `dit` into dots

Add another **Find / Replace** operation.

Configuration:

| Parameter | Value |
|---|---|
| Find | `(dit?)` |
| Find type | REGEX |
| Replace | `.` |
| Global match | Enabled |
| Multiline matching | Enabled |

The regular expression matches `di` and `dit`, allowing both forms to be converted into the Morse dot symbol.

### 3. Convert `dah` into dashes

Add a third **Find / Replace** operation.

Configuration:

| Parameter | Value |
|---|---|
| Find | `dah` |
| Find type | REGEX |
| Replace | `-` |
| Global match | Enabled |
| Multiline matching | Enabled |

The input is now normalized into a representation containing Morse dots and dashes.

### 4. Decode the Morse code

Add **From Morse Code**.

Configuration:

| Parameter | Value |
|---|---|
| Letter Delimiter | Space |
| Word Delimiter | Line Feed |

This operation translates the normalized Morse sequences into their decoded representation.

### 5. Convert the hexadecimal result into text

The activity's Morse decoding stage produces hexadecimal data. Two additional operations are required.

First, add **Drop Bytes**:

| Parameter | Value |
|---|---|
| Start | 0 |
| Length | 2 |

Then add **From Hex**:

| Parameter | Value |
|---|---|
| Delimiter | Auto |

The resulting recipe converts the decoded hexadecimal sequence into readable text.

## Result

The final output recorded for the activity was:

    Wp*lXtGQ8e8qnmMYU*svFHkjIt*RQ&JpZvjm!%%KDkfp#^N9fk4dU4lB3rToT0PZQmCQEKYB4ZMv*!Fk8l
    %bjqlPMfIGma%%FzG gigem{C1icK_cl1CK-y0u_h4v3_m4I1}
    uv4vzKZt4yomiDShLm8QEFnUtwJ@NuOYfX&8u@Gn!1%Tqv0VcRzV!j!vuup8BjdNIqE5w#$%V4UZOYZ2z7
    T25t7&xL@WO7410QI

The recognizable string within the result is:

    gigem{C1icK_cl1CK-y0u_h4v3_m4I1}

The activity's objective was to automate the transformations and recover the final output, rather than manually translating the long Morse sequence.

## Technical notes

The order of the operations is important. The Find / Replace steps normalize the custom representation, From Morse Code performs the Morse decoding, and the final byte and hexadecimal operations convert the result into text.

Changing the order or the regular expressions can prevent the recipe from producing the expected output.

## Evidence

[View Universal Class Evidence PDF — Page 2](../evidences.pdf)
