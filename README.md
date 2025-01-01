import pandas as pd
from sklearn.feature_extraction.text import TfidfVectorizer
from sklearn.metrics.pairwise import cosine_similarity

# بيانات المنتجات
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

# إنشاء DataFrame
products = pd.DataFrame(data)

# استلام مدخلات المستخدم
user_input = input("Enter a product you are interested in: ")

# تحويل البيانات إلى صيغة رقمية باستخدام TfidfVectorizer
vectorizer = TfidfVectorizer()
product_descriptions = vectorizer.fit_transform(products['Description'])

# حساب تشابه المنتج مع مدخل المستخدم
user_input_vector = vectorizer.transform([user_input])
similarities = cosine_similarity(user_input_vector, product_descriptions)

# العثور على المنتجات ذات أعلى تشابه
similar_products = similarities[0].argsort()[-3:][::-1]

# عرض النتائج
print("\nRecommended Products:")
for idx in similar_products:
    print(f"Product Name: {products.iloc[idx]['ProductName']}")
    print(f"Category: {products.iloc[idx]['Category']}")
    print(f"Description: {products.iloc[idx]['Description']}\n")
