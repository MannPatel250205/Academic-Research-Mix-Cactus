# Academic Research Remix By Cactus Communications 

This repository contains a Blazor frontend and a Flask-based backend (`app.py`) that processes research papers (PDFs), extracts key sections using the Gemini API, and generates a podcast using Google TTS.

## Features
- Upload and manage PDFs via Blazor UI.
- Extract key content from research papers using the  Gemini API.
- Generate summaries and podcasts using text-to-speech (Google TTS).
- User authentication and PDF storage using MongoDB and GridFS.
- Backend API built using Flask.
- Hosted on Render for seamless accessibility.

## Tech Stack
### Frontend:
- **Blazor** (UI for uploading PDFs and selecting output options, in progress)
- **Render** (Planned for hosting frontend)

### Backend:
- **Flask** (API for processing PDFs and handling user authentication)
- **MongoDB** (Storage for user data and PDFs)
- **GridFS** (For managing large PDF files in MongoDB)
- **Google TTS** (For generating podcasts from extracted content)
- **Google Gemini API (gemini-1.5-flash)** (For text extraction and summarization)
- **PyMuPDF** (For extracting text from PDFs)

## Approach
1. Extract text from PDFs using PyMuPDF.
2. Summarize key sections via Gemini API.
3. Convert text to speech using Google TTS.
4. Deliver the podcast through a user-friendly Blazor UI.
5. Store and retrieve processed content using MongoDB.
6. Host the backend API on Render for seamless accessibility.

## Setup Instructions
### Prerequisites:
- Python 3.x
- MongoDB (Local or Cloud)
- Flask and required dependencies

### Installation:
1. Clone the repository:
   ```sh
   git clone https://github.com/your-repo.git
   cd your-repo
   ```
2. Install dependencies:
   ```sh
   pip install -r requirements.txt
   ```
3. Set up MongoDB connection in `app.py`:
   ```python
   uri = "your-mongodb-uri"
   client = MongoClient(uri)
   ```
4. Run the backend server:
   ```sh
   python app.py
   ```
5. Deploy the Blazor frontend (instructions to be added later).

## API Endpoints
### Authentication:
- `POST /register`: Register a new user.
- `POST /login`: Authenticate user.

### PDF Management:
- `POST /user/add_pdf`: Upload a PDF.
- `POST /user/remove_pdf`: Delete a PDF.
- `POST /user/pdfs`: List all PDFs of a user.

### Processing PDFs:
- `POST /user/summary_pdf`: Extract and summarize key points.
- `POST /user/podcast_pdf`: Generate a podcast from a PDF summary.

## Explanation of Functions in `app.py`

### PDF Processing Functions
- **`process_pdf_with_gemini(pdf, context)`**: Reads a PDF file, processes it using the Gemini API, and returns extracted content.
- **`get_pdf_id(filename, username)`**: Retrieves the ObjectId of a PDF file stored in MongoDB’s GridFS.

### User Authentication Functions
- **`authenticate(username, password)`**: Checks user credentials against the database.
- **`register()` (`POST /register`)**: Registers a new user by storing credentials in MongoDB.
- **`login()` (`POST /login`)**: Authenticates a user using stored credentials.

### PDF Management Functions
- **`list_pdfs()` (`POST /user/pdfs`)**: Lists all PDFs uploaded by a user.
- **`add_pdf()` (`POST /user/add_pdf`)**: Allows a user to upload a PDF file and stores it in GridFS.
- **`remove_pdf()` (`POST /user/remove_pdf`)**: Deletes a PDF from MongoDB.

### PDF Processing and Podcast Generation
- **`query_pdf()` (`POST /user/query_pdf`)**: Processes a user query related to a PDF and fetches responses.
- **`summary_pdf()` (`POST /user/summary_pdf`)**: Extracts and summarizes content from a PDF using the Gemini API.
- **`podcast_pdf()` (`POST /user/podcast_pdf`)**: Generates a podcast script and converts it to an MP3 file using Google TTS.

## Future Enhancements
- Complete the Blazor frontend for better UI/UX.
- Implement advanced podcast generation settings.
- Improve AI summarization accuracy.
- Deploy the backend and frontend to a cloud platform.

## Contributing
Contributions are welcome! Please submit a pull request or open an issue.

## License
This project is licensed under the MIT License.
