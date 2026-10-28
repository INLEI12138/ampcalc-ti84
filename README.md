# AMPCALC — Op-amp frequency response calculator for TI-84 Plus CE

A TI-BASIC program that computes the gain, dB and phase of an **inverting** or **non-inverting** op-amp stage whose input impedance (Zin) and feedback impedance (Zf) are built from series/parallel R, L and C — for a single frequency, or as a full Bode magnitude + phase plot.

一个 TI-84 Plus CE 上的 TI-BASIC 程序:选择反相/同相运放,用串并联的 R、L、C 组成 Zin 和 Zf,计算单个频率下的增益、dB、相位,或绘制幅频/相频 Bode 图。

## Features / 功能

- Inverting `H = -Zf/Zin` or non-inverting `H = 1 + Zf/Zin`
- Zin and Zf each: series R, L, C **plus** a parallel R, L, C branch (12 values total)
- Menu-driven input with back-edit (view / re-enter any group), and a formula page showing how the result is computed
- Unit suffixes: `10K`, `4.7K`, `1UF`, `100NF`, `1NH`, `2MEG`, `P N U M K G T` (a trailing `F`/`H` is ignored)
- Single-frequency result: gain, dB, phase
- Bode plot with auto-suggested frequency range (from detected corner/resonance frequencies) or manual range
- Plot annotations: `10^n` axis labels, MAX/MIN, −3 dB line, and the −3 dB frequency (`F3DB`) when the response has one
- Phase unwrapping; vectorised list computation for speed

## Install / 安装

1. Send `AMPCALC.8xp` to the calculator with TI Connect CE (or copy `AMPCALC.txt` into a new program in the TI Connect CE editor and send that).
2. Set **MODE** to `Degree` and `a+bi` (the program sets Degree itself; `a+bi` must be set manually).
3. `PRGM` → `AMPCALC` → `ENTER`.

> TI Connect CE tip: if the transfer fails with "Calculator is Busy", exit the running program to the home screen first.

## Usage / 使用

1. Choose **INVERTING** or **NON-INVERTING**.
2. `1 ENTER ZIN` and `2 ENTER ZF`: enter the six values for each (series R, L, C, then parallel R, L, C). Type `0` for anything absent.
3. `3 VIEW/EDIT` to check or correct a group, `4 FORMULA` for the equations, `5 RUN` to calculate.
4. Pick **SINGLE FREQ** or **BODE PLOT** (then AUTO or MANUAL range).

### Example / 示例

Inverting RC low-pass: `Zin = R1 = 10K`, `Zf = R2 ∥ C2 = 100K ∥ 0.1UF`

| Quantity | Expected | Program |
|---|---|---|
| Low-frequency gain | −R2/R1 = −10 (20 dB) | 20 dB |
| fc = 1/(2π R2 C2) | 15.92 Hz | F3DB = 15.92 |
| Phase | 180° → 90° | 179.43° → 90.06° |

The calculator asks for one value per line. For ZIN enter `10K`, then `0` for the other five; for ZF enter `0, 0, 0` (series R, L, C), then `100K`, `0`, `0.1UF` (parallel R, L, C).

![Example Bode plot](images/example_rc_lowpass.png)

*Bode plot for the example above, computed with the same equations as the program (rendered on a PC, not a screenshot of the calculator).*

## Notes and limits / 注意事项

- `F3DB` is only meaningful when the response is flat then drops/rises by 3 dB. For monotonically falling/rising responses or notch/resonance circuits it is just the first point 3 dB away from the start value.
- Ideal op-amp (infinite gain, no bandwidth limit); ideal R, L, C.
- Auto range extends two decades beyond the detected corner frequencies, up to 300 points; large ranges take about a minute to draw. Use MANUAL to reduce points.
- Uses lists `L₁`–`L₆` and single-letter variables, so it will overwrite them.
- The Bode plot draws with `Line(`, and colours with `TextColor(` / coloured `Vertical`, so it needs a colour **CE** model.

## Files

- `AMPCALC.8xp` — program for the calculator
- `AMPCALC.txt` — readable source (for TI Connect CE editor / TI-Planet SourceCoder)

## License

MIT
