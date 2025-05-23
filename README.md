# Leaf Image Store & Search System

This project implements a system for preprocessing, feature extraction, and similarity search on leaf images. It includes a command-line interface for batch processing and a Streamlit web application for interactive search.

![result_2](https://github.com/user-attachments/assets/00e15865-b6fa-4eb9-a288-607be445e370)
![Screenshot 2025-05-18 at 15 16 16](https://github.com/user-attachments/assets/dd95b71a-faee-4257-95e4-52eb1ff5f96b)
![Screenshot 2025-05-18 at 15 16 39](https://github.com/user-attachments/assets/18319d3a-8f4a-4ca6-b698-258b8ad3fd0d)

## Setup

### Prerequisites

- Python 3.12 (as specified in `.python-version`)
- Pip (Python package installer)

### Installation

1.  **Clone the repository:**

    ```bash
    git clone <repository_url>
    cd csdldpt
    ```

2.  **Create and activate a virtual environment (recommended):**

    ```bash
    python3 -m venv venv
    source venv/bin/activate  # On Windows use `venv\Scripts\activate`
    ```

3.  **Install dependencies:**
    ```bash
    pip install -r requirements.txt
    ```

## Usage

### Data Preparation

1.  Place your raw leaf images into `data/stored_images/raw/` organized by tree type. For example:
    ```
    data/stored_images/raw/apple/image_1.JPG
    data/stored_images/raw/apple/image_2.JPG
    ```

### Command-Line Interface

The main entry point for CLI operations is `main.py`.

1.  **Preprocess Images:**
    This step processes images from `data/stored_images/raw/` and saves them to `data/stored_images/processed/`.

    ```bash
    python main.py preprocess
    ```

2.  **Extract Features:**
    This step extracts features from the processed images in `data/stored_images/processed/` and saves them as CSV files in `data/features/`. It will create individual CSVs per tree type and a combined `all_features.csv`.

    ```bash
    python main.py extract
    ```

3.  **Search for Similar Leaves:**
    Search for leaves similar to a given query image.

    ```bash
    python main.py search path/to/your/query_image.jpg
    ```

    **Options:**

    - `--output <path_to_save_results.png>` or `-o <path_to_save_results.png>`: Save the visual search results to an image file.
    - `--num_results <number>` or `-n <number>`: Number of similar leaves to return (default: 3).
    - `--features_file <path_to_features.csv>` or `-f <path_to_features.csv>`: Path to the features CSV file (default: `data/features/all_features.csv`).
    - `--no-preprocess`: Skip preprocessing the query image if it's already processed.

### Streamlit Web Application

The interactive web application allows you to upload a leaf image and find similar ones from the database.

1.  **Ensure you have extracted features:** The Streamlit app relies on the `data/features/all_features.csv` file (or other feature files you select in the UI). Make sure you have run the feature extraction step.

2.  **Run the Streamlit app:**
    ```bash
    python main.py app
    ```
    This will typically open the application in your web browser automatically.

## Files

- **`leaf_search_app.py`**: The Streamlit application for interactive leaf search.
- **`main.py`**: Command-line interface for preprocessing, feature extraction, and search.
- **`modules/preprocess_all_images.py`**: Script to batch preprocess all raw leaf images.
- **`modules/extract_features.py`**: Script to batch extract features from all processed leaf images.
- **`modules/search_leaves.py`**: Script to perform searching similar images for one query image.
- **`src/preprocessing.py`**: Contains functions for image preprocessing tasks like resizing, segmentation, and enhancement.
- **`src/feature_extraction.py`**: Contains functions to extract various features (shape, color, edge, vein) from leaf images.
- **`src/search.py`**: Contains functions for calculating similarity and searching for matching leaves based on extracted features.
- **`requirements.txt`**: Lists the Python dependencies for the project.
- **`pyproject.toml`**: Project metadata and build system configuration.
- **`.python-version`**: Specifies the Python version used for this project.

## Contributing

Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.
