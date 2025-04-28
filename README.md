# IDUN Guardian SDK Sample App

A minimal Next.js application demonstrating how to integrate with the IDUN Guardian SDK for authentication and connecting to IDUN Guardian Earbuds.

## Overview

This sample application shows the basic integration steps required to work with the IDUN Guardian SDK. It demonstrates:

1. Authentication with IDUN Guardian services
2. Connecting to IDUN Guardian Earbuds via Bluetooth
3. Reading battery level from connected devices
4. Clean disconnection and logout

The app follows a simple flow:

- Login with IDUN Guardian credentials
- Connect to IDUN Guardian Earbuds
- View device information
- Disconnect and logout

Sample app was initialized with the following commands:

```bash
# Create the sample app directory
mkdir -p sample-app

# Initialize a Next.js app with TypeScript, ESLint, Tailwind CSS, and app directory
cd sample-app && npx create-next-app@latest . --typescript --eslint --tailwind --app --src-dir
```

## Features

- **Authentication**: OAuth-based authentication with IDUN's services, utilizing AWS Cognito as the authentication provider.
- **Device Connection**: Bluetooth connection to IDUN Guardian Earbuds
- **Device Information**: Display device status including battery level
- **TypeScript**: Fully typed for better development experience

## Technology Stack

- **Next.js**: React framework for building web applications
- **IDUN Guardian SDK**: SDK for interacting with IDUN Guardian earbuds
- **Capacitor**: For mobile platform capabilities and native runtime
- **Web Bluetooth API**: Browser API for Bluetooth connectivity
- **TypeScript** (optional): Strongly typed programming language
- **Tailwind CSS** (optional): Utility-first CSS framework

Since the app is created with Next.js, it is recommended to deploy the app using a cloud service provider like Vercel.

## Getting Started

### Prerequisites

- Node.js 18.17.0 or higher
- npm or yarn
- For testing with actual devices:
  - A compatible browser with Web Bluetooth support (Chrome, Edge)
  - IDUN Guardian Earbuds
  - IDUN Guardian account

### Environment Variables

You can set up environment variables to customize the SDK configuration. For example, if you want to use the IDUN staging environment, you can create a `.env.local` file in the root of the sample-app directory to override them:

```
# API Endpoints (optional - defaults to production environment)
NEXT_PUBLIC_REST_ENDPOINT="https://api.stage.idun.cloud"
NEXT_PUBLIC_WEBSOCKET_ENDPOINT="wss://ws-api.stage.idun.cloud"
NEXT_PUBLIC_AUTH_BASE_URL="https://oauth.stage.idun.cloud"

# App IDs (Get these from IDUN team)
NEXT_PUBLIC_AUTH_APPID_WEB="your-web-app-id"
NEXT_PUBLIC_AUTH_APPID_ANDROID="your-android-app-id"
NEXT_PUBLIC_AUTH_APPID_IOS="your-ios-app-id"

# URI Schemes for Mobile
NEXT_PUBLIC_URI_SCHEME_ANDROID="com.idunguardian.console"
NEXT_PUBLIC_URI_SCHEME_IOS="com.idunguardian.app"
```

A template file `.env.template` is provided in the repository for your convenience. Copy it and fill in your specific values:

```bash
cp .env.template .env.local
```

**Note**: You'll need to obtain the actual App IDs from the IDUN team for authentication to work properly.

The URI scheme variables are especially important for mobile apps:

- `NEXT_PUBLIC_URI_SCHEME_ANDROID`: Used for deep linking in Android apps
- `NEXT_PUBLIC_URI_SCHEME_IOS`: Used for deep linking in iOS apps

These URI schemes must match your app's bundle identifier and must be configured in your native app's settings.

### Installation

1. Clone the repository

   ```
   git clone <repository-url>
   cd idun-guardian-sdk-js/sample-app
   ```

2. Install dependencies

   ```
   npm install
   ```

   If you're creating your own project from scratch, install the SDK with:

   ```
   npm install @iduntech/idun-guardian-sdk
   ```

3. Run the development server

   ```
   npm run dev
   ```

4. Open [http://localhost:3000](http://localhost:3000) in your browser

### Usage

1. Click the "Login with IDUN Guardian" button on the homepage
2. Complete authentication with your IDUN Guardian credentials
3. Once redirected to the dashboard, click "Connect Device" to connect to nearby IDUN Guardian Earbuds
4. After connection, you'll see the device status and battery level
5. Use "Disconnect Device" to disconnect from earbuds
6. Use "Logout" to end your session

## Key Components

- **Home Page**: Entry point with login button
- **Dashboard**: Shows authenticated state and device connection options
- **Auth Callback**: Processes OAuth callback from IDUN authentication service
- **Logout**: Handles clean logout process

## SDK API Reference

The IDUN Guardian SDK provides comprehensive methods for interacting with IDUN Guardian Earbuds. The full API documentation can be found at:

[IDUN Guardian SDK API Documentation](https://iduntech.github.io/idun-guardian-sdk-js/classes/Guardian.html)

## Mobile Development with Capacitor

**Important**: The IDUN Guardian SDK specifically requires Capacitor for mobile platform integration. Its peer dependencies include Capacitor packages for core functionality, Bluetooth LE, and OAuth/browser capabilities.

To develop this app for mobile platforms:

1. Install Capacitor core packages:

   ```
   npm install @capacitor/cli @capacitor/core
   npx cap init "IDUN Guardian Sample" "com.your-company.guardiansample" --web-dir=out
   ```

2. Add iOS and/or Android platforms:

   ```
   npm install @capacitor/ios @capacitor/android
   npx cap add ios
   npx cap add android
   ```

3. Configure your Next.js app for static export in `next.config.js`:

   ```js
   /** @type {import('next').NextConfig} */
   const nextConfig = {
     output: "export",
     images: { unoptimized: true },
   };
   module.exports = nextConfig;
   ```

4. Build your app and sync with Capacitor:
   ```
   npm run build
   npx cap sync
   ```

For detailed platform-specific configurations and deep linking setup, refer to the [Capacitor documentation](https://capacitorjs.com/docs) and the SDK's requirements.

## Resources

- [IDUN Guardian SDK API Documentation](https://iduntech.github.io/idun-guardian-sdk-js/classes/Guardian.html)
- [Next.js Documentation](https://nextjs.org/docs)
- [Capacitor Documentation](https://capacitorjs.com/docs)
