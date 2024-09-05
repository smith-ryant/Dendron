---
id: 8u7ri3cbilkwc6ke3gbmbj7
title: "@mui-storybook"
desc: ""
updated: 1724880310465
created: 1724880027601
---

**Creating a Vite + React + TypeScript project with Material-UI (MUI) and Storybook installed. I'll break it down step-by-step for you to make it easier to follow.**

### Step 1: Set Up Vite + React + TypeScript Project

1. **Create a New Vite Project:**

   Open your terminal and run the following command to create a new Vite project. Replace `my-vite-app` with your preferred project name:

   ```bash
   npm create vite@latest my-vite-app -- --template react-ts
   ```

   This command initializes a new Vite project using the React template with TypeScript support.

2. **Navigate to the Project Directory:**

   Change into your new project directory:

   ```bash
   cd my-vite-app
   ```

3. **Install Dependencies:**

   Run the following command to install the project's dependencies:

   ```bash
   npm install
   ```

### Step 2: Install Material-UI (MUI)

1. **Install MUI Core and Icons:**

   Use the following command to install Material-UI's core package and icon set:

   ```bash
   npm install @mui/material @emotion/react @emotion/styled @mui/icons-material
   ```

   - `@mui/material`: The core components of Material-UI.
   - `@emotion/react` and `@emotion/styled`: Required for styling with Material-UI.
   - `@mui/icons-material`: The icon set for Material-UI.

### Step 3: Set Up Storybook

1. **Install Storybook:**

   Storybook provides a great way to develop UI components in isolation. Run the following command to set up Storybook in your Vite project:

   ```bash
   npx storybook@latest init
   ```

   This command will automatically detect that you are using Vite with React and set up Storybook accordingly.

2. **Run Storybook:**

   After the setup is complete, you can start Storybook using:

   ```bash
   npm run storybook
   ```

   This will launch Storybook, and you should be able to view it in your browser at `http://localhost:6006`.

### Step 4: Configure Storybook for TypeScript and MUI

1. **Create a Sample Component:**

   Create a `Button.tsx` component inside a `src/components` directory:

   ```tsx
   // src/components/Button.tsx

   import React from "react";
   import Button from "@mui/material/Button";

   interface ButtonProps {
     label: string;
     onClick: () => void;
   }

   const MyButton: React.FC<ButtonProps> = ({ label, onClick }) => {
     return (
       <Button variant="contained" color="primary" onClick={onClick}>
         {label}
       </Button>
     );
   };

   export default MyButton;
   ```

2. **Create a Story for the Component:**

   Create a `Button.stories.tsx` file inside a `src/components` directory:

   ```tsx
   // src/components/Button.stories.tsx

   import React from "react";
   import { Meta, Story } from "@storybook/react";
   import MyButton from "./Button";

   export default {
     title: "Example/Button",
     component: MyButton,
   } as Meta;

   const Template: Story = (args) => <MyButton {...args} />;

   export const Primary = Template.bind({});
   Primary.args = {
     label: "Primary Button",
     onClick: () => alert("Button clicked!"),
   };
   ```

3. **Adjust Storybook Configuration for MUI:**

   Ensure that the MUI theme and emotion styling are properly set up in Storybook by editing the `.storybook/preview.js` or `.storybook/preview.tsx` file (depending on your setup):

   ```tsx
   // .storybook/preview.tsx

   import React from "react";
   import { ThemeProvider } from "@mui/material/styles";
   import CssBaseline from "@mui/material/CssBaseline";
   import { theme } from "../src/theme"; // Create your MUI theme file if you haven't already

   export const decorators = [
     (Story) => (
       <ThemeProvider theme={theme}>
         <CssBaseline />
         <Story />
       </ThemeProvider>
     ),
   ];
   ```

### Step 5: Run Your Project and Storybook

1. **Run Vite Development Server:**

   You can start your Vite development server using:

   ```bash
   npm run dev
   ```

   This will start the Vite server, and you should be able to see your React app running.

2. **Run Storybook:**

   You already ran this earlier, but for completeness, run Storybook again using:

   ```bash
   npm run storybook
   ```

### Step 6: Optional - Create a Custom MUI Theme

1. **Create a Theme File:**

   You can create a custom theme file, for example, `src/theme.ts`:

   ```tsx
   // src/theme.ts

   import { createTheme } from "@mui/material/styles";

   export const theme = createTheme({
     palette: {
       primary: {
         main: "#007bff",
       },
       secondary: {
         main: "#6c757d",
       },
     },
   });
   ```

2. **Use the Theme in Your App:**

   Wrap your app with the `ThemeProvider` using this custom theme in your `src/main.tsx`:

   ```tsx
   // src/main.tsx

   import React from "react";
   import ReactDOM from "react-dom";
   import App from "./App";
   import { ThemeProvider } from "@mui/material/styles";
   import CssBaseline from "@mui/material/CssBaseline";
   import { theme } from "./theme";

   ReactDOM.render(
     <React.StrictMode>
       <ThemeProvider theme={theme}>
         <CssBaseline />
         <App />
       </ThemeProvider>
     </React.StrictMode>,
     document.getElementById("root")
   );
   ```

### Summary

- You’ve set up a Vite + React + TypeScript project.
- Installed and configured MUI for UI components.
- Installed and set up Storybook for isolated component development.
- Created a sample MUI component and a Storybook story.

### Next Steps

**a.** Write unit tests using a framework like Jest and React Testing Library to ensure your components work as expected.

**b.** Customize your Storybook configuration to include additional addons for better component documentation and controls.
