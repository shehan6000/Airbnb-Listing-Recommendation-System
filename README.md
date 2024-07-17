# Airbnb Listing Recommendation System

This project demonstrates how to build an Airbnb listing recommendation system using MongoDB for vector search and OpenAI's GPT model for generating responses. The project also incorporates prompt compression to optimize the interaction with the AI model, ensuring that it processes only the most relevant information.

## Table of Contents

- [Installation](#installation)
- [Usage](#usage)
- [Project Structure](#project-structure)
- [Detailed Workflow](#detailed-workflow)
  - [Initialization and Setup](#initialization-and-setup)
  - [Data Loading](#data-loading)
  - [Document Modeling](#document-modeling)
  - [Database Connection](#database-connection)
  - [Data Ingestion](#data-ingestion)
  - [Vector Search Index Setup](#vector-search-index-setup)
  - [Handling User Queries](#handling-user-queries)
  - [Boosting Search Results](#boosting-search-results)
  - [Prompt Compression](#prompt-compression)
  - [Handling Compressed Query](#handling-compressed-query)
- [Additional Resources](#additional-resources)
- [License](#license)

## Installation

1. **Clone the repository**:
   ```sh
   git clone https://github.com/your-username/airbnb-recommendation-system.git
   cd airbnb-recommendation-system
   ```

2. **Install the required packages**:
   ```sh
   pip install -r requirements.txt
   ```

3. **Install custom utilities**:
   - Make sure `custom_utils.py` is in the project directory or update the import paths accordingly.

## Usage

1. **Open the Jupyter Notebook**:
   ```sh
   jupyter notebook
   ```
2. **Run the Notebook**:
   - Open the `L5_Prompt_Compression.ipynb` notebook.
   - Follow the instructions within the notebook to execute the cells step-by-step.

## Project Structure

```
airbnb-recommendation-system/
│
├── custom_utils.py          # Custom utility functions
├── L5_Prompt_Compression.ipynb  # Main Jupyter Notebook for prompt compression
├── requirements.txt         # Required Python packages
└── README.md                # Project README file
```

## Detailed Workflow

### Initialization and Setup

- **Suppress Warnings**: Warnings are disabled to avoid cluttering the notebook.
- **Import Custom Utilities**: A custom utility module containing helper functions is imported for use throughout the notebook.

### Data Loading

- **Load Dataset**: A dataset of Airbnb listings is loaded, and a sample of 100 records is selected.
- **Convert to DataFrame**: The selected records are converted into a Pandas DataFrame for easier manipulation and processing.

### Document Modeling

- **Process Records**: The records in the DataFrame are processed into a format suitable for MongoDB ingestion using a custom utility function.

### Database Connection

- **Connect to MongoDB**: A connection to a MongoDB database is established.
- **Clear Collection**: Any existing records in the MongoDB collection are deleted to ensure a fresh start for data ingestion.

### Data Ingestion

- **Insert Records**: The processed records are inserted into the MongoDB collection.

### Vector Search Index Setup

- **Create Vector Search Index**: A vector search index is set up on the MongoDB collection to enable efficient vector-based queries.

### Handling User Queries

- **Define Result Model**: A model for the search results is defined to ensure consistency in the data structure.
- **Perform Vector Search**: A function is defined to handle user queries by performing vector searches on the MongoDB collection.
- **Process Results**: The search results are processed, converted into a DataFrame, and displayed in a structured format.
- **Generate System Response**: A system response is generated using OpenAI's completion API based on the search results.

### Boosting Search Results

- **Calculate Average Review Score**: A stage is added to the query pipeline to calculate the average review score for each listing based on various review score components (accuracy, cleanliness, check-in, communication, location, value).
- **Calculate Review Count Boost**: A boost factor is calculated based on the number of reviews for each listing.
- **Combine Scores**: A new field, `combinedScore`, is created to combine the average review score and the review count boost. The weights can be adjusted based on preferences.
- **Sort by Combined Score**: The search results are sorted by the `combinedScore` in descending order to prioritize listings with higher combined scores.

### Prompt Compression

- **Import Prompt Compressor**: A prompt compression tool from `llmlingua` is imported.
- **Define Compression Function**: A function is defined to compress the prompt, reducing the size of the context while keeping essential information.
- **Compress User Query**: The user query and context are compressed using the defined function.
- **Print Compressed Prompt**: The compressed prompt is printed for debugging purposes.

### Handling Compressed Query

- **Generate System Response with Compressed Prompt**: A function is defined to handle the system response using the compressed prompt.
- **Execute Compressed Query Handling**: The function is executed to handle the user query with the compressed prompt, and the system response is generated and displayed.

## Additional Resources

- [MongoDB Developer Center](https://mdb.link/developer_center): Tutorials, articles, and videos.
- [GenAI Showcase Repo](https://github.com/mongodb-developer/GenAI-Showcase): GitHub repository showcasing AI applications and demos.
- [DeepLearning AI Forum](https://community.deeplearning.ai/): Forum for questions related to this course.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
