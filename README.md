import pandas as pd
from sklearn.feature_extraction.text import TfidfVectorizer
from sklearn.metrics.pairwise import cosine_similarity


data = {
    'ProductID': [1, 2, 3, 4, 5],
    'ProductName': ['Laptop', 'Smartphone', 'Headphones', 'Camera', 'Smartwatch'],
    'Category': ['Electronics', 'Electronics', 'Accessories', 'Electronics', 'Accessories'],
    'Description': [
        'High-performance laptop for gaming and work',
        'Latest smartphone with cutting-edge technology',
        'Wireless headphones with noise cancellation',
        'DSLR camera for professional photography',
        'Smartwatch with fitness tracking and notifications'
    ]
}


products = pd.DataFrame(data)


user_input = input("Enter a product you are interested in: ")


vectorizer = TfidfVectorizer()
product_descriptions = vectorizer.fit_transform(products['Description'])


user_input_vector = vectorizer.transform([user_input])
similarities = cosine_similarity(user_input_vector, product_descriptions)


similar_products = similarities[0].argsort()[-3:][::-1]


print("\nRecommended Products:")
for idx in similar_products:
    print(f"Product Name: {products.iloc[idx]['ProductName']}")
    print(f"Category: {products.iloc[idx]['Category']}")
    print(f"Description: {products.iloc[idx]['Description']}\n")
