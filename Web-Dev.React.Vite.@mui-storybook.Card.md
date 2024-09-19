---
id: uhg3w9vrsz5fs7kvcoabcav
title: Card
desc: ""
updated: 1725647519970
created: 1725646892197
---

To implement a `Card` component that consists of three child components (`Card.Header`, `Card.Section`, and `Card.Footer`), you can use a composition approach in React. This allows you to build a flexible and reusable `Card` component where the layout and styling of each child component are managed individually.

### Plan

1. **Card Component**: Acts as a container for the `Header`, `Section`, and `Footer`.
2. **Card.Header**: For the descriptive title.
3. **Card.Section**: For the main content or body, which can have multiple sections.
4. **Card.Footer**: For the actions (like buttons or links).
5. Provide default content for the `Card` with sections and footer content.

### Code Implementation

```tsx
import React from "react";
import MuiPaper from "@mui/material/Paper";
import Typography from "@mui/material/Typography";
import { SxProps } from "@mui/material";
import Box from "@mui/material/Box";

interface CardProps {
  sx?: SxProps;
  children: React.ReactNode;
}

interface CardHeaderProps {
  title: string;
}

interface CardSectionProps {
  children: React.ReactNode;
}

interface CardFooterProps {
  children: React.ReactNode;
}

export const Card: React.FC<CardProps> & {
  Header: React.FC<CardHeaderProps>;
  Section: React.FC<CardSectionProps>;
  Footer: React.FC<CardFooterProps>;
} = ({ sx = {}, children }) => {
  return (
    <MuiPaper
      sx={{
        width: "30vw", // 30% of the screen width
        display: "flex",
        flexDirection: "column",
        padding: 2,
        ...sx,
      }}
    >
      {children}
    </MuiPaper>
  );
};

Card.Header = ({ title }) => {
  return (
    <Box sx={{ marginBottom: 2 }}>
      <Typography variant="h5" component="div" gutterBottom>
        {title}
      </Typography>
    </Box>
  );
};

Card.Section = ({ children }) => {
  return (
    <Box sx={{ marginBottom: 2 }}>
      <Typography variant="body1" component="div">
        {children}
      </Typography>
    </Box>
  );
};

Card.Footer = ({ children }) => {
  return (
    <Box sx={{ marginTop: 2, borderTop: "1px solid #ddd", paddingTop: 2 }}>
      {children}
    </Box>
  );
};

// Example usage
export const CardExample = () => {
  return (
    <Card>
      <Card.Header title="Default Card" />
      <Card.Section>
        Card content goes here. This can be a description, text, or any other
        content.
      </Card.Section>
      <Card.Section>
        Another section of content. You can have multiple sections in the card.
      </Card.Section>
      <Card.Footer>
        <button>Primary Action</button>
      </Card.Footer>
    </Card>
  );
};
```

### Explanation:

1. **`Card` Component**:

   - The `Card` component is a wrapper that applies the basic layout and styles using Material-UI’s `MuiPaper`.
   - It accepts `children`, allowing you to nest the `Header`, `Section`, and `Footer` components inside it.

2. **`Card.Header`**:

   - Displays the title of the card.
   - Uses `Typography` with `h5` variant for the title styling.
   - Wrapped in a `Box` with some margin for spacing.

3. **`Card.Section`**:

   - Used to display the body content. You can use multiple sections inside a card.
   - Each section is wrapped in a `Box` with spacing for separation.

4. **`Card.Footer`**:

   - Used to display primary actions, such as buttons or links.
   - It includes a top border and padding for visual separation from the card content.

5. **`CardExample`**:
   - An example of how to use the `Card` component with all three child components (`Header`, `Section`, `Footer`).
   - The `Footer` contains a simple button as an action.

### Benefits:

- **Composable Design**: You can use as many `Card.Section`s as you want, and each part of the card (`Header`, `Section`, `Footer`) is modular and reusable.
- **Customization**: The `sx` prop allows you to easily customize the styling of the card.
- **Action Footer**: The `Footer` section is designed to hold primary actions like buttons or links.

### Example Usage:

```tsx
<Card>
  <Card.Header title="My Card Title" />
  <Card.Section>
    This is the content of the card section. You can add multiple sections.
  </Card.Section>
  <Card.Footer>
    <button>Submit</button>
  </Card.Footer>
</Card>
```

### Possible Enhancements:

1. **Responsive Design**: Adjust the `sx` prop to handle different screen sizes.
2. **Additional Components**: Add support for images, icons, or other elements inside `Card.Section`.
3. **Conditional Rendering**: You can enhance the component to render sections only if data is available.

Would you like to implement any of these enhancements, or need further guidance on a specific feature?
