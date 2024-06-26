# finalDatamining
1. Instalasi Paket yang Diperlukan
Pastikan Anda telah menginstal paket-paket yang diperlukan. Anda bisa menggunakan pip untuk menginstalnya:

bash
Copy code
pip install pandas matplotlib scikit-learn

2. Siapkan File CSV
Pastikan file Report Item Details - 01-01-2023 - 09-05-2023 - Outlet_1 - 645b0e0d.csv berada di direktori yang sama dengan kode Python Anda atau tentukan path yang sesuai.
3. Buat dan Jalankan Kode Python
Salin kode berikut ke dalam file Python (misalnya, sales_analysis.py):

python
Copy code
import pandas as pd
import matplotlib.pyplot as plt
from sklearn.linear_model import LinearRegression
from sklearn.model_selection import train_test_split
from sklearn.metrics import mean_squared_error, r2_score, mean_absolute_error
from sklearn.neighbors import KNeighborsRegressor

# Load data penjualan dari file CSV
file_path = 'Report Item Details - 01-01-2023 - 09-05-2023 - Outlet_1 - 645b0e0d.csv'
data = pd.read_csv(file_path)
features = ['Gross Sales', 'Quantity', 'Discounts', 'Net Sales']
target = 'Net Sales'

# Pisahkan data menjadi set pelatihan dan pengujian
X_train, X_test, y_train, y_test = train_test_split(
    data[features], data[target], test_size=0.2, random_state=42
)

# Buat model regresi linear
linear_model = LinearRegression()
# Latih model dengan data pelatihan
linear_model.fit(X_train, y_train)
# Prediksi jumlah penjualan pada data pengujian
y_pred_linear = linear_model.predict(X_test)

# Evaluasi performa model regresi linear
mse_linear = mean_squared_error(y_test, y_pred_linear)
r2_linear = r2_score(y_test, y_pred_linear)
mae_linear = mean_absolute_error(y_test, y_pred_linear)
rmse_linear = mean_squared_error(y_test, y_pred_linear, squared=False)

print('Regresi Linear:')
print(f'MAE: {mae_linear}')
print(f'RMSE: {rmse_linear}')
print(f'R-squared: {r2_linear}')

# Tentukan food terlaris berdasarkan koefisien regresi
coef = linear_model.coef_
feature_importance = dict(zip(features, coef))

# Print koefisien regresi
print('Koefisien Regresi:')
for feature, coef in feature_importance.items():
    print(f'{feature}: {coef}')

# K-Nearest Neighbors
knn_model = KNeighborsRegressor(n_neighbors=5)
# Latih model KNN dengan data pelatihan
knn_model.fit(X_train, y_train)
# Prediksi jumlah penjualan pada data pengujian dengan KNN
y_pred_knn = knn_model.predict(X_test)

# Evaluasi performa model KNN
mse_knn = mean_squared_error(y_test, y_pred_knn)
r2_knn = r2_score(y_test, y_pred_knn)
mae_knn = mean_absolute_error(y_test, y_pred_knn)
rmse_knn = mean_squared_error(y_test, y_pred_knn, squared=False)

print('K-Nearest Neighbors:')
print(f'MAE: {mae_knn}')
print(f'RMSE: {rmse_knn}')
print(f'R-squared: {r2_knn}')

# Visualisasi
plt.figure(figsize=(8, 6))
category_counts = data['Category'].value_counts()
plt.bar(category_counts.index, category_counts.values, label='Data Asli')
plt.xlabel('Category')
plt.ylabel('Count')
plt.title('Hubungan Rating dan Jumlah Penjualan')
plt.legend()
plt.show()

# Temukan produk dengan rating tertinggi (asumsi kolom 'rating' ada)
food_terlaris = data.sort_values(by='Date', ascending=False).head(10)
# Print 10 produk terlaris berdasarkan rating
print('\n10 Produk Terlaris :')
print(food_terlaris[['Category', 'Date']])

4. Jalankan Kode Python
Jalankan file Python tersebut melalui terminal atau command prompt:

bash
Copy code
python sales_analysis.py

5. Interpretasi Hasil
Regresi Linear: Akan menampilkan Mean Absolute Error (MAE), Root Mean Squared Error (RMSE), dan nilai R-squared untuk model regresi linear.
K-Nearest Neighbors: Akan menampilkan MAE, RMSE, dan nilai R-squared untuk model KNN.
Visualisasi: Akan menampilkan grafik batang hubungan antara kategori dan jumlah penjualan.
Produk Terlaris: Akan mencetak 10 produk terlaris berdasarkan kolom 'Date'.