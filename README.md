# Connecting to a SQL Database Project Tutorial

This project demonstrates how to connect to a PostgreSQL database using Python, create tables, insert data, and display the data using Pandas. It is designed to help you understand the basics of working with SQL databases in a professional Python environment.

## Features

- **Database Connection**: Connect to a PostgreSQL database using SQLAlchemy.
- **Table Creation**: Create tables for publishers, authors, books, and book-authors relationships.
- **Data Insertion**: Insert sample data into the created tables.
- **Data Display**: Use Pandas to display SQL tables as DataFrames.

## Requirements

- Python 3.x
- PostgreSQL
- Libraries: SQLAlchemy, Pandas, python-dotenv, psycopg2

## Installation

1. **Clone the Repository**:
   ```bash
   git clone https://github.com/4GeeksAcademy/connecting-to-a-sql-database-project-tutorial.git
   cd connecting-to-a-sql-database-project-tutorial
   ```

2. **Install Dependencies**:
   ```bash
   pip install -r requirements.txt
   ```

3. **Set Up PostgreSQL**:
   - Ensure PostgreSQL is installed and running on your machine.
   - Create a new database:
     ```bash
     createdb -h localhost -U <username> <db_name>
     ```
   - Replace `<username>` and `<db_name>` with your PostgreSQL username and desired database name.

4. **Configure Environment Variables**:
   - Create a `.env` file in the root directory with the following content:
     ```
     DB_USER = 'your_username'
     DB_PASSWORD = 'your_password'
     DB_HOST = 'localhost'
     DB_NAME = 'your_database_name'
     ```
   - Replace the placeholders with your actual database credentials.

## Usage

1. **Run the Script**:
   ```bash
   python src/SQL-Test.py
   ```

2. **Expected Output**:
   - The script will create tables, insert data, and print the `authors` table as a DataFrame.

## Project Structure

- **`src/`**: Contains the main Python script (`SQL-Test.py`) for database operations.
- **`.env`**: Stores database credentials (ignored by Git).
- **`requirements.txt`**: Lists the required Python libraries.
- **`INSTRUCTIONS.md`**: Provides detailed instructions for setting up and running the project.
- **`README.md`**: This file, providing an overview of the project.

## Code Overview

- **Database Connection**:
  ```python
  connection_string = f"postgresql://{os.getenv('DB_USER')}:{os.getenv('DB_PASSWORD')}@{os.getenv('DB_HOST')}/{os.getenv('DB_NAME')}"
  engine = create_engine(connection_string).execution_options(autocommit=True)
  engine.connect()
  ```

- **Table Creation**:
  ```python
  engine.execute("""
  CREATE TABLE publishers(
      publisher_id INT NOT NULL,
      name VARCHAR(255) NOT NULL,
      PRIMARY KEY(publisher_id)
  );
  """)
  ```

- **Data Insertion**:
  ```python
  engine.execute("""
  INSERT INTO publishers(publisher_id, name) VALUES (1, 'O Reilly Media');
  """)
  ```

- **Data Display**:
  ```python
  authors = pd.read_sql_query("SELECT * FROM authors", engine)
  print(authors)
  ```

## Contributing

Feel free to fork this repository and submit pull requests with improvements or new features. If you find any bugs or have suggestions, please open an issue.

## License

This project is open-source and available under the MIT License. See the LICENSE file for more details.

## Acknowledgments

- Thanks to the SQLAlchemy and Pandas communities for providing excellent documentation and resources.
- Inspired by classic database management tutorials.

Enjoy working with SQL databases in Python! 🐍