# SAW Calculator (Simple Additive Weighting)

A Vue.js application for calculating Simple Additive Weighting (SAW), a simple and commonly used Multi-Criteria Decision Making (MCDM) method. This calculator helps users make decisions by evaluating multiple alternatives based on multiple criteria with different weights.

## Features

- Dynamic input for number of alternatives and criteria
- Support for both benefit and cost type criteria
- Interactive data input table
- Weight assignment for each criterion
- Automatic normalization of values
- Clear visualization of results
- Responsive design

## Prerequisites

Before running this project, make sure you have the following installed:
- Node.js (v14.0.0 or higher)
- Yarn package manager

## Installation

1. Clone the repository
```bash
git clone https://github.com/fadlymirvan/saw-calculator.git
cd saw-calculator
```

2. Install dependencies
```bash
yarn install
```

3. Run development server
```bash
yarn serve
```

The application will be available at `http://localhost:8080`

## Build for Production

To create a production build:
```bash
yarn build
```

The built files will be in the `dist` directory.

## Usage Guide

1. **Initial Setup**
    - Enter the number of alternatives you want to compare
    - Enter the number of criteria you'll use for comparison
    - Click "Generate Table" to create the input matrix

2. **Enter Data**
    - Fill in the values for each alternative under each criterion
    - Use the "+" button to add more alternatives if needed
    - Use the "-" button to remove alternatives

3. **Configure Criteria**
    - Set the weight for each criterion (importance level)
    - Select the criterion type:
        - Benefit: Higher values are better
        - Cost: Lower values are better

4. **Calculate Results**
    - Click the "Calculate" button to process the data
    - View the results showing the ranking of alternatives

## Example Usage

Let's say you want to choose a laptop from three options based on three criteria:

1. Set up the initial matrix:
    - Number of Alternatives: 3 (Laptops)
    - Number of Criteria: 3 (Price, Performance, Battery Life)

2. Enter the criteria details:
    - Price: Weight = 30%, Type = Cost
    - Performance: Weight = 40%, Type = Benefit
    - Battery Life: Weight = 30%, Type = Benefit

3. Enter values for each laptop:
```
              Price    Performance    Battery Life
Laptop A      1200    85            10
Laptop B      800     75            8
Laptop C      1500    90            12
```

4. Click Calculate to see which laptop ranks best based on your criteria.

## Project Structure

```
src/
├── components/
│   └── FooterComponent.vue
│   └── SawCalculator.vue
│   └── SAW/
│       ├── HeaderComponent.vue
│       ├── InputControls.vue
│       ├── DataTableComponent.vue
│       ├── CriterionDetailComponent.vue
│       ├── CalculateButton.vue
│       └── ResultComponent.vue
└── App.vue
```

## Additional Commands

Lint and fix files:
```bash
yarn lint
```

Run unit tests:
```bash
yarn test:unit
```

## Customize Configuration
See [Configuration Reference](https://cli.vuejs.org/config/) for Vue CLI configuration options.

## Authors

- Fadly Muhammad Irvan - *Initial work* - [fadlymirvan](https://github.com/fadlymirvan)

## Acknowledgments

- Vue.js team for the amazing framework
- Simple Additive Weighting (SAW) method creators