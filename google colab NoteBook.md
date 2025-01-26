import kagglehub
import pandas as pd
import os

# Download the latest version of the dataset
path = kagglehub.dataset_download("ashaychoudhary/panic-attack-dataset")

# Print the path to the downloaded files
print("Path to dataset files:", path)

# Check the files inside the downloaded folder
print("Files in the downloaded directory:", os.listdir(path))

# Adjust the path to the correct CSV file based on the output
dataset_path = os.path.join(path, 'panic_attack_dataset.csv')  # Correct file name based on your output

# Load the dataset
try:
    data = pd.read_csv(dataset_path)
    # Display column names to identify the correct label
    print("Column names in the dataset:", data.columns)

    # Function to display dataset description
    def describe_dataset():
        print("Goal of Collecting this Dataset:")
        print("The goal of this dataset is to analyze panic attack occurrences based on different features. It aims to help identify factors contributing to panic attacks and their triggers.")

        print("\nSource of the Dataset:")
        print("Dataset source: https://www.kaggle.com/datasets/ashaychoudhary/panic-attack-dataset")

        print("\nGeneral Information about the Dataset:")
        print(f"Number of objects (rows): {data.shape[0]}")
        print(f"Number of attributes (columns): {data.shape[1]}")

        # Displaying the attribute names and data types
        print("\nAttributes and their data types:")
        print(data.dtypes)

        print("\nClass Name or Labels:")
        # Use the correct class label column name
        class_label_column = "Medical_History"  # Corrected column name
        if class_label_column in data.columns:
            print(f"The class label is: {class_label_column}")
            print("The unique values in the class label are:", data[class_label_column].unique())
        else:
            print(f"The column '{class_label_column}' does not exist. Please check the column name.")

    # Call the function to display the description
    describe_dataset()
except FileNotFoundError:
    print(f"Could not find the dataset at: {dataset_path}. Please check the file name and path.")
