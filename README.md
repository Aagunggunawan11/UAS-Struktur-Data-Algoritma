# Data awal
data = [
    {"nama": "Fahmi", "alamat": "Jakarta"},
    {"nama": "Romi", "alamat": "Solo"},
    {"nama": "Andri", "alamat": "Jakarta"},
    {"nama": "Fadillah", "alamat": "Banyuwangi"},
    {"nama": "Ruli", "alamat": "Bandung"},
    {"nama": "Rudi", "alamat": "Bali"},
    {"nama": "Dendi", "alamat": "Purwokerto"},
    {"nama": "Zaki", "alamat": "Madiun"}
]

# Fungsi Bubble Sort manual
def bubble_sort(arr):
    arr_copy = [dict(x) for x in arr]
    n = len(arr_copy)
    for i in range(n):
        for j in range(0, n - i - 1):
            if arr_copy[j]["nama"] > arr_copy[j + 1]["nama"]:
                arr_copy[j], arr_copy[j + 1] = arr_copy[j + 1], arr_copy[j]
    return arr_copy

# Fungsi Selection Sort manual
def selection_sort(arr):
    arr_copy = [dict(x) for x in arr]
    n = len(arr_copy)
    for i in range(n):
        min_idx = i
        for j in range(i + 1, n):
            if arr_copy[j]["nama"] < arr_copy[min_idx]["nama"]:
                min_idx = j
        arr_copy[i], arr_copy[min_idx] = arr_copy[min_idx], arr_copy[i]
    return arr_copy

# Fungsi cetak tabel
def tampilkan_tabel(arr, judul):
    print(f"=== {judul} ===")
    print(f"{'Nama':<12} | {'Alamat':<12}")
    print("-" * 27)
    for item in arr:
        print(f"{item['nama']:<12} | {item['alamat']:<12}")
    print()

# Eksekusi
tampilkan_tabel(bubble_sort(data), "Hasil Bubble Sort")
tampilkan_tabel(selection_sort(data), "Hasil Selection Sort")
def binary_search(arr, target):
    # Menyimpan pasangan (nilai, indeks_awal) menggunakan indeks basis 1
    indexed_arr = [(arr[i], i + 1) for i in range(len(arr))]
    
    # Pengurutan manual (Bubble Sort) agar Binary Search dapat berjalan
    n = len(indexed_arr)
    for i in range(n):
        for j in range(0, n - i - 1):
            if indexed_arr[j][0] > indexed_arr[j + 1][0]:
                indexed_arr[j], indexed_arr[j + 1] = indexed_arr[j + 1], indexed_arr[j]
    
    low = 0
    high = n - 1
    found_indices = []
    
    # Algoritma Binary Search
    while low <= high:
        mid = (low + high) // 2
        if indexed_arr[mid][0] == target:
            # Cek ke kiri untuk menemukan duplikat
            left = mid
            while left >= 0 and indexed_arr[left][0] == target:
                found_indices.append(indexed_arr[left][1])
                left -= 1
                
            # Cek ke kanan untuk menemukan duplikat
            right = mid + 1
            while right < n and indexed_arr[right][0] == target:
                found_indices.append(indexed_arr[right][1])
                right += 1
            break
        elif indexed_arr[mid][0] < target:
            low = mid + 1
        else:
            high = mid - 1
            
    # Menampilkan hasil pengujian
    if not found_indices:
        print(f"Output : Angka {target} tidak ada dalam array")
    else:
        found_indices.sort()
        if len(found_indices) == 1:
            print(f"Output : Angka {target} ada di indeks ke {found_indices[0]}")
        else:
            str_indices = " dan ".join(str(idx) for idx in found_indices)
            print(f"Output : Angka {target} ada di indeks ke {str_indices}")

# Data Array Awal
data_array = [19, 40, 10, 90, 2, 50, 60, 50, 1]

# Pengujian (Test Cases)
test_cases = [1, 50, 100]

for target in test_cases:
    print(f"Input  : {target}")
    binary_search(data_array, target)
    print()
