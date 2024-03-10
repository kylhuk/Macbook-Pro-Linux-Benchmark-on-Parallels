# Benchmarks of ARM Linux inside Parallels

## Motivation
I was going to use parallels to use a linux on my MacBook Pro. The device is owned by my employer which includes several Mobile Device Management (MDM) profiles. This is why I did not want to use the host system for private stuff, but instead run everything inside a linux. The distribution itself is not of matter, my focus was solely on performance. This is why I tested multiple distributions to find out, if there even is a noticable difference nowadays. To make sure others could profit as well, I wanted to make the results public.
If you have any recommendations for future tests, let me know by opening up an issue.

## Disclaimer
This is not a scientific test, as it was run on my device which has some mandatory software installed, so you might get different results, even if the hardware is the same. To minimize the effects of the desktop environment of the linux, the benchmarks were run in single-user mode (`systemctl rescue`). The software on the MacOS, which I was able to kill, was closed to reduce random impact on the performance.

## Benchmarks
For the benchmarks I used [Phoronix Test Suite (Github)](https://github.com/phoronix-test-suite/phoronix-test-suite/). The tests that were executed are all readily available in the testsuite [Workstation of OpenBenchmarking.org](https://openbenchmarking.org/suite/pts/workstation).

**Hardware**
MacBook Pro 14" (M3 Pro), 36GB Memory

**Software**
* MacOS: 14.3.1
* Parallels 19.3.0 (54924) (License limited to 4 cores)

* Fedora Linux 39 (Workstation Edition)
* Debian GNU/Linux 12 (bookworm)
* Arch Linux ARM

## Results
Test Date: 2024-03-09

| Test Name | Test Description | Value | Arch | Debian | Fedora |
|---|---|---|---|---|---|
| pts/parboil-1.2.1 | Test: OpenMP CUTCP | Seconds (less is better) | N/A | N/A | N/A |
| pts/rodinia-1.3.2 | Test: OpenMP LavaMD | Seconds (less is better) | 247.046 | 245.909 | 253.316 |
| pts/rodinia-1.3.2 | Test: OpenMP CFD Solver | Seconds (less is better) | 14.216 | 13.976 | 13.813 |
| pts/x265-1.3.0 | Video Input: Bosphorus 4K | FPS (more is better) | 2.07 | 4.68 | 5.25 |
| pts/x265-1.3.0 | Video Input: Bosphorus 1080p | FPS (more is better) | 8.89 | 24.30 | 24.29 |
| pts/himeno-1.3.0 | Poisson Pressure Solver | MFLOPS (more is better) | 9405.915608 | 9320.969418 | 9383.360189 |
| pts/swet-1.0.0 | Average | Ops per Second (more is better) | 762492084 | N/A | N/A |
| pts/sysbench-1.1.0 | Test: Memory | Events per Second (more is better) | N/A | 7937.14 | 8001.94 |
| pts/sysbench-1.1.0 | Test: CPU | Events per Second (more is better) | N/A | 39861.24 | 40148.02 |
| pts/git-1.1.0 |  | Seconds (less is better) | N/A | 37.367 | 35.115 |
| pts/brl-cad-1.5.0 |  | VGR Performance Metric (more is better) | N/A | N/A | N/A |

## Interpretation
Arch suffers from very bad video encoding results. Fedora seems to be the fastest one. As Fedora is a rolling release and tends to use bleeding edge software components, it might have some optimizations applied which Debian is missing. At the time of writing this, Debian Bookwork was released over 9 months ago. It is up to the viewer to decide which distribution fits their need the best.

## Future Work
As some tests were not running, it might be best to isolate the test suite in a docker container. This would also speed up the process of testing in the future.
