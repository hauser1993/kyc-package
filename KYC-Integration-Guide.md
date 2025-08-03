# 🔒 Ballerine KYC Integration Guide

This guide provides complete examples and instructions for integrating the Ballerine KYC (Know Your Customer) flow into your HTML website.

## 📁 Files Overview

- **`kyc-demo.html`** - Full-featured demo with advanced UI and comprehensive logging
- **`kyc-basic-example.html`** - Simple, minimal integration example
- **`KYC-Integration-Guide.md`** - This guide with detailed instructions

## 🚀 Quick Start

### 1. Choose Your Integration Type

**Option A: Container Integration** (Recommended)
```html
<!-- KYC flow appears in a specific container element -->
<div id="kyc-container" style="width: 100%; height: 600px;"></div>
```

**Option B: Modal Integration**
```html
<!-- KYC flow appears as a modal overlay -->
<!-- No container needed, modal appears over the page -->
```

### 2. Include the Ballerine SDK

Add the SDK script to your HTML:
```html
<script crossorigin src="https://cdn.ballerine.io/js/1.5.112/ballerine-sdk.umd.cjs"></script>
```

### 3. Configure and Initialize

```javascript
const kycConfig = {
    endUserInfo: {
        id: 'unique-user-id',
        firstName: 'John',
        lastName: 'Doe',
        email: 'john@example.com'
    },
    backendConfig: {
        baseUrl: 'https://your-backend-url.com',
        auth: {
            method: 'jwt',
            authorizationHeader: 'Bearer your-jwt-token'
        }
    },
    uiConfig: {
        general: {
            colors: {
                primary: '#007bff'
            }
        },
        flows: {
            'my-kyc-flow': {
                steps: [
                    { name: 'welcome', id: 'welcome' },
                    { name: 'document-selection', id: 'document-selection' },
                    { name: 'document-photo', id: 'document-photo' },
                    { name: 'selfie', id: 'selfie' },
                    { name: 'final', id: 'final' }
                ]
            }
        }
    }
};

// Initialize and mount
await BallerineSDK.flows.init(kycConfig);
await BallerineSDK.flows.mount({
    flowName: 'my-kyc-flow',
    elementId: 'kyc-container', // or useModal: true
    callbacks: {
        onFlowComplete: (payload) => console.log('KYC Complete:', payload),
        onFlowError: (payload) => console.log('KYC Error:', payload)
    }
});
```

## 🔧 Configuration Options

### EndUser Information
```javascript
endUserInfo: {
    id: 'unique-user-id',           // Required: Unique identifier
    firstName: 'John',              // Optional: User's first name
    lastName: 'Doe',                // Optional: User's last name
    email: 'john@example.com',      // Optional: User's email
    phone: '+1234567890',           // Optional: User's phone
    dateOfBirth: '1990-01-01',      // Optional: Date of birth
    language: 'en'                  // Optional: Language preference
}
```

### Backend Configuration
```javascript
backendConfig: {
    baseUrl: 'https://your-backend-url.com',
    auth: {
        method: 'jwt',                          // 'jwt', 'basic', or 'cookie'
        authorizationHeader: 'Bearer token'    // Authorization header
    },
    endpoints: {                               // Optional: Custom endpoints
        startVerification: '/api/start',
        getVerificationStatus: '/api/status',
        processStepData: '/api/process',
        uploadFile: '/api/upload'
    }
}
```

### UI Configuration
```javascript
uiConfig: {
    general: {
        colors: {
            primary: '#007bff',      // Primary color
            secondary: '#6c757d',    // Secondary color
            text: '#212529',         // Text color
            danger: '#dc3545'        // Error color
        },
        fonts: {
            name: 'Inter',
            link: 'https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700',
            weight: [400, 500, 600, 700]
        }
    },
    flows: {
        'my-kyc-flow': {
            steps: [/* flow steps */],
            showCloseButton: true,
            firstScreenBackButton: false,
            mobileNativeCamera: true
        }
    }
}
```

## 📝 KYC Flow Steps

### Complete Flow Steps
```javascript
steps: [
    { name: 'welcome', id: 'welcome' },
    { 
        name: 'document-selection', 
        id: 'document-selection',
        documentOptions: [
            { type: 'id_card', kind: 'id_card' },
            { type: 'drivers_license', kind: 'drivers_license' },
            { type: 'passport', kind: 'passport' },
            { type: 'voter_id', kind: 'voter_id' }
        ]
    },
    { name: 'document-photo', id: 'document-photo' },
    { name: 'check-document', id: 'check-document' },
    { name: 'document-photo-back-start', id: 'document-photo-back-start' },
    { name: 'document-photo-back', id: 'document-photo-back' },
    { name: 'check-document-photo-back', id: 'check-document-photo-back' },
    { name: 'selfie-start', id: 'selfie-start' },
    { name: 'selfie', id: 'selfie' },
    { name: 'check-selfie', id: 'check-selfie' },
    { name: 'loading', id: 'loading' },
    { name: 'final', id: 'final' }
]
```

### Minimal Flow Steps
```javascript
steps: [
    { name: 'welcome', id: 'welcome' },
    { name: 'document-selection', id: 'document-selection' },
    { name: 'document-photo', id: 'document-photo' },
    { name: 'selfie', id: 'selfie' },
    { name: 'final', id: 'final' }
]
```

## 🔄 Event Callbacks

### Available Callbacks
```javascript
callbacks: {
    onFlowComplete: (payload) => {
        // Called when KYC flow completes successfully
        console.log('KYC Complete:', payload);
        // payload contains verification results
    },
    onFlowError: (payload) => {
        // Called when an error occurs
        console.error('KYC Error:', payload);
        // payload contains error details
    },
    onFlowExit: (payload) => {
        // Called when user exits the flow
        console.log('KYC Exit:', payload);
        // payload contains exit reason
    },
    onFlowNavigationUpdate: (payload) => {
        // Called when user navigates between steps
        console.log('Navigation:', payload);
        // payload contains current step information
    }
}
```

## 🎨 Styling and Customization

### Custom CSS
```css
/* Override default styles */
.kyc-container {
    border-radius: 12px;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}

/* Custom button styles */
.ballerine-button {
    background: #007bff;
    border-radius: 8px;
}
```

### Theme Colors
```javascript
colors: {
    primary: '#007bff',        // Primary buttons and accents
    secondary: '#6c757d',      // Secondary elements
    text: '#212529',           // Text color
    danger: '#dc3545',         // Error messages
    success: '#28a745',        // Success messages
    warning: '#ffc107'         // Warning messages
}
```

## 📱 Mobile Support

### Mobile-Specific Options
```javascript
flows: {
    'my-kyc-flow': {
        mobileNativeCamera: true,    // Use native camera on mobile
        showCloseButton: true,       // Show close button
        firstScreenBackButton: false // Hide back button on first screen
    }
}
```

## 🔒 Security Best Practices

1. **Never expose sensitive tokens in client-side code**
2. **Use HTTPS for all communications**
3. **Validate all data on the backend**
4. **Implement proper CORS policies**
5. **Use environment variables for configuration**

### Environment-Based Configuration
```javascript
const backendConfig = {
    baseUrl: process.env.NODE_ENV === 'production' 
        ? 'https://api.yoursite.com' 
        : 'http://localhost:3001',
    auth: {
        method: 'jwt',
        authorizationHeader: `Bearer ${process.env.JWT_TOKEN}`
    }
};
```

## 🔄 Integration Examples

### React Integration
```jsx
import { useEffect } from 'react';

function KYCComponent() {
    useEffect(() => {
        const initKYC = async () => {
            await BallerineSDK.flows.init(kycConfig);
            await BallerineSDK.flows.mount({
                flowName: 'my-kyc-flow',
                elementId: 'kyc-container',
                callbacks: {
                    onFlowComplete: (payload) => {
                        // Handle completion
                    }
                }
            });
        };
        
        initKYC();
    }, []);

    return <div id="kyc-container" style={{ width: '100%', height: '600px' }} />;
}
```

### Vue.js Integration
```vue
<template>
    <div id="kyc-container" style="width: 100%; height: 600px;"></div>
</template>

<script>
export default {
    mounted() {
        this.initKYC();
    },
    methods: {
        async initKYC() {
            await BallerineSDK.flows.init(this.kycConfig);
            await BallerineSDK.flows.mount({
                flowName: 'my-kyc-flow',
                elementId: 'kyc-container',
                callbacks: {
                    onFlowComplete: (payload) => {
                        // Handle completion
                    }
                }
            });
        }
    }
}
</script>
```

## 🧪 Development Mode

### Activating Development Mode

There are several ways to enable development mode for debugging and testing:

#### 1. Configuration-Based Development Mode
```javascript
const kycConfig = {
    // ... other configuration
    settings: {
        isDevelopment: true  // Enable development mode
    },
    metricsConfig: {
        enabled: true  // Enable metrics tracking
    }
};
```

#### 2. Complete Development Configuration
```javascript
const developmentConfig = {
    endUserInfo: {
        id: 'dev-user-' + Date.now(),
        firstName: 'Test',
        lastName: 'User',
        email: 'test@example.com'
    },
    backendConfig: {
        baseUrl: 'http://localhost:3001',  // Local development server
        auth: {
            method: 'basic',
            authorizationHeader: 'Bearer dev-token'
        }
    },
    settings: {
        isDevelopment: true,
        // Add any development-specific settings
    },
    metricsConfig: {
        enabled: true,  // Track metrics for debugging
    },
    uiConfig: {
        general: {
            // Development theme
            colors: {
                primary: '#ff6b6b',  // Different color for dev mode
                secondary: '#4ecdc4'
            }
        },
        flows: {
            'my-kyc-flow': {
                showCloseButton: true,        // Easy exit during testing
                firstScreenBackButton: true,  // Enable back navigation
                mobileNativeCamera: false,    // Use web camera for testing
                syncFlow: false,              // Disable sync for testing
                steps: [
                    // ... your flow steps
                ]
            }
        }
    }
};
```

#### 3. Environment-Based Development Mode
```javascript
const isDevelopment = window.location.hostname === 'localhost' || 
                      window.location.hostname === '127.0.0.1' ||
                      window.location.hostname.includes('dev');

const kycConfig = {
    settings: {
        isDevelopment: isDevelopment
    },
    metricsConfig: {
        enabled: isDevelopment
    },
    backendConfig: {
        baseUrl: isDevelopment ? 'http://localhost:3001' : 'https://api.yoursite.com',
        auth: {
            method: isDevelopment ? 'basic' : 'jwt',
            authorizationHeader: isDevelopment ? 'Bearer dev-token' : 'Bearer prod-token'
        }
    }
};
```

### Development Mode Features

When development mode is enabled, you get:

1. **Enhanced Logging**: More detailed console output
2. **Metrics Tracking**: Performance and usage metrics
3. **Debug Information**: Additional debugging data in callbacks
4. **Flexible Configuration**: Easier testing with different settings

### Development Server Setup

For local development with the SDK source:

```bash
# Clone the repository
git clone https://github.com/ballerine-io/ballerine.git
cd ballerine/sdks/web-ui-sdk

# Install dependencies
npm install

# Start development server
npm run dev
```

### Advanced Development Options

```javascript
// Advanced development configuration
const advancedDevConfig = {
    settings: {
        isDevelopment: true,
        // Custom development settings
    },
    // Mock responses for testing
    mockConfig: {
        enabled: true,
        responses: {
            verification: { status: 'completed', result: 'approved' },
            upload: { success: true, fileId: 'mock-file-id' }
        }
    },
    // Development-specific UI modifications
    uiConfig: {
        flows: {
            'my-kyc-flow': {
                showCloseButton: true,
                firstScreenBackButton: true,
                // Skip certain steps for faster testing
                skipSteps: ['welcome', 'loading'],
                // Override step behavior
                stepOverrides: {
                    'document-photo': {
                        autoCapture: true,
                        captureDelay: 1000
                    }
                }
            }
        }
    }
};
```

## 🐛 Troubleshooting

### Common Issues

1. **SDK not loading**
   - Check network connectivity
   - Verify SDK URL is correct
   - Ensure CORS is properly configured

2. **Flow not mounting**
   - Verify element ID exists
   - Check for JavaScript errors in console
   - Ensure SDK is initialized before mounting

3. **Backend connection issues**
   - Verify backend URL is correct
   - Check authentication credentials
   - Ensure backend is running and accessible

### Debug Mode
```javascript
// Enable debug logging
console.log('KYC Config:', kycConfig);
console.log('BallerineSDK:', BallerineSDK);

// Check if development mode is active
console.log('Development Mode:', kycConfig.settings?.isDevelopment);
```

### Development Mode Debugging
```javascript
// Enhanced debugging for development mode
const flowCallbacks = {
    onFlowNavigationUpdate: (payload) => {
        if (kycConfig.settings?.isDevelopment) {
            console.group('🔄 Navigation Update');
            console.log('Current Step:', payload.currentStep);
            console.log('Flow Data:', payload);
            console.groupEnd();
        }
    },
    onFlowComplete: (payload) => {
        if (kycConfig.settings?.isDevelopment) {
            console.group('✅ Flow Complete');
            console.log('Result:', payload);
            console.log('Performance:', payload.metrics);
            console.groupEnd();
        }
    },
    onFlowError: (payload) => {
        if (kycConfig.settings?.isDevelopment) {
            console.group('❌ Flow Error');
            console.error('Error:', payload.error);
            console.log('Stack:', payload.stack);
            console.log('Context:', payload.context);
            console.groupEnd();
        }
    }
};
```

## 📚 Additional Resources

- [Ballerine Documentation](https://docs.ballerine.com/)
- [API Reference](https://docs.ballerine.com/api)
- [GitHub Repository](https://github.com/ballerine-io/ballerine)

## 🤝 Support

If you encounter issues or need help:

1. Check the browser console for error messages
2. Review the configuration settings
3. Ensure backend is properly configured
4. Contact Ballerine support for assistance

---

**Happy integrating! 🚀** 