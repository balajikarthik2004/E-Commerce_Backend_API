# 🛍️ E-Commerce Backend API

  

A complete MERN stack backend for e-commerce application with admin and customer roles, built with Node.js, Express.js, MongoDB, and JWT authentication.

  

## 🌟 Features

  

### 🔐 Authentication & Authorization

- JWT-based authentication with access & refresh tokens

- Role-based access control (Admin & Customer)

- Secure password hashing with bcrypt

- Token refresh mechanism

- Protected routes with middleware

  

### 👥 User Management

- User registration and login

- Profile management (view/update)

- Password change functionality

- Account deletion

- Admin user management (view all users, update roles, delete users)

  

### 📦 Product Management

-  **Admin**: Full CRUD operations for products

-  **Customer**: Browse and view products

- Advanced search by name and tags

- Filter by category

- Pagination support

- Product details with creator information

  

### 🛡️ Security Features

- Input validation with Joi

- Rate limiting to prevent abuse

- Helmet.js for security headers

- CORS configuration

- Password strength enforcement

- Secure token handling

  

### 📚 API Documentation

- Comprehensive Swagger/OpenAPI documentation

- Interactive API testing interface

- Request/response schemas

- Authentication examples

  

🏗️ Project Structure

text

    ecommerce-backend/
    ├── config/
    │ └── database.js       # MongoDB connection
    ├── controllers/
    │ ├── authController.js     # Authentication logic
    │ ├── productController.js # Product management
    │ └── userController.js # User management
    ├── middleware/
    │ ├── auth.js # Authentication middleware
    │ ├── validation.js # Request validation
    │ └── errorHandler.js # Error handling
    ├── models/
    │ ├── User.js # User schema
    │ └── Product.js # Product schema
    ├── routes/
    │ ├── auth.js # Authentication routes
    │ ├── products.js # Product routes
    │ └── users.js # User routes
    ├── utils/
    │ └── validation.js # Joi validation schemas
    ├── docs/
    │ └── swagger.js # Swagger configuration
    ├── .env # Environment variables
    ├── server.js # Main server file
    └── README.md     # Project documentation

## 🚀 Quick Start

**Prerequisites**

 - Node.js (v14 or higher) 
 - MongoDB Atlas account or local MongoDB 
 - npm or yarn Installation

**Clone the repository**
```
git clone https://github.com/balajikarthik2004/E-Commerce_Backend_API

cd ecommerce-backend
```

 **Install dependencies**

```
npm install
```
Environment Configuration
```
cp .env.example .env
```
# Edit .env with your configuration

**Configure Environment Variables**

## env
```
NODE_ENV=development

PORT=5000

MONGODB_URI=mongodb+srv://username:password@cluster.mongodb.net/ecommerce

JWT_ACCESS_SECRET=your_super_secret_access_key_here

JWT_REFRESH_SECRET=your_super_secret_refresh_key_here

JWT_ACCESS_EXPIRY=15m

JWT_REFRESH_EXPIRY=7d
```

## Start the server

 **Development mode with auto-restart**

    npm run dev

# Production mode

    npm start

Verify the setup

**Server should run on** http://localhost:5000

**API documentation available at** http://localhost:5000/api-docs

## 📡 API Endpoints

**🔐 Authentication Endpoints**

Method Endpoint Description Access

> POST /api/auth/register  Register new user Public
> 
> POST /api/auth/login User login Public
> 
> POST /api/auth/refresh-token Refresh access token Public
> 
> POST /api/auth/logout User logout Authenticated

**👤 User Endpoints**

Method Endpoint Description Access

> GET /api/users/profile Get user profile Authenticated
> 
> PUT /api/users/profile Update user profile Authenticated 
> 
>POST /api/users/change-password Change password Authenticated 
>
>DELETE /api/users/delete-account Delete user account Authenticated 
>
> GET /api/users Get all users Admin only 
> 
> GET /api/users/:id Get user by ID Admin only 
> 
> PUT /api/users/:id/role Update user role Admin only 
> 
> DELETE /api/users/:id Delete user Admin only

**📦 Product Endpoints**

Method Endpoint Description Access

> GET /api/products Get all products (with filters) Authenticated
> 
> GET /api/products/:id Get product by ID Authenticated
> 
> POST /api/products Create new product Admin only
> 
> PUT /api/products/:id Update product Admin only
> 
> DELETE /api/products/:id Delete product Admin only

**🩺 System Endpoints**

Method Endpoint Description

> GET /api-docs Swagger API documentation

## 🔧 API Usage Examples

## User Registration
```
curl -X POST http://localhost:5000/api/auth/register \

-H "Content-Type: application/json" \

-d '{

"name": "John Doe",

"email": "john@example.com",

"password": "password123",

"role": "customer"

}'
```
**User Login**

```bash

curl -X POST http://localhost:5000/api/auth/login \

-H "Content-Type: application/json" \

-d '{

"email": "john@example.com",

"password": "password123"

}'
```
**Create Product (Admin)**

```
curl -X POST http://localhost:5000/api/products \

-H "Content-Type: application/json" \

-H "Authorization: Bearer YOUR_ACCESS_TOKEN" \

-d '{

"name": "iPhone 15 Pro",

"description": "Latest iPhone with advanced features",

"price": 999,

"stock": 50,

"category": "Electronics",

"tags": ["smartphone", "apple"],

"imageUrl": "https://example.com/image.jpg"

}'
```
**Get Products with Pagination**

```

curl -X GET "http://localhost:5000/api/products?page=1&limit=10&category=Electronics" \

-H "Authorization: Bearer YOUR_ACCESS_TOKEN"
```
**🎯 Request/Response Format**

Success Response
```
json

{

"success": true,

"message": "Operation successful",

"data": {

// Response data

}


}

Error Response

json

{

"success": false,

"message": "Error description"

}
```

    **🗄️ Database Models**
    
    User Model
    
    javascript
    
    {
    
    name: String,
    
    email: String (unique),
    
    password: String (hashed),
    
    role: String (enum: ['admin', 'customer']),
    
    refreshToken: String,
    
    createdAt: Date,
    
    updatedAt: Date
    
    }
    
    Product Model
    
    javascript
    
    {
    
    name: String,
    
    description: String,
    
    price: Number,
    
    stock: Number,
    
    category: String,
    
    tags: [String],
    
    imageUrl: String,
    
    createdBy: ObjectId (ref: User),
    
    isActive: Boolean,
    
    createdAt: Date,
    
    updatedAt: Date
    
    }

## 🔒 Authentication Flow

Register/Login → Get accessToken and refreshToken

  

Access Protected Routes → Include Authorization: Bearer <accessToken> header

  

Token Expiry → Use /api/auth/refresh-token with refreshToken to get new tokens

  

Logout → Invalidates refreshToken on server

  

## 🚀 Deployment

> Deploy to Render
> 
> Create a new Web Service on Render
> 
>   
> 
> Connect your GitHub repository
> 
>   
> 
> Configure environment variables in Render dashboard
> 
>   
> 
> Deploy automatically on git push

  

## Environment Variables for Production

**env**

> NODE_ENV=production
> 
> MONGODB_URI=your_mongodb_atlas_connection_string
> 
> JWT_ACCESS_SECRET=strong_production_secret
> 
> JWT_REFRESH_SECRET=strong_production_refresh_secret

**🛠️ Development**

Scripts
```

npm run dev # Development mode with nodemon

npm start # Production start

npm test # Run tests
```
## 🤝 Contributing

**Fork the repository**

  

Create a feature branch (git checkout -b feature/amazing-feature)

  

Commit your changes (git commit -m 'Add amazing feature')

  

Push to the branch (git push origin feature/amazing-feature)

  

Open a Pull Request

  

## 📝 License

This project is licensed under the MIT License - see the LICENSE file for details.

  

## 🆘 Support

For support, please:

  

Check the API documentation at /api-docs

  

Review the error messages in responses

  

Check server logs for detailed errors

  

Open an issue on GitHub with detailed description

  

## 📞 Contact

GitHub Issues: Project Issues
Email: balajikarthik004@gmail.com

  

⭐ Don't forget to star the repository if you find this project useful!

  

## Live Demo

Deployed Backend Link (Render): [https://e-commerce-backend-m0uj.onrender.com](https://e-commerce-backend-m0uj.onrender.com)  

Live Swagger API Documentation: [https://e-commerce-backend-m0uj.onrender.com/api-docs](https://e-commerce-backend-m0uj.onrender.com/api-docs)



