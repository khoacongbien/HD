# Hướng dẫn nhanh sử dụng Pandas trong Python

123 Pandas là một thư viện mạnh mẽ trong Python được sử dụng để phân tích và xử lý dữ liệu. Dưới đây là hướng dẫn nhanh để bắt đầu sử dụng Pandas.

<p align="center">
  <img src="https://github.com/user-attachments/assets/74db2b3e-4fa3-4c07-ad53-0178f8aaa0fb" alt="TaskFlow Logo">
</p>

## Cài đặt Pandas

```python
pip install pandas
```

## Import thư viện

```python
import pandas as pd
import numpy as np  # Thường được sử dụng cùng với pandas
```

## Cấu trúc dữ liệu cơ bản

### Series

Series là một mảng một chiều có gán nhãn.

```python
# Tạo một Series từ một danh sách
s = pd.Series([1, 3, 5, np.nan, 6, 8])
print(s)
```

### DataFrame

DataFrame là một cấu trúc dữ liệu 2D có gán nhãn cho cả hàng và cột.

```python
# Tạo một DataFrame từ dictionary
data = {
    'Tên': ['An', 'Bình', 'Cường', 'Dung'],
    'Tuổi': [25, 30, 35, 28],
    'Thành phố': ['Hà Nội', 'TP HCM', 'Đà Nẵng', 'Huế']
}
df = pd.DataFrame(data)
print(df)
```

## Đọc và ghi dữ liệu

### Đọc file CSV

```python
# Đọc dữ liệu từ file CSV
df = pd.read_csv('duong_dan_den_file.csv')
```

### Đọc file Excel

```python
# Đọc dữ liệu từ file Excel
df = pd.read_excel('duong_dan_den_file.xlsx', sheet_name='Sheet1')
```

### Ghi dữ liệu

```python
# Ghi DataFrame ra file CSV
df.to_csv('ten_file_moi.csv', index=False)

# Ghi DataFrame ra file Excel
df.to_excel('ten_file_moi.xlsx', sheet_name='Sheet1', index=False)
```

## Xem dữ liệu

```python
# Hiển thị 5 dòng đầu tiên
df.head()

# Hiển thị 5 dòng cuối cùng
df.tail()

# Xem thông tin tổng quan của DataFrame
df.info()

# Thống kê mô tả dữ liệu số
df.describe()

# Xem kích thước (số hàng, số cột)
df.shape

# Xem tên các cột
df.columns
```

## Chọn và lọc dữ liệu

### Chọn theo cột

```python
# Chọn một cột
df['Tên']

# Chọn nhiều cột
df[['Tên', 'Tuổi']]
```

### Chọn theo hàng (sử dụng iloc - vị trí số)

```python
# Chọn hàng đầu tiên
df.iloc[0]

# Chọn nhiều hàng
df.iloc[0:3]

# Chọn hàng và cột cụ thể [hàng, cột]
df.iloc[0:3, 0:2]
```

### Chọn theo nhãn (sử dụng loc)

```python
# Nếu index là nhãn cụ thể (không phải số)
df.loc['nhan_hang', 'Tên']
```

### Lọc dữ liệu theo điều kiện

```python
# Lọc những người trên 30 tuổi
df[df['Tuổi'] > 30]

# Kết hợp nhiều điều kiện
df[(df['Tuổi'] > 25) & (df['Thành phố'] == 'Hà Nội')]
```

## Xử lý dữ liệu thiếu

```python
# Kiểm tra giá trị thiếu
df.isnull()
df.isnull().sum()  # Đếm số giá trị thiếu trong mỗi cột

# Loại bỏ hàng có giá trị thiếu
df_cleaned = df.dropna()

# Điền giá trị thiếu
df_filled = df.fillna(0)  # Điền bằng 0
df_filled = df.fillna(method='ffill')  # Điền theo giá trị trước đó
df_filled = df.fillna(df.mean())  # Điền bằng giá trị trung bình (cho cột số)
```

## Thao tác với dữ liệu

### Thêm cột mới

```python
# Thêm cột mới dựa trên cột đã có
df['Năm sinh'] = 2023 - df['Tuổi']
```

### Sắp xếp dữ liệu

```python
# Sắp xếp theo tuổi tăng dần
df_sorted = df.sort_values(by='Tuổi')

# Sắp xếp theo tuổi giảm dần
df_sorted = df.sort_values(by='Tuổi', ascending=False)

# Sắp xếp theo nhiều cột
df_sorted = df.sort_values(by=['Thành phố', 'Tuổi'])
```

### Nhóm và tổng hợp dữ liệu

```python
# Nhóm theo thành phố và tính trung bình tuổi
city_age = df.groupby('Thành phố')['Tuổi'].mean()

# Nhóm và áp dụng nhiều phép tính
result = df.groupby('Thành phố').agg({
    'Tuổi': ['mean', 'min', 'max', 'count']
})
```

## Kết hợp dữ liệu

### Nối dữ liệu (concatenate)

```python
# Nối hai DataFrame theo chiều dọc
df_combined = pd.concat([df1, df2])

# Nối hai DataFrame theo chiều ngang
df_combined = pd.concat([df1, df2], axis=1)
```

### Join và merge

```python
# Merge hai DataFrame dựa trên cột chung
merged_df = pd.merge(df1, df2, on='id_column')

# Left join
merged_df = pd.merge(df1, df2, on='id_column', how='left')

# Right join
merged_df = pd.merge(df1, df2, on='id_column', how='right')

# Outer join
merged_df = pd.merge(df1, df2, on='id_column', how='outer')
```

## Thống kê và phân tích

```python
# Tính tổng theo cột
df.sum()

# Tính trung bình theo cột
df.mean()

# Tính giá trị lớn nhất, nhỏ nhất
df.max()
df.min()

# Tìm vị trí giá trị lớn nhất, nhỏ nhất
df.idxmax()
df.idxmin()

# Tính tương quan giữa các cột số
df.corr()
```

## Trực quan hóa dữ liệu cơ bản

```python
# Import thư viện matplotlib
import matplotlib.pyplot as plt

# Vẽ biểu đồ cột
df['Tuổi'].plot(kind='bar')
plt.show()

# Vẽ biểu đồ đường
df.plot(x='Tên', y='Tuổi', kind='line')
plt.show()

# Vẽ biểu đồ scatter
df.plot.scatter(x='Tuổi', y='Năm sinh')
plt.show()

# Vẽ biểu đồ phân phối
df['Tuổi'].plot.hist()
plt.show()
```

## Xử lý thời gian và ngày tháng

```python
# Tạo chuỗi thời gian
dates = pd.date_range('20230101', periods=6)

# Chuyển đổi cột thành định dạng datetime
df['Ngày'] = pd.to_datetime(df['Ngày'])

# Trích xuất năm, tháng, ngày
df['Năm'] = df['Ngày'].dt.year
df['Tháng'] = df['Ngày'].dt.month
df['Ngày trong tuần'] = df['Ngày'].dt.day_name()
```

## Áp dụng hàm

```python
# Áp dụng một hàm cho mỗi phần tử trong Series
df['Tuổi'].apply(lambda x: x * 2)

# Áp dụng hàm cho mỗi hàng trong DataFrame
df.apply(lambda row: row['Tuổi'] * 2 if row['Thành phố'] == 'Hà Nội' else row['Tuổi'], axis=1)
```

## Tài nguyên học tập thêm

- [Trang chủ Pandas](https://pandas.pydata.org/)
- [Tài liệu chính thức](https://pandas.pydata.org/docs/)
- [Pandas Cheat Sheet](https://pandas.pydata.org/Pandas_Cheat_Sheet.pdf)
