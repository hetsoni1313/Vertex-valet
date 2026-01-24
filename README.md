 ## Vertex-Valet 

A Big Data Engineering project for processing, storing, and serving book data. This project demonstrates an end-to-end ETL (Extract, Transform, Load) pipeline for book recommendations or catalog management, culminating in a REST API built with FastAPI.

## Features

- **Data Ingestion**: Load raw book data from CSV files.
- **Data Transformation**: Clean and process the data for consistency and quality.
- **Data Storage**: Store processed data in a SQLite database.
- **API Service**: Provide RESTful endpoints to query book information by ISBN or search by title/author.

## Project Structure

```
Vertex-valet/
├── README.md                 # Project documentation
├── API/
│   ├── main.py               # FastAPI application for serving book data
│   └── __pycache__           # Python cache files
├── data/
│   ├── processed/
│   │   └── cleaned_RC_Book.csv  # Cleaned and processed book data
│   └── raw/
│       └── RC_books.csv         # Raw book data
├── ingestion/
│   └── ingestion.ipynb       # Jupyter notebook for data ingestion
├── storage/
│   └── db.ipynb              # Jupyter notebook for database setup and storage
└── transformation/
│   └── transformation.ipynb  # Jupyter notebook for data transformation
└── requirements.txt          # Required packages to run the files 
```

## Installation

### Prerequisites

- Python 3.8 or higher
- Jupyter Notebook (for running the notebooks)
- SQLite (comes with Python)


### Setup

- Install the required Python package.
- Create virutal Environment and download required packages :

```bash
1. 
  python -m venv myvenv
2.
  .\myvenv\Scripts\activate
3.
  pip install -r requirements.txt
```

### Database Setup

1. Run the storage notebook to set up the database:
   - Open `storage/db.ipynb` File.
   - Execute the all cells to create the SQLite database (`library.db`) and populate it with data.

### Data Processing

1. **Ingestion**: Run `ingestion/ingestion.ipynb` to load raw data from `data/raw/RC_books.csv`.
2. **Transformation**: Run `transformation/transformation.ipynb` to clean and process the data, outputting to `data/processed/cleaned_RC_Book.csv`.
3. **Storage**: As above, use `storage/db.ipynb` to load the processed data into the database.

## Technologies Used
  Python 3.8+
  FastAPI
  SQLite
  Pandas
  Jupyter Notebooks

### Running the API

Navigate to the `API` directory and start the FastAPI server:

```bash
cd API
uvicorn main:app --reload
```

The API will be available at `http://127.0.0.1:8000`.

### API Endpoints

- **GET /**: Health check endpoint.
  - Response: `{"status": "API is running"}`

- **GET /books/{isbn}**: Retrieve a book by its ISBN.
  - Parameters: `isbn` (string)
  - Response: Book details as JSON, or 404 if not found.

- **GET /search**: Search books by title or author.
  - Query Parameters: `q` (string, search query)
  - Response: List of matching books (up to 20), each with `isbn`, `title`, `author`.

### Example API Usage

- Health check: `curl http://127.0.0.1:8000/`
- Get book by ISBN: `curl http://127.0.0.1:8000/docs#/default/get_book_by_isbn_books__isbn__get`
- Search books: `curl http://127.0.0.1:8000/docs#/default/search_books_search_get`

## Contributing

Contributions are welcome! Please fork the repository and submit a pull request with your changes.

