This file corresponds to the English version of the project documentation.  
For the Spanish version, see [`readme.md`](readme.md).

# 📌 UltimateLibraryBE - BOOK MANAGEMENT API

Backend for book management, developed with the following technologies:

- Node.js
- Express
- dotenv
- MongoDB (Mongoose)
- uuid
- Postman (testing)

## 🌟 Features

- Full **CRUD** operations for the book entity.
- **Detailed error handling** and clear responses for situations such as:
  - Missing information or invalid identifiers.
  - Internal server errors (500).
  - Incorrect or malformed requests (400).

## 🛠️ Installation

1. **Clone the project:**
   ```bash
   git clone https://github.com/fabinnerself/ultimateLibraryBE.git  
   cd ultimateLibraryBE
   ```

2. **Install dependencies:**
   ```bash
   npm install
   ```

3. **Set up the database:**
   - Make sure you have a MongoDB instance running, either locally (`mongodb://localhost:27017`) or using a cloud service like MongoDB Atlas (e.g.:  
     `mongodb+srv://{user}:{password}@mymongodb.aofqgrl.mongodb.net/?retryWrites=true&w=majority&appName=mymongodb`).
   - Ensure that a database named `mymongodb` exists and contains data or is empty, as needed.

4. **Configure environment variables:**
   - Copy the `.env.template` file to `.env` and verify that the MongoDB configuration is correct.

5. **Run in development mode:**
   ```bash
   node index.js
   ```

6. **Test the endpoints:**
   - Use Postman or another tool to consume the API endpoints.

7. **Automated tests in Postman:**
   - API tests are performed in Postman, using global variables to facilitate test reuse and automation.
   - Main variables:
     - `BaseURl_booksP`: Defines the base URL for the books resource, allowing endpoints to be easily adapted to different environments.
     - `Libro_Id`: Stores the unique identifier of a book created during tests, enabling chained operations (retrieve, update, delete).
   - Example usage in requests:
     ```
     {{BaseURl_booksP}}/api/v1/books/{{Libro_Id}}
     ```
   - Typical test flow:
     1. **Create a book:** A POST request is made and the ID is saved in the global variable.
     2. **List books:** Verifies that the new record appears correctly.
     3. **Get book by ID:** Retrieves the newly created book.
     4. **Update book:** Updates the book using the same ID.
     5. **Delete book:** Deletes the book and checks that it no longer exists.
   - This approach ensures that tests are dynamic, repeatable, and do not depend on static data, improving the robustness and reliability of testing.
   - The `./test/` directory includes:
     - `be_l_res_sumary.png`: Summary of test results.

 ![detalle](./test/be_l_res_sumary.png)

     - `be_l_test_res_det.png`: Detailed test results.

![details](./test/be_l_test_res_det.png) 

     - `Backend Libros.postman_test_run.json`: Postman export file with the complete test run details.

  [Deatil of JSON](./test/Backend%20Libros.postman_test_run.json)


   - For more details on the test structure and execution, see the included JSON file, which can be imported directly into Postman to replicate the process.

   - **Example Postman script:**
     ```javascript
     pm.test("Response status code is 200", function () {
         pm.expect(pm.response.code).to.equal(200);
     });

     const response = pm.response.json();
     console.log(response.msg);
     console.log(`Message: ${response.msg}`);

     pm.test("Message should be 'OK'", () => {
         pm.expect(response.msg).to.eql('Ok');
         console.log("id val: ",response.data._id)
         pm.globals.set("Libro_Id",response.data._id)
     });

     pm.test("Ensure Response should have saved correctly", () => {
         const libroId = pm.globals.get("Libro_Id");
         pm.expect(libroId).to.exist; 
         pm.expect(libroId).to.not.be.empty; 
     });
     ```
     This script automates response validation and the handling of global variables to chain tests.

---

## 📘 API Documentation

This backend is designed to manage essential operations related to books, enabling efficient catalog management.

The **Book** entity allows control over the catalog, including title, author, genre, year of publication, and current status (active or blocked). The system ensures integrity and consistency in every transaction, facilitating operations such as registration, modification, query, and deletion of records.

### 🔗 Available Routes

| Resource | Base URL |
|----------|----------|
| Books    | [https://tmp-seven-azure.vercel.app/api/v1/books/](https://tmp-seven-azure.vercel.app/api/v1/books/) |

Full documentation of endpoints, usage examples, and expected responses is available in Postman: [Postman Documentation](https://documenter.getpostman.com/view/22674808/2sB34mjdwu).

---

## 🧾 Entity Description

### 📚 Books

Represents a book available in the library. It contains detailed information such as title, author, genre, year of publication, and current status (active or blocked). It also records the creation and last update dates.

**Supported operations:**

- `GET /api/v1/books` - List all books
- `GET /api/v1/books/:id` - Get book by ID
- `POST /api/v1/books` - Create new book
- `PUT /api/v1/books/:id` - Update book
- `DELETE /api/v1/books/:id` - Delete book

---

## 🧪 Usage Examples

### Create Book
```json
POST /api/v1/books
{
  "name": "One Hundred Years of Solitude",
  "autor": "Gabriel García Márquez",
  "genero": "Magic Realism",
  "precio": 1967
}
```

### Get Book by ID
```bash
GET /api/v1/books/:id
```

### Update Book
```json
PUT /api/v1/books/:id
{
  "titulo": "One Hundred Years of Solitude",
  "autor": "Gabriel García Márquez",
  "genero": "Magic Realism",
  "anio_publicacion": 1967,
  "estado": "blocked"
}
```

### Delete Book
```bash
DELETE /api/v1/books/:id
```

---

## 🤝 Contribution & Acknowledgements

This backend was developed using previous resources and projects as a foundation for its structure and functionality. In particular, concepts from the following video and repository were adapted and extended:

- [Video tutorial: Node.js REST API with MongoDB](https://www.youtube.com/watch?v=D7lDiFWF_vA)
- [Base repository](https://github.com/nhndev/node-mongodb-api.git)

Both resources provided fundamental guidance for the initial architecture. From that base, the project was adapted to meet the specific requirements of book management, incorporating automated tests and detailed documentation.

Special thanks to the original authors for sharing their knowledge and facilitating the learning and development of new solutions.

Contributions are welcome! Please submit a pull request, fork, or open an issue to report bugs or suggest new features.

---

## 📜 License

This project is licensed under the MIT License. For more details, see [MIT License](https://choosealicense.com/licenses/mit/).

---

## 🚀 Author

👤 Favian Medina Gemio

| Resource     | Address                                                                 |
|--------------|-------------------------------------------------------------------------|
| 📧 Email     | [favian.medina.gemio@gmail.com](mailto:favian.medina.gemio@gmail.com)   |
| 💻 GitHub    | [https://github.com/fabinnerself](https://github.com/fabinnerself)      |
| 🧠 LinkedIn  | [https://www.linkedin.com/in/favian-medina-gemio/](https://www.linkedin.com/in/favian-medina-gemio/) |
| 💼 Portfolio | [https://favian-medina-cv.vercel.app/](https://favian-medina-cv.vercel.app/) |

(c) 2025 