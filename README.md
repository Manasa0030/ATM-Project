# ATM Machine Application

A complete ATM simulation project built with **Java Swing** for GUI, **JDBC** for database operations, and **in-memory data storage**. The application provides a full-featured ATM experience with a user-friendly graphical interface.

---

## Table of Contents
- [Features](#features)
- [Prerequisites](#prerequisites)
- [Project Structure](#project-structure)
- [Setup & Installation](#setup--installation)
- [Compilation](#compilation)
- [Running the Application](#running-the-application)
- [Usage Guide](#usage-guide)
- [Sample Accounts](#sample-accounts)
- [Troubleshooting](#troubleshooting)
- [Technology Stack](#technology-stack)
- [Notes](#notes)

---

## Features

### Core Functionality
- **Account Access**: Login using a 4-digit account number (no PIN required)
- **Check Balance**: View current account balance in large, easy-to-read format
- **Withdraw**: Withdraw money from your account with balance validation
- **Deposit**: Deposit money into your account
- **Logout**: Securely log out from the ATM

### User Interface
- **Full-Screen Maximized Window**: Takes advantage of the full display
- **Large, Clear Fonts**: 32pt for titles, 18pt for labels, 48pt for balance display
- **Intuitive Navigation**: Card-based layout with smooth panel transitions
- **Input Validation**: Prevents invalid transactions (negative amounts, insufficient balance)
- **Confirmation Messages**: Clear feedback for all transactions

### Data Storage
- **In-Memory Database**: No external MySQL dependency required
- **Sample Accounts**: Pre-loaded with test data
- **Transaction History**: Track all deposits and withdrawals (in current session)

---

## Prerequisites

- **Java**: JDK 8 or higher (Java Runtime Environment)
- **Operating System**: Windows, macOS, or Linux

**Note**: MySQL Server is NOT required. The application uses in-memory data storage.

---

## Project Structure

```
placement project/
├── src/atm/
│   ├── Main.java                    # Application entry point
│   ├── ATMGUI.java                  # Swing GUI with all panels
│   ├── ATMService.java              # Business logic service
│   ├── InMemoryDatabase.java        # In-memory data storage
│   ├── User.java                    # User model class
│   ├── Transaction.java             # Transaction model class
│   ├── DatabaseConnection.java      # Legacy database connection (optional)
│
├── db/
│   └── atm.sql                      # SQL schema (reference only)
│
├── mysql-connector-j-8.0.33.jar    # JDBC driver (optional)
├── README.md                        # This file

```

### File Descriptions

| File | Purpose |
|------|---------|
| `Main.java` | Entry point; launches the ATMGUI |
| `ATMGUI.java` | All Swing panels: Login, Menu, Withdraw, Deposit, Balance |
| `ATMService.java` | Business logic: authentication, balance checks, withdraw/deposit operations |
| `InMemoryDatabase.java` | HashMap-based storage for users and transactions; loads sample data |
| `User.java` | Model class representing a user account |
| `Transaction.java` | Model class representing a transaction record |
| `DatabaseConnection.java` | Legacy JDBC connection class (not used with in-memory database) |

---

## Setup & Installation

### Option 1: Quick Start (Recommended)

No additional setup required! The application uses in-memory data storage.

### Option 2: With External MySQL (Optional)

If you want to use a real MySQL database:

1. **Install MySQL Server**
   - Download from [mysql.com](https://www.mysql.com/downloads/)
   - Install and start the MySQL service

2. **Import Database Schema**
   ```powershell
   mysql -u root -p < db\atm.sql
   ```

3. **Update Credentials** (if different from default)
   - Edit `src/atm/DatabaseConnection.java`
   - Change `USER` and `PASSWORD` constants
   - Rebuild the project

4. **Run**
   ```powershell
   java -cp "src;.;mysql-connector-j-8.0.33.jar" atm.Main
   ```

---

## Compilation

### Prerequisites
- JDK 8+ installed and added to PATH

### Windows Command Prompt / PowerShell

```powershell
# Navigate to project directory
cd "C:\Users\manas\Downloads\placement project"

# Compile all Java files
javac -cp ".;mysql-connector-j-8.0.33.jar" src\atm\*.java
```

**Expected Output**: No errors. Compiled `.class` files appear in `src/atm/` directory.

### macOS / Linux

```bash
cd placement\ project
javac -cp ".:mysql-connector-j-8.0.33.jar" src/atm/*.java
```

---

## Running the Application

### From Command Line

```powershell
# Windows
java -cp "src;.;mysql-connector-j-8.0.33.jar" atm.Main

# macOS / Linux
java -cp "src:.:mysql-connector-j-8.0.33.jar" atm.Main
```

### Expected Behavior
- Window opens, maximized to full screen
- Login panel displays with "Account Number" input field
- Application is ready to use

---

## Usage Guide

### 1. Login Screen
- **Input**: Enter a 4-digit account number
- **Valid Accounts**: `1234`, `5678`, `8055`
- **Click**: "Continue" button
- **Result**: Access main menu if account exists, error message otherwise

### 2. Main Menu
- **Withdraw**: Withdraw funds from account
- **Deposit**: Deposit funds into account
- **Check Balance**: View current account balance
- **Logout**: Return to login screen

### 3. Withdraw Transaction
- **Input**: Enter amount (must be > $0 and ≤ current balance)
- **Click**: "Withdraw" button
- **Feedback**: Success message with amount, or error message
- **After**: Automatically returns to main menu

### 4. Deposit Transaction
- **Input**: Enter amount (must be > $0)
- **Click**: "Deposit" button
- **Feedback**: Success message with amount, or error message
- **After**: Automatically returns to main menu

### 5. Check Balance
- **Displays**: Current account balance in large, clear text
- **Click**: "Back" button to return to main menu

### 6. Logout
- **Action**: Returns to login screen
- **Session**: All data resets (in-memory only)

---

## Sample Accounts

| Account # | Name | Initial Balance |
|-----------|------|-----------------|
| 1234 | John Doe | $1,000.00 |
| 5678 | Jane Smith | $500.00 |
| 8055 | Alex Brown | $750.00 |

**Note**: No PIN is required for login. Account number alone is sufficient.

---

## Troubleshooting

### Issue: "Invalid account number" when using correct account
**Solution**: 
- Ensure you're using one of the valid accounts: `1234`, `5678`, or `8055`
- Check that you've entered exactly 4 digits
- Click "Continue" button after input

### Issue: Compilation fails with "cannot find symbol"
**Solution**:
- Ensure you're in the project root directory
- Verify JDK is installed: `javac -version`
- Check the classpath syntax (`;` for Windows, `:` for macOS/Linux)

### Issue: "Could not find or load main class atm.Main"
**Solution**:
- Verify files are compiled: Check for `.class` files in `src/atm/`
- Ensure classpath includes `src` directory
- Recompile: `javac -cp ".;mysql-connector-j-8.0.33.jar" src\atm\*.java`

### Issue: Window doesn't maximize or display
**Solution**:
- Ensure Java version is 8+: `java -version`
- Try moving window to primary display
- Check screen resolution settings

---

## Technology Stack

| Technology | Version | Purpose |
|------------|---------|---------|
| Java | 8+ | Core language |
| Swing | Built-in | GUI framework |
| JDBC | 8.0.33 | Database connectivity (optional) |
| MySQL | 5.7+ | External database (optional) |

### Key Libraries Used
- `java.swing.*` - UI components (JFrame, JPanel, JButton, JTextField, etc.)
- `java.awt.*` - Layout managers (GridBagLayout, BorderLayout, GridLayout)
- `java.util.*` - Collections (HashMap, ArrayList, List)
- `java.sql.*` - Database operations (Connection, PreparedStatement, ResultSet)

---

## Features in Detail

### Authentication System
- **Single-Factor**: Account number only
- **No PIN Required**: For simplicity and demo purposes
- **Sample Data**: Pre-loaded in `InMemoryDatabase.java`

### Transaction Processing
- **Withdraw**: Decreases balance, validates sufficient funds
- **Deposit**: Increases balance, accepts any positive amount
- **History**: Logged in memory (not persisted after logout)

### Data Persistence
- **Current Session**: All changes persist while running
- **After Logout**: All data resets to initial state
- **Permanent Storage**: Requires external MySQL database (optional)

### UI/UX Highlights
- **Card-Based Navigation**: Smooth transitions between screens
- **Large Fonts**: Easy readability (32pt, 48pt titles)
- **Responsive Layout**: GridBagLayout with proper spacing
- **Input Validation**: Prevents invalid transactions
- **Immediate Feedback**: Confirmation dialogs for all actions

---

## Security Notes

### This is a DEMO Application
- **Not suitable for production ATMs**
- **No encryption** of credentials or transactions
- **No audit logging** of transaction history
- **In-memory only** - data lost on logout/restart

### For Production Use, Implement:
1. **Encryption**: AES for data at rest, TLS for transmission
2. **Secure Authentication**: Multi-factor authentication (PIN + biometric)
3. **Database**: Hardened MySQL or PostgreSQL with backups
4. **Logging**: Comprehensive audit trails for all transactions
5. **Rate Limiting**: Prevent brute-force attacks
6. **Testing**: Unit and integration tests before deployment
7. **Compliance**: Adhere to PCI-DSS and banking regulations

---

## How to Extend

### Add a New Account
Edit `InMemoryDatabase.java`:
```java
static {
    users.put("1234", new User("1234", "1234", "John Doe", 1000.00));
    users.put("NEW_ACCOUNT", new User("NEW_ACCOUNT", "pin", "Name", 0.00)); // Add here
}
```

### Switch to External MySQL Database
1. Uncomment JDBC code in `ATMService.java`
2. Ensure MySQL is running and database is set up
3. Update credentials in `DatabaseConnection.java`
4. Recompile and run

### Modify the UI
Edit panel constructors in `ATMGUI.java`:
- Change fonts: `setFont(new Font("Arial", Font.BOLD, size))`
- Change colors: `setBackground(new Color(r, g, b))`
- Adjust layout: Modify `GridBagConstraints` values

---

## Version History

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | April 2026 | Initial release with full-screen GUI, withdraw, deposit, and balance check features |

---

**Last Updated**: April 30, 2026
- In a real ATM system, additional security measures would be required.
