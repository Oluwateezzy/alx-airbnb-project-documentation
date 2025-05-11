# UC-1: Register Account - Flowchart

```mermaid
flowchart TD
    A[Start: User selects Sign Up] --> B[Display Registration Form]
    B --> C[User enters personal info, email, password]
    C --> D{Validate Information}
    D -- Invalid --> E[Show error message]
    E --> B
    D -- Valid --> F[Create User Account in Database]
    F --> G[Send Verification Email]
    G --> H[User clicks verification link]
    H --> I[Activate User Account]
    I --> J[Account Ready: Redirect to Login Page]
