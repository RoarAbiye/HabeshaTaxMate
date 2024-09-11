# Income Tax and Pay Calculator CLI

This project provides a command-line interface (CLI) tool for calculating income tax, net pay, and gross pay based on specific parameters. The CLI allows users to input values such as gross pay, net pay, pension, conveyance, and transportation allowances to determine tax obligations and salary breakdowns.

## Features

- **Income Tax Calculation**: Calculate income tax based on a progressive tax rate.
- **Net Pay Calculation**: Determine the net pay by accounting for income tax, pension, and other allowances (conveyance and transportation).
- **Gross Pay Calculation**: Estimate the gross pay from a given net pay.
  
### Commands

- **income-tax**: Calculate income tax based on gross pay.
- **net-pay**: Calculate net pay by subtracting income tax and optional deductions like pension and allowances from gross pay.
- **gross-pay**: Calculate gross pay from a given net pay by iteratively solving for gross income using income tax, pension, and other optional allowances.

## Prerequisites

- [Node.js](https://nodejs.org/en/) installed on your machine.
- Package manager like `npm` or `yarn`.

## Installation

1. Clone this repository:
   ```bash
   git clone https://github.com/RoarAbiye/HabeshaTaxMate.git
   cd HabeshaTaxMate
   ```

2. Install dependencies:
   ```bash
   npm install
   ```

3. Run the script:
   ```bash
   node taxet --help
   ```

## Usage

The CLI supports multiple commands and options:

### 1. Income Tax Calculation

Calculate the income tax based on gross pay:

**Linux**
```bash
./taxet income-tax --gross <gross-amount>
```

**Linux**
```bash
taxet income-tax --gross <gross-amount>
```
#### Options:
- `--gross`, `-g`: Gross pay (required).

### 2. Net Pay Calculation

Calculate net pay by subtracting income tax, pension, and optional allowances from gross pay:

```bash
./taxet net-pay --gross <gross-amount> [--pension] [--conveyance] [--transport]
```

#### Options:
- `--gross`, `-g`: Gross pay (required).
- `--pension`, `-p`: Include pension deduction (optional).
- `--conveyance`, `-c`: Include conveyance allowance for employees (optional).
- `--transport`, `-t`: Include transportation allowance (optional).

### 3. Gross Pay Calculation

Estimate gross pay from a given net pay:

```bash
./taxet gross-pay --net <net-amount> [--pension] [--conveyance] [--transport]
```

#### Options:
- `--net`, `-n`: Net pay (required).
- `--pension`, `-p`: Include pension in calculation (optional).
- `--conveyance`, `-c`: Include conveyance allowance (optional).
- `--transport`, `-t`: Include transportation allowance (optional).

## Example

Calculate net pay for a gross pay of 5000 with pension and transport allowances:

```bash
./taxet net-pay --gross 5000 --pension --transport
```

Output:
```
Net Pay:          4,500.00 ETB
```

## License

This project is licensed under the MIT License.

---

For more detailed usage, run the help command:
```bash
./taxet --help
```
