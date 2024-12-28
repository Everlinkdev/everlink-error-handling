# Everlink Error Codes Documentation

The SDK provides detailed error codes to help developers diagnose and resolve issues efficiently. Errors are grouped by type, and each code is associated with a descriptive message to clarify the issue.

---

## Error Code Structure

- **Non-server errors**: Use codes ranging from `10,000` to `19,999`, grouped into logical categories.
- **Server errors**: Use HTTP status codes (e.g., `400`, `401`, `404`, `500`).

---

## Error Categories

### 1. Token Errors (`10,000 - 10,099`)
These errors are related to token management and validation.

| **Code** | **Message**                                            |
|----------|--------------------------------------------------------|
| 10000    | Token not valid.                                       |
| 10001    | Cannot create new token.                               |
| 10002    | Token array download failed.                           |
| 10003    | Token not found.                                       |
| 10004    | Token expired.                                         |
| 10005    | Start valid date incorrect.                            |
| 10006    | Token validity period must be between 1 and 30 days.   |

---

### 2. Everlink Class Errors (`10,100 - 10,199`)
These errors indicate issues with the Everlink class setup.

| **Code** | **Message**                                            |
|----------|--------------------------------------------------------|
| 10100    | Everlink class not set up correctly.                   |
| 10101    | Error with App ID key.                                 |

---

### 3. Setup Errors (`10,200 - 10,299`)
These errors occur during the SDK setup process.

| **Code** | **Message**                                            |
|----------|--------------------------------------------------------|
| 10200    | SaveSounds requires an array of tokens.                |
| 10201    | Lack of permissions granted to the SDK.                |
| 10204    | Invalid configuration provided to the SDK.             |

---

### 4. Device Errors (`10,300 - 10,399`)
These errors are related to device functionality and hardware usage.

| **Code** | **Message**                                            |
|----------|--------------------------------------------------------|
| 10300    | Unable to start detecting.                             |
| 10301    | Device media already playing.                          |
| 10302    | Device telephone call active.                          |

---

### 5. Hardware Errors (`10,400 - 10,499`)
These errors indicate hardware malfunctions or incompatibilities.

| **Code** | **Message**                                            |
|----------|--------------------------------------------------------|
| 10400    | Could not play - Playback failed due to a hardware or software issue. |
| 10401    | Could not record - Microphone access failed or unavailable. |

---

### 6. Emitting Errors (`10,500 - 10,599`)
These errors occur during ultrasonic signal emission.

| **Code** | **Message**                                            |
|----------|--------------------------------------------------------|
| 10500    | Error with getting audiocode.                          |

---

### 7. Detecting Errors (`10,600 - 10,699`)
These errors occur during ultrasonic signal detection.

| **Code** | **Message**                                            |
|----------|--------------------------------------------------------|
| 10600    | Unable to start detecting.                             |

---

### 8. Internal Errors (`10,700 - 10,799`)
These errors indicate unexpected issues within the SDK.

| **Code** | **Message**                                            |
|----------|--------------------------------------------------------|
| 10700    | Unknown internal SDK error.                            |

---

### 9. Invalid Argument Errors (`10,800 - 10,899`)
These errors occur due to invalid arguments passed to SDK functions.

| **Code** | **Message**                                            |
|----------|--------------------------------------------------------|
| 10800    | Invalid configuration provided to the SDK.             |

---

### 10. Network Errors (`10,900 - 10,999`)
These errors are related to network and connectivity issues.

| **Code** | **Message**                                            |
|----------|--------------------------------------------------------|
| 10900    | Lack of internet connectivity.                         |

---

### 11. Server Errors (HTTP Status Codes)
These errors correspond to HTTP status codes and indicate issues with the server.

| **Code** | **Message**                                            |
|----------|--------------------------------------------------------|
| 400      | Bad Request - Invalid input.                           |
| 401      | Unauthorized - Invalid credentials.                    |
| 404      | Not Found - Requested resource not found.              |
| 500      | Internal Server Error - Server encountered an unexpected condition. |
| 503      | Service Unavailable - Server is currently unable to handle the request. |

---

## Usage Example: Handling Errors with `EverlinkError`

When an error occurs, the SDK throws an `EverlinkError` exception containing the error code and message. You can catch and handle these exceptions as shown below:

```java
try {
    // Example SDK operation that may throw an error
    sdk.startDetecting();
} catch (EverlinkError e) {
    int errorCode = e.getErrorCode();
    String errorMessage = e.getMessage();

    // Handle the error based on the error code
    switch (errorCode) {
        case 10000:
            System.out.println("Token not valid. Please check your token.");
            break;
        case 10400:
            System.out.println("Playback failed. Please check audio settings or hardware.");
            break;
        case 10900:
            System.out.println("No internet connection. Please connect to the internet and try again.");
            break;
        case 400:
            System.out.println("Bad Request - Check your input.");
            break;
        default:
            System.out.println("An unknown error occurred. Code: " + errorCode + ", Message: " + errorMessage);
            break;
    }
}
```
## Quick Troubleshooting Guide

- **Setup Issues**: Ensure the SDK is properly initialized with valid configuration and all required dependencies are available.
- **Permissions**: Verify that required permissions (e.g., microphone, internet) are granted.
- **Device Issues**: Check that the device supports ultrasonic functionality and no other apps are blocking audio input/output.
- **Network Issues**: Confirm a stable internet connection if the SDK interacts with servers.
- **Server Issues**: If a server error occurs, check the HTTP status code and refer to the server documentation or logs for further information.

