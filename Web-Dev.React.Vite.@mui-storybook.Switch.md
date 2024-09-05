---
id: id7c6ngrciglp96ueayyf5z
title: Switch
desc: ""
updated: 1725473819923
created: 1725222481043
---

The three files you provided—`SwitchType.ts`, `Switch.tsx`, and `Switch.stories.tsx`—are part of a React component setup for a `Switch` component, which integrates with the Material-UI (MUI) library. These files work together to define, implement, and test this component within Storybook, a popular tool for developing and showcasing UI components in isolation.

Let's break down the role of each file and how they are interconnected:

### 1. **`SwitchType.ts`**

This file is responsible for defining the **type interface** (`SwitchType`) that describes the expected properties (`props`) for the `Switch` component. It imports the `SwitchProps` from MUI’s `Switch` component and extends it with custom properties. Here's what's included:

- **label:** An optional string to describe the switch, both for visual and accessibility purposes.
- **disabled:** A boolean that controls whether the switch is disabled (inherited from MUI `SwitchProps`).
- **color:** Defines the possible color values for the switch, utilizing MUI's color options like `'primary'`, `'secondary'`, etc.
- **size:** Specifies the size of the switch, defaulting to `'medium'`.
- **onChange:** A callback function that fires whenever the switch is toggled, accepting an event and the new switch state (`checked`).

**Relationship to other files:**  
This interface is imported by the `Switch.tsx` file, ensuring that the component receives the correct types for each prop, making it TypeScript-friendly and safer to use in larger applications.

### 2. **`Switch.tsx`**

This file contains the actual **React component implementation** for the `Switch`. It uses the `SwitchType` interface to type its props, ensuring type safety. The key elements of this component include:

- It imports and uses MUI's `Switch` and `FormControlLabel` components to handle the UI rendering.
- The component maintains its own internal state (`isChecked`) to track whether the switch is toggled on or off.
- A handler (`handleCheckedChange`) updates the internal state and invokes the `onChange` callback whenever the switch is toggled.
- The switch's label, disabled state, color, and size are controlled via props.

**Relationship to other files:**

- This file uses the `SwitchType` interface from `SwitchType.ts` to ensure the props follow the correct type definitions.
- The `Switch` component is tested and displayed in `Switch.stories.tsx`, where different switch configurations are demonstrated using Storybook.

### 3. **`Switch.stories.tsx`**

This file defines **Storybook stories** for the `Switch` component. Storybook stories are essentially different scenarios or use cases for how a component can be rendered. In this file, multiple variations of the `Switch` are created:

- **Default:** Shows a default, unchecked switch.
- **Checked:** Shows the switch in the checked state.
- **Disabled:** Shows the switch when it is disabled.
- **CheckedAndDisabled:** Shows the switch both checked and disabled.
- **ControlledExample:** Demonstrates a controlled switch component, where its checked state is managed by React's state (`useState`).

Each story includes:

- **Args:** Arguments that control how the component is rendered (e.g., `checked`, `disabled`, `color`, etc.).
- **Actions:** Uses Storybook's `action` function to log interactions with the switch (e.g., when the switch is toggled).

**Relationship to other files:**

- The `Switch` component from `Switch.tsx` is imported here and used in different states to showcase the component in Storybook.
- The `args` in the stories correspond to the props defined in `SwitchType.ts`, ensuring that all props adhere to the interface and provide correct type checking.

### Inter-relationships:

1. **Type Definition (`SwitchType.ts`) → Component Implementation (`Switch.tsx`)**  
   The `SwitchType` interface is imported by the `Switch.tsx` file to define the structure of the props. This ensures that the component has clearly defined and strongly typed properties for a more robust development experience.

2. **Component Implementation (`Switch.tsx`) → Storybook Stories (`Switch.stories.tsx`)**  
   The `Switch.tsx` component is imported into the Storybook file to demonstrate various use cases. The stories render different versions of the switch (e.g., checked, disabled, controlled) to visualize how the switch behaves under different conditions.

3. **Storybook (`Switch.stories.tsx`) → Interactive Testing and Development**  
   Storybook allows developers to interact with and test the `Switch` component in isolation. It provides visual feedback and logs actions (like when the switch is toggled) to facilitate testing and validation.

### Summary:

- **`SwitchType.ts`** defines the types and expected props for the `Switch` component, making it easier to manage and prevent errors during development.
- **`Switch.tsx`** contains the actual logic and UI implementation of the switch, leveraging MUI components and integrating with the types defined in `SwitchType.ts`.
- **`Switch.stories.tsx`** provides multiple Storybook stories that showcase different configurations of the `Switch` component, allowing developers to interact with and verify the component's behavior in isolation.

This structure is ideal for component-based development because it promotes **modularity** (separation of types, implementation, and testing) and **reusability** across projects.

**`SwitchType.ts`**

```ts
// src/components/Switch/SwitchType.ts

import { SwitchProps as MuiSwitchProps } from "@mui/material/Switch";

export interface SwitchType extends MuiSwitchProps {
  /**
   * The label for the switch component. This can be used
   * for accessibility and can also be displayed as a visible label.
   */
  label?: string;

  /**
   * Whether the switch should be displayed in a disabled state.
   * Inherited from MUI SwitchProps.
   */
  disabled?: boolean;

  /**
   * The color of the switch. Can be one of the MUI theme's
   * predefined color options like 'primary', 'secondary', etc.
   */
  color?:
    | "primary"
    | "secondary"
    | "default"
    | "error"
    | "warning"
    | "info"
    | "success";

  /**
   * The size of the switch. It can be 'small' or 'medium'.
   * Defaults to 'medium' if not specified.
   */
  size?: "small" | "medium";

  /**
   * A callback function that is triggered when the switch
   * state is changed (toggled on or off).
   */
  onChange?: (
    event: React.ChangeEvent<HTMLInputElement>,
    checked: boolean
  ) => void;
}
```

**`Switch.tsx`**

```tsx
// src/components/Switch/Switch.tsx

import React from "react";
import MuiSwitch from "@mui/material/Switch";
import FormControlLabel from "@mui/material/FormControlLabel";
import { SwitchType } from "../../types/SwitchType";

export const Switch: React.FC<SwitchType> = ({
  checked = false, // Default checked state
  label = "", // Label for accessibility and visibility
  color = "default", // Default color
  disabled = false, // Disabled state
  size = "medium", // Default size
  onChange, // Callback function on state change
  ...rest // Any other props passed to MUI Switch
}) => {
  const [isChecked, setIsChecked] = React.useState<boolean>(checked);

  const handleCheckedChange = (event: React.ChangeEvent<HTMLInputElement>) => {
    setIsChecked(event.target.checked); // Update internal state
    if (onChange) {
      onChange(event, event.target.checked); // Pass event and checked state to parent
    }
  };

  return (
    <FormControlLabel
      control={
        <MuiSwitch
          checked={isChecked}
          color={color}
          disabled={disabled}
          size={size}
          onChange={handleCheckedChange}
          {...rest} // Spread any other MUI SwitchProps
        />
      }
      label={label} // Accessibility label
    />
  );
};

export default Switch;
```

**`Switch.stories.tsx`**

```tsx
// src/components/Switch/Switch.stories.tsx

import React, { useState } from "react";
import type { Meta, StoryObj } from "@storybook/react";
import { action } from "@storybook/addon-actions";
import { Switch } from "../components/Switch/Switch"; // Correct import path for the Switch component

// Meta configuration for the Switch stories
const meta: Meta<typeof Switch> = {
  title: "Example/Switch",
  component: Switch,
  parameters: {
    layout: "centered", // Centers the Switch in the Storybook Canvas
  },
  tags: ["autodocs"],
  argTypes: {
    checked: { control: "boolean" }, // Control to toggle the checked state
    disabled: { control: "boolean" }, // Control to toggle the disabled state
    color: {
      control: "select",
      options: [
        "default",
        "primary",
        "secondary",
        "error",
        "warning",
        "info",
        "success",
      ],
    },
    size: {
      control: "select",
      options: ["small", "medium"],
    },
    onChange: { action: "toggled" }, // Action handler to log switch toggle events
  },
};

export default meta;
type Story = StoryObj<typeof meta>;

// Default Story
export const Default: Story = {
  args: {
    checked: false,
    disabled: false,
    color: "default",
  },
};

// Checked Story
export const Checked: Story = {
  args: {
    checked: true,
    disabled: false,
    color: "primary",
  },
};

// Disabled Story
export const Disabled: Story = {
  args: {
    checked: false,
    disabled: true,
    color: "secondary",
  },
};

// Checked and Disabled Story
export const CheckedAndDisabled: Story = {
  args: {
    checked: true,
    disabled: true,
    color: "default",
  },
};

// Controlled Example
export const ControlledExample: Story = {
  render: (args) => {
    const [isChecked, setIsChecked] = useState<boolean>(args.checked || false);

    const handleChange = (
      event: React.ChangeEvent<HTMLInputElement>,
      checked: boolean
    ) => {
      setIsChecked(checked);
      action("toggled")(checked, event); // Logs the change using action
    };

    return <Switch {...args} checked={isChecked} onChange={handleChange} />;
  },
  args: {
    checked: false,
    disabled: false,
    color: "success",
    size: "medium",
    label: "Toggle me",
  },
};
```
