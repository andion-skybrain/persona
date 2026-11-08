# Persona - Offline Personal Identity Manager

> Showcase repository. The full Persona source code is private. This README and the docs folder describe what the app does and how it protects your data. Screenshots coming soon.

## Overview

Persona is a fully offline-compatible web application designed for creating, managing, and storing detailed digital personas. Each persona serves as a rich identity profile that encompasses personal, professional, and social aspects. The app enables users to create, edit, search, filter, and export personas, all while ensuring complete data privacy and robust security.

## Key Features

- **Fully Offline Compatible**: All data is stored locally with no external server dependencies
- **Comprehensive Persona Profiles**: Create detailed personas with information across multiple categories
- **Advanced Search & Filter**: Find personas quickly with powerful search and filtering capabilities
- **Multiple View Modes**: Card and list views for different ways to browse your personas
- **Data Security**: Password protection for sensitive personas and encryption for private data
- **Import/Export**: Backup and restore your personas with secure JSON export/import
- **Multi-Profile Support**: Create separate profiles, each with its own set of personas
- **Modern UI**: Clean, responsive interface with dark/light mode support

## Technology Stack

- **React**: Component-based UI library for building the interface
- **Material-UI**: Comprehensive UI component library
- **Dexie.js**: IndexedDB wrapper for offline data storage
- **Redux Toolkit**: State management
- **Formik & Yup**: Form handling and validation
- **React Router**: Navigation and routing
- **CryptoJS**: Encryption and security features

## Installation

Clone the repository, run `npm install`, then start the development server with `npm run dev`. Build for production with `npm run build`.

## Usage

Create a profile, add personas, and browse them in card or list view. Use search and filters to find personas fast, and export or import from the app when you need a backup.

## Security

Persona takes security seriously. See the [Security Guide](docs/SECURITY.md) for details on how your data is protected.

## Development

### Prerequisites

- Node.js 14.0.0 or later
- npm 6.0.0 or later

### Setup

1. Clone the repository
2. Install dependencies:
   ```
   npm install
   ```
3. Start the development server:
   ```
   npm run dev
   ```

### Building for Production

```
npm run build
```

### Running Tests

```
npm test
```

## Project Structure

```
persona-app/
├── public/              # Static assets
├── src/
│   ├── components/      # Reusable UI components
│   ├── hooks/           # Custom React hooks
│   ├── pages/           # Page components
│   ├── services/        # Database and other services
│   ├── store/           # Redux store and slices
│   ├── theme/           # UI theme configuration
│   ├── utils/           # Utility functions
│   ├── App.jsx          # Main application component
│   └── main.jsx         # Application entry point
├── docs/                # Documentation
└── tests/               # Test files
```

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Acknowledgments

- This project was created to provide a secure, offline solution for managing digital personas
- Special thanks to all the open-source libraries that made this project possible
