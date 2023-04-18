- Use Amazon Cognito
- Amplify Libraries allow interaction with AWS Services from a web or mobile application

# Install libraries

```bash
npm install aws-amplify @aws-amplify/ui-react
```

# Create Authentication Service

```bash
amplify add auth

? Do you want to use the default authentication and security configuration? Default configuration
? How do you want users to be able to sign in? Username
? Do you want to configure advanced settings? No, I am done.
```

# Deploy Using Amplify

```bash
amplify push --y
```

Creates 'aws-exports.js'

# Add Imports to index.js

```JS
import { Amplify } from 'aws-amplify';
import config from './aws-exports';
Amplify.configure(config);
```

# Add Auth to App.js

- Uses the WithAuthenticator Component

```JSX
import logo from "./logo.svg";
import "@aws-amplify/ui-react/styles.css";
import {
  withAuthenticator,
  Button,
  Heading,
  Image,
  View,
  Card,
} from "@aws-amplify/ui-react";

function App({ signOut }) {
  return (
    <View className="App">
      <Card>
        <Image src={logo} className="App-logo" alt="logo" />
        <Heading level={1}>We now have Auth!</Heading>
      </Card>
      <Button onClick={signOut}>Sign Out</Button>
    </View>
  );
}

export default withAuthenticator(App);
```