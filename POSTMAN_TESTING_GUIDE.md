# Postman Testing Guide - Product Catalog API

## 🚀 Complete API Testing Guide with Request Bodies

### **Base URL**: `http://localhost:3000`

---

## **1. Authentication Endpoints**

### **1.1 Register User**

```
POST /auth/register
```

**Headers:**

```
Content-Type: application/json
```

**Request Body:**

```json
{
  "username": "john_doe",
  "email": "john@example.com",
  "password": "password123",
  "role": "admin"
}
```

**Alternative (Customer Role):**

```json
{
  "username": "jane_customer",
  "email": "jane@example.com",
  "password": "password123",
  "role": "customer"
}
```

**Expected Response (201):**

```json
{
  "message": "User created successfully"
}
```

---

### **1.2 Login User**

```
POST /auth/login
```

**Headers:**

```
Content-Type: application/json
```

**Request Body:**

```json
{
  "email": "john@example.com",
  "password": "password123"
}
```

**Expected Response (200):**

```json
{
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
}
```

---

## **2. Category Management Endpoints**

### **2.1 Create Category (Admin Only)**

```
POST /categories
```

**Headers:**

```
Content-Type: application/json
Authorization: Bearer YOUR_JWT_TOKEN
```

**Request Body:**

```json
{
  "name": "Electronics",
  "description": "Electronic devices and gadgets"
}
```

**Alternative Categories:**

```json
{
  "name": "Clothing",
  "description": "Fashion and apparel items"
}
```

```json
{
  "name": "Books",
  "description": "Books and publications"
}
```

**Expected Response (201):**

```json
{
  "_id": "687aedeb71978cc6a617c505",
  "name": "Electronics",
  "description": "Electronic devices and gadgets",
  "__v": 0
}
```

---

### **2.2 Get All Categories**

```
GET /categories
```

**Headers:** None required

**Request Body:** None

**Expected Response (200):**

```json
[
  {
    "_id": "687aedeb71978cc6a617c505",
    "name": "Electronics",
    "description": "Electronic devices and gadgets"
  },
  {
    "_id": "687aedeb71978cc6a617c506",
    "name": "Clothing",
    "description": "Fashion and apparel items"
  }
]
```

---

### **2.3 Get Category by ID**

```
GET /categories/{category_id}
```

**Headers:** None required

**Request Body:** None

**Expected Response (200):**

```json
{
  "_id": "687aedeb71978cc6a617c505",
  "name": "Electronics",
  "description": "Electronic devices and gadgets"
}
```

---

### **2.4 Update Category (Admin Only)**

```
PUT /categories/{category_id}
```

**Headers:**

```
Content-Type: application/json
Authorization: Bearer YOUR_JWT_TOKEN
```

**Request Body:**

```json
{
  "name": "Advanced Electronics",
  "description": "High-tech electronic devices and gadgets"
}
```

**Expected Response (200):**

```json
{
  "_id": "687aedeb71978cc6a617c505",
  "name": "Advanced Electronics",
  "description": "High-tech electronic devices and gadgets"
}
```

---

### **2.5 Delete Category (Admin Only)**

```
DELETE /categories/{category_id}
```

**Headers:**

```
Authorization: Bearer YOUR_JWT_TOKEN
```

**Request Body:** None

**Expected Response (200):**

```json
{
  "message": "Category deleted"
}
```

---

## **3. Product Management Endpoints**

### **3.1 Create Product (Admin Only)**

```
POST /products
```

**Headers:**

```
Content-Type: application/json
Authorization: Bearer YOUR_JWT_TOKEN
```

**Basic Product:**

```json
{
  "name": "iPhone 15",
  "description": "Latest iPhone with advanced features",
  "category": "Electronics",
  "price": 999.99,
  "stock": 50,
  "image": "https://example.com/iphone15.jpg",
  "variants": [
    {
      "size": "128GB",
      "color": "Black",
      "quantity": 20
    },
    {
      "size": "256GB",
      "color": "Blue",
      "quantity": 30
    }
  ]
}
```

**Product with Discount:**

```json
{
  "name": "MacBook Pro",
  "description": "High-performance laptop",
  "category": "Electronics",
  "price": 1999.99,
  "discountPercentage": 15,
  "stock": 25,
  "variants": [
    {
      "size": "13-inch",
      "color": "Space Gray",
      "quantity": 15
    },
    {
      "size": "16-inch",
      "color": "Silver",
      "quantity": 10
    }
  ]
}
```

**Clothing Product:**

```json
{
  "name": "Nike Air Max",
  "description": "Comfortable running shoes",
  "category": "Clothing",
  "price": 129.99,
  "stock": 100,
  "variants": [
    {
      "size": "M",
      "color": "Red",
      "quantity": 30
    },
    {
      "size": "L",
      "color": "Blue",
      "quantity": 40
    },
    {
      "size": "XL",
      "color": "Black",
      "quantity": 30
    }
  ]
}
```

**Expected Response (201):**

```json
{
  "name": "iPhone 15",
  "description": "Latest iPhone with advanced features",
  "category": "687aedeb71978cc6a617c505",
  "price": 999.99,
  "salePrice": null,
  "discountPercentage": 0,
  "isOnSale": false,
  "stock": 50,
  "variants": [
    {
      "size": "128GB",
      "color": "Black",
      "quantity": 20,
      "_id": "687aefb690b6b5d154320ae6"
    },
    {
      "size": "256GB",
      "color": "Blue",
      "quantity": 30,
      "_id": "687aefb690b6b5d154320ae7"
    }
  ],
  "_id": "687aefb690b6b5d154320ae5",
  "createdAt": "2025-07-19T01:07:02.085Z",
  "updatedAt": "2025-07-19T01:07:02.096Z",
  "__v": 0,
  "finalPrice": 999.99
}
```

---

### **3.2 Get All Products**

```
GET /products
```

**Headers:** None required

**Request Body:** None

**Expected Response (200):**

```json
[
    {
        "_id": "687aefb690b6b5d154320ae5",
        "name": "iPhone 15",
        "description": "Latest iPhone with advanced features",
        "category": {
            "_id": "687aedeb71978cc6a617c505",
            "name": "Electronics"
        },
        "price": 999.99,
        "salePrice": null,
        "discountPercentage": 0,
        "isOnSale": false,
        "stock": 50,
        "variants": [...],
        "createdAt": "2025-07-19T01:07:02.085Z",
        "updatedAt": "2025-07-19T01:07:02.096Z"
    }
]
```

---

### **3.3 Get Product by ID**

```
GET /products/{product_id}
```

**Headers:**

```
Authorization: Bearer YOUR_JWT_TOKEN
```

**Request Body:** None

**Expected Response (200):**

```json
{
    "_id": "687aefb690b6b5d154320ae5",
    "name": "iPhone 15",
    "description": "Latest iPhone with advanced features",
    "category": {
        "_id": "687aedeb71978cc6a617c505",
        "name": "Electronics"
    },
    "price": 999.99,
    "salePrice": null,
    "discountPercentage": 0,
    "isOnSale": false,
    "stock": 50,
    "variants": [...],
    "createdAt": "2025-07-19T01:07:02.085Z",
    "updatedAt": "2025-07-19T01:07:02.096Z"
}
```

---

### **3.4 Update Product (Admin Only)**

```
PUT /products/{product_id}
```

**Headers:**

```
Content-Type: application/json
Authorization: Bearer YOUR_JWT_TOKEN
```

**Update Price and Stock:**

```json
{
  "price": 899.99,
  "stock": 75
}
```

**Update with Discount:**

```json
{
  "discountPercentage": 20,
  "description": "Updated description with new features"
}
```

**Update Variants:**

```json
{
  "variants": [
    {
      "size": "128GB",
      "color": "Black",
      "quantity": 25
    },
    {
      "size": "512GB",
      "color": "Gold",
      "quantity": 15
    }
  ]
}
```

**Expected Response (200):**

```json
{
    "message": "Product updated successfully",
    "product": {
        "_id": "687aefb690b6b5d154320ae5",
        "name": "iPhone 15",
        "price": 899.99,
        "salePrice": 719.99,
        "discountPercentage": 20,
        "isOnSale": true,
        "stock": 75,
        "variants": [...],
        "updatedAt": "2025-07-19T01:10:00.000Z"
    }
}
```

---

### **3.5 Delete Product (Admin Only)**

```
DELETE /products/{product_id}
```

**Headers:**

```
Authorization: Bearer YOUR_JWT_TOKEN
```

**Request Body:** None

**Expected Response (200):**

```json
{
  "message": "Product deleted"
}
```

---

## **4. Search and Filtering Endpoints**

### **4.1 Search Products by Name**

```
GET /products?search=iPhone
```

**Headers:** None required

**Request Body:** None

**Expected Response (200):**

```json
[
    {
        "_id": "687aefb690b6b5d154320ae5",
        "name": "iPhone 15",
        "description": "Latest iPhone with advanced features",
        "category": {
            "_id": "687aedeb71978cc6a617c505",
            "name": "Electronics"
        },
        "price": 999.99,
        "stock": 50,
        "variants": [...]
    }
]
```

---

### **4.2 Filter by Category**

```
GET /products?categories=Electronics
```

**Headers:** None required

**Request Body:** None

---

### **4.3 Filter by Price Range**

```
GET /products?minPrice=500&maxPrice=1500
```

**Headers:** None required

**Request Body:** None

---

### **4.4 Filter Products on Sale**

```
GET /products?onSale=true
```

**Headers:** None required

**Request Body:** None

---

### **4.5 Filter by Color**

```
GET /products?color=Black
```

**Headers:** None required

**Request Body:** None

---

### **4.6 Filter by Size**

```
GET /products?size=128GB
```

**Headers:** None required

**Request Body:** None

---

### **4.7 Filter by Date Created**

```
GET /products?createdAfter=2024-01-01&createdBefore=2024-12-31
```

**Headers:** None required

**Request Body:** None

---

## **5. Reporting Endpoints (Admin Only)**

### **5.1 Low Stock Report**

```
GET /products/reports/low-stock?threshold=30
```

**Headers:**

```
Authorization: Bearer YOUR_JWT_TOKEN
```

**Request Body:** None

**Expected Response (200):**

```json
{
    "threshold": 30,
    "count": 1,
    "products": [
        {
            "_id": "687aefb690b6b5d154320ae5",
            "name": "MacBook Pro",
            "category": {
                "_id": "687aedeb71978cc6a617c505",
                "name": "Electronics"
            },
            "price": 1999.99,
            "stock": 25,
            "variants": [...]
        }
    ]
}
```

---

### **5.2 Products on Sale Report**

```
GET /products/reports/on-sale
```

**Headers:**

```
Authorization: Bearer YOUR_JWT_TOKEN
```

**Request Body:** None

**Expected Response (200):**

```json
{
  "count": 1,
  "totalDiscountValue": "7499.96",
  "products": [
    {
      "_id": "687aefb690b6b5d154320ae5",
      "name": "MacBook Pro",
      "category": {
        "_id": "687aedeb71978cc6a617c505",
        "name": "Electronics"
      },
      "price": 1999.99,
      "salePrice": 1699.99,
      "discountPercentage": 15,
      "stock": 25
    }
  ]
}
```

---

### **5.3 Inventory Summary Report**

```
GET /products/reports/inventory
```

**Headers:**

```
Authorization: Bearer YOUR_JWT_TOKEN
```

**Request Body:** None

**Expected Response (200):**

```json
{
  "totalProducts": 2,
  "totalStock": 75,
  "categorySummary": [
    {
      "_id": "687aedeb71978cc6a617c505",
      "categoryName": ["Electronics"],
      "productCount": 2,
      "totalStock": 75
    }
  ]
}
```

---

## **6. User Management Endpoints**

### **6.1 Get All Users (Admin Only)**

```
GET /users
```

**Headers:**

```
Authorization: Bearer YOUR_JWT_TOKEN
```

**Request Body:** None

**Expected Response (200):**

```json
[
  {
    "_id": "687aedeb71978cc6a617c502",
    "username": "john_doe",
    "email": "john@example.com",
    "role": "admin"
  },
  {
    "_id": "687aedeb71978cc6a617c503",
    "username": "jane_customer",
    "email": "jane@example.com",
    "role": "customer"
  }
]
```

---

## **7. Postman Collection Setup**

### **Environment Variables to Set:**

```
BASE_URL: http://localhost:3000
JWT_TOKEN: (will be set after login)
```

### **Pre-request Script for Authentication:**

```javascript
// After successful login, set the token
pm.environment.set("JWT_TOKEN", pm.response.json().token);
```

### **Authorization Header Setup:**

```
Authorization: Bearer {{JWT_TOKEN}}
```

---

## **8. Testing Workflow**

### **Step 1: Authentication**

1. Register a user (POST /auth/register)
2. Login to get JWT token (POST /auth/login)
3. Copy token to environment variable

### **Step 2: Create Categories**

1. Create Electronics category (POST /categories)
2. Create Clothing category (POST /categories)

### **Step 3: Create Products**

1. Create iPhone product (POST /products)
2. Create MacBook product with discount (POST /products)
3. Create Nike shoes product (POST /products)

### **Step 4: Test Search & Filtering**

1. Search by name (GET /products?search=iPhone)
2. Filter by category (GET /products?categories=Electronics)
3. Filter by price (GET /products?minPrice=500&maxPrice=1500)
4. Filter on sale (GET /products?onSale=true)

### **Step 5: Test Reporting**

1. Low stock report (GET /products/reports/low-stock)
2. Sale products report (GET /products/reports/on-sale)
3. Inventory summary (GET /products/reports/inventory)

### **Step 6: Test Updates & Deletes**

1. Update product (PUT /products/{id})
2. Delete product (DELETE /products/{id})

---

## **9. Error Testing Examples**

### **Invalid Registration:**

```json
{
  "username": "ab",
  "email": "invalid-email",
  "password": "123"
}
```

**Expected:** 400 Validation Error

### **Invalid Product Creation:**

```json
{
  "name": "",
  "price": -10
}
```

**Expected:** 400 Validation Error

### **Unauthorized Access:**

```
GET /users
```

**Without Authorization Header**
**Expected:** 401 Unauthorized

### **Invalid Token:**

```
Authorization: Bearer invalid_token
```

**Expected:** 401 Unauthorized

---

## **10. Success Criteria**

✅ **All endpoints return correct status codes**  
✅ **Validation errors provide clear messages**  
✅ **Authentication works properly**  
✅ **Search and filtering function correctly**  
✅ **Reports generate accurate data**  
✅ **CRUD operations work as expected**

**Happy Testing! 🚀**
