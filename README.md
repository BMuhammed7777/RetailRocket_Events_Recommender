# RetailRocket Events Recommender

An e-commerce recommendation system built using the RetailRocket events dataset.

The project explores user-item interactions and develops several recommendation approaches, including a popularity-based baseline, item-based collaborative filtering, and matrix factorization using Alternating Least Squares (ALS).

## Project Overview

Recommendation systems are widely used in e-commerce platforms to help users discover relevant products.

This project uses implicit user behavior such as:

- Product views
- Add-to-cart events
- Transactions

to analyze user-item interactions and generate personalized product recommendations.

The main goal of the project is to investigate how different recommendation approaches perform on a highly sparse e-commerce interaction dataset.

## Dataset

This project uses the RetailRocket e-commerce dataset.

The dataset contains user interaction events with products, including:

- `visitorid` — user identifier
- `event` — type of interaction (view, addtocart, transaction)
- `itemid` — product identifier
- `transactionid` — transaction identifier
- `timestamp` — event timestamp

### Dataset files

The project uses the following dataset file:
events.csv
textThe dataset is not included in this repository because of its large file size.

To run the project:

1. Download the RetailRocket e-commerce dataset.
2. Extract the dataset.
3. Copy `events.csv` into the same directory as the notebook.
4. Run the notebook.

The expected project structure is:
RetailRocket_Events_Recommender/
│
├── RetailRocket_Events_Recommender.ipynb
├── events.csv
├── requirements.txt
├── README.md
└── .gitignore
text## Project Workflow

The notebook is organized into several phases.

### 1. Data Understanding

The dataset is initially explored to understand:

- Dataset dimensions
- Data types
- Missing values
- Unique users
- Unique items
- Event types
- Timestamp range
- Transaction relationships

### 2. Data Quality Analysis

The project checks for:

- Exact duplicate rows
- Duplicate user-item-event-timestamp combinations
- Invalid IDs
- Timestamp statistics
- Repeated interactions

### 3. Data Cleaning

The following cleaning operations are performed:

- Removal of exact duplicate rows
- Removal of anomalous visitor IDs
- Removal of invalid transaction IDs
- Conversion of timestamps into datetime format

### 4. Exploratory Data Analysis

The project investigates:

- User activity
- Item popularity
- Funnel conversion
- Dataset sparsity
- Popularity concentration
- Most active users
- Most popular products

### 5. User Behavior Analysis

User behavior is analyzed through:

- Number of unique products per user
- Repeated user-item interactions
- Purchasing vs. non-purchasing users
- Interaction patterns

### 6. Interaction Matrix

A user-item interaction representation is constructed to support recommendation algorithms.

The project also examines the high sparsity of the user-item interaction space.

### 7. Train / Validation / Test Split

The interaction data is divided into separate datasets for model development and evaluation.

### 8. Recommendation Models

Three recommendation approaches are evaluated.

#### Popularity-based Recommendation

A simple baseline that recommends the most popular products.

#### Item-based Collaborative Filtering

Items are compared based on user interaction patterns to generate recommendations for users.

#### Matrix Factorization

The project uses Alternating Least Squares (ALS) from the `implicit` library to learn latent representations of users and items.

The final model is trained with:

- `factors = 128`
- `alpha = 60`
- `iterations = 25`
- `regularization = 0.1`

Hyperparameter experiments are also performed using different values of:

- `factors = [32, 64, 128]`
- `alpha = [20, 40, 60]`

## Evaluation

The recommendation models are evaluated using:

- Hit Rate@10
- Hit Rate@20

The model comparison reported in the notebook is:

| Model                  | Hit Rate@10 | Hit Rate@20 |
|------------------------|-------------|-------------|
| Popularity             | 0.0081      | 0.0121      |
| Item-based CF          | 0.0279      | 0.0353      |
| Matrix Factorization   | 0.0576      | 0.0852      |

The evaluation shows how the different recommendation approaches perform under the project's evaluation setup.

## Recommendation Pipeline

After training the matrix factorization model, a recommendation function is implemented:

```python
recommend_for_user(user_id, K=10)
The function:

Checks whether the user exists in the training data.
Retrieves the user's latent representation.
Calculates scores for available items.
Removes previously interacted items.
Selects the top-K items.
Returns the recommended product IDs.

The project also includes a cold-start check for users who are not present in the training data.
Model Persistence
The notebook demonstrates how to save and load the trained ALS model and its mappings.
The following artifacts are generated locally:
textsaved_model/
│
├── als_model.npz
└── mappings.pkl
These files are not included in this repository because of their large size.
If you want to reproduce the project, train the model by running the notebook. The model and mappings will then be generated locally.
Installation
Clone the repository and install the required Python packages:
Bashpip install -r requirements.txt
How to Run
1. Clone the repository
Bashgit clone <your-repository-url>
2. Move into the project directory
Bashcd RetailRocket_Events_Recommender
3. Download the RetailRocket dataset
Download the RetailRocket e-commerce dataset and place:
textevents.csv
inside the project directory.
4. Install dependencies
Bashpip install -r requirements.txt
5. Open the notebook
Open:
textRetailRocket_Events_Recommender.ipynb
using Jupyter Notebook, JupyterLab, Google Colab, or another compatible environment.
6. Run the notebook
Run the notebook cells in order.
The notebook will perform:
textData Loading
      ↓
Data Understanding
      ↓
Data Quality Analysis
      ↓
Data Cleaning
      ↓
EDA
      ↓
User Behavior Analysis
      ↓
Interaction Matrix
      ↓
Train / Validation / Test Split
      ↓
Popularity Baseline
      ↓
Item-based Collaborative Filtering
      ↓
Matrix Factorization (ALS)
      ↓
Hyperparameter Testing
      ↓
Model Evaluation
      ↓
Recommendation Pipeline
Technologies
The project uses:

Python
Pandas
NumPy
Matplotlib
Seaborn
SciPy
Scikit-learn
Implicit
Jupyter Notebook
Pickle

Limitations
Several limitations should be considered:

The interaction matrix is extremely sparse.
A large proportion of users have very limited interaction history.
New users and items can create cold-start problems.
The project mainly uses interaction data rather than detailed product metadata.
The recommendation quality depends on the available historical interaction data.

Future Improvements
Possible future improvements include:

Incorporating item metadata
Using interaction strengths such as views, add-to-cart events, and transactions
Exploring additional recommendation algorithms
Improving cold-start handling
Testing additional ranking metrics
Performing more extensive hyperparameter optimization
Building an API or web application for real-time recommendations

Project Structure
textRetailRocket_Events_Recommender/
│
├── RetailRocket_Events_Recommender.ipynb
├── README.md
├── requirements.txt
└── .gitignore
The dataset and trained model artifacts are intentionally excluded from the repository because of their large file sizes.
