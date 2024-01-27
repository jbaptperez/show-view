# ShowView (VCR Controller Code)

## Target

Find a ShowView implementation that encodes/decodes ShowView codes of French TV guides.

The initial code source (anonymous, see [here](http://www.cryptome.org/vcrpp.c)) doesn't work as expected.

## Compilation

Using Linux or macOS, using `make`:

```bash
make        # Builds vcrpp1.
make clean  # Removes vcrpp1.
```

Manually: See the command of the *all* rule in the [Makefile](Makefile).

## Non-working example

Taking a French TV guide, the following program doesn't work:

| Parameter  | Value      | Comment                             |
|------------|------------|-------------------------------------|
| Year       | 1996       | Manually entered.                   |
| Month      | January    | Manually entered.                   |
| Day        | 25         |                                     |
| Channel    | Canal+     | Officially #4 but can be different. |
| Start time | 7:25       | AM.                                 |
| Duration   | 10 minutes |                                     |

The code in the TV guide is **3120361** but the command

```bash
./vcrpp1 -y 1996 -m 1 3120361
```

returns

```text
Program: January 25 1996, channel 56 (???), at 2 AM, duration 6:00.
```

If we try to encode all parameters (assuming channel 4):

```bash
./vcrpp1 -e -y 1996 -m 1 -d 25 -c 4 -t 725 -l 10
```

We get

```text
85997748  # Not 3120361
```

Trying to browse all channels doesn't help (no results):

```bash
for c in $(seq 1 100); do
    ./vcrpp1 -e -y 1996 -m 1 -d 25 -c $c -t 725 -l 10
done | grep 3120361
``````

## Resources

* [Wikipedia](https://en.wikipedia.org/wiki/Video_recorder_scheduling_code#cite_note-1)
* [1-8 digit source code directory](https://www.cs.cmu.edu/~dst/VCRPlus+/)
* [1-6 digit paper](http://files.righto.com/papers/vcr.ps)
* [1-6 digit paper - figure 1](http://files.righto.com/papers/vcr.fig1.ps)
* [1-6 digit paper - figure 2](http://files.righto.com/papers/vcr.fig2.ps)

Local links:

* [1-6 digit paper](vcr.ps)
* [1-6 digit paper - figure 1](vcr.fig1.ps)
* [1-6 digit paper - figure 2](vcr.fig2.ps)
