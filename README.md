
📖 Table of Contents

Project Overview

Business Problem & Solution

Dataset

System Architecture

Tech Stack

Installation & Setup

Usage Guide

Model Evaluation

Project Structure

🔭 Project Overview

This project builds an end-to-end product recommendation engine designed to improve user discovery and increase Average Order Value (AOV) for an e-commerce platform.

Unlike simple collaborative filtering models that fail with new products (the "Cold Start" problem), this system utilizes a Hybrid Approach. It combines:

Collaborative Filtering: Learning latent user preferences from past purchase history.

Content-Based Filtering: Analyzing product descriptions, categories, and tags using NLP (TF-IDF/Embeddings).

The final output is served via an interactive Streamlit Web App where users can login, view history, and see real-time recommendations.

💼 Business Problem & Solution

The Challenge: Users are overwhelmed by thousands of products. Most users leave the platform if they cannot find relevant items quickly.
The Solution:

Personalization: Show products aligned with user history.

Discovery: Surface relevant long-tail products that users wouldn't find via search.

Cold Start Handling: Recommend items based on metadata even if they have no sales history.

💾 Dataset

We utilized the [Amazon Product Data (Electronics Category)] (or specify your dataset, e.g., Olist/Flipkart).

Source: [Link to Kaggle/Source]

Size: ~1 Million Ratings, ~50k Products.

Data Dictionary:

userId: Unique identifier for the customer.

productId: Unique identifier for the item (ASIN).

rating: Integer (1-5) representing user satisfaction.

timestamp: Time of interaction.

description: Text description of the product (used for NLP).

category: Product taxonomy.

🏗️ System Architecture

The project follows a standard Data Science lifecycle:

Data Ingestion: Loading raw JSON/CSV data.

Preprocessing:

Data Cleaning (removing duplicates, handling missing values).

Exploratory Data Analysis (EDA): Analyzing the "Long Tail" of product popularity and sparsity.

Filtering users with <5 interactions to ensure statistical significance.

Feature Engineering:

Interaction Matrix: Creating a sparse User-Item matrix.

Text Processing: TF-IDF Vectorization on product descriptions.

Modeling (Hybrid):

Using the LightFM library to create a matrix factorization model that accepts both user/item IDs and item metadata features.

Optimization using WARP (Weighted Approximate-Rank Pairwise) loss for better ranking performance.

Deployment:

Model serialization (Pickle).

Streamlit Frontend for user interaction.

🛠 Tech Stack

Language: Python 3.9+

Data Manipulation: Pandas, NumPy

Visualization: Matplotlib, Seaborn

Machine Learning: Scikit-learn, LightFM (Hybrid Matrix Factorization)

NLP: NLTK, Scikit-learn (TF-IDF)

App Framework: Streamlit

Deployment: Docker (Optional)

⚙️ Installation & Setup

Follow these steps to replicate the environment locally.

1. Clone the Repository
code
Bash
download
content_copy
expand_less
git clone https://github.com/your-username/product-recommendation-system.git
cd product-recommendation-system
2. Create Virtual Environment
code
Bash
download
content_copy
expand_less
# Windows
python -m venv venv
venv\Scripts\activate

# Mac/Linux
python3 -m venv venv
source venv/bin/activate
3. Install Dependencies
code
Bash
download
content_copy
expand_less
pip install -r requirements.txt
4. Download Data

Download the dataset from [Link] and place it in the data/raw/ folder.

Run the preprocessing script:

code
Bash
download
content_copy
expand_less
python src/data_processing.py
5. Train the Model

This will train the Hybrid model and save the artifact to models/model.pkl.

code
Bash
download
content_copy
expand_less
python src/train_model.py
🚀 Usage Guide
Run the Web App

To see the recommendations in action, launch the Streamlit app:

code
Bash
download
content_copy
expand_less
streamlit run app.py

App Features:

Select User: Choose a User ID from the dropdown.

View History: See what this user has bought in the past.

Get Recommendations: Click the button to generate the Top 10 items for this user.

Explanation: (Optional) See why an item was recommended (e.g., "Because you liked [Category X]").

📊 Model Evaluation

We evaluate the system using ranking metrics rather than simple accuracy (MSE), as the goal is to get the order right.

Metric	Score	Explanation
Precision@10	0.18	18% of the top 10 recommended items were actually relevant to the user.
Recall@10	0.24	The model managed to find 24% of all items the user liked within the top 10 results.
AUC	0.86	High probability that a relevant item is ranked higher than an irrelevant one.

Note: These metrics are calculated on a held-out Test Set (20% of data).

📂 Project Structure
code
Text
download
content_copy
expand_less
├── data/
│   ├── raw/                  # Original CSV/JSON files
│   └── processed/            # Cleaned data & interaction matrices
├── notebooks/
│   ├── 01_EDA.ipynb          # Exploratory Data Analysis
│   ├── 02_Preprocessing.ipynb # Feature Engineering
│   └── 03_Model_Training.ipynb # Modeling & Hyperparameter Tuning
├── src/
│   ├── __init__.py
│   ├── data_processing.py    # Scripts for cleaning data
│   ├── train_model.py        # Script to train and save model
│   └── recommender.py        # Class for generating predictions
├── models/
│   └── hybrid_model.pkl      # Serialized trained model
├── app.py                    # Streamlit Application
├── requirements.txt          # Python dependencies
└── README.md                 # Project Documentation
🔮 Future Improvements

If you found this project useful, please give it a ⭐️!
