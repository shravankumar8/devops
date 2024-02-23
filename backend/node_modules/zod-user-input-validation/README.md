# Input Validation using Zod

This module provides a simple function for input validation using the Zod library in JavaScript/TypeScript. It validates a username and password based on specified criteria.

## Installation

Before using this module, make sure you have the Zod library installed. You can install it using npm:

```bash
npm install zod
```

## Usage

```javascript
// Import the z object from Zod library
import { z } from "zod";
// Alternatively, if you prefer CommonJS syntax:
// const z = require("zod");

// Function for input validation
function inputValidation(username, password) {
    // Define input schema using Zod
    let inputSchema = z.object({
        username: z.string().min(1).email(),
        password: z.string().min(6),
    });

    // Parse the input against the schema
    const parsedInput = inputSchema.safeParse({
        username,
        password,
    });

    // Return the parsed input
    return parsedInput;
}

// Export the function for use in other modules
export { inputValidation };
```

## Example

```javascript
// Import the inputValidation function
import { inputValidation } from "./path/to/inputValidation";

// Example usage
const userInput = inputValidation("user@example.com", "securePassword");

if (userInput.success) {
    console.log("Input is valid!");
    console.log("Validated Data:", userInput.data);
} else {
    console.error("Invalid input. Errors:", userInput.error.errors);
}
```

In the example above, `inputValidation` is a function that takes a username and a password as arguments, validates them according to the specified criteria, and returns an object containing information about the validation result. If the input is valid, the `success` property will be `true`, and the validated data can be accessed through the `data` property. If the input is invalid, the `success` property will be `false`, and the specific validation errors can be accessed through the `error.errors` property.