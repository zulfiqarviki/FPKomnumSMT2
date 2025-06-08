# FPKomnumSMT2
## Nama dan Anggota Kelompok
R10:
1. Muhammad Zulfiqar 5053241006
2. Azmii Maulawiy Said 5053241024
3. Jovan Oberto Mishael Sinaga 5053241031
4. Oktavian Ramadhan 5053241028
5. Muhammad Khalid Ash-Siddiqi 5053241030

## Kode
class NewtonInterpolation:
    def __init__(self, x, fx):
        self.x = x
        self.fx = fx
        self.n = len(x);
        self.divided_diff = [[0 for _ in range(self.n)] for _ in range(self.n)]
        for i in range(self.n):
            self.divided_diff[i][0] = fx[i];

    def Calculate(self, target_x):
        self.__FirstOrde()
        self.__SecondOrde()
        self.__ThirdOrde()

        x0 = self.x[0]
        x1 = self.x[1]
        x2 = self.x[2]

        b0 = self.divided_diff[0][0]
        b1 = self.divided_diff[0][1]
        b2 = self.divided_diff[0][2]
        b3 = self.divided_diff[0][3]

        result = b0
        result += b1 * (target_x - x0)
        result += b2 * (target_x - x0) * (target_x - x1)
        result += b3 * (target_x - x0) * (target_x - x1) * (target_x - x2)

        return round(result, 2)

    def __FirstOrde(self):
        for i in range(self.n - 1):
            self.divided_diff[i][1] = (self.divided_diff[i + 1][0] - self.divided_diff[i][0]) / (self.x[i + 1] - self.x[i])

    def __SecondOrde(self):
        for i in range(self.n - 2):
            self.divided_diff[i][2] = (self.divided_diff[i + 1][1] - self.divided_diff[i][1]) / (self.x[i + 2] - self.x[i])

    def __ThirdOrde(self):
        for i in range(self.n - 3):
            self.divided_diff[i][3] = (self.divided_diff[i + 1][2] - self.divided_diff[i][2]) / (self.x[i + 3] - self.x[i])

x = [8, 10, 12, 14]
fx = [660, 1326, 2280, 3570]
target = 11

newtonInterpolation = NewtonInterpolation(x, fx)
result = newtonInterpolation.Calculate(target);

print(f"{result: .2f}");

### Penjelasan Kode
class NewtonInterpolation
1. konstruktor __init__(self, x, fx),
   konstruktor ini berfungsi untuk menginisialisasi atribut objek atau menetapkan nilai-nilai awal pada program, menyimpan array x dan f(x) ke dalam objek. inisialisasi array 2D divided_diff berukuran n x n. Baris pertama (kolom 0) langsung diisi oleh nilai f(x).
2. method Calculate(self, target_x),
   method ini akan menghitung nilai interpolasi dari target_x (pada soal ini, x = 11) menggunakan: __FirstOrde(), __SecondOrde(), dan __ThirdOrde(), yang dimana dari ketiganya akan mengisi kolom 1, 2, dan 3. Method ini menggunakan rumus: ![image](https://github.com/user-attachments/assets/3e3fcb66-8de5-4b71-ac17-64b02d865a44) dan hasilnya akan dibulatkan ke dua angka di belakang koma menggunakan return round(result, 2).
   - __FirstOrde(self), yang mengisi kolom 1 dari array 2D/tabel divided_diff, menggunakan rumus: ![image](https://github.com/user-attachments/assets/9205e7e5-95fa-4881-89ef-a060dc1c629d)
   - __SecondOrde(self), mengisi kolom 2: ![image](https://github.com/user-attachments/assets/9bc28d9d-d3c2-42a7-b30c-c1ef4d35e11b)
   - __ThirdOrde(self), mengisi kolom 3: ![image](https://github.com/user-attachments/assets/f42b5bfd-dfe7-4874-8e49-725a6b23c626)



