## Writeup

The intent of this project is to gain a basic understanding of control. A PID controller is one
algorithm used to accomplish this task. PID is an acronym and is described below.

```
P - proportion
I - integral // sum
D - derivative // differential
```

The equation used to control the steering angle is as follows:
```
                 |- p term -|   |- d term -|         |- i term -|
steering_angle = -tau_p * CTE - tau_d * d/dt (CTE) - tau_i * sum(CTE)
```

The proportional gain or `P` term can be thought of as the magnitude of change. The higher the
proportional gain, the more aggressive a correction the car will make.

The derivative or differential gain (the `D` term) can be thought of as the rate of the change. The
higher the `D` term, the more quickly or even jerky the correction will be made, while the lower the
gain, more slowly the correction will be made.

The integral or summed gain (the `I` term) is a running total of the error and helps account for
bias in the system (drift is the example given during the lectures). Very small values produced the
best results in the trial and error runs I tested, leading me to believe that the simulator does not
actively account for this. In the final solution, this gain is ignored completely.

Through a manual approach (inspired by Twiddle and bisection) the parameters were manually tuned.

*Note: all gains are negative.
|  P  |  I  |  D  |
|-----|-----|-----|
| 1.0 | 0.0 | 0.0 |
| 0.1 | 0.0 | 0.0 |
|0.07 | 0.0 | 0.25| Not reacting strong enough post-bridge
|0.05 | 0.0 | 0.17| Not reacting strong enough post-bridge
|0.055| 0.0 | 1.0 | handling v well. not making turns strong enough.
|0.10 | 0.0 | 1.0 | makes it around the track!
|0.10 | 0.0 | 10.0| A more stable run around the track

To run:
```
$ cmake .. && make && ./pid -0.10 0.0 -10.0
```

