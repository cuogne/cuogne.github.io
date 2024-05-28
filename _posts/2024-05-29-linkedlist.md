---
layout: post
description: >-
  Tìm hiểu về Singly Linked List - Danh sách liên kết đơn trong C++
title: Singly Linked List
date: 2024-05-29 01:00:00 +0700
categories: [Blog, Code]
---

Bài viết dựa trên sự tìm hiểu và học hỏi của mình, nếu có sai sót hãy inbox trực tiếp mình để mình fix nhé !

Mình cũng sẽ để link các nguồn mình đã tìm hiểu và học hỏi trong quá trình học lập trình cũng như viết cái blog này bên dưới cuối bài blog.

# Linked List - Danh sách liên kết
## Danh sách Liên kết là gì? 

Nó là một trong những cấu trúc dữ liệu cơ bản và quan trọng nhất trong lập trình và khoa học máy tính. Nó cho phép bạn lưu trữ và quản lý các phần tử dữ liệu theo một cách động, linh hoạt hơn so với mảng (array).

## Cấu tạo của Danh sách Liên kết (Linked List)

Trước hết thì bạn có thể hiểu đơn giản như cái tên của nó, thì nó là 1 dãy danh sách được kết nối với nhau thông qua các liên kết.

Còn chính xác nhất thì danh sách liên kết là một cấu trúc dữ liệu gồm một chuỗi các phần tử, mỗi phần tử được gọi là một node. Mỗi node chứa hai thành phần chính:

- Data : đây là phần dữ liệu của Node
- Next : con trỏ lưu trữ địa chỉ của Node kế tiếp trong danh sách (đó cũng là lý do nó thường được đặt tên là next)

Cú pháp khai báo của một Node trong C++

```console
struct Node {
    int data ;
    Node* next ;
};
```

![Cấu tạo của một Node](/img/linkedlist/node.png)
_Cấu tạo của một Node_

Kiểu dữ liệu của data có thể thay đổi tùy vào loại dữ liệu mà người dùng muốn quản lý.

## Các loại danh sách liên kết

Linked List có 3 loại chính:

- Danh sách liên kết đơn (Singly Linked List): Mỗi node chứa một con trỏ trỏ đến node kế tiếp.
- Danh sách liên kết đôi (Doubly Linked List): Mỗi node chứa hai con trỏ, một trỏ đến node kế tiếp và một trỏ đến node trước đó.
- Danh sách liên kết vòng (Circular Linked List): Node cuối cùng trỏ đến node đầu tiên, tạo thành một vòng khép kín. Có thể là liên kết đơn hoặc đôi.

Ở đây thì mình chỉ tập trung vào Danh sách liên kết đơn, vì đây là loại phổ biến nhất và dễ hiểu nhất trong các loại danh sách liên kết, được ứng dụng rộng rãi trong quá trình học tập cũng như làm việc.

# Singly Linked List - Danh sách Liên kết đơn
## Cấu tạo của DSLK đơn

Danh sách liên kết đơn cũng có cấu tạo gồm các Node được liên kết với nhau. 

Phần tử đầu tiên của một DSLK đơn sẽ được quản lý bởi một con trỏ Head, phần tử cuối cùng của một DSLK đơn sẽ được quản lý bởi con trỏ Tail.

Trên thực tế, lúc làm việc với DSLK đơn, bạn chỉ cần đúng 1 con trỏ Head ở đầu danh sách là đã có thể quản lý được DSLK đơn, bởi vì DSLK đơn chỉ có thể duyệt theo 1 chiều thôi.

Node cuối cùng của DSLK đơn sẽ luôn trỏ vào NULL(hoặc nullptr), báo hiệu sự kết thúc của DSLK đơn.

![Danh sách liên kết đơn](/img/linkedlist/eng_node.png)
_Cấu tạo của một DSLK đơn_

## Đặc điểm của DSLK đơn

Do danh sách liên kết đơn là một cấu trúc dữ liệu động, được tạo nên nhờ việc cấp phát động nên nó có một số đặc điểm sau đây:

### Ưu điểm
- Được cấp phát bộ nhớ khi chạy chương trình
- Có thể thay đổi kích thước một cách linh hoạt, không cần phải khai báo kích thước cố định như mảng. Kích thước tối đa phụ thuộc vào bộ nhớ khả dụng của RAM
- Chèn và xóa phần tử nhanh chóng. Độ phức tạp là O(1) nếu biết trước vị trí
- Các phần tử được lưu trữ ngẫu nhiên (không liên tiếp) trong RAM

### Nhược điểm
- Duyệt chậm do phải duyệt qua từng Node trong danh sách. Độ phức tạp là O(n)
- Vì thế nên truy cập phần tử ngẫu nhiên rất chậm vì phải duyệt từ đầu danh sách đến phần tử cần tìm.
- Tốn bộ nhớ: Mỗi node cần phải cấp phát bộ nhớ để lưu con trỏ.
- Khó quản lý hơn: Việc quản lý các con trỏ phức tạp hơn, dễ gặp lỗi nếu bạn không nắm vững con trỏ.

## Các thao tác cơ bản trên DSLK đơn

### Khai báo cú pháp của Node

```console
struct Node {
    int data ;
    Node* next ;

    // constructor
    Node(int x){
        data = x ;
        next = nullptr ;
    }
};
```
Ở đây mình sử dụng luôn Constructor để khởi tạo các data cụ thể, và để dễ quản lý thì mình chọn kiểu số nguyên (int)

### Thêm một phần tử vào linked list
``` console
void addData(Node*& head, int data){
    Node* newNode = new Node(data);
    if (head == nullptr){
        head = newNode ;
    }
    else {
        Node* temp = head ;
        while (temp -> next != nullptr){
            temp = temp -> next ;
        }
        temp -> next = newNode;
    }
}
```
Bên trên là một hàm thực hiện chức năng thêm data vào cuối linked list được quản lý bởi con trỏ head

Ở đây hàm addData nhận vào 2 tham số là con trỏ head và biến data. Tham số Node*& head là một tham chiếu đến một con trỏ. Điều này cho phép hàm sửa đổi con trỏ head trong hàm gọi.

- Giải thích Code

```console
Node* newNode = new Node(data);
```
Ở đây, ta cấp phát động cho Node có tên là newNode với data được truyền vào từ hàm.

Cú pháp này chỉ khả dụng khi các bạn sử dụng constructor như mình. Nếu các bạn không dùng constructor như mình thì các bạn chỉ cần khai báo:

```console
Node* newNode = new Node {data,nullptr};
```


```console
if (head == nullptr){
    head = newNode ;
}
```
Ở đây, ta kiểm tra xem head có bằng nullptr hay không, tức là danh sách liên kết có đang rỗng không, không có phần tử. Nếu điều này đúng, ta lấy head gán bằng phần tử vừa được cấp phát ở trên. Vậy là danh sách liên kết đã có phần tử đầu tiên.

```console
else {
    Node* temp = head ;
    while (temp -> next != nullptr){
        temp = temp -> next ;
    }
    temp -> next = newNode;
}
```

Nếu danh sách đã có phần tử rồi, ta tạo một con trỏ temp tạm thời dể duyệt qua danh sách, tránh sử dụng trực tiếp con trỏ head.

Sau đó, tạo một vòng lặp để duyệt qua danh sách. Vòng lặp kết thúc chỉ khi vòng lặp duyệt tới phần tử cuối cùng trong linked list (lúc này con trỏ next của node cuối đang trỏ vào nullptr đó)

Câu lệnh temp = temp -> next di chuyển đến nút tiếp theo trong danh sách

Khi thoát khỏi vòng lặp cũng là lúc con trỏ temp đã đi đến cuối danh sách, ta thực hiện thao tác lấy temp -> next = newNode. Vì lúc này temp -> next đang có giá trị là nullptr, nên chỉ cần gắn node mới cấp phát thì ngay lập tức node mới đã được thêm vào cuối danh sách

Còn vấn đề phải gán lại newNode -> next = nullptr thì không cần đâu, vì phía bên trên mình đã chỉ các bạn sử dụng constructor để khởi tạo các data cụ thể, trong đó có cả next và nó đang được gán bằng nullptr mà.
