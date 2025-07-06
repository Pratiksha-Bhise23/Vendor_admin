# Vendor Admin Dashboard
A modern, responsive vendor admin dashboard template designed to streamline administrative tasks and provide an intuitive interface for managing web applications, services, or data workflows. This project offers a clean and customizable solution for developers to build feature-rich dashboards with ease.

### Table of Contents

- Introduction
- Features
- Technologies
- Installation
- Folder Structure
- API Endpoints
- Usage
- Contributing

### Introduction
The Vendor Admin Dashboard is a free and open-source template built to provide a user-friendly interface for managing backend systems. It includes a variety of components and layouts suitable for web applications, e-commerce platforms, or data management systems. With a focus on responsiveness and customization, this dashboard is ideal for developers looking to create professional admin panels quickly.


### Features
Responsive Design: Fully responsive layout that adapts to all screen sizes, from mobile to desktop.
Modular Components: Reusable UI components like charts, tables, forms, and cards.
Customizable Themes: CSS variables for easy theming and styling adjustments.
User Management: Interface for managing users, roles, and permissions (if applicable).
Data Visualization: Integration with charting libraries for displaying data insights.
Cross-Browser Compatibility: Works seamlessly across modern browsers.


### Technologies
Frontend:
Reactjs
JavaScript (ES6+)
Tailwind CSS


Backend (if applicable):
Node.js (with Express.js for API, if included)
RESTful API


Build Tools:
npm (for dependency management)


Libraries (optional, based on common dashboard setups):
Chart.js or ApexCharts for data visualization
jQuery (if used for DOM manipulation)


Version Control:
Git



### Installation
Follow these steps to set up the project locally:

Clone the Repository:
git clone s://github.com/Pratiksha-Bhise23/admin_dashboard.git
cd admin_dashboard


Install Dependencies:
npm install


Start the Development Server:
npm start

The application will be available at ://localhost:5000 (port may vary).

Build for Production:
npm run build

The optimized build will be available in the dist/ directory.



## API Reference

### Authentication and Vendor Management APIs (`/api/auth`)

#### Login
```
  POST /api/auth/login
```
| Parameter  | Type     | Description                          |
| :--------- | :------- | :----------------------------------- |
| `email`    | `string` | **Required**. Vendor admin's email   |
| `password` | `string` | **Required**. Vendor admin's password|

**Description**: Authenticates a vendor admin by email and password, returning a JWT token upon successful login.

**Response**:
- Success: `{ message: "Login successful", token: "..." }`
- Error: `{ message: "Vendor Admin not found" }`, `{ message: "Invalid credentials" }`, or `{ message: "Server error", error: "..." }`

---

#### Logout
```
  POST /api/auth/logout
```
| Parameter      | Type     | Description                          |
| :------------- | :------- | :----------------------------------- |
| `Authorization`| `string` | **Required**. Bearer JWT token       |

**Description**: Logs out the vendor admin by clearing the token cookie.

**Response**:
- Success: `{ message: "Logout successful" }`
- Error: `{ message: "Server error", error: "..." }`

---

#### Add Vendor
```
  POST /api/auth/addVendor
```
| Parameter       | Type     | Description                          |
| :-------------- | :------- | :----------------------------------- |
| `Authorization` | `string` | **Required**. Bearer JWT token       |
| `name`          | `string` | **Required**. Vendor's full name     |
| `company_name`  | `string` | **Required**. Vendor's company name  |
| `company_type`  | `string` | **Required**. Type of company        |
| `gstin`         | `string` | **Required**. GSTIN number           |
| `contact_number`| `string` | **Required**. Contact phone number   |
| `email`         | `string` | **Required**. Vendor's email         |
| `password`      | `string` | **Required**. Vendor's password      |
| `address`       | `string` | **Required**. Vendor's address       |
| `pincode`       | `string` | **Required**. Vendor's pincode       |

**Description**: Adds a new vendor to the database, hashes the password, and sends an email with account details. Only accessible to users with the "vendor" role.

**Response**:
- Success: `{ message: "Vendor added successfully", vendor: { id, name, company_name, email } }`
- Error: `{ message: "Unauthorized: Only Super Admins can add Vendors" }`, `{ message: "All fields are required" }`, `{ message: "Vendor with this email already exists" }`, or `{ message: "Server error", error: "..." }`

---

#### Get All Vendors
```
  GET /api/auth/getAllVendors
```
| Parameter      | Type     | Description                          |
| :------------- | :------- | :----------------------------------- |
| `Authorization`| `string` | **Required**. Bearer JWT token       |

**Description**: Retrieves a list of all vendors, including their details and active status. Only accessible to users with the "vendor" role.

**Response**:
- Success: `{ message: "Vendors fetched successfully", vendors: [{ id, name, company_name, company_type, gstin, contact_number, email, address, pincode, created_at, is_active }, ...] }`
- Error: `{ message: "Unauthorized: Only vendor Admins can view Vendors" }` or `{ message: "Server error", error: "..." }`

---

#### Update Vendor
```
  PUT /api/auth/update-vendor/:id
```
| Parameter       | Type     | Description                          |
| :-------------- | :------- | :----------------------------------- |
| `Authorization` | `string` | **Required**. Bearer JWT token       |
| `id`            | `string` | **Required**. Vendor ID (path)       |
| `name`          | `string` | **Optional**. Vendor's full name     |
| `company_name`  | `string` | **Optional**. Vendor's company name  |
| `company_type`  | `string` | **Optional**. Type of company        |
| `gstin`         | `string` | **Optional**. GSTIN number           |
| `contact_number`| `string` | **Optional**. Contact phone number   |
| `email`         | `string` | **Optional**. Vendor's email         |
| `password`      | `string` | **Optional**. Vendor's new password  |
| `address`       | `string` | **Optional**. Vendor's address       |
| `pincode`       | `string` | **Optional**. Vendor's pincode       |

**Description**: Updates an existing vendor's details. If a new password is provided, it is hashed and an email is sent with the updated details. Only accessible to users with the "vendor" role.

**Response**:
- Success: `{ message: "Vendor updated successfully", vendor: { id, name, company_name, email, company_type } }`
- Error: `{ message: "Unauthorized: Only Vendor Admins can update vendors" }`, `{ message: "Vendor not found" }`, or `{ message: "Server error", error: "..." }`

---

#### Request Vendor Deactivation
```
  POST /api/auth/vendors/:id/deactivate
```
| Parameter      | Type     | Description                          |
| :------------- | :------- | :----------------------------------- |
| `Authorization`| `string` | **Required**. Bearer JWT token       |
| `id`           | `string` | **Required**. Vendor ID (path)       |

**Description**: Submits a deactivation request for a vendor, setting the status to "pending_deactivation". Only accessible to users with the "vendor" role.

**Response**:
- Success: `{ message: "Vendor deactivation request submitted successfully. Awaiting Super Admin approval." }`
- Error: `{ message: "Unauthorized: Only Vendor Admins can request vendor deactivation" }`, `{ message: "Vendor not found" }`, `{ message: "A deactivation request is already pending for this vendor" }`, `{ message: "Vendor is already deactivated" }`, or `{ message: "Server error", error: "..." }`

---

#### Request Vendor Reactivation
```
  POST /api/auth/vendors/:id/activate
```
| Parameter      | Type     | Description                          |
| :------------- | :------- | :----------------------------------- |
| `Authorization`| `string` | **Required**. Bearer JWT token       |
| `id`           | `string` | **Required**. Vendor ID (path)       |

**Description**: Submits a reactivation request for a vendor, setting the status to "pending_activation". Only accessible to users with the "vendor" role.

**Response**:
- Success: `{ message: "Vendor activation request submitted successfully. Awaiting Super Admin approval." }`
- Error: `{ message: "Unauthorized: Only Vendor Admins can request reactivation" }`, `{ message: "Vendor not found" }`, `{ message: "Activation request is already pending" }`, `{ message: "Vendor is already active" }`, or `{ message: "Server error", error: "..." }`

---

#### Reset Vendor Status
```
  POST /api/auth/vendors/:id/reset-status
```
| Parameter      | Type     | Description                          |
| :------------- | :------- | :----------------------------------- |
| `Authorization`| `string` | **Required**. Bearer JWT token       |
| `id`           | `string` | **Required**. Vendor ID (path)       |

**Description**: Resets a vendor's status to "active". Note: This endpoint references a MongoDB `Vendor` model (`Vendor.findById`), which conflicts with the PostgreSQL-based `vendors` table used elsewhere. This may indicate incomplete or inconsistent implementation.

**Response**:
- Success: `{ message: "Vendor reactivated successfully." }`
- Error: `{ message: "Vendor not found" }` or `{ message: "Internal Server Error" }`

---

### Notes
- **Authentication**: All routes except `/api/auth/login` require a valid JWT token in the `Authorization` header (Bearer format).
- **Environment Variables**: Ensure `process.env.JWT_SECRET` and other required variables are set in `.env`.
- **Database**: Assumes a PostgreSQL database with a `vendors` table for most endpoints, but `resetVendorStatus` references a MongoDB model, suggesting a potential inconsistency.
- **Role-Based Access**: Most endpoints are restricted to users with the "vendor" role.
- **Email Service**: The `addVendor` and `updateVendor` endpoints use a `sendEmail` service to send account details when a new vendor is added or a password is updated.
- **Error Handling**: All endpoints include error handling with appropriate status codes and messages.



## API Reference

### Authentication and Vendor Management APIs (`/api/auth`)

#### Login
```
  POST /api/auth/login
```
| Parameter  | Type     | Description                          |
| :--------- | :------- | :----------------------------------- |
| `email`    | `string` | **Required**. Vendor admin's email   |
| `password` | `string` | **Required**. Vendor admin's password|

**Description**: Authenticates a vendor admin by email and password, returning a JWT token upon successful login.

**Response**:
- Success: `{ message: "Login successful", token: "..." }`
- Error: `{ message: "Vendor Admin not found" }`, `{ message: "Invalid credentials" }`, or `{ message: "Server error", error: "..." }`

---

#### Logout
```
  POST /api/auth/logout
```
| Parameter      | Type     | Description                          |
| :------------- | :------- | :----------------------------------- |
| `Authorization`| `string` | **Required**. Bearer JWT token       |

**Description**: Logs out the vendor admin by clearing the token cookie.

**Response**:
- Success: `{ message: "Logout successful" }`
- Error: `{ message: "Server error", error: "..." }`

---

#### Add Vendor
```
  POST /api/auth/addVendor
```
| Parameter       | Type     | Description                          |
| :-------------- | :------- | :----------------------------------- |
| `Authorization` | `string` | **Required**. Bearer JWT token       |
| `name`          | `string` | **Required**. Vendor's full name     |
| `company_name`  | `string` | **Required**. Vendor's company name  |
| `company_type`  | `string` | **Required**. Type of company        |
| `gstin`         | `string` | **Required**. GSTIN number           |
| `contact_number`| `string` | **Required**. Contact phone number   |
| `email`         | `string` | **Required**. Vendor's email         |
| `password`      | `string` | **Required**. Vendor's password      |
| `address`       | `string` | **Required**. Vendor's address       |
| `pincode`       | `string` | **Required**. Vendor's pincode       |

**Description**: Adds a new vendor to the database, hashes the password, and sends an email with account details. Only accessible to users with the "vendor" role.

**Response “‘:
- Success: `{ message: "Vendor added successfully", vendor: { id, name, company_name, email } }`
- Error: `{ message: "Unauthorized: Only Super Admins can add Vendors" }`, `{ message: "All fields are required" }`, `{ message: "Vendor with this email already exists" }`, or `{ message: "Server error", error: "..." }`

---

#### Get All Vendors
```
  GET /api/auth/getAllVendors
```
| Parameter      | Type     | Description                          |
| :------------- | :------- | :----------------------------------- |
| `Authorization`| `string` | **Required**. Bearer JWT token       |

**Description**: Retrieves a list of all vendors, including their details and active status. Only accessible to users with the "vendor" role.

**Response “‘:
- Success: `{ message: "Vendors fetched successfully", vendors: [{ id, name, company_name, company_type, gstin, contact_number, email, address, pincode, created_at, is_active }, ...] }`
- Error: `{ message: "Unauthorized: Only vendor Admins can view Vendors" }` or `{ message: "Server error", error: "..." }`

---

#### Update Vendor
```
  PUT /api/auth/update-vendor/:id
```
| Parameter       | Type     | Description                          |
| :-------------- | :------- | :----------------------------------- |
| `Authorization` | `string` | **Required**. Bearer JWT token       |
| `id`            | `string` | **Required**. Vendor ID (path)       |
| `name`          | `string` | **Optional**. Vendor's full name     |
| `company_name`  | `string` | **Optional**. Vendor's company name  |
| `company_type`  | `string` | **Optional**. Type of company        |
| `gstin`         | `string` | **Optional**. GSTIN number           |
| `contact_number`| `string` | **Optional**. Contact phone number   |
| `email`         | `string` | **Optional**. Vendor's email         |
| `password`      | `string` | **Optional**. Vendor's new password  |
| `address`       | `string` | **Optional**. Vendor's address       |
| `pincode`       | `string` | **Optional**. Vendor's pincode       |

**Description**: Updates an existing vendor's details. If a new password is provided, it is hashed and an email is sent with the updated details. Only accessible to users with the "vendor" role.

**Response “‘:
- Success: `{ message: "Vendor updated successfully", vendor: { id, name, company_name, email, company_type } }`
- Error: `{ message: "Unauthorized: Only Vendor Admins can update vendors" }`, `{ message: "Vendor not found" }`, or `{ message: "Server error", error: "..." }`

---

#### Request Vendor Deactivation
```
  POST /api/auth/vendors/:id/deactivate
```
| Parameter      | Type     | Description                          |
| :------------- | :------- | :----------------------------------- |
| `Authorization`| `string` | **Required**. Bearer JWT token       |
| `id`           | `string` | **Required**. Vendor ID (path)       |

**Description**: Submits a deactivation request for a vendor, setting the status to "pending_deactivation". Only accessible to users with the "vendor" role.

**Response “‘:
- Success: `{ message: "Vendor deactivation request submitted successfully. Awaiting Super Admin approval." }`
- Error: `{ message: "Unauthorized: Only Vendor Admins can request vendor deactivation" }`, `{ message: "Vendor not found" }`, `{ message: "A deactivation request is already pending for this vendor" }`, `{ message: "Vendor is already deactivated" }`, or `{ message: "Server error", error: "..." }`

---

#### Request Vendor Reactivation
```
  POST /api/auth/vendors/:id/activate
```
| Parameter      | Type     | Description                          |
| :------------- | :------- | :----------------------------------- |
| `Authorization`| `string` | **Required**. Bearer JWT token       |
| `id`           | `string` | **Required**. Vendor ID (path)       |

**Description**: Submits a reactivation request for a vendor, setting the status to "pending_activation". Only accessible to users with the "vendor" role.

**Response “‘:
- Success: `{ message: "Vendor activation request submitted successfully. Awaiting Super Admin approval." }`
- Error: `{ message: "Unauthorized: Only Vendor Admins can request reactivation" }`, `{ message: "Vendor not found" }`, `{ message: "Activation request is already pending" }`, `{ message: "Vendor is already active" }`, or `{ message: "Server error", error: "..." }`

---

#### Reset Vendor Status
```
  POST /api/auth/vendors/:id/reset-status
```
| Parameter      | Type     | Description                          |
| :------------- | :------- | :----------------------------------- |
| `Authorization`| `string` | **Required**. Bearer JWT token       |
| `id`           | `string` | **Required**. Vendor ID (path)       |

**Description**: Resets a vendor's status to "active". Note: This endpoint references a MongoDB `Vendor` model (`Vendor.findById`), which conflicts with the PostgreSQL-based `vendors` table used elsewhere. This may indicate incomplete or inconsistent implementation.

**Response “‘:
- Success: `{ message: "Vendor reactivated successfully." }`
- Error: `{ message: "Vendor not found" }` or `{ message: "Internal Server Error" }`

---

### Notes
- **Authentication**: All routes except `/api/auth/login` require a valid JWT token in the `Authorization` header (Bearer format).
- **Environment Variables**: Ensure `process.env.JWT_SECRET` and other required variables are set in `.env`.
- **Database**: Assumes a PostgreSQL database with a `vendors` table for most endpoints, but `resetVendorStatus` references a MongoDB model, suggesting a potential inconsistency.
- **Role-Based Access**: Most endpoints are restricted to users with the "vendor" role.
- **Email Service**: The `addVendor` and `updateVendor` endpoints use a `sendEmail` service to send account details when a new vendor is added or a password is updated.
- **Error Handling**: All endpoints include error handling with appropriate status codes and messages.


Open the dashboard in your browser at http://localhost:5000 after running npm start.

### Contributing
Contributions are welcome! To contribute:

Fork the repository.
Create a new branch (git checkout -b feature/your-feature).
Make your changes and commit (git commit -m "Add your feature").
Push to the branch (git push origin feature/your-feature).
Open a pull request to the main branch.

Please ensure your code follows the project's coding standards and includes relevant tests (if applicable). Check the CONTRIBUTING.md file for detailed guidelines (if available).

