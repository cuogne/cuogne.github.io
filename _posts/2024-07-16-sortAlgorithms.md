---
description: >-
  12 Thuật toán sắp xếp
title: Sort Algorithms
date: 2024-07-16 10:00:00 +0700
categories: [Blog, Code]
---

[Nguồn bài viết 1](https://github.com/dungbachviet/SortingAlgorithms/blob/master/README.md)

[Nguồn bài viết 2](https://github.com/nxhawk/SortAlgorithms?tab=readme-ov-file)

Mình có chỉnh sửa một số chỗ so với các bài viết gốc.

# 12 THUẬT TOÁN SẮP XẾP CƠ BẢN

### Mở đầu

*Xin chào mọi người,* 

Trong bài viết đầu tay này, mình xin trình bày về 12 giải thuật phổ biến và cơ bản trong lớp bài toán sắp xếp các chuỗi số, chuỗi ký tự. Ý tưởng của bài viết được khảo cứu và trích dẫn chủ yếu từ một số nguồn tài liệu hữu ích như : Geeksforgeeks.org, tutorialspoint.com, stackoverflow.com…  

Với mỗi giải thuật, tớ sẽ cố gắng trình bày và làm rõ chúng theo bố cục với những nội chính sau : 
+ Tư tưởng của giải thuật
+ Mã nguồn ( được minh họa trên ngôn ngữ lập trình C/console)
+ Độ phức tạp của thuật toán
+ Đưa ra nhận xét và đánh giá thuật toán.
+ So sánh với các giải thuật khác và Đưa ra giải pháp tối ưu cùng khả năng ứng dụng của bài toán trong thực tế cuộc sống.

Một điều nữa là mình rất mong chờ để nhận được nhiều ý kiến đóng góp và phản hồi từ mọi người để bài viết này ngày càng trở nên hoàn thiện và có sức lan tỏa mạnh mẽ hơn !

## **1.	Thuật toán Selection Sort (Sắp xếp chọn)**

### **1.1	Code minh họa**

```c++
// algorithm for Selection Sort
void selectionSort (int a[], int n){
    for (int i = 0 ; i < n - 1 ; ++i){
        int minIdx = i ;

        for (int j = i + 1 ; j < n ; ++j){
            if (a[j] < a[minIdx]){
                minIdx = j;
            }
        }

        // swap
        int temp = a[i];
        a[i] = a[minIdx];
        a[minIdx] = temp ;        
    }
}

```

### **1.2	Ý tưởng giải thuật** 

Với một mảng số ban đầu chưa được sắp xếp gồm n phần tử. Ý tưởng của thuật toán được mô tả thông qua các bước chính như sau : 
+ Chọn 1 phần tử đầu tiên của dãy số, giả sử phần tử này là nhỏ nhất, sau đó lưu lại chỉ số phần tử đó.
+ Duyệt để so sánh phần tử nhỏ nhất này với các phần tử còn lại (tức các phần tử tiếp theo của dãy số). Nếu phát hiện có bất kỳ phần tử nào nhỏ hơn phần tử cần so sánh, tiến hành thay đổi giá trị của chỉ số lưu trữ phần tử nhỏ nhất.
+ Sau khi duyệt xong toàn bộ mảng, kết quả chúng ta tìm được đó là: vị trí (chỉ số) của phần tử nhỏ nhất trong mảng đó. Lúc này, thực hiện hoán đổi vị trí của : phần tử đầu tiên trong mảng và vị trí của phần tử nhỏ nhất (đã xác định tử bước trên).
+ Sau khi hoán đổi, phần tử nhỏ nhất sẽ luôn nằm “cố định” ở đầu mảng và phần tử này sẽ không còn đóng góp vai trò nào cho những lần sắp xếp tiếp theo. Do phần tử đầu tiên đã cố định, quá trình sắp xếp chỉ còn tác động lên n - 1 tiếp theo (không xét phần tử thứ nhất). Và thực hiện lặp lại một cách tương tự quá trình trên từ bước 1 tới bước cuối cùng … Sau mỗi quá trình lặp lại đó, ta sẽ lần lượt xác định và cố định ra được phần tử nhỏ thứ 2, phần tử nhỏ thứ 3 …, phần tử nhỏ thứ n – 1. Tới đây giải thuật kết thúc !  

### **1.3	Độ phức tạp của thuật toán :**  

Trường hợp tốt nhất: `(O(n^2))`

- Ngay cả trong trường hợp tốt nhất, khi mảng đã được sắp xếp, thuật toán vẫn phải so sánh mỗi phần tử với mọi phần tử khác để tìm ra phần tử nhỏ nhất. Do đó, số lần so sánh không thay đổi và là `(n(n - 1)/2)`, dẫn đến độ phức tạp là `(O(n^2))`.

Trường hợp trung bình và xấu nhất: `(O(n^2))`

- Trong trường hợp trung bình và xấu nhất, mỗi phần tử trong mảng cần được so sánh với mọi phần tử khác chưa được sắp xếp để tìm ra phần tử nhỏ nhất. Điều này dẫn đến tổng số lần so sánh là `(n(n - 1)/2)`, và do đó, độ phức tạp thời gian là `(O(n^2))`.

### **1.4. Nhận xét thuật toán**  

#### **1.4.1. Ưu điểm**  

- Selection Sort là một giải thuật đã hạn chế được khá nhiều số hoán vị (đổi chỗ 2 phần tử trong mảng) so với giải thuật Sắp xếp Nổi bọt (do nó sử dụng biến chỉ số để lưu lại phần tử nhỏ nhất,… để đến cuối cùng mới tiến hành hoán vị)
- Giải thuật này có tính chất ổn định : Tức vị trí tương đối của các phần tử "bằng nhau về giá trị" trong mảng vẫn được giữ nguyên trước và khi sắp xếp (nghĩa là nếu có 2 phần tử bằng nhau trong mảng, phần tử 1 nằm bên bên trái phần tử 2 thì sau khi sắp xếp thứ tự này vẫn không thay đổi)
- Không đòi hỏi thêm không gian nhớ phụ, nên giải thuật mang tính chất “ Tại chỗ”
- Trong thực tế, giải thuật này có thể được sử dụng như một giải pháp hỗ trợ cho một giai đoạn nào đó trong những giải thuật sắp xếp khác

#### **1.4.2. Nhược điểm :**   

- Độ phức tạp của giải thuật tuy đã được cải thiện nhưng nhìn chung vẫn còn khá lớn so với các thuật toán sắp xếp hiệu quả khác (như QuickSort, MergeSort)
- Chưa giải quyết được vấn đề khi mà đầu vào của dãy số đã được sắp xếp (nghĩa là nếu đầu vào là một dãy số đã được sắp xếp thì thuật toán này vẫn cứ "máy móc" để sắp xếp lại)

### **1.5. Giải pháp tối ưu :**  

- Trong tình huống dãy số đầu vào đã được sắp xếp, giải pháp được đưa ra sẽ là : Sử dụng một biến hasSwapped để duyệt từ đầu tới cuối mảng, để phát hiện xem dãy số đã được sắp xếp tăng dần hay giảm dần hay chưa? Nếu hasSwapped = 0 khi duyệt theo chiều thuận tức dãy đã được sắp xếp tăng dần. Nếu hasSwapped = 0 khi duyệt theo chiều nghịch, tức dãy đã được sắp xếp giảm dần, vì thế chỉ cần đảo ngược lại dãy số đó để có một thứ tự đúng!

## **2.Thuật toán Insertion Sort (Sắp xếp chèn)** 

### **2.1. Mã nguồn minh họa :**  

```c++
// algorithm for Insertion Sort
void insertionSort(int a[], int n){
    for (int i = 1; i < n; i++) {
        int key = a[i];
        int j = i - 1;

        while (j >= 0 && a[j] > key) {
            a[j + 1] = a[j];
            j = j - 1;
        }
        a[j + 1] = key;
    }
}
```  


```c++
// algorithm for Insertion Sort With Binary Searching
void InsertSortWithBinarySearch(int a [], int n) {
	for (int i = 1; i < n; i++) {
		int tmp = a[i], l = 0, r = i - 1;
		
		while (l <= r)// ket hop chat nhi phan tim vi tri thoa trong khoang phia truoc vi da sap xep khoang nay
		{
			int mid = (l + r) / 2;
			if (tmp < a[mid]) r = mid - 1;
			else l = mid + 1;
		}

		for (int j = i; j > l; j--) 
				a[j] = a[j - 1];
		a[l] = tmp;
	} 
}
```  

### **2.2. Ý tưởng của giải thuật :**  

Giải thuật này xuất phát từ các thao tác sắp xếp của những người chơi bài. Tư tưởng đó được thể hiện như sau :   

+ Từ một tập bài gồm n quân bài của người chơi, họ cần phải sắp xếp thứ tự các quân bài trên tay theo một thứ tự tăng dần. Lúc này, họ sẽ duyệt từ quân bài thứ 2 tới quân bài cuối cùng (thứ n). Đối với quân bài thứ 2, họ cần phải so sánh quân bài này với các quân bài phía trước nó, tức lúc này là quân bài thứ 1. Rõ ràng, các quân bài phía trước quân bài thứ 2 đều đã được sắp xếp ( do chỉ có 1 quân bài phía trước). Công việc của người chơi lúc này là chỉ cần chèn quân bài thứ 2 vào vị trí thích hợp trong số các quân bài phía trước sao cho sau thao tác chèn này, các quân bài phía trước cũng phải được sắp xếp theo một thứ tự tăng dần
+ Tiếp tục với việc xét quân bài thứ 3, ta tiến hành so sánh quân bài này với dãy các quân bài đã được sắp xếp ở phía trước nó. Sau đó tiến hành thực hiện thao tác chèn quân bài này vào ví trí thích hợp trong dãy các quân bài phía trước để tạo thành một dãy con được sắp xếp tăng dần.
+ Một cách hoàn toàn tương tự với các quân bài thứ 4, 5 … n.   
Kết thúc quá trình này, ta sẽ thu được một dãy số được sắp xếp tăng dần  

### **2.3. Độ phức tạp của thuật toán**   

Trường hợp tốt nhất: `(O(n))`

- Trong trường hợp tốt nhất, khi mảng đã được sắp xếp, mỗi phần tử chỉ cần được so sánh một lần và không cần chèn; do đó, độ phức tạp thời gian là `(O(n))`. 

Trường hợp trung bình và xấu nhất: `(O(n^2))`

- Trong trường hợp trung bình và xấu nhất, mỗi phần tử trong mảng có thể cần được so sánh và chèn qua mỗi phần tử đã được sắp xếp trước đó. Điều này dẫn đến một số lượng lớn các phép so sánh và chèn, với tổng số lần là khoảng `(n(n - 1)/2)`, dẫn đến độ phức tạp thời gian là `(O(n^2))`.

### **2.4. Nhận xét và đánh giá**  

#### **2.4.1. Ưu điểm :**  

- Làm việc tốt trong trường hợp mảng có ít phần tử
- Giải thuật có tính chất ổn định và tại chỗ
- Được sử dụng như một sự hỗ trợ trong một vài giai đoạn con ở một số thuật toán sắp xếp khác
- Đơn giản, dễ hiểu và dễ cài đặt
- Là thuật toán sắp xếp tốt nhất đối với dãy đã gần được sắp xếp , nghĩa là mỗi phần tử đã đứng ở vị trí rất gần vị trí trong thứ tự cần sắp xếp  

#### **2.4.2. Nhược điểm :**   

- Độ phức tạp trung bình vẫn còn khá lớn O(n^2) so với các thuật toán sắp xếp nhanh nhất hiện nay như QuickSort  

### **2.5. Sự tối ưu, so sánh và mở rộng :**   

- Thuật toán tuy đã giải quyết được tình huống dãy số đầu vào đã được sắp xếp tăng dần ( tức nó chỉ mất O(n) thời gian sắp xếp). Nhưng còn với trường hợp dãy số đầu vào lại được sắp xếp theo thứ tự giảm dần, trong tình huống này giải thuật vẫn sẽ mất thời gian O(n^2) (thậm chí đây được xếp vào tình huống đầu vào tồi nhất). Để tối ưu giải thuật, xin đề xuất một giải pháp với cách sử dụng biến hasSwapped (như giải pháp tối ưu trong Selection Sort) để phát hiện dãy đầu vào đã được sắp xếp giảm dần mất O(n) thời gian,sau đó tốn thêm O(n/2) thời gian để đảo ngược dãy số đầu vào đó.
- Một giải pháp tối ưu khá hay được đề xuất tiếp theo đó là : Thay vì trong giai đoạn chèn 1 quân bài vào dãy các quân bài phía trước nó bằng giải pháp tìm kiếm tuần tự, ta sẽ sử dụng giải thuật tìm kiếm nhị phân trong chính quá trình chèn đó. Điều này sẽ giúp tiết kiệm được thời gian cho thao tác tìm kiếm và thao tác chèn một cách đáng kể từ O(i) xuống còn O(log(i)) với i là chỉ số cần chèn tại đó
- Điều gì sẽ xảy ra nếu giải thuật này được cài bằng danh sách liên kết : Liệu nó sẽ bất lợi hay có lợi? 
  + Trong tình huống này, việc sử dụng danh sách liên kết để cài đặt chỉ có lợi khi mà dữ liệu cần sắp xếp đến một cách liên tục (đó có thể là dữ liệu online). Vì vậy, với cách cài đặt Danh sách Liên kết, ta có thể chủ động cấp phát vùng nhớ tùy thích
  + Nhưng khi cài đặt bằng Danh sách liên kết cũng sẽ nảy sinh vài vấn đề : Do việc truy cập vào 1 phần tử trong danh sách liên kết không mang tính trực truy tức phải mất thời gian tuyến tính. Điều này, có thể làm giảm hiệu suất của giải thuật  

Tuy nhiên, trong thực tế để cài đặt Danh sách Liên kết cho giải thuật này, mọi người có thể tham khảo tại đây : 
[InsertionSort for Singly Linked List](http://www.geeksforgeeks.org/insertion-sort-for-singly-linked-list/)

## **3.Thuật toán Bubble Sort (Sắp xếp nổi bọt)** 

### **3.1. Mã nguồn minh họa :** 

```c++
// algorithm for Bubble Sort
void bubbleSort(int a[], int n){
    bool swapped ;
    for (int i = 0 ; i < n - 1 ; ++i){
        swapped = false ;
        
        for (int j = 0 ; j < n - i - 1 ; ++j){
            if (a[j] > a[j + 1]){
                int temp = a[i];
                a[j] = a[j + 1];
                a[j + 1] = temp ;
                swapped = true ;
            }
        }

        if (!swapped){
            break ;
        }
    }
}
```

### **3.2. Ý tưởng của giải thuật :**

Giải thuật sắp xếp này được tiến hành dựa trên việc so sánh cặp phần tử liền kề nhau và tráo đổi thứ tự nếu chúng không theo thứ tự tăng dần hoặc giảm dần.


### **3.3. Độ phức tạp của giải thuật :** 

Trường hợp tốt nhất (Best Case)

- Trường hợp tốt nhất xảy ra khi mảng đã được sắp xếp. Trong trường hợp này, Bubble Sort chỉ cần thực hiện một lần duyệt qua mảng để xác định rằng không cần hoán đổi nào cần được thực hiện. Điều này đòi hỏi `(O(n))` so sánh và không có hoán đổi nào được thực hiện.
- Độ phức tạp thời gian: `(O(n))`

Trường hợp xấu nhất và trung bình (Worst and Average Case)

- Trường hợp xấu nhất xảy ra khi mảng được sắp xếp theo thứ tự ngược lại. Trong trường hợp này, mỗi phần tử cần được hoán đổi qua mỗi vị trí của mảng cho đến khi nó đạt đến vị trí cuối cùng của nó. Điều này đòi hỏi `((n-1) + (n-2) + ... + 1 = n(n - 1)/2)` so sánh và hoán đổi, dẫn đến độ phức tạp thời gian là `(O(n^2))`.
- Độ phức tạp thời gian: `(O(n^2))`

Tóm tắt

- Trường hợp tốt nhất: `(O(n))`
- Trường hợp xấu nhất và trung bình: `(O(n^2))`

### **3.4. Nhận xét và đánh giá :** 

#### **3.4.1 Ưu điểm:** 

+ Thể hiện được tính ổn định và tại chỗ
+ Đơn giản, dễ hiểu… được sử dụng làm ví dụ minh họa trong quá trình giảng dạy

#### **3.4.2  Nhược điểm :**

- Nhược điểm lớn nhất của giải thuật sắp xếp nổi bọt đó là số lần hoán vị quá nhiều so với các giải thuật đã trình bày phía trên. Trong thực tế, giải thuật này hiếm khi được ứng dụng trong các bài toán thực nghiệm (do tốn kém khá nhiều thao tác hoán vị)

### **3.5. Tối ưu và so sánh :**

Chúng ta thấy rằng giải thuật sắp xếp nổi bọt so sánh mỗi cặp phần tử trong mảng trừ khi cả toàn bộ mảng đó đã hoàn toàn được sắp xếp theo thứ tự tăng dần. Điều này có thể làm tăng độ phức tạp, tức là tăng các thao tác so sánh và tráo đổi không cần thiết nếu như mảng này không cần sự tráo đổi nào nữa khi tất cả các phần tử đã được sắp xếp theo thứ tự tăng dần rồi.

Để tránh việc này xảy ra, chúng ta có thể sử dụng một biến swapped chẳng hạn để giúp chúng ta biết có cần thực hiện thao tác tráo đổi thứ tự hay không. Nếu không cần thiết thì thoát khỏi vòng lặp.


## **4.Thuật toán Merge Sort (Sắp xếp trộn)**

### **4.1. Mã nguồn minh họa**

```c++
void merge (int a[], int left, int middle, int right){
	int leftSize = middle - left + 1;
	int rightSize = right - middle ;

	int* L = new int[leftSize];
	int* R = new int[rightSize];

	for (int i = 0; i < leftSize; i++){
		L[i] = a[i + left];
	} 

	for (int i = 0; i < rightSize; i++){
		R[i] = a[i + middle + 1];
	} 

	int i = 0, j = 0, k = left;
	while (i < leftSize && j < rightSize)
		a[k++] = (L[i] < R[j]) ? L[i++] : R[j++];

	while (i < leftSize)
		a[k++] = L[i++];

	while (j < rightSize)
		a[k++] = R[j++];

	delete[] L;
	delete[] R;
}

void MergeSort(int a[], int left, int right) {
	if (left < right) {
		int middle = (left + right) / 2;
		MergeSort(a, left, middle);
		MergeSort(a, middle + 1, right);
		merge(a, left, middle, right);
	}
}    
```
    
### **4.2. Ý tưởng của giải thuật :** 

- Sử dụng tư tưởng đệ quy “chia để trị” với quan điểm việc sắp xếp tăng dần một dãy số sẽ tương ứng với các thao tác sau : 

  + Chia dãy số đó làm hai nửa (nửa trái và nửa phải)
  + Thực hiện sắp xếp một cách đệ quy trên từng nửa đó (tức gọi hàm đệ quy mergeSort(…) trên lần lượt nửa trái và nửa phải)
  + Mỗi nửa sau khi được sắp xếp sẽ được kết hợp, trộn lẫn với nhau để tạo ra một mảng hoàn chỉnh đã được sắp xếp như mong muốn (sử dụng một hàm trộn merge(…) với đầu vào là 2 mảng đã được sắp xếp, hợp nhất hai mảng này để tạo thành mảng mới đã được sắp xếp)

- Đối với hàm mergeSort(…), điều kiện neo đệ quy là : chỉ số `left >= right`. Tức tại điểm xảy ra điều kiện neo, lúc này dãy số đã được phân tách nhỏ nhất có thể (nghĩa là chỉ chứa 1 phần tử), ta gọi các dãy con nhỏ nhất này là các dãy con đơn vị. Lúc này, các dãy con đơn vị đó sẽ đôi một thông qua hàm merge(…) để hợp nhất tạo thành một mảng lớn hơn đã được sắp xếp. Rồi mảng lớn hơn này sẽ gặp một mảng lớn hơn khác để hợp nhất … Quá trình “hổi quy” này liên tục diễn ra cho tới khi chúng trở về lời gọi của hàm đệ quy gốc, để hợp nhất 2 nửa mảng cuối cùng còn lại và trả về một mảng hoàn chỉnh, đầy đủ và đã được sắp xếp

- Trực quan hình ảnh có thể xem tại link sau : [Merge Sort](http://www.geeksforgeeks.org/merge-sort/)

### **4.3. Độ phức tạp của giải thuật :**

Tất cả các trường hợp: `(O(n*log n))`

- Chia: Quá trình chia mảng thành hai nửa có độ phức tạp là `(O(1))` vì chỉ đơn giản là tính toán chỉ số giữa.
- Trị: Việc gọi đệ quy MergeSort cho mỗi nửa mảng có độ phức tạp là `(2T(n/2))`, với (T) là thời gian cần thiết để sắp xếp một mảng n phần tử.
- Kết hợp: Hàm merge có độ phức tạp là `(O(n))` vì mỗi phần tử từ hai mảng con được xem xét đúng một lần.

Ta có độ phức tạp của thuật toán :  `T(n) = 2T(n/2) + O(n)`

Từ công thức trên + áp dụng với Định lý Thợ rút gọn (Trang 48, Sách Cấu trúc dữ liệu và giải thuật, Nguyễn Đức Nghĩa), ta dễ dàng tìm được độ phức tạp của giải thuật trên là : `O(n*log(n))` cho tất cả các trường hợp.

### **4.4. Nhận xét và đánh giá** 

#### **4.4.1 Ưu điểm**

- Đơn giản và dễ hiểu, thời gian sắp xếp với độ phức tạp đã được giảm xuống một cách đáng kể (O(nlog(n)) so với các giải thuật Sắp xếp Chèn, Nổi bọt, Chọn
- Giải thuật Sắp xếp Trộn giữ được tính ổn định tương đối của các phần tử

#### **4.4.2. Nhược điểm**

- Giải thuật Sắp xếp Trộn do cần phải sử dụng thêm vùng nhớ bên ngoài ( vùng nhớ dùng thêm này tỉ lệ với số lượng phần tử n) nên giải thuật không có tính chất tại chỗ
- Độ phức tạp của giải thuật đều như nhau khi xét trên cả 3 trường hợp : Tốt nhất, Trung bình và Tệ nhất

### **4.5. Tối ưu thuật toán và các bài toán ứng dụng thực tế**

- Một cách tối ưu được để xuất cho giải thuật sắp xếp Trộn đó là sử dụng cấu trúc dữ liệu Danh sách Liên kết thay vì sử dụng mảng. 
  + Bởi vì điểm mạnh của DSLK đó là khả năng đáp ứng một tập dữ liệu đến một cách liên tục (dữ liệu thực tế). Hơn nữa, các thao tác chèn, sửa, xóa một phần tử trong danh sách liên kết chỉ tốn thời gian O(1), nhanh chóng hơn so với thời gian tuyến tính khi chèn, sửa, xóa một phần tử trong mảng. Áp dụng tính chất của DSLK vào giải thuật Sắp xếp Trộn, sẽ giúp tiết kiệm được vùng nhớ ( tức ko cần sử dụng vùng nhớ ngoài – giữ được tính chất “tại chỗ” của giải thuật), đồng thời giải quyết được các bài toán với luồng dữ liệu đến liên tục (online) trong thực tế cuộc sống
  + Sử dụng thêm biến hasSwapped trong từng đoạn nhỏ mảng ( có nghĩa sử dụng điều kiện này kết hợp làm điều kiện neo trong đệ quy), điều này giúp nhanh chóng nhận biết một số đoạn nhỏ trong mảng đã được sắp xếp rồi, từ đó hạn chế được tối đa số bước đệ quy lãng phí tiếp sau. Tương tự cũng nên kiểm tra xem đoạn nhỏ mảng đó có đang là sắp xếp giảm dần (từ đó ta chỉ việc đảo ngược vị trí các phần tử trong mảng). 
- Một số bài toán thực tế có thể áp dụng giải thuật Merge Sort : 
  + Bài toán đếm số đảo ngược :  [Counting Inversion](http://www.geeksforgeeks.org/counting-inversions/)
  + Bài toán liên quan tới lĩnh vực sắp xếp tại vùng nhớ ngoài (not sorting in RAM) : [External_Sorting](https://en.wikipedia.org/wiki/External_sorting)

## **5. Thuật toán Quick Sort (Sắp xếp nhanh)**

### **5.1. Mã nguồn minh họa :** 
```c++
   void QuickSort(int a[], int left, int right) {
	int i = left, j = right, pivot = a[(left + right) / 2];
	while (i < j) {
		while (a[i] < pivot) i++;
		while (a[j] > pivot) j--;
		if (i <= j) {
			int tmp = a[i];
			a[i] = a[j];
			a[j] = tmp;
			i++, j--;
		}
	} 
	if (i < right) QuickSort(a, i, right);
	if (left < j) QuickSort(a, left, j);
}
```

### **5.2. Tư tưởng của giải thuật** 

Giải thuật Quick Sort với tư tưởng chính : 

+ Lựa chọn một phần tử trong mảng đóng vai trò như một pivot, sau đó từ giá trị pivot này tiến hành phân lớp mảng thành 2 phần với một phần chỉ toàn gồm các phần tử nhỏ hơn hoặc bằng pivot, trong khi phần còn lại chứa các phần tử lớn hơn pivot. 
+ Từ hai nửa còn lại (không xét tới phần tử pivot, bởi vì vị trí của nó đã là cố định), ta tiến hành gọi một cách đệ quy hàm quickSort(...) trên từng nửa đó. Kết quả cuối cùng ta thu được, đó là mảng ban đầu đã được sắp xếp
Vấn đề của thao tác lựa chọn Pivot :  
- Có một câu hỏi được đặt ra đó là làm sao để lựa chọn 1 phần tử pivot tốt nhất có thể (tức giá trị của nó nằm ở mức trung bình so với các phần tử còn lại). Dưới đây là một vài đề xuất lựa chọn pivot mà chúng ta có thể tham khảo : 
  + Lựa chọn Pivot nằm ở đầu mảng
  + Lựa chọn Pivot nằm ở cuối mảng
  + Lựa chọn Pivot một cách bất kỳ và tùy ý
  + Lựa chọn Pivot tại chỉ số index = (left + right) / 2 

### **5.3. Độ phức tạp của giải thuật**

Độ phức tạp của giải thuật QuickSort là : `T(n) = T(k) + T(n-k-1) + O(n)` , với k là số phần tử bên nửa trái. Từ đó, trong từng trường hợp : 
+ Tồi tệ nhất, ứng với k = 0 : 
`T(n) = T(0) + T(n-1) + O(n) = T(n-1) + O(n) = O(n^2)`
+ Tốt nhất, ứng với k = n/2 
`T(n) = 2T(n/2) + O(n) = O(nlog(n))`
+ Trung bình : `T(n) = O(nlog(n))`

### **5.4. Nhận xét và đánh giá**

- Mặc dù, thuật toán có độ phức tạp O(n^2) đối với trường hợp tồi tệ nhất. Tuy nhiên trong thực nghiệm, độ phức tạp trung bình của giải thuật ổn định ở mức O(n.log(n))
- Là một trong số những giải thuật có tốc độ nhanh, hiệu quả và phổ biến top đầu lớp các giải thuật sắp xếp (QuickSort, HeapSort, MergeSort)
- Giải thuật có tính “tại chỗ”, nhưng không ổn định
- Hoạt động tối ưu hơn khi cài đặt sử dụng mảng
- Có sự hạn chế khi cài đặt giải thuật sử dụng cấu trúc dữ liệu Danh sách Liên kết (bởi vì trong giải thuật Quick Sort có khá nhiều thao tác so sánh, và cần phải thường xuyên truy xuất phần tử … nên cần tiêu tốn một khoảng thời gian tuyến tính để tìm phần tử đó trong dánh sách liên kết)

### **5.5. Tối ưu và các bài toán ứng dụng** 

- Tối ưu 1 : Sử dụng phương pháp Quick 3 chiều, có nghĩa là sau khi lựa được giá trị pivot, ta sẽ chia mảng thành 3 phần, gồm các phần tử nhỏ hơn pivot, bằng pivot và lớn hơn pivot ( details at following link : [Quick Sort](http://www.geeksforgeeks.org/quick-sort/)
- Tối ưu 2 : Đối với việc lựa chọn pivot luôn nằm ở cực trái (hoặc cực phải) của mảng mang tới nguy cơ dẫn tới các trường hợp tồi tệ nhất, tức: Mảng đã được sắp xếp theo đúng thứ tự, hoặc mảng đã được sắp xếp theo thứ tự ngược lại, hoặc tất cả các phần tử của mảng đều bằng nhau. Để hạn chế được các tình huống trên, ta sẽ lựa chọn pivot theo những cách khác, như: pivot nằm ở index trung bình, pivot có index ngẫu nhiên, … Sau đó ta có thể dễ dàng quy các bài toán này về bài toán chọn pivot nằm ở cực trái hoặc cực phải
- Tối ưu 3 : Mặc dù thuật toán QuickSort có tính ổn định, tuy nhiên nó vẫn sử dụng bộ nhớ để lưu các lời gọi đệ quy, trong các trường hợp tồi tệ nó có thể tốn tới lượng bộ nhớ O(n) tức tuyến tính với số lượng phần tử của dãy số. Một số giải pháp tối ưu : Khử đệ quy [Iterative Quick Sort](http://www.geeksforgeeks.org/iterative-quick-sort/), sử dụng lời gọi đệ quy đuôi (tail call, details at this link :[Tail Recursion](http://www.geeksforgeeks.org/quicksort-tail-call-optimization-reducing-worst-case-space-log-n/))
- Tối ưu 4 : Sử dụng một ưu điểm của giải thuật Insertion Sort, đó là nó sẽ tỏ ra nổi bật khi sắp xếp một lượng dữ liệu nhỏ. Vì vậy, ta sẽ áp dụng Insertion Sort vào những giai đoạn khi mà kích thước của mảng đạt tới (<= 7 phần tử) trong giải thuật Quick Sort
- Một số cài đặt Quick Sort sử dụng Danh sách liên kết : 
  + Sử dụng danh sách liên kết đơn :[Singly Linked List](http://www.geeksforgeeks.org/quicksort-on-singly-linked-list/)
  + Sử dụng danh sách liên kết đôi:[Doubly Linked List](http://www.geeksforgeeks.org/quicksort-for-linked-list/)

## **6.Thuật toán Heap Sort (Sắp xếp vun đống)**

### **6.1. Mã nguồn minh họa :**

```c++
 void heapify(int a[], int n, int i) {
  // khoi tao vt max, nut trai va nut phai cua node hien tai dang kiem tra
	int max = i, l = i*2 + 1, r = i*2 + 2;
	if (l < n && a[l] > a[max]) max = l;// tim vi tri max
	if (r < n && a[r] > a[max]) max = r;// tim vi tri max

	if (max != i) {
		swap(a[i], a[max]);// doi cho phan tu lon nhat
		heapify(a, n, max);// vun lai dong phia duoi
	} 
}

void HeapSort(int a[], int n) {
	for (int i = n / 2 - 1; i >= 0; i--)
		heapify(a, n, i);// vun lai tung dinh

	for (int i = n - 1; i > 0; i--) { // loai bo lan luot cac phan tu cuoi ra khoi heap
		swap(a[0], a[i]);// doi vi tri phan tu max ve cuoi
		heapify(a, i, 0);// vun lai dong 
	} 
}
```

### **6.2. Ý tưởng giải thuật**

Tư tưởng của giải thuật xuất phát từ cơ sở Cây vun đống Max (hay Cây vun đống Min). Một cách tương tự nhau, ta sẽ lựa chọn cây vun đống Max để minh họa giải thuật Sắp xếp vun đống.

Cây vun đống Max ở đây được quan niệm là cây nhị phân hoàn chỉnh, tức với mỗi nút cha sẽ luôn bao gồm 2 con (trừ hàng ở độ sâu cuối cùng), và các con luôn được phân bố một cách trái nhất có thể. Do cây vun đống được đề xuất minh họa trong giải thuật này là Max Heap Tree, nên có thêm tính chất Maximum được thể hiện như sau: Nút cha phải lớn hơn hoặc bằng hai nút con (còn các nút con cùng cấp thì không có ràng buộc với nhau). Như vậy, mỗi nhánh mà được đại diện bởi bất cứ nút nào đó trong cây cũng sẽ phải là một nhánh Max Heap.

Cây vun đống có thể được cài đặt sử dụng Mảng hoặc Danh sách Liên kết. Để đơn giản trong sự minh họa, chúng ta sẽ lựa chọn Mảng cho quá trình cài đặt giải thuật.

Tiếp theo đó, ta sẽ làm gì với cây Max Heap Tree này, khi biết được một tính chất vô cùng quan trọng của nó: Giá trị của cha luôn lớn hơn hoặc bằng giá trị của mỗi con. Điều đó cho thấy phần tử gốc sẽ là phần tử lớn nhất trong dãy. Ta tiến hành hoán đổi phần tử gốc với 1 phần tử cuối cùng của lá (nút cuối cùng), lúc này, nút lá (“thấp bé nhỏ con”) được đưa lên đầu (root, rễ cây), đồng thời tách biệt và cất giữ phần tử lớn nhất ở một nơi nào đó. Tại thời điểm này, cây hiện tại không còn mang tính chất Max Heap (bởi vì lá được đưa lên gốc có thể nhỏ hơn 2 con của nút cha bị thay thế). Tại đây ta cần phải tiến hành xây dựng một giải thuật mang tên `heapify(...)` giúp cập nhật lại cây trên để đưa nó trở về đúng dạng cây Max Heap Tree. Hàm này sẽ sử dụng tính chất quan trọng từ cây “bị sai lệch” trên, đó là: 2 nhánh con của phần tử gốc hiện tại vẫn mang tính chất Max Heap. Sau khi đi qua hàm này, cây trên sẽ được cập nhật về đúng dạng Max Heap… Rồi ta lại hoán đổi gốc của cây với phần tử lá cuối cùng, đồng thời lại tách biệt phần tử lớn nhất ra khỏi cây, rồi lại cập nhật lại cây… Các quá trình cứ diễn ra một cách tuần hoàn cho tới khi cây chỉ còn duy nhất một phần tử (đó cũng sẽ chính là phần tử nhỏ nhất trong dãy số). Kết thúc giải thuật Heap Sort, chúng ta sẽ thu được một mảng dãy số đã được sắp xếp như ý muốn!

Khi cài đặt cây Max Heap theo dạng mảng số, có một tính chất sau cần chú ý:
- `LeftChildIndex = 2 * ParentIndex + 1`
- `RightChildIndex = 2 * ParentIndex + 2`

Vì input hay mỗi dãy số ban đầu (được lưu trữ dưới dạng mảng) là ngẫu nhiên, chưa được có tính chất Max Heap, vì thế ta cần có phải có một bước đầu để chuyển hóa cây trên thành một cây mang đặc điểm Max Heap (thủ tục này được tạo trong hàm `heapSort(...)`).

Như vậy, hàm `heapSort` sẽ bao quát những công việc sau:
1. Khởi tạo một cây Max Heap Tree từ một dãy ngẫu nhiên.
2. Từ cây Max Heap Tree, tiến hành trích lấy phần tử lớn nhất ở root, và thay thế vị trí root bởi nút lá cuối cùng. Sau đó, gọi hàm `heapify(...)` cập nhật lại cây trên tại root mới đó, rồi lại trích lấy phần tử root, và thay thế vị trí root bởi lá,… Quá trình diễn ra một cách tương tự, cho tới khi cây chỉ còn 1 phần tử. Và phần tử đó sẽ là phần tử nhỏ nhất trong mảng. Kết quả, ta thu được một mảng gồm các số đã được sắp xếp tăng dần!  
  
### **6.3. Độ phức tạp của giải thuật :**

- Thủ tục heapify (...) có độ phức tạp là `O(log(n))` : Do số lần duyệt của thủ tục này cỡ bằng độ sâu của cây nhị phân
- Đối với thủ tục heapSort, ta có thể đánh giá độ phức tạp một cách tương đối như sau : 
  + Vòng for đầu tiên : `O(log(n/2) + log(n/2 + 1) + ... + log(n)) <= O(n.log(n))`
  + Vòng for thứ hai : `O(log(n) + log(n-1) + ... + log(1)) <= O(n.log(n))`
  
Như vậy, độ phức tạp của giải thuật Heap Sort là : `O(n.log(n))`

### **6.4. Nhận xét và đánh giá**

#### **6.4.1 Ưu điểm :**

  + Khá nhanh (O(n*log(n)), tuy nhiên trong thực nghiệm lại kém hơn so với giải thuật QuickSort và MergeSort.
  + Cấu trúc dữ liệu dạng vun đống được sử dụng rộng rãi trong nhiều bài toán
  + Heap Sort là một giải thuật sắp xếp tại chỗ

#### **6.4.2 Nhược điểm :**  

  + Với cách cài đặt trên, giải thuật này chưa có tính chất ổn định. Tuy nhiên, có thể cài đặt giải thuật trên để nó có tính chất ổn định, hãy tham khảo từ nguồn sau đây: [Improve HeapSort](http://www.geeksforgeeks.org/stability-in-sorting-algorithms/)
  + Hơi phức tạp trong cài đặt giải thuật
  
### **6.5. Sự tối ưu và ứng dụng thực tế**

- Một số ứng dụng của Sắp xếp vun đống có thể kể tới : 
  + Sort a nearly sorted array : http://www.geeksforgeeks.org/nearly-sorted-algorithm/
  + K largest (or smallest) elements in an array : http://www.geeksforgeeks.org/k-largestor-smallest-elements-in-an-array/
  + Applications of Heap Data Structure : http://www.geeksforgeeks.org/applications-of-heap-data-structure/
  
## **7.Thuật toán Counting Sort (Sắp xếp đếm)**

### **7.1 Mã nguồn minh họa :**

```c++
void CountingSort(int a[], int n) {
	int tmp[N];
	int minn = a[0], maxx = a[0];

	for (int i = 1; i < n; i++)// tim min max cua cac phan tu trong mang
		minn = min(minn, a[i]), maxx = max(maxx, a[i]);

	int k = maxx - minn + 1;// khoang gia tri trai dai tu 0 den k - 1

	int cnt[N];
	for (int i = 0; i < k; i++) 
			cnt[i] = 0;// khoi tao gia tri dem phan phoi trong khoang = 0

	for (int i = 0; i < n; i++) 
			cnt[a[i] - minn]++;// thuc hien viec den phan phoi so luong phan tu bang cach quy ve khoang 0 den k - 1

	for (int i = 1; i < k; i++)
			cnt[i] += cnt[i - 1];// cong don mang

	for (int i = 0; i < n; i++)
			tmp[--cnt[a[i] - minn]] = a[i];// xac dinh lai vi tri chinh xac, co the chay tu n - 1 den 0 de dam bao tinh on dinh cua thuat toan sx 
	 
	for (int i = 0; i < n; i++)
		a[i] = tmp[i];// cap nhap mang sau khi sap xep cho mang chinh 
}

```

### **7.2. Ý tưởng của giải thuật**

Giải thuật được xuất phát từ ý tưởng “Đếm” áp dụng cho dãy số nguyên được thể hiện như sau : 

+ Chọn một miền giá trị bao phủ được tất cả các giá trị của từng phần tử trong mảng, sau đó tạo mới một mảng trung gian có sức chứa bằng đúng số vạch chia đơn vị trong miền giá trị (được lựa chọn trên). Gán giá trị cho tất cả phần tử trong mảng bằng 0
+ Như vậy, giá trị của mỗi phần tử từ dãy số ban đầu sẽ được thể hiện bằng giá trị của chỉ số trong mảng trung gian. Tiếp theo, tiến hành duyệt từng phần tử của mảng gốc, ứng với mỗi phần tử xuất hiện trong mảng gốc này sẽ được cộng thêm 1 vào phần tử có chỉ số bằng với giá trị của phần tử trong mảng gốc. Sau khi duyệt xong toàn bộ mảng gốc, mảng trung gian lúc này sẽ chứa số lần xuất hiện của các phần tử trong mảng gốc trong dãy số ban đầu
+ Tiếp tục khai thác và chế biến mảng trung gian để nó trở nên hữu ích hơn bằng cách duyệt từng phần tử của mảng trung gian, từ phần tử thứ 2 trở đi. Sau đó cộng dồn phần tử hiện tại với phần tử trước đó và gán lại vào phần tử hiện tại. Cứ như vậy, tới khi duyệt hết mảng, ta sẽ thu được một mảng trung gian vô cũng hữu ích, lúc này giá trị của trong mỗi phần tử trung gian sẽ cho biết giá trị index thực sự của giá trị gốc đó trong mảng khi đã được sắp xếp
+ Thao tác cuối cùng, chỉ đơn giản là duyệt lại mảng gốc, kết hợp với mảng trung gian để lấy ra các phần tử tương ứng theo thứ tự đã được sắp xếp!!!

### **7.3. Độ phức tạp của giải thuật :**

Thủ tục Counting Sort yêu cầu duyệt qua n phần tử từ dãy số gốc, và m phần tử (số vạch chia trong miền giá trị bao phủ). Do vậy, độ phức tạp sẽ là : O(n + m)

### **7.4. Nhận xét và đánh giá :**

- Thuật toán chỉ hiệu quả khi mà miền giá trị của dữ liệu không lớn hơn quá nhiều so với tổng số phần tử trong mảng gốc. Nó sẽ không hiệu quả nếu miền giá trị là một hàm mũ, lũy thừa so với số phần tử cần phải sắp xếp. Vì vậy, cần phải cân nhắc kỹ
- Không sử dụng phương pháp sắp xếp dựa trên quá trình so sánh, mà sử dụng chủ yếu vào bộ nhớ lưu trữ

### **7.5. Tối ưu và ứng dụng thực tế :** 

- Giải thuật được sử dụng như một giai đoạn trong giải thuật Radix Sort
- Giải thuật cũng có thể được mở rộng để làm việc với các số nguyên âm, hay sắp xếp các chuỗi ký tự

## **8. Thuật toán Radix Sort (Sắp xếp theo cơ số)** ###  

### **8.1. Mã nguồn minh họa**
```c++
void countingSort(int a[], int n, int div) {
	int countingKeys[10] = {0};
	int* res = new int[n];
	int key;

	for (int i = 0; i < n; i++) {
		key = (a[i] / div) % 10;
		countingKeys[key]++;
	} 

	for (int i = 1; i < 10; i++)
		countingKeys[i] += countingKeys[i - 1];

	for (int i = n - 1; i >= 0; i--) {// chay tu cuoi len de dat duoc su on dinh cua thuat toan sap xep
		key = (a[i] / div) % 10;
		res[--countingKeys[key]] = a[i];
	} 

	for (int i = 0; i < n; i++)
		a[i] = res[i];

	delete[] res;
}

void RadixSort(int a[], int n) {
	int maxx = a[0];
	for (int i = 1; i < n; i++) 
		maxx = max(a[i], maxx);

	for (int divisionUnit = 1; divisionUnit <= maxx; divisionUnit *= 10)// chay co so
		countingSort(a, n, divisionUnit);// sort theo co so
}

```
### **8.2. Ý tưởng của giải thuật :**

Giải thuật sắp xếp theo cơ số 10 với tư tưởng chính sau:

+ Tiến hành sắp xếp tất cả các phần tử trong dãy số ban đầu lần lượt từ hàng đơn vị, hàng chục, hàng trăm,… như các so sánh của con người
+ Với mỗi thao tác sắp xếp các phần tử là theo một hàng nhất định (đơn vị, chục, trăm…) và miền giá trị ở mỗi hàng là khá nhỏ (từ 0 đến 9), nên trong giải thuật trên tác giả lựa chọn Sắp xếp Đếm (Counting Sort) cho từng quá trình sắp xếp này.
+ Như vậy, quá trình trên sử dụng Counting Sort để sắp xếp dãy số từ hàng đơn vị, hàng chục, hàng trăm, … đến hàng cao nhất. Kết thúc quá trình sắp xếp, ta thu được dãy số đã được sắp xếp như mong đợi ### !

### **8.3. Độ phức tạp của thuật toán :**

- Gọi k là số lượng chữ số trong số lớn nhất của dãy số, do thuật toán áp dụng giải thuật Counting Sort để sắp xếp trên từng chữ số. Vì thế độ phức tạp của thuật toán là : `d * O(n + b) = O(d * (n+ b))`, với b là hệ số (trong giải thuật trên ta chọn hệ số là 10 tức miền giá trị từ 0 đến 9)

### **8.4. Nhận xét và đánh giá :**

- Mặc dù giải thuật trên khá nhanh. Tuy nhiên vẫn chưa thể đánh bại giải thuật sắp xếp dựa trên so sánh (như QuickSort, HeapSort, Merge Sort) 

## **9.Thuật toán Bucket Sort( Sắp xếp phân cụm)**

### **9.1. Mã nguồn minh họa**
```c++
void BucketSort(double a[], int n) {
	
	//1) Create empty buckets 
	vector<double> b[N];

	//2) Put array elements in different buckets
	for (int i = 0; i < n; i++) {
		int bi = int (a[i] * n);// Index in bucket
		b[bi].pb(a[i]);
	} 

	//3) Sort individual buckets
	for (int i = 0; i < n; i++)
		sort(b[i].begin(), b[i].end());// goi ham sap xep co san trong thu vien <(^-^)>

	//4) Concatenate all buckets into arr
	int index = 0;
	for (int i = 0; i < n; i++)
		for (int j = 0; j < b[i].size(); j++)
			a[index++] = b[i][j];
}

```

### **9.2. Ý tưởng của giải thuật**

Giải thuật phân cụm được áp dụng cho lớp bài toán sắp xếp phần tử mà các phần tử trong dãy có sự phân bố đều đặn trong miền giá trị của nó. Giải thuật này được trình bày cụ thể trong bài toán sắp xếp dãy số có miền giá trị từ 0 đến 1, và các phần tử có sự phân bố đều đặn trên miền đó

+ Tạo ra n vector hay n mảng được gọi là bucket
+ Duyệt các phần tử trong mảng gốc, với mỗi phần tử này ta sẽ đưa nó vào trong một bucket phù hợp (như thế nào là phù hợp? nghĩa là : phần tử có giá trị x sẽ được đưa vào buckets (cụm) có chỉ số là `(int) x * n `. Như vậy có thể trong một buket có thể chứa nhiều hơn một phần tử (tư tưởng bảng băm)
+ Sử dụng ưu thế của giải thuật sắp xếp chèn cho một lượng nhỏ các phần tử. Ta tiến hành thực hiện giải thuật Insertion Sort trên từng cụm bucket. Quá trình này hoàn tất đồng nghĩa với việc tất cả các phần tử trong mỗi bucket đều đã được xếp thứ tự
+ Công việc đơn giản cuối cùng chỉ còn là : Duyệt từ bucket đầu tiên tới bucket cuối cùng để lấy ra các phần tử và ghi đè lần lượt vào mảng ban đầu. Kết quả : Mảng ban đầu đã được sắp xếp !

### **9.3. Độ phức tạp của giải thuật**

Trong thủ tục bucketSort, độ phức tạp của từng bước được thể hiện như sau : 

+ Bước đưa các phần tử vào các bucket phù hợp : `O(n)`
+ Sắp xếp các phần tử trên từng cụm buckets sử dụng Insertion Sort  : `O(n)` (trong trường hợp các phần tử trong dãy số phải được phân bố đều đặn )
Như vậy độ phức tạp của bài toán : `O(n)`

### **9.4. Nhận xét và đánh giá :**

- Giải thuật cho phép độ phức tạp thời gian sắp xếp dãy số theo thời gian tuyến tính trong trường hợp dãy số ban đầu phải được phân bố đều đặn trên miền giá trị của chúng

## **10.Thuật toán Shell Sort (Tối ưu Insertion Sort)**

### **10.1 Mã nguồn minh họa** 
```c++
void ShellSort(int a[], int n) {
	int j, interval = 1;// buoc nhay
	
	while (interval <= (n / 3)) 
			interval = interval * 3 + 1;// toi uu cua buoc nhay nhat co the

	while (interval > 0)
	{
		for (int i = interval; i < n; i++) {// su dung chen truc tiep de dam bao su on dinh cua thuat toan
			int comp = a[i];
			for (j = i; j >= interval && a[j - interval] > comp; j -= interval)
				a[j] = a[j - interval];
			a[j] = comp;
		}
		interval = (interval - 1) / 3;
	}
}
```

### **10.2. Ý tưởng của giải thuật :**

Đây là một giải thuật giúp tối ưu hơn giải thuật Insertion Sort. Ý tưởng của giải thuật được thể hiện như sau : 

+ Bình thường trong giải thuật Insertion Sort (trong ví dụ Người chơi bài), người chơi bài sẽ so sánh quân bài hiện tại với lần lượt các quân bài phía trước. Một để xuất tối ưu được đưa ra đó là, thay vì cứ thao tác cứ "chăm chăm" so sánh với các phần từ liền kề phía trước, họ nảy sinh một ý tưởng : Tại sao không tiến hành so sánh ngắt quãng (interval) (tức phần tử hiện tại được so sánh với các phần tử phía trước (giống như Insertion sort) nhưng khoảng cách giữa chúng phải là bội của interval (quãng)). Mọi thao tác trong giải thuật này cơ bản sẽ giống hệt với giải thuật Insertion Sort. Tuy nhiên có một điểm khác đặc biệt, đó là bước interval sẽ liên tục giảm sau mỗi lần lặp (quy tắc giảm được tuân theo một công thức đã được thực nghiệm xác định), vậy interval sẽ giảm tới khi nào? Nó sẽ giảm tới khi interval = 1 (tức quãng nhỏ nhất có thể), lúc này bài toán thuần túy trở về nguyên gốc giải thuật insertion sort. Tuy nhiên, bước cuối cùng này chủ yếu mang tính kiểm nghiệm và rà soát một lần nữa, chứ ko làm tiêu tốn quá nhiều các thao tác hoán vị !!!

+ **Chú ý** : Ta cần phải khởi tạo giá trị interval theo công thức của Knuth nhằm đảm bảo thuật toán sẽ làm việc một cách hiệu quả (`interval = interval * 3 + 1`)

### **10.3. Độ phức tạp của giải thuật**

Dù đã có sự cải tiến tuy nhiên độ phức tạp của thuật toán trên vẫn cỡ O(n^2)

### **10.4. Nhận xét và đánh giá** 

- Đây là giải thuật tối ưu hóa giải thuật Insertion Sort
- Sử dụng công thức Knuth để tỉm ra interval phù hợp (interval = interval * 3 + 1)

## **11. Thuật toán Comb Sort (Cải tiến giải thuật Bubble Sort)**

### **11.1. Mã nguồn minh họa :**

```c++
int getNextGap(int gap) {
	gap = gap * 10 / 13;
	if (gap < 1)
			return 1;
	return gap;
}

void CompSort(int a[], int n) {
	int gap = n;
	bool swapped = true;

	while (gap != 1 || swapped) {
		gap = getNextGap(gap);
		swapped = false;

		for (int i = 0; i < n - gap; i++)
			if (a [i] > a[i + gap])
			{// doi cho va danh dau da thuc hien swap
				int tmp = a[i];
				a[i] = a[i + gap];
				a[i + gap] = tmp;
				swapped = true;
			}
	} 
	 
}
```
### **11.2. Ý tưởng của giải thuật :**  

Giải thuật này là một sự cải tiến cho giải thuật Sắp xếp Nổi bọt (Bubble Sort). Tư tưởng chủ đạo của giải thuật này được thể hiện một cách cụ thể như sau :

+ Đối với giải thuật sắp xếp nổi bọt, quá trình so sánh và hoán vị được thực hiện trên các phần tử liền kề, liên tiếp. Sự sáng tạo trong phương pháp tối ưu của giải thuật này được thể hiện bằng việc sử dụng phương pháp so sánh ngắt quãng (như trong giải thuật Shell Sort), ta gọi các quãng này là gap. Ban đầu gap được khởi tạo bằng kích cỡ của mảng, trong quá trình lặp ta cần phải thu nhỏ, hay làm giảm giá trị của gap bằng một hệ số đã được kiểm định là : `1.3` (tức là cứ sau mỗi lần lặp, giá trị của gap sẽ giảm đi `1.3` lần). Các thao tác lúc này diễn ra cơ bản rất giống với Insertion Sort. Nó cứ tiếp diễn, cho tới khi gap = 1, lúc này giải thuật đã thực sự “quy chụp” về đúng giải thuật Insertion Sort với quãng so sánh = 1. 
+ Tuy nhiên, do việc giảm gap khá nhanh, nên tác giả giải thuật đã lồng ghép vào đó một biến `hasSwapped`. Biến này có ý nghĩa vô cùng quan trọng. Vậy nó quan trọng như thế nào? Nếu không có nó liệu kết quả có còn đúng đắn? Nhìn vào giải thuật trên, cụ thể điều kiện lặp trong vòng while, ta phát hiện thấy : Vòng while sẽ chỉ dừng khi phải thỏa mãn đồng thời cả 2 điều kiện sau : quãng gap phải giảm về 1 đồng thời không còn bất kỳ sự hoán đổi nào trong lần duyệt trước. Điều này là hoàn toàn đúng đắn ( do tính hội tụ nhanh của gap, nên bắt buộc phải có một biến hasSwapped để kiểm soát tính “đã sắp xếp” của dãy số ban đầu)

### **11.3. Độ phức tạp của giải thuật**

- Dù có một sự cải tiến đáng kể, nhưng độ phức tạp của giải thuật vẫn cỡ `O(n^2)`

### **11.4 Nhận xét và đánh giá**

- Giải thuật là một sự cải tiến từ giải thuật Bubble Sort truyền thống với tư duy “so sánh theo quãng” khá hay
- Hãy chú tới nhân tố giúp “hội tụ” hay co hẹp giá trị của gap (quãng) là : 1.3 (theo thực nghiệm)

## **12. Thuật toán Pigeonhole Sort (Sắp xếp nhốt chim vào lồng)**

### **12.1. Mã nguồn minh họa**

```c++
void PigeonHoleSort(int a[], int n) {
	int maxx = a[0], minn = a[0];
	for (int i = 1; i < n; i++) 
		maxx = max(a[i], maxx), minn = min(a[i], minn);

	int range = maxx - minn + 1;
	vector<int> *holes = new vector<int> [range];

	for (int i = 0; i < n; i++)
		holes[a[i] - minn].push_back(a[i]);
	
	int index = 0;

	for (int i = 0; i < range; i++)
		for (int j = 0; j < holes[i].size(); j++)
			a[index++] = holes[i][j];

	delete[] holes;
}
```
### **12.2. Ý tưởng của thuật toán :**

Thuật toán xuất phát từ ý tưởng nhốt chim vào lồng áp dụng cho các số nguyên được thể hiện như sau : 

- Đầu tiên, duyệt toàn bộ các phần tử trong mảng để tìm ra phần tử lớn nhất và nhỏ nhất trong mảng. Trừ hai giá trị này cho nhau, ta thu được một miền giá trị.
- Từ miền giá trị này, ta tạo ra một tập các lồng chim, có số lượng bằng số vạch chia đơn vị trong miền giá trị đó
- Duyệt dãy số ban đầu (tức tập các con chim bồ câu có gắn các số ngẫu nhiên ), với mỗi giá trị số trên từng con chim, ta sẽ tương ứng nhốt nó vào một chiếc lồng thích hợp (lồng thích hợp là chiếc lồng có chỉ số index bằng với giá trị số trên con chim đó). Sau khi duyệt xong toàn bộ, tất cả các chú chim đã được nhốt vào lồng. Như vậy, các con chim bồ câu có cùng giá trị sẽ nằm trong cùng một lồng. Từ các lồng trên, ta sẽ biết được vị trí chính xác của mỗi con chim bồ câu theo một thứ tự sắp xếp tăng dần
- Công việc còn lại chỉ đơn giản là mở từ lồng thứ nhất đến lồng cuối cùng để đưa lần lượt từng chú chim bồ câu nối đuôi nhau đi ra ngoài. Thứ tự bước ra ngoài của các con chim bồ câu đó chính là thứ tự sắp xếp tăng dần mà ta cần tìm !!!

### **12.3. Độ phức tạp của giải thuật :** 

- Do bài toán cần phải duyệt qua m chiếc lồng, và n chú chim. Nên độ phức tạp của giải thuật sẽ là : O(n+m)

### **12.4. Nhận xét và đánh giá**

- Yêu cầu của giải thuật Nhốt chim vào lồng : Số lượng các phần tử và miền giá trị của chúng phải khá gần nhau
