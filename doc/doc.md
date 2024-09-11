# Income Tax and Pay Calculator CLI Documentation

This project is a command-line tool written in Node.js that provides functionalities to calculate income tax, net pay, and gross pay based on various inputs such as gross salary, net salary, pension contributions, conveyance, and transport allowances. This tool is designed to help users quickly compute these values using simple commands and options.

## Table of Contents

1. [Features](#features)
2. [Prerequisites](#prerequisites)
3. [Installation](#installation)
4. [Usage](#usage)
    - [Commands](#commands)
        - [income-tax](#income-tax-command)
        - [net-pay](#net-pay-command)
        - [gross-pay](#gross-pay-command)
    - [Options](#options)
        - [--gross](#gross-option)
        - [--net](#net-option)
        - [--pension](#pension-option)
        - [--conveyance](#conveyance-option)
        - [--transport](#transport-option)
5. [Calculation Logic](#calculation-logic)
6. [Examples](#examples)
7. [License](#license)

## Features

- **Income Tax Calculation**: Calculates income tax based on progressive tax rates.
- **Net Pay Calculation**: Computes net pay by deducting income tax, pension, and allowances from gross salary.
- **Gross Pay Estimation**: Reverses the process by calculating gross salary from net pay.
- **Supports Pension Contributions**: Optionally includes pension contributions in both net and gross pay calculations.
- **Handles Allowances**: Supports conveyance and transport allowances.

## Prerequisites

- [Node.js](https://nodejs.org) installed on your machine.
- Package manager like `npm` or `yarn`.

## Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/your-username/income-tax-calculator.git
   cd HabeshaTaxMate
   ```

2. Install required dependencies:
   ```bash
   npm install
   ```
3. Run the script to check if everything is working:

**Windows**:
```bash
To run the application on Windows, execute the batch file:
```
```bash
taxet.bat
```
**Linux**:
```bash
# On Linux, make the `taxet` file executable:
```
```bash
chmod +x taxet
./taxet
```


## Usage

**Windows**:
```bash
Run the tool by executing `taxet.bat` in the command line.
```

**Linux**:
```bash
Run the tool by executing `./taxet` in the terminal.
```
The tool provides several commands to perform different types of salary and tax calculations. Each command accepts specific options.

### Commands

#### 1. `income-tax` Command

The `income-tax` command calculates the income tax based on the given gross salary using the Ethiopian progressive tax rates.

```bash
./taxet income-tax --gross <gross-amount>
```

- **Description**: This command computes the amount of income tax for a given gross salary based on a tiered tax system.

**Options**:
- `--gross`, `-g` (required): Specifies the gross salary to calculate the income tax for.

##### Example:

```bash
./taxet income-tax --gross 5000
```

**Output**:
```
Income Tax:         695.00 ETB
```

#### 2. `net-pay` Command

The `net-pay` command calculates the net salary by subtracting income tax, pension, and optional allowances (conveyance and transport) from the gross salary.

```bash
./taxet net-pay --gross <gross-amount> [--pension] [--conveyance] [--transport]
```

- **Description**: Computes net salary after deductions and allowances.

**Options**:
- `--gross`, `-g` (required): Specifies the gross salary.
- `--pension`, `-p` (optional): Deduct pension contributions (7% of gross salary).
- `--conveyance`, `-c` (optional): Includes conveyance allowance for employees using transport during work.
- `--transport`, `-t` (optional): Adds a fixed transport allowance (600 ETB for work-home transport).

##### Example:

```bash
./taxet net-pay --gross 5000 --pension --transport
```

**Output**:
```
Net Pay:         4,420.00 ETB
```

#### 3. `gross-pay` Command

The `gross-pay` command calculates gross salary based on a given net salary by reversing the income tax, pension, and allowances.

```bash
./taxet gross-pay --net <net-amount> [--pension] [--conveyance] [--transport]
```

- **Description**: Estimates the gross salary required to achieve a specified net salary.

**Options**:
- `--net`, `-n` (required): Specifies the net salary.
- `--pension`, `-p` (optional): Considers pension deduction when calculating gross pay.
- `--conveyance`, `-c` (optional): Includes conveyance allowance.
- `--transport`, `-t` (optional): Adds transportation allowance to the calculation.

##### Example:

```bash
./taxet gross-pay --net 4000 --pension --conveyance
```

**Output**:
```
Gross Pay:         5,230.00 ETB
```

### Options

These are the available options across the commands:

#### --gross Option

- **Flag**: `--gross`, `-g`
- **Description**: Specifies the gross salary amount for calculations.
- **Type**: `number`
- **Required**: Yes (for `income-tax` and `net-pay` commands)

#### --net Option

- **Flag**: `--net`, `-n`
- **Description**: Specifies the net salary amount for calculations.
- **Type**: `number`
- **Required**: Yes (for `gross-pay` command)

#### --pension Option

- **Flag**: `--pension`, `-p`
- **Description**: Includes pension contribution (7% of gross salary) in calculations.
- **Type**: `boolean`
- **Required**: No (optional)

#### --conveyance Option

- **Flag**: `--conveyance`, `-c`
- **Description**: Includes conveyance allowance for employees using transport during work.
- **Type**: `boolean`
- **Required**: No (optional)

#### --transport Option

- **Flag**: `--transport`, `-t`
- **Description**: Includes a fixed transport allowance of 600 ETB for commuting between home and work.
- **Type**: `boolean`
- **Required**: No (optional)

## Calculation Logic

1. **Income Tax**: 
   The income tax is calculated using a tiered tax system. For example:
   - Gross pay up to 600 ETB: 0% tax.
   - Gross pay from 600 to 1650 ETB: 10% tax minus 60 ETB.
   - The tax rate increases progressively up to 35% for salaries over 10,900 ETB.

2. **Pension Deduction**:
   Pension contribution is assumed to be 7% of gross salary and is deducted from gross pay when applicable.

3. **Allowances**:
   - **Conveyance Allowance**: This allowance is calculated based on the employee's usage of transport for work-related activities.
   - **Transport Allowance**: A fixed allowance of 600 ETB is provided for commuting between home and work.

4. **Net Pay**:
   Net pay is derived by subtracting income tax and optional pension and allowances from the gross salary.

5. **Gross Pay**:
   Gross pay is estimated by iteratively solving for the value using a binary search method, adjusting the gross value until the calculated net pay matches the input net pay within a small tolerance.

## Examples

### 1. Calculate Income Tax for a Gross Pay of 5000 ETB

```bash
./taxet income-tax --gross 5000
```

**Output**:
```
Income Tax:         695.00 ETB
```

### 2. Calculate Net Pay with Pension and Transport Allowance

```bash
./taxet net-pay --gross 5000 --pension --transport
```

**Output**:
```
Net Pay:         4,420.00 ETB
```

### 3. Calculate Gross Pay from a Net Pay of 4000 ETB

```bash
./taxet gross-pay --net 4000 --pension --conveyance
```

**Output**:
```
Gross Pay:         5,230.00 ETB
```

## License

This project is licensed under the MIT License. You are free to use, modify, and distribute the code as per the terms of the license.

---

For detailed help on the available commands and options, run:

```bash
./taxet --help
```
