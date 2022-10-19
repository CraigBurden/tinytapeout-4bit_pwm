# Dual output 4-bit complementary PWM

This is a basic 4-bit PWM with two channels and phase control

## Features:
* Dual independantly controlled channels
* Control of both set and reset values

## Applications
* Motor control
* Phase controlled PWM outputs
* LED controller

## Interface

### Input

| Signal   | Name        |
|----------|-------------|
| 0        | Clock       |
| 1        | Run/~Stop   |
| 2        | Address 0   |
| 3        | Address 1   |
| 4        | Data 0      |
| 5        | Data 1      |
| 6        | Data 2      |
| 7        | Data 3      |

### Output

| Signal   | Name               |
|----------|--------------------|
| 0        | NC                 |
| 1        | Channel A          |
| 2        | Inverted Channel A |
| 3        | NC                 |
| 4        | Channel B          |
| 5        | Inverted Channel B |
| 6        | NC                 |
| 7        | NC                 |

### Configuration
The registers are only accessable when the PWM is is stop mode. When in stop mode, any data present on the data lines will be clocked into the addressed register. The registers are as follows:

| Address | Name                      |
|---------|---------------------------|
| 0       | Channel A Reset Threshold |
| 1       | Channel A Set Threshold   |
| 2       | Channel B Reset Threshold |
| 3       | Channel B Set Threshold   |

#### Example 

Below is a sample of what the output of the module will look like for the following configuration:

| Register                  | Value   |
|---------------------------|---------|
| Channel A Reset Threshold | 11      |
| Channel A Set Threshold   | 0       |
| Channel B Reset Threshold | 8       |
| Channel B Set Threshold   | 5       |

```
|--------------------|----|----------------------------------------------------------------------------------------|
|                    |    |                                                                                        |
|                    | 15 |                 /|               /|               /|               /|               /| |
|                    | 14 |                / |              / |              / |              / |              / | |
|                    | 13 |               /  |             /  |             /  |             /  |             /  | |
|                    | 12 |              /   |            /   |            /   |            /   |            /   | |
|                    | 11 |             /    |           /    |           /    |           /    |           /    | |
|                    | 10 |            /     |          /     |          /     |          /     |          /     | |
|                    | 09 |           /      |         /      |         /      |         /      |         /      | |
|                    | 08 |          /       |        /       |        /       |        /       |        /       | |
|       Counter      | 07 |         /        |       /        |       /        |       /        |       /        | |
|                    | 06 |        /         |      /         |      /         |      /         |      /         | |
|                    | 05 |       /          |     /          |     /          |     /          |     /          | |
|                    | 04 |      /           |    /           |    /           |    /           |    /           | |
|                    | 03 |     /            |   /            |   /            |   /            |   /            | |
|                    | 02 |    /             |  /             |  /             |  /             |  /             | |
|                    | 01 |   /              | /              | /              | /              | /              | |
|                    | 00 |  /               |/               |/               |/               |/               | |
|                    |    |                                                                                        |
|--------------------|----|----------------------------------------------------------------------------------------|
|                    |    |                                                                                        |
|                    | HI |  -----------      -----------      -----------      -----------      -----------       |
|      Channel A     |    |             |    |           |    |           |    |           |    |           |    | |
|                    |    |             |    |           |    |           |    |           |    |           |    | |
|                    | LO |             |____|           |____|           |____|           |____|           |____| |
|                    |    |                                                                                        |
|--------------------|----|----------------------------------------------------------------------------------------|
|                    |    |                                                                                        |
|                    | HI |              ----             ----             ----             ----             ----  |
| Inverted Channel A |    |             |    |           |    |           |    |           |    |           |    | |
|                    |    |             |    |           |    |           |    |           |    |           |    | |
|                    | LO |  ___________|    |___________|    |___________|    |___________|    |___________|    | |
|                    |    |                                                                                        |
|--------------------|----|----------------------------------------------------------------------------------------|
|                    |    |                                                                                        |
|                    | HI |        --               --               --               --               --          |
|      Channel B     |    |       |  |             |  |             |  |             |  |             |  |         |
|                    |    |       |  |             |  |             |  |             |  |             |  |         |
|                    | LO |  _____|  |_____________|  |_____________|  |_____________|  |_____________|  |________ |
|                    |    |                                                                                        |
|--------------------|----|----------------------------------------------------------------------------------------|
|                    |    |                                                                                        |
|                    | HI |  -----    -------------    -------------    -------------    -------------    -------- |
| Inverted Channel B |    |       |  |             |  |             |  |             |  |             |  |         |
|                    |    |       |  |             |  |             |  |             |  |             |  |         |
|                    | LO |       |__|             |__|             |__|             |__|             |__|         |
|                    |    |                                                                                        |
|--------------------|----|----------------------------------------------------------------------------------------|
```
