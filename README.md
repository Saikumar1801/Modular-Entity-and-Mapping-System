# Modular Entity and Mapping System

This project is a TypeScript/Express implementation of the "Django Intern Assignment: Modular Entity and Mapping System Using APIView".

## Architecture
The project is structured into separate modules (mimicking Django apps):
- `vendor`: Master entity for Vendors
- `product`: Master entity for Products
- `course`: Master entity for Courses
- `certification`: Master entity for Certifications
- `vendor_product_mapping`: Mapping between Vendors and Products
- `product_course_mapping`: Mapping between Products and Courses
- `course_certification_mapping`: Mapping between Courses and Certifications

Each module contains:
- `models.ts`: Data interfaces
- `serializers.ts`: Validation schemas (using Zod)
- `views.ts`: Manual API handlers (mimicking APIView)
- `urls.ts`: Router definitions

## Tech Stack
- **Backend**: Node.js, Express, TypeScript
- **Database**: SQLite (using `sqlite3` and `sqlite`)
- **Validation**: Zod
- **Documentation**: Swagger UI (`drf-yasg` equivalent)

## Setup and Run
1. Install dependencies: `npm install`
2. Run migrations (automatic on start): `npm run dev`
3. Access Swagger UI: `http://localhost:3000/swagger`
4. Access ReDoc: `http://localhost:3000/redoc`

## API Usage Examples

### Master Entities
- `GET /api/vendors/` - List all vendors
- `POST /api/vendors/` - Create a new vendor
- `GET /api/vendors/:id/` - Retrieve a vendor
- `PUT /api/vendors/:id/` - Update a vendor
- `PATCH /api/vendors/:id/` - Partial update a vendor
- `DELETE /api/vendors/:id/` - Delete a vendor

### Filtering
- `/api/products/?vendor_id=1` - List products mapped to vendor 1
- `/api/courses/?product_id=2` - List courses mapped to product 2
- `/api/certifications/?course_id=3` - List certifications mapped to course 3

### Mappings
- `POST /api/vendor-product-mappings/` - Create a mapping
  - Validates required fields
  - Prevents duplicate mappings
  - Ensures only one `primary_mapping` per parent

## Implementation Notes
- **APIView Style**: All handlers are written manually in `views.ts` without using high-level abstractions like ViewSets.
- **Modularity**: Each app is self-contained with its own logic.
- **Validation**: Manual validation is performed using Zod schemas in the views, returning appropriate HTTP status codes and error messages.
