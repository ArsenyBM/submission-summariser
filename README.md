# submission-summariser

**See Jupyter Notebook file for more details and the code itself.**

The following is a summary of how the code works by GPT-4.

The code imports necessary modules and functions, such as pdfplumber to extract text from PDFs, openai for generating content using GPT-4 and other modules for dealing with files, data, and databases (sqlite3).

The code first checks if the submitted PDF file exists in the database. If it doesn't exist, the code extracts text from the PDF, processes the text, counts pages, words, and tokens, and stores the data in the submissions table. The database table 'submissions' has columns including page_count, word_count, text, tokens, and manual_summarisation.

The code then connects to the SQLite database and fetches all rows from the 'submissions' table for processing. It also creates a new table 'summaries' with corresponding columns for storing summarization data.

The code iterates over each submission and checks if:
1. The submission is already summarized in the 'summaries' table - If yes, it skips the file.
2. The submission requires manual summarization - If yes, it stores 'Manual summarization required' in the summary, ideas, concerns, category, sentiment, and text fields.

For the rest of the submissions, the code:
1. Selects the appropriate GPT model based on the number of tokens.
2. Summarizes the text using the GPT model by sending an appropriate prompt to the model.
3. Parses the response as JSON and extracts 'summary', 'ideas', 'concerns', 'category', and 'sentiment' fields. If JSON parsing fails, it asks the GPT model to convert the response into JSON format and attempts to parse again.

After retrieving all fields from the GPT model response, the code inserts the data into a new database table called 'summaries'.

Finally, the code commits changes to the database and closes the connection.