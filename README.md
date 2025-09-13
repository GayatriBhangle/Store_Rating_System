# Store Rating Application

A full-stack web application that allows users to submit ratings for registered stores with role-based access control.

## 🚀 Features

### User Roles & Functionalities

#### 1. System Administrator
- ✅ Add new stores, normal users, and admin users
- ✅ View dashboard with total users, stores, and ratings statistics
- ✅ Manage users with full CRUD operations
- ✅ View and manage stores with ratings
- ✅ Apply filters on all listings (Name, Email, Address, Role)
- ✅ View detailed user information including store owner ratings
- ✅ Sorting functionality on all data tables

#### 2. Normal User
- ✅ Sign up and login to the platform
- ✅ Update password after logging in
- ✅ View list of all registered stores
- ✅ Search stores by name and address
- ✅ Submit ratings (1-5) for individual stores
- ✅ Modify previously submitted ratings
- ✅ View personal dashboard with rating statistics

#### 3. Store Owner
- ✅ Login to the platform
- ✅ Update password after logging in
- ✅ View dashboard with store statistics
- ✅ See list of users who rated their store
- ✅ View average rating of their store
- ✅ View rating distribution

## 🛠 Tech Stack

### Backend
- **Framework**: Express.js
- **Database**: PostgreSQL
- **Authentication**: JWT (JSON Web Tokens)
- **Password Hashing**: bcrypt
- **Validation**: Joi
- **Security**: Helmet, CORS, Rate limiting

### Frontend
- **Framework**: React 18
- **Styling**: Tailwind CSS
- **Icons**: Lucide React (star ratings)
- **HTTP Client**: Fetch API
- **State Management**: React Context API

### Database Schema
- **Users Table**: Stores all user types with role-based access
- **Stores Table**: Store information with owner relationships
- **Ratings Table**: User ratings for stores with constraints

## 📋 Form Validations

All forms include comprehensive client and server-side validation:

- **Name**: 20-60 characters
- **Address**: Maximum 400 characters
- **Password**: 8-16 characters, must include at least one uppercase letter and one special character
- **Email**: Standard email validation
- **Rating**: Integer between 1-5

## 🔒 Security Features

- JWT-based authentication
- Role-based access control
- Password hashing with bcrypt (12 rounds)
- Rate limiting (100 requests per 15 minutes)
- CORS protection
- SQL injection prevention with parameterized queries
- XSS protection with Helmet

## 🗄 Database Features

- **ACID Compliance**: Full transaction support
- **Referential Integrity**: Foreign key constraints
- **Data Validation**: Check constraints for ratings and text lengths
- **Indexing**: Optimized queries with strategic indexes
- **Triggers**: Automatic timestamp updates
- **Unique Constraints**: Prevent duplicate ratings per user per store

## 📦 Installation & Setup

### Prerequisites
- Node.js (v14 or higher)
- PostgreSQL (v12 or higher)
- npm or yarn

### Backend Setup

1. **Clone and navigate to project**
   ```bash
   mkdir store-rating-app
   cd store-rating-app
   mkdir backend
   cd backend
   ```

2. **Install dependencies**
   ```bash
   npm init -y
   npm install express pg bcrypt jsonwebtoken cors helmet express-rate-limit joi dotenv
   npm install -D nodemon
   ```

3. **Database Setup**
   ```bash
   # Create database
   createdb store_rating
   
   # Run the SQL schema from the database_schema.sql file
   psql -d store_rating -f schema.sql
   ```

4. **Environment Configuration**
   Create a `.env` file:
   ```env
   DB_HOST=localhost
   DB_PORT=5432
   DB_NAME=store_rating
   DB_USER=postgres
   DB_PASSWORD=your_password
   JWT_SECRET=your-very-long-random-jwt-secret-key
   PORT=5000
   NODE_ENV=development
   FRONTEND_URL=http://localhost:3000
   ```

5. ## 📁 Project Structure

```
store-rating-system/
├── backend/
│   ├── src/
│   │   ├── config/
│   │   │   ├── database.js
│   │   │   └── database.sql
│   │   ├── controllers/
│   │   │   ├── adminController.js
│   │   │   ├── ratingController.js
│   │   │   ├── storeController.js
│   │   │   └── userController.js
│   │   ├── middleware/
│   │   │   ├── auth.js
│   │   │   ├── errorHandler.js
│   │   │   └── rateLimiter.js
│   │   ├── routes/
│   │   │   ├── adminRoutes.js
│   │   │   ├── authRoutes.js
│   │   │   ├── ratingRoutes.js
│   │   │   ├── storeOwnerRoutes.js
│   │   │   └── storeRoutes.js
│   │   ├── utils/
│   │   │   └── validation.js
│   │   ├── app.js
│   │   └── server.js
│   ├── .env
│   └── package.json
└── frontend/
    ├── src/
    │   ├── components/
    │   │   ├── admin/
    │   │   ├── auth/
    │   │   ├── common/
    │   │   ├── dashboard/
    │   │   ├── store/
    │   │   └── user/
    │   ├── context/
    │   │   └── AuthContext.jsx
    │   ├── services/
    │   │   └── api.js
    │   ├── utils/
    │   │   ├── constants.js
    │   │   └── validation.js
    │   ├── App.jsx
    │   └── main.jsx
    ├── .env
    ├── vite.config.js
    └── package.json
```


6. **Start the server**
   ```bash
   npm run dev  # Development mode with nodemon
   # or
   npm start    # Production mode
   ```

### Frontend Setup

1. **Create React app**
   ```bash
   cd ..  # Back to project root
   npx create-react-app frontend
   cd frontend
   ```

2. **Install additional dependencies**
   ```bash
   npm install react-router-dom@6 axios react-hook-form react-hot-toast lucide-react
   npm install -D tailwindcss postcss autoprefixer
   npx tailwindcss init -p
   ```

3. **Configure Tailwind** (update tailwind.config.js as provided)

4. **Replace src/App.js** with the React application code

5. **Start the frontend**
   ```bash
   npm start
   ```

### Alternative: Single HTML File

For quick testing, use the complete HTML file (complete_react_app.html):

1. Save the HTML file locally
2. Update the API_BASE_URL in the script to match your backend
3. Open in a web browser
4. Ensure backend is running on localhost:5000

## 🚀 Usage

### Default Admin Account
- **Email**: admin@system.com
- **Password**: Admin123!

### API Endpoints

#### Authentication
- `POST /api/auth/register` - User registration
- `POST /api/auth/login` - User login
- `GET /api/auth/verify` - Token verification

#### Users (Admin only)
- `GET /api/users` - Get all users
- `POST /api/users` - Create new user
- `GET /api/users/:id` - Get user by ID
- `PATCH /api/users/password` - Update password
- `DELETE /api/users/:id` - Delete user

#### Stores
- `GET /api/stores` - Get stores (with user ratings)
- `GET /api/stores/admin` - Get stores (admin view)
- `POST /api/stores` - Create store (admin only)
- `GET /api/stores/:id` - Get store by ID

#### Ratings
- `POST /api/ratings` - Submit/update rating
- `GET /api/ratings/store/:storeId` - Get user's rating for store
- `GET /api/ratings/store/:storeId/all` - Get all ratings for store

#### Dashboard
- `GET /api/dashboard/admin` - Admin dashboard data
- `GET /api/dashboard/user` - User dashboard data
- `GET /api/dashboard/store-owner` - Store owner dashboard data

## 🔧 Advanced Features

### Pagination & Sorting
- All data tables support pagination
- Configurable page sizes
- Multi-column sorting (ascending/descending)
- Search and filter capabilities

### Real-time Updates
- Dynamic rating updates without page refresh
- Live dashboard statistics
- Instant form validation feedback

### Responsive Design
- Mobile-first approach
- Responsive navigation
- Optimized for all screen sizes
- Touch-friendly interfaces

### Performance Optimizations
- Database query optimization with indexes
- Efficient pagination queries
- Minimal data transfer
- Optimized bundle size

## 🧪 Testing

### Manual Testing Checklist

#### User Registration & Authentication
- [ ] Register new user with valid data
- [ ] Test form validation for all fields
- [ ] Login with correct credentials
- [ ] Login with incorrect credentials
- [ ] Password change functionality

#### Admin Functions
- [ ] View admin dashboard
- [ ] Create new users (all roles)
- [ ] Search and filter users
- [ ] Create new stores
- [ ] View store listings with ratings

#### User Functions
- [ ] View user dashboard
- [ ] Browse store listings
- [ ] Search stores by name/address
- [ ] Submit store ratings
- [ ] Update existing ratings

#### Store Owner Functions
- [ ] View store dashboard
- [ ] See rating statistics
- [ ] View customer ratings list

## 🚨 Troubleshooting

### Common Issues

1. **Database Connection Error**
   - Verify PostgreSQL is running
   - Check database credentials in .env
   - Ensure database exists

2. **JWT Token Error**
   - Check JWT_SECRET in .env
   - Clear localStorage and login again

3. **CORS Error**
   - Verify FRONTEND_URL in backend .env
   - Check API_BASE_URL in frontend

4. **Port Already in Use**
   ```bash
   # Kill process on port 5000
   lsof -ti:5000 | xargs kill -9
   ```

### Database Reset
```sql
-- Reset all tables
TRUNCATE users, stores, ratings RESTART IDENTITY CASCADE;

-- Recreate admin user
INSERT INTO users (name, email, password, address, role) VALUES 
('System Administrator User', 'admin@system.com', '$2b$10$X8zLNdX8vW5vqW5z8vW5z8vW5z8vW5z8vW5z8vW5z8vW5z8vW5z8vW', '123 Admin Street, Admin City', 'admin');
```

## 📈 Future Enhancements

- Email notifications for new ratings
- Advanced analytics and reporting
- Bulk operations for admin
- Export functionality (CSV, PDF)
- API rate limiting per user
- Image uploads for stores
- Review comments along with ratings
- Mobile app development
- Multi-language support

## 🤝 Contributing

1. Fork the project
2. Create a feature branch
3. Commit your changes
4. Push to the branch
5. Create a Pull Request

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

---

**Note**: This application is built for educational purposes and demonstrates full-stack development best practices including security, validation, and proper API design.
