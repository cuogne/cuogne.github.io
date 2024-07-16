---
description: >-
  4 Thuật toán tìm kiếm
title: Search Algorithms
date: 2024-07-17 00:00:00 +0700
categories: [Blog, Code]
---

## 4 Thuật toán tìm kiếm

### 1. Linear Search (Tìm kiếm tuyến tính)

Đây là thuật toán đơn giản nhất trong tất cả các thuật toán tìm kiếm. Trong kiểu tìm kiếm này, một hoạt động tìm kiếm liên tiếp được diễn ra qua tất cả từng phần tử. Mỗi phần tử đều được kiểm tra và nếu tìm thấy bất kỳ kết nối nào thì phần tử cụ thể đó được trả về; nếu không tìm thấy thì quá trình tìm kiếm tiếp tục diễn ra cho tới khi tìm kiếm hết dữ liệu.

Code minh họa

```c++
int linearSearch(int arr[], int target, int n) {
    for(int i = 0; i < n; i++) {
        if (arr[i] == target) {
            return i;
        }
    }
    return -1;
}
```

Độ phức tạp:
+ Trường hợp tốt nhất: O(1) - Khi phần tử mục tiêu nằm ở vị trí đầu tiên của mảng.
+ Trường hợp trung bình và xấu nhất: O(n) - Khi phải duyệt qua toàn bộ mảng để tìm phần tử mục tiêu hoặc phần tử mục tiêu không tồn tại trong mảng. Trong trường hợp này, (n) là số lượng phần tử trong mảng.

### 2. Binary Search (Tìm kiếm nhị phân)

Tìm kiếm nhị phân, còn gọi là tìm kiếm nửa khoảng, tìm kiếm logarit, hay chặt nhị phân là một giải thuật tìm kiếm được sử dụng để tìm vị trí của một giá trị mục tiêu trong một mảng đã được sắp xếp. Nó hoạt động dựa trên thuật toán chia để trị (Divide and Conquer) bằng cách liên tục chia đôi khoảng tìm kiếm cho đến khi tìm thấy giá trị mục tiêu hoặc khoảng tìm kiếm trống. Khoảng tìm kiếm được chia đôi bằng cách so sánh phần tử mục tiêu với giá trị ở giữa không gian tìm kiếm.

Cách thức hoạt động
- Xác định chỉ số của phần tử giữa mảng: mid = (left + right) / 2.
- So sánh giá trị của phần tử giữa mid với giá trị mục tiêu target.
- Nếu target == array[mid], trả về chỉ số mid.
- Nếu target < array[mid], tiếp tục tìm kiếm trong nửa mảng bên trái.
- Nếu target > array[mid], tiếp tục tìm kiếm trong nửa mảng bên phải.
- Lặp lại quá trình trên cho đến khi tìm thấy giá trị mục tiêu hoặc khi không còn phần tử nào để kiểm tra (nếu left > right).

Code minh họa

```c++
int binarySearch(int arr[], int target, int left, int right){
  if (left > right){
    return -1;
  }
  int mid = (left + right) / 2 ; // tranh tran so thi l + (r - l) /2 

  if (arr[mid] == target){
    return mid ;
  }
  else if (arr[mid] > target){
    return binarySearch(arr, target, left, mid - 1);
  }
  else return binarySearch(arr,target, mid + 1, right);
}
```

Độ phức tạp
+ Trường hợp tốt nhất: O(1) - Khi phần tử mục tiêu nằm ở vị trí giữa mảng.
+ Trường hợp trung bình và xấu nhất: O(logn) - Do mỗi lần so sánh giảm kích thước mảng tìm kiếm xuống một nửa.

### 3. Ternary Search (Tìm kiếm tam phân)

Thuật toán Tìm kiếm tam phân (Ternary Search) là một kỹ thuật tìm kiếm trên một mảng đã được sắp xếp hoặc một hàm mục tiêu unimodal (hàm có một cực trị duy nhất, có thể là cực đại hoặc cực tiểu) bằng cách chia không gian tìm kiếm thành ba phần bằng nhau và loại bỏ một hoặc hai phần không chứa giá trị mục tiêu. 

Cách thức hoạt động
- Chọn hai điểm chia, mid1 và mid2, sao cho không gian tìm kiếm được chia thành ba phần có kích thước gần bằng nhau. Thông thường, mid1 = left + (right-left)/3 và mid2 = right - (right-left)/3.
- So sánh giá trị tại mid1 và mid2 với giá trị mục tiêu target:
- Nếu target == array[mid1], trả về mid1.
- Nếu target == array[mid2], trả về mid2.
- Xác định khoảng chứa giá trị mục tiêu dựa trên so sánh:
- Nếu target < array[mid1], tiếp tục tìm kiếm trong khoảng từ left đến mid1 - 1.
- Nếu target > array[mid2], tiếp tục tìm kiếm trong khoảng từ mid2 + 1 đến right.
- Nếu không, tiếp tục tìm kiếm trong khoảng từ mid1 + 1 đến mid2 - 1.
- Lặp lại quá trình trên cho đến khi tìm thấy giá trị mục tiêu hoặc khi left > right.

Code minh họa

```c++
int ternarySearch(int arr[], int l, int r, int target) {
    if (r >= l) {
        int mid1 = l + (r - l) / 3;
        int mid2 = r - (r - l) / 3;

        if (arr[mid1] == target) return mid1;
        if (arr[mid2] == target) return mid2;

        if (target < arr[mid1])
            return ternarySearch(arr, l, mid1 - 1, target);

        if (target > arr[mid2])
            return ternarySearch(arr, mid2 + 1, r, target);

        return ternarySearch(arr, mid1 + 1, mid2 - 1, target);
    }
    return -1;
}
```

Độ phức tạp
- Trường hợp tốt nhất: O(1) - Khi target trùng với mid1 hoặc mid2
- Trường hợp trung bình và xấu nhất: O(logn) với cơ số của log là 3 - thuật toán giảm kích thước của không gian tìm kiếm xuống một phần ba sau mỗi lần so sánh.
- Thường thì biểu diễn độ phức tạp thời gian thông thường không phân biệt cơ sở của logarit. Do đó, dù là (log_2 n) hay (log_3 n), chúng ta thường biểu diễn độ phức tạp thời gian là (O(logn)) để thể hiện rằng số lần thực hiện so sánh tăng lên một cách logaritmic so với kích thước của mảng.

### 4. Jump Search (Tìm kiếm nhảy)

Thuật toán Tìm kiếm Nhảy (Jump Search) là một giải thuật tìm kiếm trên mảng đã được sắp xếp bằng cách nhảy qua các phần tử với một khoảng cố định, sau đó thực hiện tìm kiếm tuyến tính trong khoảng đã nhảy qua để tìm giá trị mục tiêu. Đây là một cách tiếp cận giữa tìm kiếm tuyến tính và tìm kiếm nhị phân.

Cách thức hoạt động
- Chọn một khoảng nhảy block (thường là căn bậc hai của kích thước mảng).
- Nhảy qua các phần tử với khoảng cách block cho đến khi tìm thấy phần tử lớn hơn hoặc bằng giá trị mục tiêu hoặc đến cuối mảng.
- Khi tìm thấy phần tử lớn hơn hoặc bằng giá trị mục tiêu, thực hiện tìm kiếm tuyến tính từ vị trí cuối cùng đã nhảy qua đến vị trí hiện tại để tìm giá trị mục tiêu.
- Nếu tìm thấy giá trị mục tiêu, trả về chỉ số của nó; nếu không, trả về -1

Code minh họa
```c++
int jumpSearch(int arr[], int x, int n) {
    int step = sqrt(n); // buoc nhay
    int prev = 0; // vi tri bat dau cua buoc nhay
    while (arr[min(step, n) - 1] < x) {
        prev = step;
        step += sqrt(n);
        if (prev >= n)
            return -1;
    }

    while (arr[prev] < x) {
        prev++;
        if (prev == min(step, n))
            return -1;
    }

    if (arr[prev] == x)
        return prev;
    return -1;
}
```

Độ phức tạp
- Trường hợp tốt nhất: O(1) - Điều này xảy ra khi phần tử mục tiêu x nằm ở vị trí đầu tiên của mảng hoặc rất gần với điểm bắt đầu của mảng. Trong trường hợp này, thuật toán sẽ tìm thấy x ngay trong lần kiểm tra đầu tiên hoặc sau một vài bước nhảy và tìm kiếm tuyến tính, dẫn đến độ phức tạp thời gian là (O(1)).
- Trường hợp trung bình và xấu nhất: O(sqrt(n)) - Trường hợp xấu nhất xảy ra khi phần tử mục tiêu x nằm ở cuối mảng hoặc không có trong mảng. Trong trường hợp này, thuật toán cần thực hiện đầy đủ các bước nhảy qua mảng và sau đó là tìm kiếm tuyến tính trong khoảng cuối cùng.

### Nguồn tài liệu tham khảo
[Codelearn.io](https://codelearn.io/sharing/5-thuat-toan-tim-kiem-moi-ltv-nen-biet)

[Geeksforgeeks](https://www.geeksforgeeks.org/jump-search/)
